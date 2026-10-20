# CU-038 — Enviar notificación por email

| Campo | Valor |
|---|---|
| **ID** | CU-038 |
| **Nombre** | Enviar notificación por email |
| **Breve descripción** | Envía un correo electrónico a uno o varios destinatarios a través del servicio de email, con el contenido que indica el caso de uso que lo incluye, y deja registro del envío. |
| **Prioridad** | Alta |
| **Complejidad** | Media |
| **Actor principal** | — (caso de uso incluido) |
| **Actores secundarios** | Servicio de Email |
| **Precondiciones** | — |
| **Postcondiciones** | **Éxito:** el correo queda enviado a cada destinatario y cada envío queda registrado con su fecha y hora, destinatario, asunto y resultado. <br> **Fracaso:** el correo no se envía a uno o más destinatarios y cada fallo queda registrado. |

## Flujo principal

1. El caso de uso comienza cuando es incluido por otro caso de uso, que le
   indica los destinatarios, el asunto y el contenido del mensaje y, si
   corresponde, un enlace (de invitación, de recuperación, de confirmación
   o al reclamo).
2. El sistema arma el correo con el formato institucional de SIGRE:
   encabezado con el logo y el nombre del espacio, el contenido, el
   enlace, si lo hay, y un pie con la aclaración "Este es un mensaje
   automático, no lo respondas".
3. Para cada destinatario, el sistema:
   a. envía el correo a través del Servicio de Email.
   b. registra el envío con la fecha y hora, el destinatario, el asunto y
      el resultado.
4. Finaliza el caso de uso.

## Flujos alternativos

- **3.a El Servicio de Email no está disponible o rechaza el envío:**
  - 3.a.1 El sistema reintenta el envío hasta 3 veces, con 5 minutos de
    diferencia entre cada intento.
  - 3.a.2 Si el envío sigue fallando, el sistema registra el fallo con la
    fecha y hora, el destinatario, el asunto y el error.
  - 3.a.3 Continúa con el siguiente destinatario.

## Flujos de excepción

Ninguno.

## Observaciones

- El envío se realiza en segundo plano: el caso de uso que lo incluye no
  espera el resultado y continúa normalmente, aunque el envío falle.
- Los destinatarios los define el caso de uso que incluye a este. Las
  notificaciones de cambio de estado se envían a los **interesados del
  reclamo**: el autor, los adherentes, el propietario actual de la unidad
  sobre la que se registró (si no es el autor) y, en los reclamos de
  convivencia con unidad involucrada, el propietario y el inquilino
  actuales de esa unidad. En todos los casos se omite al usuario que
  realizó la acción.
- A los usuarios dados de baja no se les envían notificaciones, salvo el
  aviso de la propia baja.
- Los enlaces enviados por email (invitación, recuperación de contraseña,
  confirmación de email) tienen su vencimiento definido en el caso de uso
  que los genera.
