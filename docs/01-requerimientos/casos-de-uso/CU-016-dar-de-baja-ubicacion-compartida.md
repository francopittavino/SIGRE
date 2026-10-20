# CU-016 — Dar de baja ubicación compartida

| Campo | Valor |
|---|---|
| **ID** | CU-016 |
| **Nombre** | Dar de baja ubicación compartida |
| **Breve descripción** | Permite al administrador dar de baja en forma definitiva un área común o instalación compartida que ya no existe, conservando sus reclamos e historial. |
| **Prioridad** | Baja |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. <br> La ubicación compartida seleccionada está en estado "Activa". |
| **Postcondiciones** | **Éxito:** la ubicación compartida queda en estado "Dada de baja", con la fecha y el administrador que la realizó registrados, y deja de estar disponible para registrar reclamos. <br> **Fracaso:** la ubicación compartida permanece en estado "Activa". |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Dar de baja"
   sobre una ubicación compartida seleccionada.
2. El sistema valida que la ubicación no tenga reclamos abiertos, es
   decir, en un estado distinto de "Cerrado", "Rechazado" o "Cancelado".
3. El sistema muestra el mensaje "¿Confirmás la baja de la ubicación
   *nombre*? La baja es definitiva. Sus reclamos e historial se
   conservarán" y los botones "Confirmar baja" y "Cancelar".
4. El administrador presiona "Confirmar baja".
5. El sistema registra la baja de la ubicación con la fecha y el
   administrador que la realizó, y muestra el mensaje "La ubicación
   *nombre* fue dada de baja".

## Flujos alternativos

- **2.a La ubicación tiene reclamos abiertos:**
  - 2.a.1 El sistema muestra el mensaje "No se puede dar de baja la
    ubicación *nombre* porque tiene *N* reclamo(s) abierto(s)".
  - 2.a.2 El administrador presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.

## Flujos de excepción

- En el paso 3 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema no realiza ningún cambio y finaliza el caso de
  uso.

## Observaciones

- La baja es definitiva: no existe la reactivación de ubicaciones
  compartidas. Si vuelve a existir, se registra una nueva con "Agregar
  ubicación compartida" (CU-014), que puede reutilizar el nombre.
- Los reclamos y el historial de la ubicación dada de baja se conservan y
  pueden consultarse desde "Consultar historial de ubicación" (CU-034).
