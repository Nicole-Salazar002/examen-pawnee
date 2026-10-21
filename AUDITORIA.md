# Auditoría · Versión A
Código: e3238
Repositorio público propio: https://github.com/Nicole-Salazar002/examen-pawnee
Rama: examen/323238

## A-01 · No se registra el avistamiento
### Síntoma
El formulario de alta construía el campo `criaturaId`; el contrato del servicio espera `criatura` y rechaza campos desconocidos. No se reprodujo en navegador antes del cambio.

### Causa
`frontend/src/paginas/FormularioAvistamiento.tsx` enviaba un nombre distinto en altas y ediciones. La lista blanca de `backend/src/validacion.ts` acepta `criatura`.

### Cambio
El formulario envía ahora `criatura` en altas y ediciones. Cambio incluido en el commit `ec438ce`.

### Prueba
La prueba HTTP creó un registro temporal con 201; GET del detalle confirmó que persistió asociado a la criatura elegida. Una referencia inexistente devolvió 404 y el registro temporal se eliminó después. En la interfaz, el formulario abrió el detalle y la asociación persistió tras recargar. Evidencia API: `evidencias/2026-10-21-pruebas-api.md`; verificación visual: `PRUEBAS-MANUALES.md`.

### Estado
Resuelto; se verificaron la creación, el detalle y la persistencia después de recargar.

## A-02 · La lista no identifica a la criatura
### Síntoma
El servicio devolvía la referencia cruda; el helper de React mostraba `ID: ...` en lugar del nombre. No se reprodujo visualmente antes del cambio.

### Causa
`backend/src/services/avistamientos.service.ts` no poblaba `criatura` en `listar`, aunque el detalle sí lo hace.

### Cambio
`listar` ahora hace `populate('criatura')`. Una lista vacía sigue devolviendo un arreglo vacío. Cambio incluido en el commit `ec438ce`.

### Prueba
GET de la lista devolvió cada referencia como objeto poblado con nombre; la interfaz mostró los nombres y el estado vacío sin errores. Evidencia API: `evidencias/2026-10-21-pruebas-api.md`; verificación visual: `PRUEBAS-MANUALES.md`.

### Estado
Resuelto; el listado muestra el nombre de cada criatura y la consulta sin resultados presenta el estado vacío sin errores.

## A-03 · Se acepta un peligro inválido
### Síntoma
La ruta de actualización no habilitaba validadores de Mongoose, por lo que el rango del esquema no protegía el PUT. No se envió la petición antes del cambio.

### Causa
Faltaba `runValidators` en las opciones de `findByIdAndUpdate` de `backend/src/services/criaturas.service.ts`.

### Cambio
Se añadió `runValidators: true`; el manejador existente convierte errores de validación en 400. Cambio incluido en el commit `ec438ce`.

### Prueba
PUT con nivel 7 devolvió 200; PUT con 999 devolvió 400; GET confirmó que se conservaba 7. El valor original (2) fue restaurado y verificado.

### Estado
Resuelto y verificado por API.

## A-04 · El filtro no actualiza la pantalla
### Síntoma
El cambio de selector modificaba `tipo`, pero el efecto de carga dependía solo de `recarga`; no consultaba hasta pulsar Actualizar lista. No se reprodujo visualmente antes del cambio.

### Causa
El array de dependencias en `frontend/src/paginas/ListaCriaturas.tsx` omitía `tipo`, que usa la consulta.

### Cambio
Se agregó `tipo` a las dependencias. Se conservan los estados de carga, error y vacío. Cambio incluido en el commit `ec438ce`.

### Prueba
La consulta API `tipo=mecanica` devolvió total 0 y el check/compilación pasan. En la interfaz, cambiar el selector actualizó la lista sin pulsar “Actualizar lista”; se comprobó loading, error y empty, y volver a “Todos” restauró la lista. Evidencia API: `evidencias/2026-10-21-pruebas-api.md`; verificación visual: `PRUEBAS-MANUALES.md`.

### Estado
Resuelto; el filtro actualiza la lista al cambiar el tipo y conserva los estados de carga, error y vacío.
