# CU-030 — Consultar reclamos

| Campo | Valor |
|---|---|
| **ID** | CU-030 |
| **Nombre** | Consultar reclamos |
| **Breve descripción** | Permite al administrador buscar y listar todos los reclamos del espacio, filtrando por estado, rubro, ubicación, prioridad y otros criterios, para gestionarlos. |
| **Prioridad** | Alta |
| **Complejidad** | Media |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** se muestran los reclamos que cumplen con los filtros seleccionados. <br> **Fracaso:** no aplica; el caso de uso no modifica el estado del sistema. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Reclamos".
2. El sistema muestra los siguientes filtros y, debajo, el botón "Buscar":
   - Texto: campo de texto, opcional, máximo 100 caracteres. Busca por
     número de reclamo exacto o por coincidencia parcial en el título o en
     el nombre y apellido del autor.
   - Estado: lista desplegable, opcional, con las opciones "Abiertos"
     (todos excepto "Cerrado", "Rechazado" y "Cancelado"), "Todos",
     "Ingresado", "Asignado", "En curso", "Esperando repuesto/tercero",
     "Resuelto", "Reabierto", "Cerrado", "Rechazado" y "Cancelado". Valor
     por defecto: "Abiertos".
   - Rubro: lista desplegable, opcional, que contiene "Todos", "Sin
     categorizar" y todos los rubros del espacio, ordenados
     alfabéticamente; de cada uno se muestra el nombre. Valor por defecto:
     "Todos".
   - Tipo: lista desplegable, opcional, con las opciones "Todos",
     "Mantenimiento" y "Convivencia". Valor por defecto: "Todos".
   - Ubicación: lista desplegable, opcional, que contiene "Todas", las
     unidades (se muestra el identificador) y las ubicaciones compartidas
     (se muestra el nombre) del espacio. Valor por defecto: "Todas".
   - Prioridad: lista desplegable, opcional, con las opciones "Todas",
     "Urgente", "Alta", "Media" y "Baja". Valor por defecto: "Todas".
   - Solo comunitarios: casilla de verificación, opcional, desmarcada por
     defecto.
   - Solo vencidos: casilla de verificación, opcional, desmarcada por
     defecto. Muestra solo los reclamos abiertos cuya fecha objetivo de
     resolución ya pasó.
3. El sistema busca los reclamos que cumplen con los filtros seleccionados.
   - Si hay resultados, los muestra en un listado paginado de 20 por
     página, ordenado por prioridad en forma descendente y, a igual
     prioridad, por fecha de registro en forma ascendente. Para cada
     reclamo se muestra:
     - Número.
     - Título.
     - Ubicación.
     - Rubro (si no fue categorizado, el rubro sugerido con la indicación
       "Sugerido", o "Sin categorizar" si no hay sugerencia).
     - Estado.
     - Prioridad.
     - Cantidad de adhesiones, si es comunitario.
     - Fecha de registro.
     - Fecha objetivo de resolución, con la indicación "Vencido" si se
       superó y el reclamo sigue abierto.

     Al presionar el encabezado de una columna, el listado se ordena por
     esa columna, alternando entre orden ascendente y descendente. Debajo
     del listado se encuentran los controles para pasar de una página a
     otra. Para cada reclamo se muestra el botón "Ver detalle" y, si el
     reclamo está abierto y no está en estado "Resuelto", los botones
     "Categorizar" y "Cambiar estado".
     Punto de extensión: "GestionarReclamo".
   - Si no hay resultados, muestra el mensaje "No se encontraron reclamos
     con los filtros seleccionados".
4. El administrador puede modificar los filtros y presionar "Buscar". El
   sistema vuelve al paso 3.

## Flujos alternativos

Ninguno.

## Flujos de excepción

Ninguno.

## Observaciones

- El orden por defecto (prioridad y antigüedad) busca que el administrador
  atienda primero los reclamos más urgentes y los que llevan más tiempo
  esperando.
- Un reclamo en estado "Resuelto" queda a la espera de la confirmación del
  residente (CU-028, CU-029) o del cierre automático (CU-036), por lo que
  no muestra acciones de gestión.
