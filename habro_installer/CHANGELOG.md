# Changelog

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
