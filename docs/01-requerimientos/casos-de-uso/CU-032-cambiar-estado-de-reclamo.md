# CU-032 — Cambiar estado de reclamo

| Campo | Valor |
|---|---|
| **ID** | CU-032 |
| **Nombre** | Cambiar estado de reclamo |
| **Breve descripción** | Permite al administrador avanzar un reclamo por el circuito de estados (en curso, esperando repuesto o tercero, resuelto) o rechazarlo, dejando registro inmutable del cambio y notificando a los interesados. |
| **Prioridad** | Alta |
| **Complejidad** | Alta |
| **Actor principal** | Administrador |
| **Actores secundarios** | — (el Servicio de Email participa a través de CU-038) |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** el reclamo queda en el nuevo estado y el cambio queda registrado en el historial del reclamo con la fecha y hora, el autor, el estado anterior, el nuevo y el motivo o comentario, si se indicó. Los interesados son notificados. <br> **Fracaso:** el reclamo conserva su estado. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Cambiar
   estado" sobre un reclamo seleccionado.
2. El sistema obtiene los estados a los que puede pasar el reclamo según su
   estado actual:

   | Estado actual | Estados posibles |
   |---|---|
   | Ingresado | Rechazado |
   | Asignado | En curso, Rechazado |
   | En curso | Esperando repuesto/tercero, Resuelto |
   | Esperando repuesto/tercero | En curso, Resuelto |
   | Reabierto | En curso, Resuelto |

3. El sistema muestra el número, el título y el estado actual del
   reclamo, y los siguientes campos y, debajo, el botón "Guardar":
   - Nuevo estado: lista desplegable, obligatoria, que contiene los
     estados obtenidos en el paso anterior.
   - Comentario para el residente: área de texto, máximo 1000 caracteres.
     Es obligatorio, con un mínimo de 10 caracteres, si el nuevo estado es
     "Rechazado" (motivo del rechazo) o "Resuelto" (qué se hizo); en los
     demás casos es opcional.
4. El administrador selecciona el nuevo estado, completa el comentario y
   presiona "Guardar".
5. El sistema valida que los campos cumplan con el formato requerido.
6. El sistema cambia el estado del reclamo y registra en el historial del
   reclamo el cambio, con la fecha y hora, el administrador como autor, el
   estado anterior, el nuevo y el comentario, si se indicó. El comentario
   también se agrega a los comentarios visibles del reclamo.
7. include(Enviar notificación por email), con el nuevo estado y el
   comentario, dirigido al autor del reclamo, a sus adherentes y, si el
   autor no es el propietario de la unidad, al propietario. Si el nuevo
   estado es "Resuelto", el aviso indica además que el autor tiene 7 días
   para confirmar la resolución o reabrir el reclamo, o se cerrará
   automáticamente.
8. El sistema muestra el mensaje "El reclamo N° *número* pasó a estado
   *nuevo estado*".

## Flujos alternativos

- **2.a El estado actual no admite cambios por parte del administrador
  ("Resuelto", "Cerrado", "Rechazado" o "Cancelado"):**
  - 2.a.1 El sistema muestra el mensaje "El reclamo está en estado
    *estado* y no puede cambiar de estado desde la administración".
  - 2.a.2 El administrador presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.
- **5.a La validación de formato falla:**
  - 5.a.1 El sistema vuelve al paso 3. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.

## Flujos de excepción

- En el paso 3 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema no realiza ningún cambio y finaliza el caso de
  uso.

## Observaciones

- El paso de "Ingresado" a "Asignado" no se hace desde aquí, sino al
  categorizar el reclamo (CU-031).
- Los pasos de "Resuelto" a "Cerrado" o a "Reabierto" los realiza el
  residente (CU-028, CU-029) o el sistema (CU-036).
- "Rechazado" es un estado final. Un reclamo rechazado no puede reabrirse;
  si el residente no está de acuerdo, registra un reclamo nuevo.
- El historial es inmutable: los registros no pueden editarse ni
  eliminarse.
