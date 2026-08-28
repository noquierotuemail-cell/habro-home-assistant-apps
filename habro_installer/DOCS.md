# HABRO Installer 0.1.24

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
- persiste y revalida un preflight de solo lectura del destino exacto: permisos, montaje, dispositivo, espacio, topología, API atómica y ausencia de cambios concurrentes.
- incorpora una única operación reanudable con bloqueo entre procesos y una política HTTP que exige el gateway y la ruta autenticada de Ingress, CSRF y JSON acotado; ambos contratos permanecen desconectados de la interfaz.
- conecta la operación a una interfaz guiada con preparación, aprobación, ejecución y rollback separados. La aplicación solo construye como destino `/homeassistant/custom_components` y revalida la capacidad y el preflight inmediatamente antes de mutar.
- inicia automáticamente el diagnóstico y la preparación al abrir la interfaz; la única acción humana dentro de HABRO antes del reinicio es la confirmación comprensible posterior a todas las verificaciones. Los pasos internos permanecen separados, y un rollback pendiente se reanuda sin exponer controles técnicos.
- admite navegadores y WebViews autenticados de Home Assistant con metadatos de origen distintos o ausentes; sigue exigiendo gateway y ruta Ingress, CSRF, JSON y límite de cuerpo, y rechaza solicitudes marcadas como `cross-site`.
- usa `renameat2(RENAME_EXCHANGE)` mediante el wrapper de libc o la syscall Linux fijada para `aarch64` y `amd64`, y mantiene el bloqueo seguro si el kernel o la arquitectura no son compatibles.
- cuando la transacción alcanza `restart_pending` o `rolled_back`, vuelve a verificar journal, backup, staging y destino y muestra una evidencia copiable sin identificadores internos, rutas ni secretos.
- entrega una pantalla Ingress completa antes de calcular el diagnóstico o verificar la evidencia transaccional; después carga ambos resultados en segundo plano sin bloquear la apertura.
- sirve el JavaScript por la ruta exacta de Ingress, sin parámetros de consulta, y registra de forma segura cuándo termina cada respuesta HTTP.

## Qué no hace todavía

No reinicia Home Assistant ni configura las integraciones. El montaje de configuración es escribible porque Home Assistant no ofrece un montaje limitado a un subdirectorio, pero la única ruta admitida por el código transaccional es `/homeassistant/custom_components`. La preparación automática no modifica los componentes activos; la sustitución requiere una aprobación visible y no solicita credenciales EBRO.

## Uso

Inicia la app y pulsa **Abrir interfaz web**. La pantalla abre primero y calcula después el diagnóstico y el estado persistido. Si existe una operación exportable, la evidencia segura aparece en su propio bloque, sin necesidad de abrir la información de diagnóstico.
