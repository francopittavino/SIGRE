# CU-039 — Reactivar usuario

| Campo | Valor |
|---|---|
| **ID** | CU-039 |
| **Nombre** | Reactivar usuario |
| **Breve descripción** | Permite al administrador devolver el acceso al sistema a un usuario dado de baja. |
| **Prioridad** | Baja |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — (el Servicio de Email participa a través de CU-038) |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. <br> El usuario seleccionado está en estado "Dado de baja". |
| **Postcondiciones** | **Éxito:** el usuario queda en estado "Activo", sin unidades vinculadas, y la reactivación queda registrada con la fecha y el administrador que la realizó. <br> **Fracaso:** el usuario permanece en estado "Dado de baja". |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Reactivar"
   sobre un usuario seleccionado.
2. El sistema muestra el mensaje "¿Confirmás la reactivación de *nombre y
   apellido*? El usuario podrá volver a iniciar sesión con su contraseña
   anterior. Sus unidades no se restituyen: asocialas desde 'Invitar
   usuario'" y los botones "Confirmar" y "Cancelar".
3. El administrador presiona "Confirmar".
4. El sistema cambia el estado del usuario a "Activo" y registra la
   reactivación con la fecha y el administrador que la realizó.
5. include(Enviar notificación por email), con el aviso de la
   reactivación, dirigido al usuario.
6. El sistema muestra el mensaje "El usuario fue reactivado".

## Flujos alternativos

Ninguno.

## Flujos de excepción

- En el paso 2 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema no realiza ningún cambio y finaliza el caso de
  uso.

## Observaciones

- La reactivación no restituye las unidades, los reclamos cancelados ni
  las adhesiones retiradas al momento de la baja. Para volver a vincular
  unidades se usa "Invitar usuario" (CU-006), que asocia la unidad
  directamente a la cuenta existente.
- El usuario conserva sus datos personales y su contraseña anterior; si no
  la recuerda, puede usar "Recuperar contraseña" (CU-002).
