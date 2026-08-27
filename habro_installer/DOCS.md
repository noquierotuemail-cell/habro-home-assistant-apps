# HABRO Installer 0.1.7

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

## Qué no hace todavía

No instala, actualiza, repara, elimina ni reinicia Home Assistant. La transacción aislada todavía no está conectada a la interfaz ni solicita credenciales EBRO.

## Uso

Inicia la app y pulsa **Abrir interfaz web**. El informe se calcula de nuevo cada vez que recargas la pantalla.
