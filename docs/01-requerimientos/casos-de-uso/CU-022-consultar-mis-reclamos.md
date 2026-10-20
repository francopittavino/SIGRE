# CU-022 — Consultar mis reclamos

| Campo | Valor |
|---|---|
| **ID** | CU-022 |
| **Nombre** | Consultar mis reclamos |
| **Breve descripción** | Permite al residente listar los reclamos que registró, los reclamos a los que adhirió y, si es propietario, los reclamos registrados sobre sus unidades, filtrando por texto, estado, ubicación y origen. |
| **Prioridad** | Alta |
| **Complejidad** | Media |
| **Actor principal** | Residente |
| **Actores secundarios** | — |
| **Precondiciones** | El residente tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** se muestran los reclamos del residente que cumplen con los filtros seleccionados. <br> **Fracaso:** no aplica; el caso de uso no modifica el estado del sistema. |

## Flujo principal

1. El caso de uso comienza cuando el residente presiona "Mis reclamos".
2. El sistema muestra los siguientes filtros y, debajo, el botón "Buscar":
   - Texto: campo de texto, opcional, máximo 100 caracteres. Busca por
     número de reclamo exacto o por coincidencia parcial en el título.
   - Estado: lista desplegable, opcional, con las opciones "Abiertos"
     (todos excepto "Cerrado", "Rechazado" y "Cancelado"), "Todos",
     "Ingresado", "Asignado", "En curso", "Esperando repuesto/tercero",
     "Resuelto", "Cerrado", "Rechazado" y "Cancelado". Valor
     por defecto: "Abiertos".
   - Ubicación: lista desplegable, opcional, que contiene "Todas", las
     unidades vinculadas al residente (se muestra el identificador) y las
     ubicaciones compartidas del espacio (se muestra el nombre). Valor por
     defecto: "Todas".
   - Origen: lista desplegable, opcional, con las opciones "Todos",
     "Registrados por mí", "Adheridos" y, solo si el residente es
     propietario o inquilino de alguna unidad, "De mis unidades". Valor por
     defecto:
     "Todos".
3. El sistema busca los reclamos que cumplen con los filtros seleccionados,
   entre los siguientes:
   - los reclamos registrados por el residente.
   - los reclamos comunitarios a los que el residente adhirió.
   - si el residente es propietario, todos los reclamos registrados sobre
     las unidades de las que es propietario actualmente, incluidos los
     registrados antes de que lo fuera.
   - si el residente es inquilino, los reclamos registrados sobre la unidad
     que alquila desde que es su inquilino.

   - Si hay resultados, los muestra en un listado paginado de 20 por
     página, ordenado por fecha de última actualización en forma
     descendente. Para cada reclamo se muestra:
     - Número.
     - Título.
     - Ubicación (identificador de la unidad o nombre de la ubicación
       compartida).
     - Rubro ("Sin categorizar" si el administrador todavía no lo
       categorizó).
     - Estado.
     - Origen ("Registrado por mí", "Adherido" o "De mi unidad").
     - Fecha de registro.
     - Fecha de última actualización.

     Al presionar el encabezado de una columna, el listado se ordena por
     esa columna, alternando entre orden ascendente y descendente. Debajo
     del listado se encuentran los controles para pasar de una página a
     otra. Para cada reclamo se muestra el botón "Ver detalle".
     Punto de extensión: "GestionarMiReclamo".
   - Si no hay resultados, muestra el mensaje "No se encontraron reclamos
     con los filtros seleccionados".
4. El residente puede modificar los filtros y presionar "Buscar". El
   sistema vuelve al paso 3.

## Flujos alternativos

Ninguno.

## Flujos de excepción

Ninguno.

## Observaciones

- El propietario actual ve todos los reclamos registrados sobre su
  unidad, incluidos los de su inquilino y los de propietarios e inquilinos
  anteriores: el historial pertenece a la unidad. Si deja de ser
  propietario, conserva solo los que él mismo registró (ver CU-007).
- El inquilino actual ve los reclamos que el propietario u otros
  registren sobre la unidad que alquila mientras vive en ella, pero no los
  anteriores a su llegada.
- Un usuario sin unidades vinculadas puede usar este caso de uso para
  consultar los reclamos que registró anteriormente.
