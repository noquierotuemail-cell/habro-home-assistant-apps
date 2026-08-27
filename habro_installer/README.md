# HABRO Installer

App experimental para diagnosticar la preparación de una instalación HABRO sobre Home Assistant OS.

Home Assistant continúa montado estrictamente en solo lectura: esta versión no instala, actualiza, elimina ni reinicia componentes. La transacción con autorización persistente, candidato completo y commit/rollback reanudable se prueba únicamente sobre una réplica exacta del destino; todavía no está conectada a la interfaz.
