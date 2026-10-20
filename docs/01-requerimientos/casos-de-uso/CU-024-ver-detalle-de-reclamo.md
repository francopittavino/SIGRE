# CU-024 — Ver detalle de reclamo

| Campo | Valor |
|---|---|
| **ID** | CU-024 |
| **Nombre** | Ver detalle de reclamo |
| **Breve descripción** | Permite al residente o al administrador ver toda la información de un reclamo: sus datos, fotos, historial de estados y comentarios, y acceder a las acciones disponibles sobre él. |
| **Prioridad** | Alta |
| **Complejidad** | Media |
| **Actor principal** | Residente, Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El usuario tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** se muestra el detalle del reclamo seleccionado. <br> **Fracaso:** no se muestra el detalle; el caso de uso no modifica el estado del sistema. |

## Flujo principal

1. El caso de uso comienza cuando el usuario presiona "Ver detalle" sobre
   un reclamo seleccionado.
2. El sistema valida que el usuario tenga acceso al reclamo. Tienen acceso:
   - el administrador, a todos los reclamos.
   - el residente que lo registró.
   - el propietario actual de la unidad sobre la que se registró, incluso
     si el reclamo se registró antes de que fuera su propietario.
   - el inquilino actual de la unidad sobre la que se registró, si el
     reclamo se registró mientras es su inquilino.
   - el propietario y el inquilino actuales de la unidad involucrada, si
     el reclamo es de convivencia.
   - cualquier residente con unidades vinculadas, si el reclamo es
     comunitario.
3. El sistema muestra:
   - Número, título y descripción.
   - Ubicación (identificador de la unidad o nombre de la ubicación
     compartida) y, si es de convivencia, la indicación "Convivencia" y la
     unidad involucrada.
   - Rubro (o rubro sugerido con la indicación "Sugerido", si no fue
     categorizado todavía).
   - Estado actual y prioridad.
   - Fecha de registro y, si fue categorizado, fecha objetivo de
     resolución, con la indicación "Vencido" si se superó y el reclamo
     sigue abierto.
   - Si es comunitario, la cantidad de adhesiones y los votos de
     resolución ("*N* de *M* residentes lo dieron por resuelto").
   - Las fotos adjuntas, en miniatura; al presionar una, se muestra en
     tamaño completo.
   - El historial del reclamo, ordenado por fecha en forma ascendente:
     para cada registro, la fecha y hora, el estado o evento, el autor y
     el motivo, si lo tiene.
   - Los comentarios, ordenados por fecha en forma ascendente: para cada
     uno, la fecha y hora, el autor y el texto.

   - El nombre y apellido del autor del reclamo y, si es comunitario, la
     lista de adherentes.

   Si el usuario es el administrador, el sistema muestra además los
   comentarios internos, identificados con la indicación "Interno".
   Debajo se muestran los botones de las acciones disponibles para el
   usuario según el estado del reclamo.
   Punto de extensión: "AccionesSobreReclamo".

## Flujos alternativos

- **2.a El usuario no tiene acceso al reclamo:**
  - 2.a.1 El sistema muestra el mensaje "No tenés acceso a este reclamo".
  - 2.a.2 El usuario presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.

## Flujos de excepción

Ninguno.

## Observaciones

- El residente nunca ve los comentarios internos de la administración.
- No hay anonimato: todos los que tienen acceso al reclamo ven quién lo
  registró, quiénes adhirieron y el nombre de quien escribió cada
  comentario.
- En los reclamos de convivencia, el propietario y el inquilino de la
  unidad involucrada ven el reclamo completo, incluidos el nombre y
  apellido de su autor y la unidad desde la que se registró, y pueden
  comentar (CU-033). No pueden adherir, modificar, cancelar ni marcarlo
  como resuelto.
- Las acciones disponibles en el punto de extensión dependen del usuario y
  del estado del reclamo, y se detallan en cada caso de uso que lo
  extiende.
