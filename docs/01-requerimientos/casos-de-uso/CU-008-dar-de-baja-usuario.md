# CU-008 — Dar de baja usuario

| Campo | Valor |
|---|---|
| **ID** | CU-008 |
| **Nombre** | Dar de baja usuario |
| **Breve descripción** | Permite al administrador dar de baja a un usuario: el usuario pierde el acceso al sistema y se lo desvincula de sus unidades. La baja puede revertirse reactivando al usuario. |
| **Prioridad** | Media |
| **Complejidad** | Media |
| **Actor principal** | Administrador |
| **Actores secundarios** | — (el Servicio de Email participa a través de CU-038) |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. <br> El usuario seleccionado está en estado "Activo". |
| **Postcondiciones** | **Éxito:** el usuario queda en estado "Dado de baja", con el motivo, la fecha y el administrador que la realizó registrados. Además, queda desvinculado de todas sus unidades, sus sesiones quedan cerradas, sus reclamos en estado "Ingresado" sin adhesiones pasan a "Cancelado" y sus adhesiones a reclamos comunitarios quedan retiradas. <br> **Fracaso:** el usuario permanece en estado "Activo" y no se modifica ningún dato. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Dar de baja"
   sobre un usuario seleccionado.
2. El sistema valida que, en las unidades donde el usuario es propietario,
   no haya un inquilino vinculado ni una invitación pendiente de
   inquilino.
3. El sistema muestra el mensaje "¿Confirmás la baja de *nombre y
   apellido*? El usuario perderá el acceso al sistema y será desvinculado
   de sus unidades". Debajo muestra el siguiente campo y los botones
   "Confirmar baja" y "Cancelar":
   - Motivo: área de texto, obligatoria, entre 10 y 500 caracteres.
4. El administrador completa el motivo y presiona "Confirmar baja".
5. El sistema valida que el motivo cumpla con el formato requerido.
6. El sistema:
   a. registra la baja del usuario con el motivo, la fecha y el
      administrador que la realizó.
   b. cierra todas las sesiones abiertas del usuario.
   c. desvincula al usuario de todas sus unidades.
   d. para cada reclamo registrado por el usuario que está en estado
      "Ingresado" y no tiene adhesiones, cambia el estado a "Cancelado" y
      lo registra en el historial del reclamo con el motivo "Baja del
      usuario".
   e. retira todas las adhesiones del usuario a reclamos comunitarios.
7. include(Enviar notificación por email), con el aviso de la baja,
   dirigido al usuario.
8. El sistema muestra el mensaje "El usuario fue dado de baja".

## Flujos alternativos

- **2.a El usuario es propietario de una unidad con inquilino:**
  - 2.a.1 El sistema muestra el mensaje "No se puede dar de baja a *nombre
    y apellido* porque es propietario de la unidad *identificador*, que
    tiene un inquilino vinculado o invitado. Desvinculá primero al
    inquilino".
  - 2.a.2 El administrador presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.
- **5.a El motivo no cumple con el formato requerido:**
  - 5.a.1 El sistema vuelve al paso 3. Debajo del campo se muestra la
    regla que no se cumple.

## Flujos de excepción

- En el paso 3 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema no realiza ningún cambio y finaliza el caso de
  uso.

## Observaciones

- La baja puede revertirse con "Reactivar usuario" (CU-039). La
  reactivación no restituye las unidades, los reclamos cancelados ni las
  adhesiones retiradas.
- Los reclamos del usuario que no se cancelan (los que no están en
  "Ingresado" y los "Ingresado" con adhesiones) siguen su curso y el
  administrador los sigue gestionando. Al usuario dado de baja ya no se le
  envían notificaciones.
- Al retirar sus adhesiones, se recalcula la prioridad de los reclamos
  comunitarios afectados.
- Los reclamos registrados por el usuario y su historial se conservan.
