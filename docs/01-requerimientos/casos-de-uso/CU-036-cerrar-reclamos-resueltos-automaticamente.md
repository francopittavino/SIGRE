# CU-036 — Cerrar reclamos resueltos automáticamente

| Campo | Valor |
|---|---|
| **ID** | CU-036 |
| **Nombre** | Cerrar reclamos resueltos automáticamente |
| **Breve descripción** | Cierra automáticamente los reclamos que permanecen en estado "Resuelto" durante más de 7 días sin que su autor confirme la resolución ni los reabra. |
| **Prioridad** | Media |
| **Complejidad** | Baja |
| **Actor principal** | Tiempo (todos los días a las 00:00 hs) |
| **Actores secundarios** | — (el Servicio de Email participa a través de CU-038) |
| **Precondiciones** | — |
| **Postcondiciones** | **Éxito:** cada reclamo que llevaba más de 7 días en estado "Resuelto" queda en estado "Cerrado", con el cierre automático registrado en su historial. <br> **Fracaso:** no aplica; si no hay reclamos que cumplan la condición, no se realiza ningún cambio. |

## Flujo principal

1. El caso de uso comienza todos los días a las 00:00 hs.
2. El sistema busca los reclamos en estado "Resuelto" cuya fecha de paso a
   ese estado sea anterior en más de 7 días a la fecha actual.
3. Para cada reclamo obtenido en el paso anterior, el sistema:
   a. cambia el estado del reclamo a "Cerrado".
   b. registra en el historial del reclamo el cierre, con la fecha y hora,
      el autor "Sistema" y el motivo "Cierre automático: no se confirmó ni
      se reabrió en 7 días".
   c. include(Enviar notificación por email), con el aviso de cierre
      automático, dirigido al autor del reclamo y a sus adherentes.
4. Finaliza el caso de uso.

## Flujos alternativos

- **2.a No hay reclamos que cumplan la condición:**
  - 2.a.1 Finaliza el caso de uso.

## Flujos de excepción

Ninguno.

## Observaciones

- El plazo de 7 días es el mismo que se informa al residente cuando el
  administrador marca el reclamo como "Resuelto" (CU-032).
- Si el autor del reclamo fue dado de baja, el reclamo igualmente se
  cierra al cumplirse el plazo y el aviso se envía solo a los adherentes.
