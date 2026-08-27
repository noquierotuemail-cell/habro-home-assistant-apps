# HABRO Installer

App experimental para diagnosticar la preparación de una instalación HABRO sobre Home Assistant OS.

Home Assistant continúa montado estrictamente en solo lectura: esta versión no instala, actualiza, elimina ni reinicia componentes. La transacción integral, el candidato completo y su commit/rollback reanudable se prueban únicamente sobre raíces aisladas; todavía no están conectados a la interfaz.
