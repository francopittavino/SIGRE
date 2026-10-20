# CU-009 — Consultar unidades

| Campo | Valor |
|---|---|
| **ID** | CU-009 |
| **Nombre** | Consultar unidades |
| **Breve descripción** | Permite al administrador buscar y listar las unidades privadas del espacio, con su propietario e inquilino, filtrando por texto, tipo y estado. |
| **Prioridad** | Alta |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** se muestran las unidades que cumplen con los filtros seleccionados. <br> **Fracaso:** no aplica; el caso de uso no modifica el estado del sistema. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Unidades".
2. El sistema muestra los siguientes filtros y, debajo, el botón "Buscar":
   - Texto: campo de texto, opcional, máximo 50 caracteres. Busca
     coincidencias parciales en identificador, piso/sector y en el nombre y
     apellido del propietario o inquilino.
   - Tipo: lista desplegable, opcional, con las opciones "Todos",
     "Departamento", "Casa", "Habitación", "Local", "Cochera" y "Otro".
     Valor por defecto: "Todos".
   - Estado: lista desplegable, opcional, con las opciones "Todas",
     "Activa" y "Dada de baja". Valor por defecto: "Activa".
3. El sistema busca las unidades que cumplen con los filtros seleccionados.
   - Si hay resultados, los muestra en un listado paginado de 20 por
     página, ordenado por identificador en forma ascendente. Para cada
     unidad se muestra:
     - Identificador.
     - Tipo.
     - Piso/sector ("—" si no tiene).
     - Propietario: nombre y apellido; "Invitación pendiente" si hay una
       invitación pendiente para ese rol; "—" si no tiene.
     - Inquilino: nombre y apellido; "Reside el propietario" si el
       propietario reside en la unidad; "Invitación pendiente" si hay una
       invitación pendiente para ese rol; "—" si no tiene.
     - Estado.

     Al presionar el encabezado de una columna, el listado se ordena por
     esa columna, alternando entre orden ascendente y descendente. Debajo
     del listado se encuentran los controles para pasar de una página a
     otra. Para cada unidad en estado "Activa" se muestran los botones
     "Modificar" y "Dar de baja".
     Punto de extensión: "GestionarUnidadExistente".
   - Si no hay resultados, muestra el mensaje "No se encontraron unidades
     con los filtros seleccionados".
4. El administrador puede modificar los filtros y presionar "Buscar". El
   sistema vuelve al paso 3.

## Flujos alternativos

Ninguno.

## Flujos de excepción

Ninguno.

## Observaciones

- Las unidades dadas de baja no muestran botones: la baja de una unidad es
  definitiva. Sus reclamos e historial se conservan y pueden consultarse
  desde "Consultar historial de ubicación" (CU-034).
