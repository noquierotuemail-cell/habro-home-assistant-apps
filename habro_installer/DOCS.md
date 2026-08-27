# HABRO Installer 0.1.8

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

## Qué no hace todavía

No instala, actualiza, repara, elimina ni reinicia Home Assistant. La transacción y el candidato de destino activo permanecen aislados, no están conectados a la interfaz ni solicitan credenciales EBRO.

## Uso

Inicia la app y pulsa **Abrir interfaz web**. El informe se calcula de nuevo cada vez que recargas la pantalla.
