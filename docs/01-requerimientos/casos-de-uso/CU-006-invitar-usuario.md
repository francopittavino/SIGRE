# CU-006 — Invitar usuario

| Campo | Valor |
|---|---|
| **ID** | CU-006 |
| **Nombre** | Invitar usuario |
| **Breve descripción** | Permite al administrador invitar por email a una persona para que ocupe el rol de propietario o inquilino de una unidad. Si la persona ya tiene cuenta, la unidad se asocia directamente a esa cuenta. |
| **Prioridad** | Alta |
| **Complejidad** | Media |
| **Actor principal** | Administrador |
| **Actores secundarios** | — (el Servicio de Email participa a través de CU-038) |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** queda registrada una invitación pendiente, con el rol de la unidad reservado y el email de invitación enviado, o bien la unidad queda asociada con el rol indicado a la cuenta existente. <br> **Fracaso:** no se registra ninguna invitación ni asociación. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Invitar
   usuario".
2. El sistema muestra los siguientes campos a completar:
   - Email: campo de texto, obligatorio, formato de email válido, máximo
     254 caracteres.
   - Rol: lista desplegable, obligatoria, con las opciones "Propietario" e
     "Inquilino".
   - Unidad: lista desplegable, obligatoria. Contiene las unidades activas
     en las que el rol seleccionado no tiene un usuario asignado ni una
     invitación pendiente. Si el rol es "Inquilino", contiene además solo
     las unidades que tienen propietario (activo o con invitación
     pendiente) y cuyo propietario no reside en ella. De cada unidad se
     muestra su identificador, ordenadas por identificador. Si ninguna
     unidad cumple las condiciones, la lista muestra "No hay unidades
     disponibles para el rol seleccionado".
   - Reside en la unidad: casilla de verificación, opcional, desmarcada por
     defecto. Solo se muestra si el rol es "Propietario".

   Debajo se muestra el botón "Enviar invitación".
3. El administrador completa los campos y presiona "Enviar invitación".
4. El sistema valida que los campos cumplan con el formato requerido.
5. El sistema valida que el email no pertenezca a un usuario dado de baja.
6. El sistema valida que el email no tenga otra invitación pendiente.
7. El sistema valida que el email no corresponda a una cuenta que ya tenga
   otro rol en la unidad seleccionada.
8. El sistema busca una cuenta activa registrada con el email ingresado.
   - Si no existe, el sistema:
     a. registra la invitación con la unidad, el rol y, si corresponde, la
        indicación de que el propietario reside en la unidad. La
        invitación es válida por 7 días.
     b. reserva el rol de la unidad para la invitación.
     c. include(Enviar notificación por email), con el enlace para
        completar el registro.
     d. muestra el mensaje "Invitación enviada a *email*. Vence el
        *dd/mm/aaaa*".
   - Si existe, el sistema:
     a. asocia la unidad a la cuenta con el rol indicado y, si
        corresponde, la indicación de que el propietario reside en la
        unidad.
     b. include(Enviar notificación por email), con el aviso "Se te asoció
        la unidad *identificador* como *rol*".
     c. muestra el mensaje "El usuario ya tenía una cuenta: se le asoció
        la unidad *identificador* como *rol*".

## Flujos alternativos

- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.
- **5.a El email pertenece a un usuario dado de baja:**
  - 5.a.1 El sistema muestra el mensaje "El email pertenece a un usuario
    dado de baja. Para asociarle una unidad, reactivalo primero desde
    'Usuarios'" y vuelve al paso 2.
- **6.a El email tiene una invitación pendiente:**
  - 6.a.1 El sistema muestra el mensaje "El email ya tiene una invitación
    pendiente. Podrás asociarle otra unidad cuando complete su registro" y
    vuelve al paso 2.
- **7.a La cuenta ya tiene otro rol en la unidad seleccionada:**
  - 7.a.1 El sistema muestra el mensaje "El usuario ya es *rol* de esa
    unidad" y vuelve al paso 2.

## Flujos de excepción

- En el paso 2 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema descarta los datos ingresados y finaliza el caso
  de uso.

## Observaciones

- La invitación es por una sola unidad. Para un propietario con varias
  unidades, se lo invita por la primera y, una vez que completa su
  registro (CU-004), las demás se asocian a su cuenta repitiendo este caso
  de uso.
- Un propietario que vive en su unidad no se invita además como inquilino:
  se usa la indicación "Reside en la unidad". Esa indicación puede
  cambiarse después desde "Modificar unidad" (CU-011).
- Las invitaciones no se reenvían ni se anulan; al vencer, liberan el rol
  reservado (ver CU-005).
