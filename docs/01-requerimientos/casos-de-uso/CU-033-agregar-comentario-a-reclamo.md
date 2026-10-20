# CU-033 — Agregar comentario a reclamo

| Campo | Valor |
|---|---|
| **ID** | CU-033 |
| **Nombre** | Agregar comentario a reclamo |
| **Breve descripción** | Permite a un residente con acceso a un reclamo, o al administrador, agregar un comentario. El administrador puede marcarlo como interno para que no lo vean los residentes. |
| **Prioridad** | Media |
| **Complejidad** | Baja |
| **Actor principal** | Residente, Administrador |
| **Actores secundarios** | — (el Servicio de Email participa a través de CU-038) |
| **Precondiciones** | El usuario tiene una sesión iniciada en el sistema. <br> El usuario tiene acceso al reclamo seleccionado. |
| **Postcondiciones** | **Éxito:** el comentario queda registrado en el reclamo con la fecha y hora y el autor, como visible o interno. <br> **Fracaso:** no se registra el comentario. |

## Flujo principal

1. El caso de uso comienza cuando el usuario presiona "Agregar comentario"
   sobre un reclamo seleccionado.
2. El sistema valida que el reclamo no esté en estado "Cerrado",
   "Rechazado" o "Cancelado".
3. El sistema muestra los siguientes campos y, debajo, el botón
   "Publicar":
   - Comentario: área de texto, obligatoria, entre 1 y 2000 caracteres.
   - Interno: casilla de verificación, desmarcada por defecto, que solo se
     muestra si el usuario es el administrador. Junto a ella se aclara
     "Los comentarios internos no son visibles para los residentes".
4. El usuario completa el comentario y presiona "Publicar".
5. El sistema valida que el comentario cumpla con el formato requerido.
6. El sistema registra el comentario con la fecha y hora, el autor y la
   indicación de visible o interno.
7. Según el autor y la visibilidad del comentario:
   - Si el autor es el administrador y el comentario es visible,
     include(Enviar notificación por email), con el comentario, dirigido
     al autor del reclamo.
   - Si el autor es un residente, include(Enviar notificación por email),
     con el aviso de nuevo comentario, dirigido al administrador.
   - Si el comentario es interno, no se envía ninguna notificación.
8. El sistema muestra el comentario al final de la lista de comentarios
   del reclamo.

## Flujos alternativos

- **2.a El reclamo está cerrado, rechazado o cancelado:**
  - 2.a.1 El sistema muestra el mensaje "El reclamo está en estado
    *estado* y ya no admite comentarios".
  - 2.a.2 El usuario presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.
- **5.a La validación de formato falla:**
  - 5.a.1 El sistema vuelve al paso 3. Debajo del campo se muestra la
    regla que no se cumple.

## Flujos de excepción

- En el paso 3 el usuario puede cancelar la operación presionando
  "Cancelar". El sistema descarta el comentario y finaliza el caso de uso.

## Observaciones

- Los comentarios no pueden editarse ni eliminarse, igual que el
  historial del reclamo.
- Los comentarios visibles del administrador se notifican solo al autor
  del reclamo. Los adherentes y el propietario reciben avisos únicamente
  ante cambios de estado, para no saturarlos de correos.
- Cada comentario se muestra con el nombre y apellido de su autor, sea
  residente o administrador. Los comentarios visibles del administrador
  los ven todos los que tienen acceso al reclamo; los internos, solo el
  administrador.
- Tienen acceso al reclamo el administrador, el residente que lo
  registró, el propietario actual de la unidad, el inquilino actual (para
  los reclamos registrados mientras es inquilino), el propietario y el
  inquilino actuales de la unidad involucrada en un reclamo de convivencia
  y, si el reclamo es comunitario, cualquier residente con unidades
  vinculadas.
