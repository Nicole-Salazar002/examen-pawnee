# Pruebas de API 2026-10-21

Pruebas realizadas contra la base individual `parcial_e3238` con el servidor local. No se guardaron URI, contraseñas, tokens ni cuerpos que contengan secretos.

## Diagnóstico de conexión

Desde `backend`, `npm run diagnostico` terminó correctamente: conexión `ok`, 3 criaturas y 4 avistamientos.

## A-01 Alta y referencia

- POST `/api/avistamientos` con una criatura existente y datos temporales: HTTP 201.
- GET `/api/avistamientos/:id`: el documento persistió y su referencia coincidió con la criatura seleccionada.
- POST con id de criatura inexistente: HTTP 404.
- Limpieza: se eliminó el avistamiento temporal mediante DELETE.

## A-02 Nombre de criatura en la lista

- GET `/api/avistamientos`: las referencias devueltas fueron objetos poblados con el nombre de la criatura.
- GET `/api/criaturas?tipo=mecanica`: total 0.
- La comprobación visual de la lista React queda pendiente.

## A-03 Validación del peligro

- PUT de `nivelPeligro: 7` para la criatura de prueba: HTTP 200.
- PUT de `nivelPeligro: 999`: HTTP 400.
- GET posterior al rechazo: el valor siguió en 7.
- Limpieza: se restauró el nivel original 2 y se verificó por GET.

## A-04 Filtro de React

- La consulta de API para `tipo=mecanica` devolvió total 0.
- `npm run check` y `npm run build` pasaron para backend y frontend.
- Falta comprobar en el navegador que el selector actualice la pantalla sin pulsar el botón.
