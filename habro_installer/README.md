# HABRO Installer

Desde 0.1.52, cuando EBRO Auto está correcto y cargado pero falta HABRO Companion, la interfaz ofrece una instalación directa. Verifica el paquete firmado, publica únicamente `ebro_remoteapp` y reinicia Home Assistant Core; no reemplaza EBRO Auto ni el resto de `custom_components`.

Desde 0.1.47, el diagnóstico es también la autorización obligatoria de la preparación: solo `repair_available` y `update_available` pueden preparar la transacción existente. `ready`, configuración incompleta, diagnóstico insuficiente o bloqueo no escriben. La persona mantiene una única confirmación antes de aplicar la mutación activa.

Desde 0.1.46, el diagnóstico incorpora el clasificador de la Fase 7. Distingue una instalación lista, configuración incompleta, reparación, actualización, continuación, rollback, reintento y bloqueo. La clasificación es de solo lectura: esta versión no añade acciones de reparación. Una versión posterior compatible nunca se degrada al paquete anterior del Installer.

App experimental para diagnosticar, preparar e instalar de forma transaccional HABRO sobre Home Assistant OS.

La preparación comienza automáticamente al abrir Ingress, pero no modifica los componentes activos. La sustitución conjunta de EBRO Auto y HABRO Companion solo se ejecuta tras una confirmación visible y queda restringida por código a `/homeassistant/custom_components`. Desde 0.1.30, esa confirmación inicia un recorrido reanudable que instala EBRO Auto 1.0.1 y HABRO Companion 0.3.32, reinicia exclusivamente Home Assistant Core, verifica el código persistente y completa o restaura sin controles técnicos adicionales. Antes del reinicio, Installer muestra la ruta exacta para volver a su interfaz si Home Assistant cierra el WebView; al reabrirla, la verificación continúa sin repetir la instalación. Al terminar, una única acción abre el config flow oficial de EBRO; las credenciales nunca pasan por HABRO Installer y EBRO encadena Companion con la entrada exacta.

Para completar ese recorrido declara el rol mínimo `homeassistant` de Supervisor. Este rol permite consultar, comprobar y reiniciar Core, pero no concede acceso a backups, host, red, sistema operativo, otras apps ni administración del Supervisor.

La respuesta inicial de Ingress es una pantalla estática y completa. El estado persistido, la evidencia segura y el diagnóstico se cargan después para que una verificación física lenta nunca impida abrir la interfaz.

Desde 0.1.31, la interfaz mantiene visible qué está haciendo HABRO, pide conservar abierta la pantalla y explica el siguiente paso esperado. Mientras una operación está activa no presenta el estado `idle` ni sugiere repetirla; **Reintentar preparación** solo aparece después de un fallo real y seguro.

Desde 0.1.33, la Web UI consulta el estado cada pocos segundos durante operaciones largas, mantiene ocultos los pasos técnicos y avisa de que el reinicio y la verificación pueden tardar hasta 10 minutos.

Desde 0.1.32, una reinstalación puede reconocer una única copia de rollback huérfana de una transacción anterior sin ignorar las protecciones del destino. La preparación verifica su ruta, huella y contenido ajeno sin modificarla; su retirada atómica y reanudable solo ocurre dentro de la misma confirmación visible. Las transacciones nuevas eliminan su rollback después de completar la verificación para que una desinstalación posterior del Installer no vuelva a dejar ese estado.


Desde 0.1.42, la continuación posterior al reinicio pertenece al proceso del Installer y no al navegador: un trabajador interno consulta la API documentada de Home Assistant y completa o restaura el journal después de verificar el árbol instalado aunque el WebView se haya cerrado. Solo los errores transitorios 502/503/504 permanecen en espera.
