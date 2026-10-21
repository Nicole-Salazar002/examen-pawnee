# Auditoría · Versión A
Código: pendiente de completar por el estudiante
Repositorio público propio: pendiente
Rama: examen/323238

> Las causas se identificaron en el código; no se reprodujeron los fallos antes de aplicar los cambios. Se ejecutaron comprobaciones posteriores contra la base individual y se documentan en `evidencias/2026-10-21-pruebas-api.md`. A-01, A-02 y A-04 aún requieren completar la comprobación en la interfaz.

## A-01 · No se registra el avistamiento
### Síntoma
El formulario de alta construía el campo `criaturaId`; el contrato del servicio espera `criatura` y rechaza campos desconocidos. No se reprodujo en navegador antes del cambio.

### Causa
`frontend/src/paginas/FormularioAvistamiento.tsx` enviaba un nombre distinto en altas y ediciones. La lista blanca de `backend/src/validacion.ts` acepta `criatura`.

### Cambio
El formulario envía ahora `criatura` en ambos casos. Commit: pendiente.

### Prueba
La prueba HTTP creó un registro temporal con 201; GET del detalle confirmó que persistió asociado a la criatura elegida. Una referencia inexistente devolvió 404. El registro temporal se eliminó después. Falta comprobar el alta desde el formulario React y recargar el navegador.

### Estado
Resuelto; el formulario creó el registro, abrió el detalle y la asociación persistió después de recargar

## A-02 · La lista no identifica a la criatura
### Síntoma
El servicio devolvía la referencia cruda; el helper de React mostraba `ID: ...` en lugar del nombre. No se reprodujo visualmente antes del cambio.

### Causa
`backend/src/services/avistamientos.service.ts` no poblaba `criatura` en `listar`, aunque el detalle sí lo hace.

### Cambio
`listar` ahora hace `populate('criatura')`. Una lista vacía sigue devolviendo un arreglo vacío. Commit: pendiente.

### Prueba
GET de la lista devolvió cada referencia como objeto poblado con nombre; el filtro sin resultados devolvió total 0. Falta confirmar su presentación visual en React.

### Estado
Resuelto; la lista muestra el nombre de cada criatura y una consulta sin resultados presenta el estado vacío sin errores. Se muestra bien visualmente.

## A-03 · Se acepta un peligro inválido
### Síntoma
La ruta de actualización no habilitaba validadores de Mongoose, por lo que el rango del esquema no protegía el PUT. No se envió la petición antes del cambio.

### Causa
Faltaba `runValidators` en las opciones de `findByIdAndUpdate` de `backend/src/services/criaturas.service.ts`.

### Cambio
Se añadió `runValidators: true`; el manejador existente convierte errores de validación en 400. Commit: pendiente.

### Prueba
PUT con nivel 7 devolvió 200; PUT con 999 devolvió 400; GET confirmó que se conservaba 7. El valor original (2) fue restaurado y verificado.

### Estado
Resuelto y verificado por API. Commit: pendiente.

## A-04 · El filtro no actualiza la pantalla
### Síntoma
El cambio de selector modificaba `tipo`, pero el efecto de carga dependía solo de `recarga`; no consultaba hasta pulsar Actualizar lista. No se reprodujo visualmente antes del cambio.

### Causa
El array de dependencias en `frontend/src/paginas/ListaCriaturas.tsx` omitía `tipo`, que usa la consulta.

### Cambio
Se agregó `tipo` a las dependencias. Se conservan los estados de carga, error y vacío. Commit: pendiente.

### Prueba
La consulta API `tipo=mecanica` devolvió total 0 y el check/compilación pasan. Falta cambiar Todos → mitica → mecanica en la interfaz sin pulsar Actualizar lista y volver a Todos. La herramienta de control visual no pudo verificar la URL de la ventana y se detuvo; no se declara prueba visual.

### Estado
Se actualizan los tipos sin necesidad de estar presionando "Actualizar lista".
