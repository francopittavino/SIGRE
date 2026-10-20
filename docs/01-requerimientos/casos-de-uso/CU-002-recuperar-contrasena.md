# CU-002 — Recuperar contraseña

| Campo | Valor |
|---|---|
| **ID** | CU-002 |
| **Nombre** | Recuperar contraseña |
| **Breve descripción** | Permite a un usuario que olvidó su contraseña definir una nueva, a través de un enlace de un solo uso que recibe por email. |
| **Prioridad** | Alta |
| **Complejidad** | Media |
| **Actor principal** | Usuario |
| **Actores secundarios** | — (el Servicio de Email participa a través de CU-038) |
| **Precondiciones** | El usuario no tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** la contraseña de la cuenta queda reemplazada por la nueva, el enlace queda inutilizado y se cierran todas las sesiones abiertas de la cuenta. <br> **Fracaso:** la contraseña de la cuenta no se modifica. |

## Flujo principal

1. El caso de uso comienza cuando el usuario presiona "¿Olvidaste tu
   contraseña?" en la pantalla de inicio de sesión.
2. El sistema muestra el siguiente campo y, debajo, el botón "Enviar
   enlace":
   - Email: campo de texto, obligatorio, formato de email válido, máximo
     254 caracteres.
3. El usuario completa el email y presiona "Enviar enlace".
4. El sistema valida que el campo esté completo y con el formato
   requerido.
5. El sistema busca una cuenta activa registrada con el email ingresado.
6. El sistema valida que la cuenta no haya realizado ya 5 solicitudes de
   recuperación en el mes calendario en curso.
7. El sistema registra la solicitud, genera un enlace de recuperación de un
   solo uso, válido por 30 minutos, e invalida cualquier enlace anterior de
   esa cuenta.
8. include(Enviar notificación por email), con el enlace generado.
9. El sistema muestra el mensaje "Si el email ingresado está registrado,
   recibirás un enlace para restablecer tu contraseña. El enlace vence en
   30 minutos".
10. El usuario abre el enlace recibido por email.
11. El sistema valida que el enlace exista, no haya sido usado y no esté
    vencido.
12. El sistema muestra los siguientes campos y, debajo, el botón "Guardar":
    - Nueva contraseña: campo de contraseña, obligatorio, entre 8 y 64
      caracteres, con al menos una letra y un número.
    - Confirmar contraseña: campo de contraseña, obligatorio, debe
      coincidir con la nueva contraseña.
13. El usuario completa los campos y presiona "Guardar".
14. El sistema valida que la contraseña cumpla las reglas y que ambos
    campos coincidan.
15. El sistema guarda la nueva contraseña, inutiliza el enlace, cierra
    todas las sesiones abiertas de la cuenta, muestra el mensaje "Tu
    contraseña fue actualizada. Iniciá sesión con tu nueva contraseña" y
    redirige a la pantalla de inicio de sesión.

## Flujos alternativos

- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2. Debajo del campo se muestra el
    formato requerido.
- **5.a No existe una cuenta activa con ese email:**
  - 5.a.1 El sistema no genera ningún enlace y muestra el mensaje del
    paso 9.
  - 5.a.2 Finaliza el caso de uso.
- **6.a La cuenta ya realizó 5 solicitudes en el mes:**
  - 6.a.1 El sistema no genera ningún enlace y muestra el mensaje
    "Alcanzaste el límite de solicitudes de recuperación de este mes.
    Comunicate con la administración".
  - 6.a.2 El usuario presiona "Aceptar".
  - 6.a.3 Finaliza el caso de uso.
- **11.a El enlace no existe, ya fue usado o está vencido:**
  - 11.a.1 El sistema muestra el mensaje "El enlace no es válido o venció.
    Solicitá uno nuevo desde la pantalla de inicio de sesión".
  - 11.a.2 El usuario presiona "Aceptar".
  - 11.a.3 Finaliza el caso de uso.
- **14.a La validación falla:**
  - 14.a.1 El sistema vuelve al paso 12. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.

## Flujos de excepción

- En los pasos 2 y 12 el usuario puede cancelar la operación presionando
  "Cancelar". El sistema vuelve a la pantalla de inicio de sesión y
  finaliza el caso de uso.

## Observaciones

- El mensaje del paso 9 es el mismo exista o no la cuenta, para no revelar
  qué emails están registrados (mismo criterio que CU-001). La excepción es
  el mensaje de límite alcanzado (6.a), que se decidió mostrar explícito
  para que el usuario sepa que debe recurrir a la administración.
- El límite de 5 solicitudes por mes calendario evita que alguien que
  conozca el email de otro usuario le envíe correos de recuperación en
  forma indiscriminada. El contador vuelve a 0 el día 1 de cada mes, y el
  administrador puede reiniciarlo antes desde "Modificar usuario"
  (CU-007).
- Las reglas de contraseña son las mismas que en CU-003 y CU-004.
- El caso de uso tiene dos momentos: la solicitud (pasos 1 a 9) y el uso
  del enlace (pasos 10 a 15), que puede ocurrir hasta 30 minutos después.
