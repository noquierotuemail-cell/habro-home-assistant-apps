# Changelog

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
