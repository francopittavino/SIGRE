# CU-026 — Cancelar reclamo

| Campo | Valor |
|---|---|
| **ID** | CU-026 |
| **Nombre** | Cancelar reclamo |
| **Breve descripción** | Permite al residente que registró un reclamo cancelarlo mientras todavía no fue tomado por la administración. |
| **Prioridad** | Media |
| **Complejidad** | Baja |
| **Actor principal** | Residente |
| **Actores secundarios** | — |
| **Precondiciones** | El residente tiene una sesión iniciada en el sistema. <br> El residente es el autor del reclamo seleccionado. |
| **Postcondiciones** | **Éxito:** el reclamo queda en estado "Cancelado" y la cancelación queda registrada en el historial del reclamo, con la fecha y hora, el autor y el motivo, si se indicó. <br> **Fracaso:** el reclamo conserva su estado. |

## Flujo principal

1. El caso de uso comienza cuando el residente presiona "Cancelar reclamo"
   sobre un reclamo seleccionado.
2. El sistema valida que el reclamo esté en estado "Ingresado".
3. El sistema valida que el reclamo no tenga adhesiones.
4. El sistema muestra el mensaje "¿Confirmás la cancelación del reclamo
   N° *número*? Esta acción no puede deshacerse". Debajo muestra el
   siguiente campo y los botones "Confirmar cancelación" y "Volver":
   - Motivo: área de texto, opcional, máximo 500 caracteres.
5. El residente presiona "Confirmar cancelación".
6. El sistema valida que el motivo cumpla con el formato requerido.
7. El sistema cambia el estado del reclamo a "Cancelado" y registra en el
   historial del reclamo la cancelación, con la fecha y hora, el autor y
   el motivo, si se indicó.
8. include(Enviar notificación por email), con el aviso de cancelación y
   el motivo, si se indicó, dirigido al administrador.
9. El sistema muestra el mensaje "El reclamo N° *número* fue cancelado".

## Flujos alternativos

- **2.a El reclamo no está en estado "Ingresado":**
  - 2.a.1 El sistema muestra el mensaje "El reclamo ya fue tomado por la
    administración y no puede cancelarse. Si ya no es necesario, avisá
    con un comentario".
  - 2.a.2 El residente presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.
- **3.a El reclamo tiene adhesiones:**
  - 3.a.1 El sistema muestra el mensaje "El reclamo tiene adhesiones de
    otros residentes y no puede cancelarse".
  - 3.a.2 El residente presiona "Aceptar".
  - 3.a.3 Finaliza el caso de uso.
- **6.a El motivo supera los 500 caracteres:**
  - 6.a.1 El sistema vuelve al paso 4. Debajo del campo se muestra la
    regla que no se cumple.

## Flujos de excepción

- En el paso 4 el residente puede presionar "Volver". El sistema no
  realiza ningún cambio y finaliza el caso de uso.

## Observaciones

- Un reclamo con adhesiones no se cancela porque afecta a otros
  residentes; mismo criterio que en la baja de usuario (CU-008).
- "Cancelado" es un estado final: el reclamo no puede reabrirse.
- La cancelación solo se notifica al administrador: como el reclamo no
  tiene adhesiones y todavía no fue categorizado, no hay otros
  interesados.
