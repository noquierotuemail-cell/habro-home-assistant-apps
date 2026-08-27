# HABRO Installer 0.1.12

## Qué hace

- identifica la versión y arquitectura de Home Assistant;
- detecta los archivos de EBRO Auto y HABRO Companion;
- comprueba si Home Assistant ha cargado ambos dominios;
- muestra bloqueos con lenguaje comprensible;
- incorpora la base persistente y reanudable de la futura instalación, aislada en los datos propios de la app;
- incorpora inventario y backup verificable/restaurable de ambos componentes como módulo aislado, todavía sin ejecutarlo contra Home Assistant.
- incorpora descarga anónima, staging inmutable y validación completa de la publicación firmada como módulo aislado, todavía sin aplicarla a Home Assistant.
- incorpora preparación, intercambio atómico y rollback exacto de ambos componentes sobre una raíz nueva y aislada, todavía sin aplicarlos a Home Assistant.
- conecta inventario, backup, staging, commit conjunto y rollback en una transacción reanudable sobre raíces aisladas, todavía sin activarla desde la interfaz.
- construye en sandbox un candidato completo que sustituye solo los dos dominios HABRO y conserva byte a byte las demás integraciones, sin intercambiarlo con el destino activo.
- persiste y revalida la evidencia del candidato, lo intercambia de forma atómica en sandbox y ejecuta rollback exacto y reanudable ante fallos o interrupciones.
- coordina en un único sandbox inventario, backup, staging firmado, candidato completo, commit activo y rollback, con reanudación desde cada checkpoint sin repetir una mutación ya confirmada.
- incorpora una capacidad de escritura persistente, inmutable y denegada por defecto, ligada a la transacción, publicación, hashes y destino exactos; todavía no la activa desde la interfaz.
- separa preparación y aprobación, liga la capacidad al coordinador inmediatamente antes de crear el candidato y prueba la operación completa sobre una réplica exacta de `/homeassistant/custom_components`.

## Qué no hace todavía

No instala, actualiza, repara, elimina ni reinicia Home Assistant. La ruta autorizada permanece montada en solo lectura y la transacción con capacidad se ejecuta únicamente sobre réplicas de prueba; no está conectada a la interfaz ni solicita credenciales EBRO.

## Uso

Inicia la app y pulsa **Abrir interfaz web**. El informe se calcula de nuevo cada vez que recargas la pantalla.
