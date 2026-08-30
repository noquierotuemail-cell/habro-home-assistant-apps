# HABRO Installer 0.1.44

## Qué hace

- cierra la configuración con un estado inequívoco: solicita EBRO Auto solo si falta, ofrece completar Companion si EBRO ya está cargado y muestra **HABRO está listo** cuando ambos están operativos.
- mantiene una URL estable y versionada para el JavaScript, recupera WebViews que conserven una huella histórica válida y renderiza el estado persistido desde el servidor; incluso sin JavaScript, una instalación completada muestra **Configurar HABRO**.
- muestra el avance durante operaciones largas, serializa los sondeos con la instalación y, si otra sesión posee el paso, espera mediante consultas de solo lectura sin repetir la escritura;
- identifica la versión y arquitectura de Home Assistant;
- detecta los archivos de EBRO Auto y HABRO Companion;
- comprueba si Home Assistant ha cargado ambos dominios;
- muestra bloqueos con lenguaje comprensible;
- incorpora la base persistente y reanudable de la futura instalación, aislada en los datos propios de la app;
- ejecuta inventario y backup verificable/restaurable de ambos componentes antes de modificar el destino.
- descarga anónimamente, prepara un staging inmutable y valida completamente la publicación firmada.
- prepara un candidato completo y usa intercambio atómico y rollback exacto sobre el destino autorizado.
- conecta inventario, backup, staging, commit conjunto y rollback en una única transacción reanudable.
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
- comprueba la configuración, persiste una solicitud ligada al journal y pide una sola vez a Supervisor el reinicio de Home Assistant Core.
- usa el rol mínimo `homeassistant` de Supervisor para consultar y reiniciar únicamente Core; no recibe permisos de backup, host, red, sistema operativo, apps ni administración.
- verifica de forma reanudable la API documentada de Core, el recibo aceptado, las versiones autorizadas y el árbol activo exacto antes de completar el journal; no exige configurar las integraciones antes de mostrar **Configurar HABRO**.
- mantiene un trabajador interno que reanuda la verificación o el rollback posterior al reinicio aunque no haya un navegador abierto; el WebView se limita a observar el journal.
- conecta ambas etapas al recorrido guiado: tras la única confirmación, HABRO continúa, reinicia exclusivamente Core, espera su regreso, verifica la instalación y completa o restaura sin controles técnicos adicionales. Antes del reinicio muestra la ruta exacta **Ajustes → Aplicaciones → HABRO Installer → Abrir interfaz web** por si Home Assistant cierra el WebView; al volver, la operación se recupera sin repetir ninguna acción.
- reconoce una única copia de rollback huérfana de otra transacción solo cuando su ruta es canónica y conserva exactamente el contenido ajeno a HABRO; la preparación no la modifica y su retirada queda incluida en la confirmación visible.
- retira las copias de recuperación mediante una cuarentena atómica reanudable y elimina el rollback de las transacciones nuevas únicamente después de verificar el estado `completed`.

## Qué no hace todavía

Después de instalar y verificar los componentes, muestra **Configurar HABRO**, que abre el config flow oficial de EBRO en Home Assistant. Las credenciales se introducen únicamente allí; HABRO Installer no las lee, almacena ni registra. EBRO Auto 1.0.1 inicia después el flujo de HABRO Companion 0.3.31 con el `entry_id` exacto. El montaje de configuración es escribible porque Home Assistant no ofrece un montaje limitado a un subdirectorio, pero la única ruta admitida por el código transaccional es `/homeassistant/custom_components`.

## Uso

Inicia la app y pulsa **Abrir interfaz web**. La pantalla abre primero y calcula después el diagnóstico y el estado persistido. Confirma una sola vez cuando la operación esté preparada; si se ha validado una copia de recuperación anterior, su retirada segura forma parte de esa misma autorización. Si Home Assistant deja de mostrar la pantalla durante el reinicio, espera a que vuelva y entra en **Ajustes → Aplicaciones → HABRO Installer → Abrir interfaz web**. La verificación se reanuda dentro del propio Installer incluso con el WebView cerrado; volver a la pantalla solo permite observar el resultado. No pulses instalar ni reintentar. Al terminar, pulsa **Configurar HABRO** e introduce las credenciales EBRO en el formulario oficial de Home Assistant. Si existe una operación exportable, la evidencia segura aparece en su propio bloque.
