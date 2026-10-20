# CU-017 — Consultar rubros

| Campo | Valor |
|---|---|
| **ID** | CU-017 |
| **Nombre** | Consultar rubros |
| **Breve descripción** | Permite al administrador buscar y listar los rubros con los que se categorizan los reclamos, filtrando por texto, tipo y estado. |
| **Prioridad** | Alta |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** se muestran los rubros que cumplen con los filtros seleccionados. <br> **Fracaso:** no aplica; el caso de uso no modifica el estado del sistema. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Rubros".
2. El sistema muestra los siguientes filtros y, debajo, el botón "Buscar":
   - Texto: campo de texto, opcional, máximo 50 caracteres. Busca
     coincidencias parciales en el nombre y la descripción.
   - Tipo: lista desplegable, opcional, con las opciones "Todos",
     "Mantenimiento" y "Convivencia". Valor por defecto: "Todos".
   - Estado: lista desplegable, opcional, con las opciones "Todos",
     "Activo" y "Dado de baja". Valor por defecto: "Activo".
3. El sistema busca los rubros que cumplen con los filtros seleccionados.
   - Si hay resultados, los muestra en un listado paginado de 20 por
     página, ordenado por nombre en forma ascendente. Para cada rubro se
     muestra:
     - Nombre.
     - Tipo.
     - Plazo objetivo de resolución (en días).
     - Cantidad de reclamos abiertos (en un estado distinto de "Cerrado",
       "Rechazado" o "Cancelado").
     - Estado.

     Al presionar el encabezado de una columna, el listado se ordena por
     esa columna, alternando entre orden ascendente y descendente. Debajo
     del listado se encuentran los controles para pasar de una página a
     otra. Para cada rubro en estado "Activo" se muestran los botones
     "Modificar" y "Dar de baja".
     Punto de extensión: "GestionarRubroExistente".
   - Si no hay resultados, muestra el mensaje "No se encontraron rubros
     con los filtros seleccionados".
4. El administrador puede modificar los filtros y presionar "Buscar". El
   sistema vuelve al paso 3.

## Flujos alternativos

Ninguno.

## Flujos de excepción

Ninguno.

## Observaciones

- Los rubros dados de baja no muestran botones: la baja es definitiva.
- Al crearse el espacio, el sistema carga un conjunto inicial de rubros
  activos, que el administrador puede modificar o dar de baja como
  cualquier otro:
  - Mantenimiento: Plomería, Electricidad, Gas, Ascensores, Limpieza,
    Albañilería, Portones y accesos.
  - Convivencia: Ruidos molestos, Mascotas, Uso de espacios comunes.

  Así la sugerencia automática de rubro (CU-037) funciona desde el primer
  reclamo.
