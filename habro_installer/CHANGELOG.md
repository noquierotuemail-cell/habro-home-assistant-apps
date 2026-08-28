# Changelog

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
