# HABRO Installer

App experimental para diagnosticar la preparación de una instalación HABRO sobre Home Assistant OS.

Home Assistant continúa montado estrictamente en solo lectura: esta versión no instala, actualiza, elimina ni reinicia componentes. La transacción integral conecta journal, backup, staging y commit conjunto únicamente sobre raíces aisladas; todavía no está conectada a la interfaz.
