# CU-004 — Completar registro

| Campo | Valor |
|---|---|
| **ID** | CU-004 |
| **Nombre** | Completar registro |
| **Breve descripción** | Permite a una persona invitada por el administrador crear su cuenta, con sus datos personales y una contraseña, y quedar asociada a la unidad y el rol indicados en la invitación. |
| **Prioridad** | Alta |
| **Complejidad** | Media |
| **Actor principal** | Residente invitado |
| **Actores secundarios** | — |
| **Precondiciones** | El invitado no tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** se crea la cuenta del usuario, queda asociada a la unidad con el rol indicado en la invitación (propietario o inquilino), la invitación queda utilizada y se inicia la sesión del usuario. <br> **Fracaso:** no se crea la cuenta y la invitación conserva su estado. |

## Flujo principal

1. El caso de uso comienza cuando el invitado abre el enlace de invitación
   recibido por email.
2. El sistema valida que la invitación exista, no haya sido utilizada ni
   anulada y no tenga más de 7 días desde su envío.
3. El sistema muestra en solo lectura el email, la unidad y el rol de la
   invitación, y debajo los siguientes campos a completar:
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
   - Contraseña: campo de contraseña, obligatorio, entre 8 y 64
     caracteres, con al menos una letra y un número.
   - Confirmar contraseña: campo de contraseña, obligatorio, debe
     coincidir con la contraseña.

   Debajo se muestra el botón "Registrarme".
4. El invitado completa los campos y presiona "Registrarme".
5. El sistema valida que los campos cumplan con el formato requerido.
6. El sistema valida que no exista otra cuenta registrada con el mismo
   tipo y número de documento.
7. El sistema crea la cuenta, la asocia a la unidad con el rol indicado en
   la invitación, marca la invitación como utilizada, inicia la sesión del
   usuario y muestra la pantalla de inicio con el mensaje "¡Bienvenido/a a
   SIGRE!".

## Flujos alternativos

- **2.a La invitación no existe, ya fue utilizada, fue anulada o venció:**
  - 2.a.1 El sistema muestra el mensaje "La invitación no es válida o
    venció. Pedí a la administración que te envíe una nueva".
  - 2.a.2 El invitado presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.
- **5.a La validación de formato falla:**
  - 5.a.1 El sistema vuelve al paso 3. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.
- **6.a Ya existe una cuenta con ese documento:**
  - 6.a.1 El sistema muestra el mensaje "El documento ingresado ya está
    registrado. Comunicate con la administración" y vuelve al paso 3.

## Flujos de excepción

- En el paso 3 el invitado puede cancelar la operación presionando
  "Cancelar". El sistema no guarda ningún dato, la invitación sigue vigente
  y finaliza el caso de uso.

## Observaciones

- El email, la unidad y el rol los define el administrador en "Invitar
  usuario" (CU-006) y el invitado no puede modificarlos.
- Si el email invitado ya tenía una cuenta, este caso de uso no se
  ejecuta: la unidad se asocia directamente a esa cuenta en CU-006.
- Mientras una invitación está pendiente, el rol de esa unidad queda
  reservado y no se puede invitar a otra persona para ocuparlo (se valida
  en CU-006).
- El tipo y número de documento no pueden ser modificados por el usuario
  después del registro; solo el administrador puede hacerlo (CU-007).
- Las reglas de contraseña y de datos personales son las mismas que en
  CU-002 y CU-003.
