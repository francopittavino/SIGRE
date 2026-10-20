# CU-003 — Modificar datos de perfil

| Campo | Valor |
|---|---|
| **ID** | CU-003 |
| **Nombre** | Modificar datos de perfil |
| **Breve descripción** | Permite al usuario actualizar sus datos personales, su email (con confirmación) y su contraseña. |
| **Prioridad** | Media |
| **Complejidad** | Baja |
| **Actor principal** | Usuario |
| **Actores secundarios** | — (el Servicio de Email participa a través de CU-038) |
| **Precondiciones** | El usuario tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** los datos modificados quedan registrados. Si cambió la contraseña, se cierran las demás sesiones abiertas de la cuenta. Si cambió el email, el cambio queda pendiente y se aplica cuando el usuario lo confirma. <br> **Fracaso:** no se modifica ningún dato del usuario. |

## Flujo principal

1. El caso de uso comienza cuando el usuario presiona "Mi perfil".
2. El sistema muestra los datos actuales del usuario en los siguientes
   campos:
   - Tipo de documento: solo lectura.
   - Número de documento: solo lectura.
   - Nombre: campo de texto, obligatorio, máximo 50 caracteres; solo
     letras, espacios, apóstrofo y guion.
   - Apellido: campo de texto, obligatorio, máximo 50 caracteres; solo
     letras, espacios, apóstrofo y guion.
   - Teléfono: campo de texto, obligatorio, entre 8 y 20 caracteres; solo
     dígitos, espacios, "+" y "-".
   - Email: campo de texto, obligatorio, formato de email válido, máximo
     254 caracteres.

   Debajo muestra la sección opcional "Cambiar contraseña", con los
   siguientes campos (si se completa alguno, los tres pasan a ser
   obligatorios):
   - Contraseña actual: campo de contraseña.
   - Nueva contraseña: campo de contraseña, entre 8 y 64 caracteres, con
     al menos una letra y un número.
   - Confirmar contraseña: campo de contraseña, debe coincidir con la
     nueva contraseña.

   Al final se muestra el botón "Guardar".
3. El usuario modifica los datos que desea y presiona "Guardar".
4. El sistema valida que los campos cumplan con el formato requerido.
5. Si se completó la sección "Cambiar contraseña", el sistema valida que
   la contraseña actual sea correcta.
6. Si se modificó el email, el sistema valida que no esté registrado por
   otra cuenta.
7. El sistema guarda nombre, apellido y teléfono. Si se completó la
   sección "Cambiar contraseña", guarda la nueva contraseña y cierra las
   demás sesiones abiertas de la cuenta.
8. Si se modificó el email, el sistema:
   a. genera un enlace de confirmación de un solo uso, válido por 30
      minutos.
   b. include(Enviar notificación por email), con el enlace de
      confirmación, dirigido al email nuevo.
   c. include(Enviar notificación por email), con un aviso de que se
      solicitó el cambio de email, dirigido al email actual.
9. El sistema muestra el mensaje "Tus datos fueron actualizados". Si se
   modificó el email, agrega: "Te enviamos un enlace a *email nuevo* para
   confirmar el cambio. Hasta entonces seguís usando tu email actual".
10. El usuario abre el enlace recibido en el email nuevo.
11. El sistema valida que el enlace exista, no haya sido usado y no esté
    vencido.
12. El sistema reemplaza el email de la cuenta por el nuevo, inutiliza el
    enlace y muestra el mensaje "Tu email fue actualizado".

## Flujos alternativos

- **3.a El usuario no modificó ningún dato:**
  - 3.a.1 El sistema muestra el mensaje "No hay cambios para guardar" y
    vuelve al paso 2.
- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.
- **5.a La contraseña actual es incorrecta:**
  - 5.a.1 El sistema muestra el mensaje "La contraseña actual es
    incorrecta" y vuelve al paso 2 sin guardar ningún dato.
- **6.a El email ya está registrado por otra cuenta:**
  - 6.a.1 El sistema muestra el mensaje "El email ingresado no está
    disponible" y vuelve al paso 2 sin guardar ningún dato.
- **11.a El enlace no existe, ya fue usado o está vencido:**
  - 11.a.1 El sistema muestra el mensaje "El enlace no es válido o venció.
    Tu email no fue modificado".
  - 11.a.2 El usuario presiona "Aceptar".
  - 11.a.3 Finaliza el caso de uso.

## Flujos de excepción

- En el paso 2 el usuario puede cancelar la operación presionando
  "Cancelar". El sistema descarta los cambios y finaliza el caso de uso.

## Observaciones

- El tipo y número de documento no son editables por el usuario; solo el
  administrador puede modificarlos desde "Modificar usuario" (CU-007).
- El cambio de email se confirma desde la casilla nueva para asegurar que
  el usuario tiene acceso a ella. El aviso al email actual permite detectar
  un cambio no autorizado.
- El caso de uso tiene dos momentos cuando se modifica el email: la
  modificación (pasos 1 a 9) y la confirmación (pasos 10 a 12), que puede
  ocurrir hasta 30 minutos después.
- Las reglas de contraseña son las mismas que en CU-002 y CU-004.
