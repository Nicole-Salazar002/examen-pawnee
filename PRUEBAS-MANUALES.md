# Verificación manual · Versión A

## A-01
- [✓] El formulario crea el registro (201) y abre su detalle.
- [✓] GET y recarga confirman persistencia y asociación a la criatura elegida.
- [✓] Una referencia inexistente por cliente HTTP devuelve 404 sin crear un registro.

## A-02
- [✓] Cada avistamiento semilla muestra el nombre de su criatura, no solo el id.
- [✓] Respuesta API y uso del dato en React tienen una forma coherente.
- [✓] Una consulta sin resultados muestra vacío, no una pantalla rota.

## A-03
- [✓] Un valor válido como 7 se guarda con status 200.
- [✓] El valor 999 se rechaza con 400 y mensaje comprensible.
- [✓] Un GET después del rechazo conserva el último valor válido.

## A-04
- [✓] El cambio de selector inicia la consulta correcta y actualiza datos.
- [✓] Se distinguen loading, error y empty; mecanica está vacío en la semilla.
- [✓] Volver a Todos restaura el listado sin actualización manual.

## Recorrido integrado final
1. Consultar criaturas y cambiar filtro por tipo.
2. Actualizar criatura con peligro válido.
3. Registrar avistamiento desde el formulario.
4. Ver listado con nombre de criatura.
5. Recargar y comprobar persistencia.
6. Rechazar peligro 999 y comprobar dato anterior.

## Loading, error y empty
Puedes usar throttling en DevTools para observar carga. Detén únicamente TU backend, cambia la consulta y observa el error; vuelve a iniciarlo y reintenta. No desconectes la red del aula ni modifiques permisos Atlas.

## Regresión
Crear una criatura válida sigue funcionando. Un id bien formado inexistente devuelve 404. Comprobar una operación que funcionaba antes de corregir, con datos descartables.
Si aparece un fallo no intencional ajeno a los reportes, informa al docente; no se convierte automáticamente en otra tarea evaluable.

- MongoDB no funcionaba adecuadamente en un inicio. [✓]
- Se fue el internet. :D [✓]