# CU-005 — Consultar usuarios

| Campo | Valor |
|---|---|
| **ID** | CU-005 |
| **Nombre** | Consultar usuarios |
| **Breve descripción** | Permite al administrador buscar y listar los usuarios del espacio y las invitaciones enviadas, filtrando por texto, unidad, rol y estado. |
| **Prioridad** | Alta |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** se muestran los usuarios e invitaciones que cumplen con los filtros seleccionados. <br> **Fracaso:** no aplica; el caso de uso no modifica el estado del sistema. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Usuarios".
2. El sistema muestra los siguientes filtros y, debajo, el botón "Buscar":
   - Texto: campo de texto, opcional, máximo 100 caracteres. Busca
     coincidencias parciales en nombre, apellido, email y número de
     documento.
   - Unidad: lista desplegable, opcional, que contiene todas las unidades
     activas del espacio, ordenadas por identificador. De cada unidad se
     muestra su identificador (por ejemplo, "3B"). Valor por defecto:
     "Todas".
   - Rol: lista desplegable, opcional, con las opciones "Todos",
     "Propietario" e "Inquilino". Valor por defecto: "Todos".
   - Estado: lista desplegable, opcional, con las opciones "Todos",
     "Activo", "Dado de baja", "Invitación pendiente" e "Invitación
     vencida". Valor por defecto: "Activo".
3. El sistema busca los usuarios e invitaciones que cumplen con los filtros
   seleccionados.
   - Si hay resultados, los muestra en un listado paginado de 20 por
     página, ordenado por apellido en forma ascendente. Para cada resultado
     se muestra:
     - Nombre y apellido ("—" en el caso de invitaciones).
     - Email.
     - Unidades y rol en cada una (por ejemplo, "3B (Propietario), 5A
       (Inquilino)").
     - Estado.

     Al presionar el encabezado de una columna, el listado se ordena por
     esa columna, alternando entre orden ascendente y descendente. Debajo
     del listado se encuentran los controles para pasar de una página a
     otra. Para cada usuario en estado "Activo" se muestran los botones
     "Modificar" y "Dar de baja"; para cada usuario en estado "Dado de
     baja", el botón "Reactivar".
     Punto de extensión: "GestionarUsuarioExistente".
   - Si no hay resultados, muestra el mensaje "No se encontraron usuarios
     con los filtros seleccionados".
4. El administrador puede modificar los filtros y presionar "Buscar". El
   sistema vuelve al paso 3.

## Flujos alternativos

Ninguno.

## Flujos de excepción

Ninguno.

## Observaciones

- Las invitaciones no tienen acciones asociadas: no se reenvían ni se
  anulan. Si una invitación vence, el rol de la unidad se libera y el
  administrador puede volver a invitar desde "Invitar usuario" (CU-006).
  Una invitación cargada por error mantiene el rol reservado hasta que
  vence, a los 7 días.
- Las invitaciones (pendientes o vencidas) no muestran botones.
