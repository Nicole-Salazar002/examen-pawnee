# Uso de IA
- Herramientas utilizadas: Codex (asistente de IA).
- Solicitud representativa: Revisar el enunciado y ayudar a corregir los cuatro reportes.
- Decisión técnica: se aplicaron cambios al payload del formulario, al `populate` de lecturas relacionadas, a los validadores de actualizaciones Mongoose y a las dependencias del filtro React. Se conservaron MongoDB, las validaciones y los flujos existentes.
- Verificación: `npm.cmd run check` y `npm.cmd run build` pasaron para ambos proyectos. Se probó a: A-01, A-02 y A-03 por API contra la base individual, restauré el peligro original y eliminé el avistamiento temporal. A-04 quedó verificado por API y compilación; su comprobación visual sigue pendiente.
- No se comparte información importante cómo MONGODB_URI, usuarios, contraseñas, etc.
