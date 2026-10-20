# CU-020 — Dar de baja rubro

| Campo | Valor |
|---|---|
| **ID** | CU-020 |
| **Nombre** | Dar de baja rubro |
| **Breve descripción** | Permite al administrador dar de baja en forma definitiva un rubro que ya no se utiliza, conservando la categorización de los reclamos históricos. |
| **Prioridad** | Baja |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. <br> El rubro seleccionado está en estado "Activo". |
| **Postcondiciones** | **Éxito:** el rubro queda en estado "Dado de baja", con la fecha y el administrador que la realizó registrados, y deja de estar disponible para categorizar reclamos y para la sugerencia automática. <br> **Fracaso:** el rubro permanece en estado "Activo". |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Dar de baja"
   sobre un rubro seleccionado.
2. El sistema valida que el rubro no tenga reclamos abiertos, es decir, en
   un estado distinto de "Cerrado", "Rechazado" o "Cancelado".
3. El sistema muestra el mensaje "¿Confirmás la baja del rubro *nombre*?
   La baja es definitiva. Los reclamos ya categorizados con este rubro lo
   conservarán" y los botones "Confirmar baja" y "Cancelar".
4. El administrador presiona "Confirmar baja".
5. El sistema registra la baja del rubro con la fecha y el administrador
   que la realizó, y muestra el mensaje "El rubro *nombre* fue dado de
   baja".

## Flujos alternativos

- **2.a El rubro tiene reclamos abiertos:**
  - 2.a.1 El sistema muestra el mensaje "No se puede dar de baja el rubro
    *nombre* porque tiene *N* reclamo(s) abierto(s). Recategorizalos
    primero".
  - 2.a.2 El administrador presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.

## Flujos de excepción

- En el paso 3 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema no realiza ningún cambio y finaliza el caso de
  uso.

## Observaciones

- La baja es definitiva: no existe la reactivación de rubros. Si vuelve a
  necesitarse, se registra uno nuevo con "Agregar rubro" (CU-018), que
  puede reutilizar el nombre.
- Los reclamos cerrados, rechazados o cancelados conservan el rubro dado
  de baja, para que el historial y los reportes sigan siendo correctos.
