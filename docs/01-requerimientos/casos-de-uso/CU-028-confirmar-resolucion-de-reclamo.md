# CU-028 — Confirmar resolución de reclamo

| Campo | Valor |
|---|---|
| **ID** | CU-028 |
| **Nombre** | Confirmar resolución de reclamo |
| **Breve descripción** | Permite al residente que registró un reclamo confirmar que el problema fue resuelto, dando el reclamo por cerrado. |
| **Prioridad** | Alta |
| **Complejidad** | Baja |
| **Actor principal** | Residente |
| **Actores secundarios** | — (el Servicio de Email participa a través de CU-038) |
| **Precondiciones** | El residente tiene una sesión iniciada en el sistema. <br> El residente es el autor del reclamo seleccionado. |
| **Postcondiciones** | **Éxito:** el reclamo queda en estado "Cerrado" y el cierre queda registrado en el historial del reclamo con la fecha y hora y el autor. <br> **Fracaso:** el reclamo conserva su estado. |

## Flujo principal

1. El caso de uso comienza cuando el residente presiona "Confirmar
   resolución" sobre un reclamo seleccionado.
2. El sistema valida que el reclamo esté en estado "Resuelto".
3. El sistema muestra el mensaje "¿Confirmás que el problema del reclamo
   N° *número* fue resuelto? El reclamo se cerrará y no podrá reabrirse"
   y los botones "Confirmar" y "Volver".
4. El residente presiona "Confirmar".
5. El sistema cambia el estado del reclamo a "Cerrado" y registra en el
   historial del reclamo el cierre, con la fecha y hora y el autor.
6. include(Enviar notificación por email), con el aviso de cierre,
   dirigido al administrador y a los adherentes del reclamo.
7. El sistema muestra el mensaje "El reclamo N° *número* fue cerrado.
   ¡Gracias por confirmar!".

## Flujos alternativos

- **2.a El reclamo no está en estado "Resuelto":**
  - 2.a.1 El sistema muestra el mensaje "El reclamo no está pendiente de
    confirmación".
  - 2.a.2 El residente presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.

## Flujos de excepción

- En el paso 3 el residente puede presionar "Volver". El sistema no
  realiza ningún cambio y finaliza el caso de uso.

## Observaciones

- Solo el autor del reclamo confirma la resolución; los adherentes reciben
  el aviso pero no confirman.
- Si el autor no confirma ni reabre el reclamo dentro de los 7 días de
  marcado como "Resuelto", el sistema lo cierra automáticamente (CU-036).
- "Cerrado" es un estado final: si el problema vuelve a aparecer, se
  registra un reclamo nuevo.
