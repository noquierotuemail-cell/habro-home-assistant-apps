# Changelog

## 0.1.19

- Solo muestra la confirmación cuando el preflight físico sigue siendo válido.
- Si el preflight no terminó, conserva el bloqueo y ofrece reintentar la preparación.
- Registra únicamente la condición segura que impide el preflight, sin cabeceras ni secretos.

## 0.1.18

- Corrige la preparación guiada desde navegadores y la app móvil de Home Assistant.
- Mantiene el perímetro autenticado de Ingress y la protección CSRF.
- Conserva en pantalla el motivo seguro cuando una preparación no puede empezar.

