# HABRO Installer 0.1.4

## Qué hace

- identifica la versión y arquitectura de Home Assistant;
- detecta los archivos de EBRO Auto y HABRO Companion;
- comprueba si Home Assistant ha cargado ambos dominios;
- muestra bloqueos con lenguaje comprensible;
- incorpora la base persistente y reanudable de la futura instalación, aislada en los datos propios de la app;
- incorpora inventario y backup verificable/restaurable de ambos componentes como módulo aislado, todavía sin ejecutarlo contra Home Assistant.

## Qué no hace todavía

No instala, actualiza, repara, elimina ni reinicia Home Assistant. La máquina de estados y el módulo de backup todavía no están conectados a la interfaz ni solicitan credenciales EBRO.

## Uso

Inicia la app y pulsa **Abrir interfaz web**. El informe se calcula de nuevo cada vez que recargas la pantalla.
