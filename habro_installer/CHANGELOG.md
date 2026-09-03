# Changelog

## 0.1.49

- Sustituye «Preparando HABRO» por «Estado de HABRO», válido tanto durante la comprobación como al finalizar.
- Cuando EBRO Auto y HABRO Companion ya están cargados, muestra un único resultado «HABRO está listo» sin repetir una segunda tarjeta.


## 0.1.48

- Depura los errores visibles del diagnóstico para no exponer tokens, rutas privadas ni detalles internos.
- Rechaza y oculta versiones de manifest no válidas en lugar de mostrarlas en el informe.
- Verifica en una matriz de interfaz los ocho estados de la Fase 7 y su única continuación segura.


## 0.1.47

- Conecta la decisión de la Fase 7 con la preparación transaccional existente y mantiene una única confirmación explícita antes de modificar los componentes activos.
- Impide preparar archivos cuando el sistema está listo, solo necesita configuración, falta evidencia o existe un bloqueo.
- Bloquea cualquier reparación o actualización conjunta que degradaría un componente más reciente.


## 0.1.46

- Inicia la Fase 7 con un clasificador puro que distingue sistema listo, configuración incompleta, reparación, actualización, reanudación, rollback, reintento y bloqueo.
- Acepta versiones posteriores dentro de la misma línea compatible y prohíbe degradarlas; Companion 0.3.35 no se sustituye por el paquete 0.3.32 del Installer.
- Publica la decisión como parte de `habro.installation_report.v2`, sin añadir todavía endpoints ni acciones de reparación.


## 0.1.45

- Publica la versión firmada `2026.08.30.1`: conserva EBRO Auto 1.0.1 y actualiza HABRO Companion a 0.3.32 con el nombre público HABRO.
- Conserva como publicaciones históricas autorizadas 0.3.30 y 0.3.31 para que una operación ya completada pueda avanzar sin perder su journal ni repetir credenciales.
- Alinea la confirmación del Installer, la documentación y las pruebas con la versión que realmente instala.

## 0.1.44

- Cierra el recorrido según el estado real de Home Assistant: **Configurar EBRO Auto**, **Completar HABRO Companion** o **HABRO está listo**.
- Evita volver a pedir credenciales cuando EBRO Auto y HABRO Companion ya están cargados, y comunica expresamente que no queda ninguna acción pendiente.
- Añade pruebas del cierre para las tres combinaciones de configuración y conserva la selección explícita cuando existe ambigüedad.

## 0.1.43

- Mantiene una URL estable y versionada para `installer.js` y acepta huellas históricas estrictamente validadas, de modo que una WebView conservada por Home Assistant no quede sin JavaScript tras actualizar la app.
- Renderiza desde el servidor el estado persistido de la operación —incluido el resultado completado y la acción **Configurar HABRO**— para que el recorrido no dependa de que JavaScript llegue a arrancar.
- Sustituye la ruta obsoleta de regreso por **Ajustes → Aplicaciones → HABRO Installer → Abrir interfaz web** y añade pruebas para HTML sin JavaScript, activos antiguos y nombres de activo malformados.

## 0.1.42

- Sustituye la comprobación redundante de Supervisor por la API de Core documentada y exige que Home Assistant responda con una versión válida antes de verificar el árbol instalado.
- Reintenta únicamente errores transitorios de arranque (`502`, `503` y `504`); un rechazo permanente deja de presentarse como una espera infinita.
- Reanuda la verificación y, si hiciera falta, el rollback desde un trabajador interno del Installer, aunque el WebView del móvil esté cerrado o no envíe ninguna petición.

## 0.1.41

- Antes de confirmar y mientras se instala, muestra una guía destacada con la ruta exacta para volver tras el reinicio: **Ajustes → Aplicaciones → HABRO Installer → Abrir interfaz web**.
- Explica que el avance queda guardado y que volver a la interfaz solo reanuda la consulta; no hay que repetir la instalación ni pulsar otra vez ningún botón.
- Al recuperar Home Assistant, confirma **Has vuelto al lugar correcto** y oculta la guía de regreso mientras completa automáticamente la verificación final.

## 0.1.40

- Registra antes del reinicio los trabajos existentes del Supervisor y reconoce después un nuevo trabajo `home_assistant_core_restart` como prueba persistente de que la solicitud fue entregada, incluso si la conexión HTTP se pierde.
- Recupera de forma compatible los recibos 0.1.39 que quedaron en `prepared`: si el reinicio ya está ejecutándose continúa sin repetirlo; en caso contrario migra el recibo y realiza una única solicitud controlada.
- Devuelve el estado ocupado como una instantánea de solo lectura con `200`, sin ejecutar sondas costosas; la Web UI cancela acciones automáticas y se limita a consultar hasta que cambie el journal.
- Reserva la generación de evidencia exportable para estados terminales y evita que un fallo de presentación o hashing oculte un resultado ya verificado y persistido.
- Reduce a 30 segundos la espera de la respuesta síncrona del reinicio y registra el inicio de cada operación para distinguir una petición activa de una pantalla detenida.

## 0.1.39

- Serializa las consultas de estado con la misma exclusión mutua de la instalación, evitando que el sondeo revalide y rehaga hashes del árbol completo mientras se materializa el candidato.
- Cuando otra sesión posee la operación, devuelve `operation_busy` de inmediato y la Web UI espera mediante consultas de solo lectura; no vuelve a enviar `execute`.
- Ante una respuesta de escritura perdida, recupera primero el estado persistido y solo reanuda el siguiente paso autorizado después de confirmar que el propietario anterior terminó.

## 0.1.38

- Sirve el cliente de la Web UI desde un nombre de archivo derivado de su contenido, sin parámetros de consulta, para impedir que Home Assistant reutilice un JavaScript anterior.
- Mantiene oculto el reloj hasta que el cliente real ha arrancado y comprueba que avanza de 10:00 a 09:59.
- Permite preparar automáticamente una actualización desde una instalación terminal perteneciente a una publicación histórica autorizada, sin exigir que su staging antiguo siga disponible.
- Reintenta automáticamente la consulta de estado ante indisponibilidades transitorias, sin pedir al usuario que recargue o repita la operación.

## 0.1.37

- Versiona la URL de `installer.js` para impedir que Home Assistant o su WebView combinen el HTML nuevo con un JavaScript anterior almacenado en caché.
- Conserva la ruta anterior por compatibilidad, pero la Web UI carga siempre el activo exacto de 0.1.37 con `Cache-Control: no-store`.
- Garantiza que la cuenta atrás visible de 10:00 se actualice cada segundo al abrir esta versión.

## 0.1.36

- Muestra una cuenta atrás visible desde 10:00 durante la preparación y durante el recorrido de instalación, reinicio y verificación.
- Indica expresamente que el plazo es orientativo y puede alcanzar 10 minutos; al superarlo, muestra el tiempo excedido sin declarar un fallo ni permitir repetir la operación.
- Oculta el reloj en estados que requieren una acción del usuario o cuando la operación ya ha terminado.

## 0.1.35

- Muestra que HABRO está verificando el historial seguro y preparando la actualización mientras releva una transacción terminal anterior.
- Oculta el paso de configuración completada durante ese relevo para no presentar un éxito antiguo como resultado de la actualización actual.
- Conserva sin cambios la validación histórica exacta, el archivo persistente del journal y la reparación segura 0.3.30 → 0.3.31 introducidos en 0.1.34.

## 0.1.34

- Verifica las evidencias terminales de publicaciones anteriores únicamente contra la política firmada exacta con la que se instalaron.
- Archiva de forma persistente el journal y el recibo de reinicio de una transacción terminal verificada antes de preparar una publicación posterior.
- Permite que una instalación 2026.08.29.1 ya completada continúe de forma segura: vuelve a verificar y publicar EBRO Auto 1.0.1 junto con la actualización de HABRO Companion 0.3.30 → 0.3.31, sin perder el historial.
- Mantiene bloqueados los recibos desconocidos, las versiones no permitidas y cualquier transacción que todavía no sea terminal.

## 0.1.33

- Publica la versión firmada `2026.08.29.2`: conserva EBRO Auto 1.0.1 y actualiza HABRO Companion a 0.3.31.
- Evita que la consulta remota opcional de la entidad de actualización bloquee el arranque de HABRO Companion.
- Mantiene oculto el paso técnico de ejecución tras «Confirmar e instalar» y reintenta automáticamente si Home Assistant devuelve un conflicto transitorio.
- Consulta el estado en segundo plano mientras una operación larga sigue abierta, de modo que la Web UI refleja el reinicio y la verificación sin quedarse visualmente congelada.
- Muestra tiempo transcurrido y avisa de que el reinicio y la verificación pueden tardar hasta 10 minutos; si se supera ese tiempo, pide no repetir la instalación y conservar la evidencia segura.

## 0.1.32

- Recupera de forma segura una única copia de rollback huérfana dejada por una instalación anterior, incluso si HABRO Installer se desinstaló y perdió su journal propio.
- Mantiene la preparación en solo lectura: comprueba nombre canónico, huella completa y contenido ajeno antes de incluir la retirada en la misma confirmación visible de instalación.
- Retira el rollback mediante una cuarentena atómica y reanudable; cualquier ruta ambigua, múltiple o con contenido ajeno distinto continúa bloqueando la operación.
- Finaliza las nuevas transacciones eliminando su rollback únicamente después de alcanzar `completed`, sin perder la verificación estable frente a bytecode de ejecución.
- Explica en la pantalla qué ocurrirá con una copia anterior y recuerda mantenerla abierta, pulsar una sola vez y esperar la continuación automática.

## 0.1.31

- Muestra de forma persistente qué está haciendo HABRO, qué debe esperar la persona y cuál será el siguiente paso.
- Indica no cerrar, recargar ni volver a iniciar HABRO Installer durante preparación, instalación, reinicio, verificación o restauración.
- Evita que una preparación en curso vuelva a mostrar el mensaje `idle` y reserva **Reintentar preparación** para un fallo real y seguro.
- No cambia la transacción, los permisos, los paquetes firmados ni la única confirmación de escritura visible.

## 0.1.30

- Autoriza exclusivamente la publicación firmada 2026.08.29.1: EBRO Auto 1.0.1 y HABRO Companion 0.3.30, con orígenes y URLs exactos.
- Conserva instalación limpia, actualización desde 1.0.0/0.3.29, reparación, reinicio, verificación y rollback bajo la misma transacción reanudable.
- Tras completar la verificación muestra una única acción **Configurar HABRO**, que abre el config flow oficial de EBRO fuera de Ingress.
- HABRO Installer no solicita, lee, guarda ni registra credenciales; EBRO Auto encadena HABRO Companion mediante el `entry_id` exacto.
- Mantiene `boot: manual_only`, el rol mínimo `homeassistant` y la única confirmación de escritura visible.

## 0.1.29

- Corrige el smoke físico de 0.1.28: `/core/check` importó los componentes y creó bytecode bajo `__pycache__`, que la huella del árbol completo interpretó como una alteración del código.
- Verifica una proyección estable que excluye únicamente `.pyc` válidos ligados a su fuente `.py`; cualquier otro archivo, enlace o caché mal formada continúa bloqueando la operación.
- Reconstruye el candidato desde staging, rollback y plan persistidos antes de aceptar esa proyección, sin confiar en el árbol activo por sí solo.
- Recupera automáticamente el journal físico `failed` solo cuando coinciden el historial exacto, el recibo del único reinicio, los artefactos persistentes y el código activo normalizado.

## 0.1.28

- Corrige el smoke físico de 0.1.27: la comprobación válida de Home Assistant tardó más de 30 segundos y HABRO la canceló antes de que Supervisor respondiera.
- Usa plazos explícitos de 180 segundos para los trabajos de comprobación y reinicio de Core, manteniendo la exclusión mutua de la operación.
- Registra únicamente la operación fija y el estado HTTP ante un rechazo de Supervisor, sin exponer su cuerpo ni datos internos.

## 0.1.27

- Conecta instalación, reinicio de Home Assistant Core y verificación posterior mediante un único recorrido reanudable.
- Declara el rol mínimo `homeassistant` de Supervisor; no concede permisos de backup, host, red, sistema operativo, apps ni administración.
- Añade una continuación automática protegida por Ingress y CSRF, sin mostrar un segundo botón ni repetir el reinicio.
- Reintenta mientras Core arranca y ejecuta rollback automático únicamente ante una discrepancia determinista de la evidencia.
- Bloquea redirecciones y limita destinos, tiempo y tamaño al consultar Supervisor después del reinicio.

## 0.1.26

- Añade la verificación reanudable posterior al reinicio sin conectarla todavía a Ingress.
- Exige respuesta coherente de Supervisor y de la API de Core, recibo aceptado, versiones autorizadas y árbol activo exacto.
- Solo entonces avanza el journal a `completed`; una indisponibilidad o discrepancia conserva `verifying_after_restart`.

## 0.1.25

- Añade el contrato aislado para comprobar la configuración y solicitar un único reinicio de Home Assistant Core.
- Persiste un recibo privado ligado a la transacción y a la revisión exacta del journal antes de llamar a Supervisor.
- Si la confirmación del reinicio es ambigua, bloquea la repetición automática en vez de arriesgar un segundo reinicio.
- No conecta todavía el reinicio a la API, la interfaz ni el Green.

## 0.1.24

- Entrega primero una pantalla Ingress completa sin esperar diagnóstico, hashes ni verificación transaccional.
- Carga después el estado, la evidencia segura y el diagnóstico sin bloquear la apertura de la interfaz.
- Añade una prueba HTTP real que impide volver a acoplar la respuesta inicial a operaciones lentas.
- Registra cuándo cada respuesta HTTP ha terminado de escribirse, sin incluir cabeceras ni secretos.

## 0.1.23

- Restaura la ruta exacta `installer.js` compatible con Ingress.
- Conserva la evidencia renderizada en el HTML inicial sin depender de una consulta de versión.
- Mantiene la transacción en `restart_pending` sin repetir ninguna escritura.

## 0.1.22

- Renderiza la evidencia segura desde el servidor para que no dependa del JavaScript del WebView.
- Versiona el activo de la interfaz y conserva una evidencia verificada durante el refresco.
- Mantiene Home Assistant sin reiniciar y no repite ninguna etapa de la transacción.

## 0.1.21

- Verifica de nuevo journal, backup, staging y destino sin repetir la transacción.
- Muestra un informe copiable limitado a estados, versiones, recuentos y SHA-256.
- Excluye UUID internos, rutas, fechas, URLs, archivos, cabeceras, tokens y credenciales.

## 0.1.20

- Corrige el preflight en Alpine/musl cuando libc no exporta `renameat2`.
- Usa la syscall Linux fijada para `aarch64` y `amd64` sin sustituir `RENAME_EXCHANGE` por una secuencia no atómica.
- Mantiene el bloqueo seguro ante arquitectura, kernel o filesystem no compatibles.

## 0.1.19

- Solo muestra la confirmación cuando el preflight físico sigue siendo válido.
- Si el preflight no terminó, conserva el bloqueo y ofrece reintentar la preparación.
- Registra únicamente la condición segura que impide el preflight, sin cabeceras ni secretos.

## 0.1.18

- Corrige la preparación guiada desde navegadores y la app móvil de Home Assistant.
- Mantiene el perímetro autenticado de Ingress y la protección CSRF.
- Conserva en pantalla el motivo seguro cuando una preparación no puede empezar.
