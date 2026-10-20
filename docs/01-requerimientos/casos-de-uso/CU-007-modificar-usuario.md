# CU-007 — Modificar usuario

| Campo | Valor |
|---|---|
| **ID** | CU-007 |
| **Nombre** | Modificar usuario |
| **Breve descripción** | Permite al administrador corregir los datos personales de un usuario, desvincularlo de sus unidades y reiniciar su contador de solicitudes de recuperación de contraseña. |
| **Prioridad** | Media |
| **Complejidad** | Media |
| **Actor principal** | Administrador |
| **Actores secundarios** | — (el Servicio de Email participa a través de CU-038) |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. <br> El usuario seleccionado está en estado "Activo". |
| **Postcondiciones** | **Éxito:** quedan registrados los cambios realizados: datos personales, unidades desvinculadas y contador de solicitudes de recuperación reiniciado, según corresponda. Si se modificó el email, se cierran las sesiones abiertas del usuario. <br> **Fracaso:** no se modifica ningún dato del usuario. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Modificar"
   sobre un usuario seleccionado.
2. El sistema muestra los datos actuales del usuario en los siguientes
   campos editables:
   - Tipo de documento: lista desplegable, obligatoria, con las opciones
     "DNI" y "Pasaporte".
   - Número de documento: campo de texto, obligatorio. Si el tipo es DNI,
     solo dígitos, 7 u 8 caracteres. Si el tipo es Pasaporte, solo letras
     y dígitos, entre 6 y 15 caracteres.
   - Nombre: campo de texto, obligatorio, máximo 50 caracteres; solo
     letras, espacios, apóstrofo y guion.
   - Apellido: campo de texto, obligatorio, máximo 50 caracteres; solo
     letras, espacios, apóstrofo y guion.
   - Teléfono: campo de texto, obligatorio, entre 8 y 20 caracteres; solo
     dígitos, espacios, "+" y "-".
   - Email: campo de texto, obligatorio, formato de email válido, máximo
     254 caracteres.

   Debajo muestra:
   - La sección "Unidades": para cada unidad vinculada al usuario, su
     identificador, el rol del usuario en ella y una casilla de
     verificación "Desvincular", desmarcada por defecto.
   - La sección "Recuperación de contraseña": el texto "Solicitudes en el
     mes en curso: *N* de 5" y una casilla de verificación "Reiniciar
     contador", desmarcada por defecto y habilitada solo si *N* es mayor
     que 0.

   Al final se muestra el botón "Guardar".
3. El administrador modifica los datos que desea y presiona "Guardar".
4. El sistema valida que los campos cumplan con el formato requerido.
5. Si se modificó el tipo o número de documento, el sistema valida que no
   exista otra cuenta con el mismo tipo y número de documento.
6. Si se modificó el email, el sistema valida que no esté registrado por
   otra cuenta, activa o dada de baja.
7. Para cada unidad marcada para desvincular en la que el usuario es
   propietario, el sistema valida que la unidad no tenga un inquilino
   vinculado ni una invitación pendiente de inquilino.
8. El sistema guarda los datos personales, desvincula al usuario de las
   unidades marcadas y, si se marcó "Reiniciar contador", pone en 0 el
   contador de solicitudes de recuperación del mes en curso.
9. Si se modificó el email, el sistema cierra las sesiones abiertas del
   usuario e include(Enviar notificación por email), con un aviso del
   cambio, dirigido al email anterior y al nuevo.
10. Si se desvinculó alguna unidad, include(Enviar notificación por email),
    con un aviso de las unidades de las que el usuario fue desvinculado.
11. El sistema muestra el mensaje "Los datos del usuario fueron
    actualizados".

## Flujos alternativos

- **3.a No se modificó ningún dato:**
  - 3.a.1 El sistema muestra el mensaje "No hay cambios para guardar" y
    vuelve al paso 2.
- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.
- **5.a Ya existe otra cuenta con ese documento:**
  - 5.a.1 El sistema muestra el mensaje "El documento ingresado ya está
    registrado en otra cuenta" y vuelve al paso 2 sin guardar ningún dato.
- **6.a El email ya está registrado por otra cuenta:**
  - 6.a.1 El sistema muestra el mensaje "El email ingresado no está
    disponible" y vuelve al paso 2 sin guardar ningún dato.
- **7.a Una unidad a desvincular tiene inquilino:**
  - 7.a.1 El sistema muestra el mensaje "No se puede desvincular al
    propietario de la unidad *identificador* porque tiene un inquilino
    vinculado o invitado. Desvinculá primero al inquilino" y vuelve al
    paso 2 sin guardar ningún dato.

## Flujos de excepción

- En el paso 2 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema descarta los cambios y finaliza el caso de uso.

## Observaciones

- Desvincular no borra información: los reclamos que el usuario registró
  sobre esa unidad y su historial se conservan. El usuario sigue viendo los
  reclamos que él mismo registró, pero no los que se registren después
  sobre esa unidad. El nuevo inquilino no ve los reclamos registrados
  antes de su llegada; el nuevo propietario sí, porque el propietario actual ve
  todo el historial de su unidad (ver CU-024).
- Un usuario puede quedar sin unidades vinculadas y sigue pudiendo iniciar
  sesión para consultar sus reclamos anteriores. Para impedirle el acceso
  se lo da de baja (CU-008).
- El cambio de email realizado por el administrador se aplica sin
  confirmación; se avisa a ambas casillas para que el usuario pueda
  detectar un error.
