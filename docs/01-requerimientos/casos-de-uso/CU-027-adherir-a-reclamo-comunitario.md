# CU-027 — Adherir a reclamo comunitario

| Campo | Valor |
|---|---|
| **ID** | CU-027 |
| **Nombre** | Adherir a reclamo comunitario |
| **Breve descripción** | Permite a un residente sumarse a un reclamo comunitario registrado por otro residente, lo que aumenta su prioridad y le permite seguir su evolución. |
| **Prioridad** | Alta |
| **Complejidad** | Media |
| **Actor principal** | Residente |
| **Actores secundarios** | — |
| **Precondiciones** | El residente tiene una sesión iniciada en el sistema. <br> El residente tiene al menos una unidad vinculada. |
| **Postcondiciones** | **Éxito:** la adhesión del residente queda registrada con su fecha y hora, la prioridad del reclamo queda recalculada y el residente pasa a recibir las notificaciones de cambio de estado del reclamo. <br> **Fracaso:** no se registra la adhesión. |

## Flujo principal

1. El caso de uso comienza cuando el residente presiona "Adherir" sobre un
   reclamo comunitario seleccionado.
2. El sistema valida que:
   - el reclamo esté en estado "Ingresado", "Asignado", "En curso",
     "Esperando repuesto/tercero" o "Reabierto".
   - el residente no sea el autor del reclamo.
   - el residente no haya adherido ya al reclamo.
3. El sistema muestra el mensaje "¿Querés adherir al reclamo N° *número*
   — *título*? Vas a recibir por email los cambios de estado" y los
   botones "Adherir" y "Volver".
4. El residente presiona "Adherir".
5. El sistema registra la adhesión con la fecha y hora y recalcula la
   prioridad del reclamo: la prioridad asignada sube un nivel por cada 3
   adhesiones, con tope "Urgente".
6. Si la prioridad cambió, el sistema registra el cambio en el historial
   del reclamo, con la fecha y hora y el motivo "Aumento por adhesiones".
7. El sistema muestra el mensaje "Adheriste al reclamo N° *número*. Ya son
   *N* residentes adheridos".

## Flujos alternativos

- **2.a No se cumple alguna de las condiciones:**
  - 2.a.1 El sistema muestra el mensaje correspondiente: "El reclamo ya no
    admite adhesiones", "No podés adherir a un reclamo que registraste" o
    "Ya adheriste a este reclamo".
  - 2.a.2 El residente presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.

## Flujos de excepción

- En el paso 3 el residente puede presionar "Volver". El sistema no
  realiza ningún cambio y finaliza el caso de uso.

## Observaciones

- La prioridad de un reclamo es la asignada por el administrador (o la
  base "Media" si todavía no fue categorizado) más un nivel por cada 3
  adhesiones. Por ejemplo, un reclamo de prioridad "Baja" con 6 adhesiones
  queda en "Alta".
- Las adhesiones no se retiran a pedido del residente; solo se retiran
  cuando el residente es dado de baja (CU-008).
