# CU-023 — Consultar reclamos comunitarios

| Campo | Valor |
|---|---|
| **ID** | CU-023 |
| **Nombre** | Consultar reclamos comunitarios |
| **Breve descripción** | Permite al residente listar los reclamos registrados sobre las ubicaciones compartidas del espacio, para conocerlos y adherir a ellos. |
| **Prioridad** | Alta |
| **Complejidad** | Baja |
| **Actor principal** | Residente |
| **Actores secundarios** | — |
| **Precondiciones** | El residente tiene una sesión iniciada en el sistema. <br> El residente tiene al menos una unidad vinculada. |
| **Postcondiciones** | **Éxito:** se muestran los reclamos comunitarios que cumplen con los filtros seleccionados. <br> **Fracaso:** no aplica; el caso de uso no modifica el estado del sistema. |

## Flujo principal

1. El caso de uso comienza cuando el residente presiona "Reclamos
   comunitarios".
2. El sistema muestra los siguientes filtros y, debajo, el botón "Buscar":
   - Texto: campo de texto, opcional, máximo 100 caracteres. Busca por
     número de reclamo exacto o por coincidencia parcial en el título.
   - Ubicación compartida: lista desplegable, opcional, que contiene
     "Todas" y las ubicaciones compartidas del espacio, ordenadas
     alfabéticamente; de cada una se muestra el nombre. Valor por defecto:
     "Todas".
   - Estado: lista desplegable, opcional, con las mismas opciones que en
     "Consultar mis reclamos" (CU-022). Valor por defecto: "Abiertos".
3. El sistema busca los reclamos comunitarios que cumplen con los filtros
   seleccionados.
   - Si hay resultados, los muestra en un listado paginado de 20 por
     página, ordenado por fecha de registro en forma descendente. Para
     cada reclamo se muestra:
     - Número.
     - Título.
     - Ubicación compartida.
     - Rubro ("Sin categorizar" si todavía no fue categorizado).
     - Autor (nombre y apellido).
     - Estado.
     - Cantidad de adhesiones.
     - Fecha de registro.
     - Una indicación "Registrado por mí" o "Adherido", si corresponde.

     Al presionar el encabezado de una columna, el listado se ordena por
     esa columna, alternando entre orden ascendente y descendente. Debajo
     del listado se encuentran los controles para pasar de una página a
     otra. Para cada reclamo se muestra el botón "Ver detalle" y, si el
     residente no lo registró, no adhirió todavía y el reclamo está en
     estado "Ingresado", "Asignado", "En curso" o "Esperando
     repuesto/tercero", el botón "Adherir".
     Punto de extensión: "GestionarReclamoComunitario".
   - Si no hay resultados, muestra el mensaje "No se encontraron reclamos
     comunitarios con los filtros seleccionados".
4. El residente puede modificar los filtros y presionar "Buscar". El
   sistema vuelve al paso 3.

## Flujos alternativos

Ninguno.

## Flujos de excepción

Ninguno.

## Observaciones

- Son comunitarios todos los reclamos registrados sobre una ubicación
  compartida, incluidos los de convivencia (ver CU-021).
- No hay anonimato: el listado muestra quién registró cada reclamo.
