# CU-012 — Dar de baja unidad

| Campo | Valor |
|---|---|
| **ID** | CU-012 |
| **Nombre** | Dar de baja unidad |
| **Breve descripción** | Permite al administrador dar de baja en forma definitiva una unidad que ya no existe o no debe seguir operando en el sistema, conservando sus reclamos e historial. |
| **Prioridad** | Baja |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. <br> La unidad seleccionada está en estado "Activa". |
| **Postcondiciones** | **Éxito:** la unidad queda en estado "Dada de baja", con la fecha y el administrador que la realizó registrados. Deja de estar disponible para invitar usuarios y para registrar reclamos. <br> **Fracaso:** la unidad permanece en estado "Activa". |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Dar de baja"
   sobre una unidad seleccionada.
2. El sistema valida que la unidad no tenga usuarios vinculados ni
   invitaciones pendientes.
3. El sistema valida que la unidad no tenga reclamos abiertos, es decir,
   en un estado distinto de "Cerrado", "Rechazado" o "Cancelado".
4. El sistema muestra el mensaje "¿Confirmás la baja de la unidad
   *identificador*? La baja es definitiva. Sus reclamos e historial se
   conservarán" y los botones "Confirmar baja" y "Cancelar".
5. El administrador presiona "Confirmar baja".
6. El sistema registra la baja de la unidad con la fecha y el
   administrador que la realizó, y muestra el mensaje "La unidad
   *identificador* fue dada de baja".

## Flujos alternativos

- **2.a La unidad tiene usuarios vinculados o invitaciones pendientes:**
  - 2.a.1 El sistema muestra el mensaje "No se puede dar de baja la unidad
    *identificador* porque tiene usuarios vinculados o invitaciones
    pendientes. Desvinculá primero a sus usuarios".
  - 2.a.2 El administrador presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.
- **3.a La unidad tiene reclamos abiertos:**
  - 3.a.1 El sistema muestra el mensaje "No se puede dar de baja la unidad
    *identificador* porque tiene *N* reclamo(s) abierto(s)".
  - 3.a.2 El administrador presiona "Aceptar".
  - 3.a.3 Finaliza el caso de uso.

## Flujos de excepción

- En el paso 4 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema no realiza ningún cambio y finaliza el caso de
  uso.

## Observaciones

- La baja es definitiva: no existe la reactivación de unidades. Si la
  unidad vuelve a existir, se registra una nueva con "Agregar unidad"
  (CU-010), que puede reutilizar el identificador.
- Los reclamos y el historial de la unidad dada de baja se conservan y
  pueden consultarse desde "Consultar historial de ubicación" (CU-034).
