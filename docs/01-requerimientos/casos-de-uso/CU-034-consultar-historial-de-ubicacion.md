# CU-034 — Consultar historial de ubicación

| Campo | Valor |
|---|---|
| **ID** | CU-034 |
| **Nombre** | Consultar historial de ubicación |
| **Breve descripción** | Permite al administrador, o al propietario de una unidad, consultar todos los reclamos registrados a lo largo del tiempo sobre una unidad o ubicación compartida, para detectar problemas recurrentes. |
| **Prioridad** | Media |
| **Complejidad** | Media |
| **Actor principal** | Administrador, Propietario |
| **Actores secundarios** | — |
| **Precondiciones** | El usuario tiene una sesión iniciada en el sistema. <br> Si el usuario es propietario, tiene al menos una unidad vinculada como propietario. |
| **Postcondiciones** | **Éxito:** se muestra el historial de reclamos de la ubicación seleccionada. <br> **Fracaso:** no aplica; el caso de uso no modifica el estado del sistema. |

## Flujo principal

1. El caso de uso comienza cuando el usuario presiona "Historial de
   ubicación".
2. El sistema muestra los siguientes campos y, debajo, el botón
   "Consultar":
   - Ubicación: lista desplegable, obligatoria. Si el usuario es el
     administrador, contiene todas las unidades (se muestra el
     identificador) y ubicaciones compartidas (se muestra el nombre) del
     espacio, incluidas las dadas de baja, que se identifican con la
     indicación "(baja)". Si el usuario es propietario, contiene solo las
     unidades de las que es propietario. Si hay una sola opción, aparece
     preseleccionada.
   - Desde: campo de tipo calendario, opcional, que solo permite fechas
     hasta el día de hoy.
   - Hasta: campo de tipo calendario, opcional, que solo permite fechas
     hasta el día de hoy y posteriores o iguales a "Desde".
3. El usuario selecciona la ubicación, completa el período si lo desea y
   presiona "Consultar".
4. El sistema valida que los campos cumplan con el formato requerido.
5. El sistema busca todos los reclamos registrados sobre la ubicación
   seleccionada en el período indicado, en cualquier estado.
   - Si hay resultados, muestra:
     - Un resumen con la cantidad total de reclamos, la cantidad por
       rubro, la cantidad de reclamos reabiertos al menos una vez y, para
       cada rubro con 3 o más reclamos en los últimos 12 meses, la
       indicación "Problema recurrente".
     - Un listado paginado de 20 por página, ordenado por fecha de
       registro en forma descendente. Para cada reclamo se muestra:
       número, título, rubro, estado, fecha de registro, fecha de cierre,
       días hasta la resolución y cantidad de reaperturas.

     Para cada reclamo al que el usuario tiene acceso se muestra el botón
     "Ver detalle".
     Punto de extensión: "VerReclamoDelHistorial".
   - Si no hay resultados, muestra el mensaje "No hay reclamos registrados
     sobre esta ubicación en el período seleccionado".
6. El usuario puede modificar la ubicación o el período y presionar
   "Consultar". El sistema vuelve al paso 4.

## Flujos alternativos

- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.

## Flujos de excepción

Ninguno.

## Observaciones

- El historial queda asociado a la ubicación y no a quien registró los
  reclamos: el propietario ve en el resumen y en el listado todos los
  reclamos de su unidad, incluidos los registrados antes de que fuera
  propietario. Sin embargo, solo puede ver el detalle de los reclamos a
  los que tiene acceso (ver CU-024).
- Los reclamos de convivencia en los que la unidad figura como unidad
  involucrada no forman parte de su historial.
- "Días hasta la resolución" se calcula desde la fecha de registro hasta
  la primera vez que el reclamo pasó a "Resuelto".
