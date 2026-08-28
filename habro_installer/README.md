# HABRO Installer

App experimental para diagnosticar, preparar e instalar de forma transaccional HABRO sobre Home Assistant OS.

La preparación comienza automáticamente al abrir Ingress, pero no modifica los componentes activos. La sustitución conjunta de EBRO Auto y HABRO Companion solo se ejecuta tras una confirmación visible y queda restringida por código a `/homeassistant/custom_components`. Esta versión todavía no reinicia Home Assistant ni configura las integraciones.

La respuesta inicial de Ingress es una pantalla estática y completa. El estado persistido, la evidencia segura y el diagnóstico se cargan después para que una verificación física lenta nunca impida abrir la interfaz.
