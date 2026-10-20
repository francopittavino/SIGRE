# CU-013 — Consultar ubicaciones compartidas

| Campo | Valor |
|---|---|
| **ID** | CU-013 |
| **Nombre** | Consultar ubicaciones compartidas |
| **Breve descripción** | Permite al administrador buscar y listar las áreas comunes e instalaciones compartidas del espacio, filtrando por texto, tipo y estado. |
| **Prioridad** | Alta |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** se muestran las ubicaciones compartidas que cumplen con los filtros seleccionados. <br> **Fracaso:** no aplica; el caso de uso no modifica el estado del sistema. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Ubicaciones
   compartidas".
2. El sistema muestra los siguientes filtros y, debajo, el botón "Buscar":
   - Texto: campo de texto, opcional, máximo 50 caracteres. Busca
     coincidencias parciales en el nombre y la descripción.
   - Tipo: lista desplegable, opcional, con las opciones "Todos", "Área
     común" e "Instalación". Valor por defecto: "Todos".
   - Estado: lista desplegable, opcional, con las opciones "Todas",
     "Activa" y "Dada de baja". Valor por defecto: "Activa".
3. El sistema busca las ubicaciones compartidas que cumplen con los
   filtros seleccionados.
   - Si hay resultados, los muestra en un listado paginado de 20 por
     página, ordenado por nombre en forma ascendente. Para cada ubicación
     se muestra:
     - Nombre.
     - Tipo.
     - Cantidad de reclamos abiertos (en un estado distinto de "Cerrado",
       "Rechazado" o "Cancelado").
     - Estado.

     Al presionar el encabezado de una columna, el listado se ordena por
     esa columna, alternando entre orden ascendente y descendente. Debajo
     del listado se encuentran los controles para pasar de una página a
     otra. Para cada ubicación en estado "Activa" se muestran los botones
     "Modificar" y "Dar de baja".
     Punto de extensión: "GestionarUbicacionExistente".
   - Si no hay resultados, muestra el mensaje "No se encontraron
     ubicaciones compartidas con los filtros seleccionados".
4. El administrador puede modificar los filtros y presionar "Buscar". El
   sistema vuelve al paso 3.

## Flujos alternativos

Ninguno.

## Flujos de excepción

Ninguno.

## Observaciones

- Las ubicaciones dadas de baja no muestran botones: la baja es
  definitiva. Sus reclamos e historial se conservan y pueden consultarse
  desde "Consultar historial de ubicación" (CU-034).
