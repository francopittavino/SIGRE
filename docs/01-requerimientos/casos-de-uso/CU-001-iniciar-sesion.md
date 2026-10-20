# CU-001 — Iniciar sesión

| Campo | Valor |
|---|---|
| **ID** | CU-001 |
| **Nombre** | Iniciar sesión |
| **Breve descripción** | Permite a un usuario registrado identificarse con su email y contraseña para acceder a las funcionalidades de su rol. |
| **Prioridad** | Alta |
| **Complejidad** | Media |
| **Actor principal** | Usuario |
| **Actores secundarios** | — |
| **Precondiciones** | El usuario no tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** se inicia la sesión del usuario y se reinicia el contador de intentos fallidos de ese email en ese dispositivo. <br> **Fracaso:** no se inicia la sesión. Si las credenciales fueron incorrectas, se registra el intento fallido y, si corresponde, se aplica una espera antes de permitir un nuevo intento desde ese dispositivo. |

## Flujo principal

1. El caso de uso comienza cuando el usuario accede a la pantalla de inicio
   de sesión.
2. El sistema muestra los siguientes campos y, debajo, el botón "Ingresar":
   - Email: campo de texto, obligatorio, formato de email válido, máximo
     254 caracteres.
   - Contraseña: campo de contraseña (caracteres ocultos), obligatorio.
3. El usuario completa los campos y presiona "Ingresar".
4. El sistema valida que los campos estén completos y con el formato
   requerido.
5. El sistema valida que no haya una espera activa para el email ingresado
   desde el dispositivo del usuario.
6. El sistema valida que exista una cuenta activa registrada con el email
   ingresado y que la contraseña sea correcta.
7. El sistema reinicia el contador de intentos fallidos del email en ese
   dispositivo, inicia la sesión y muestra la pantalla de inicio con las
   opciones disponibles para el rol del usuario.

## Flujos alternativos

- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2. Debajo de cada campo erróneo se
    muestra el formato requerido.
- **5.a Hay una espera activa:**
  - 5.a.1 El sistema muestra el mensaje "Superó la cantidad de intentos
    permitidos. Podrá intentar nuevamente en *N* minuto(s)", donde *N* es
    el tiempo restante de la espera.
  - 5.a.2 El usuario presiona "Aceptar".
  - 5.a.3 Finaliza el caso de uso.
- **6.a No existe una cuenta activa con ese email o la contraseña es
  incorrecta:**
  - 6.a.1 El sistema incrementa el contador de intentos fallidos del email
    ingresado en el dispositivo del usuario.
  - 6.a.2 Si el contador llega a un múltiplo de 3, el sistema aplica una
    espera escalonada: 1 minuto la primera vez, 5 minutos la segunda y 15
    minutos a partir de la tercera. Muestra el mensaje de 5.a.1, el
    usuario presiona "Aceptar" y finaliza el caso de uso.
  - 6.a.3 En caso contrario, el sistema muestra el mensaje "Email o
    contraseña incorrectos" y vuelve al paso 2.

## Flujos de excepción

Ninguno.

## Observaciones

- El mensaje es el mismo para un email inexistente, una cuenta dada de baja
  y una contraseña incorrecta, para no revelar qué emails están
  registrados. Por el mismo motivo, los intentos fallidos se cuentan
  también para emails inexistentes.
- La espera se aplica por combinación de email y dispositivo, no a la
  cuenta: así, quien conozca el email de otro usuario no puede impedirle
  ingresar desde su propio dispositivo.
- El contador de intentos y el escalonamiento de la espera se reinician
  con un ingreso exitoso desde ese dispositivo.
- Desde esta pantalla se accede a "Recuperar contraseña" (CU-002).
