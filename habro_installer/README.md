# HABRO Installer

App experimental para diagnosticar, preparar e instalar de forma transaccional HABRO sobre Home Assistant OS.

La preparación comienza automáticamente al abrir Ingress, pero no modifica los componentes activos. La sustitución conjunta de EBRO Auto y HABRO Companion solo se ejecuta tras una confirmación visible y queda restringida por código a `/homeassistant/custom_components`. Desde 0.1.29, esa confirmación inicia un recorrido reanudable que instala, reinicia exclusivamente Home Assistant Core, verifica el código persistente sin confundirlo con bytecode derivado y completa o restaura sin controles técnicos adicionales. Todavía no configura las cuentas ni crea entradas de integración.

Para completar ese recorrido declara el rol mínimo `homeassistant` de Supervisor. Este rol permite consultar, comprobar y reiniciar Core, pero no concede acceso a backups, host, red, sistema operativo, otras apps ni administración del Supervisor.

La respuesta inicial de Ingress es una pantalla estática y completa. El estado persistido, la evidencia segura y el diagnóstico se cargan después para que una verificación física lenta nunca impida abrir la interfaz.
