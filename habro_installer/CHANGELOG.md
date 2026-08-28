# Changelog

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

