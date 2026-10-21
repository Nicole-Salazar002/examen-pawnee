# Uso de IA
- Herramientas utilizadas: Codex (asistente de IA).
- Solicitud representativa: Revisar el enunciado y ayudar a corregir los cuatro reportes.
- Decisión técnica: se aplicaron cambios al payload del formulario, al `populate` de lecturas relacionadas, a los validadores de actualizaciones Mongoose y a las dependencias del filtro React. Se conservaron MongoDB, las validaciones y los flujos existentes.
- Verificación: `npm.cmd run check` y `npm.cmd run build` pasaron para ambos proyectos. A-01, A-02 y A-03 se comprobaron por API contra la base individual; el peligro original se restauró y el avistamiento temporal se eliminó. El checklist registra también las verificaciones visuales A-01, A-02 y A-04. No se compartieron URI, usuarios ni contraseñas.
