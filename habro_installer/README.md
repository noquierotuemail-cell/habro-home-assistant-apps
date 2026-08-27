# HABRO Installer

App experimental para diagnosticar la preparación de una instalación HABRO sobre Home Assistant OS.

Home Assistant continúa montado estrictamente en solo lectura: esta versión no instala, actualiza, elimina ni reinicia componentes. El journal transaccional y el almacén aislado de backups se limitan a `/data`, el almacenamiento propio de la app, y todavía no están conectados a la interfaz.
