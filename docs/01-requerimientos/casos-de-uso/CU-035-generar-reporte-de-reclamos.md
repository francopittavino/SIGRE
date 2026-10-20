# CU-035 — Generar reporte de reclamos

| Campo | Valor |
|---|---|
| **ID** | CU-035 |
| **Nombre** | Generar reporte de reclamos |
| **Breve descripción** | Permite al administrador generar reportes sobre los reclamos de un período: cantidad por estado y rubro, tiempos de resolución y reclamos recurrentes por ubicación. |
| **Prioridad** | Media |
| **Complejidad** | Alta |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** se muestra el reporte seleccionado para el período indicado. <br> **Fracaso:** no aplica; el caso de uso no modifica el estado del sistema. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Reportes".
2. El sistema muestra los siguientes campos y, debajo, el botón "Generar":
   - Tipo de reporte: lista desplegable, obligatoria, con las opciones
     "Reclamos por estado y rubro", "Tiempos de resolución" y "Reclamos
     recurrentes por ubicación".
   - Desde: campo de tipo calendario, obligatorio, que solo permite fechas
     hasta el día de hoy. Valor por defecto: 12 meses antes del día de
     hoy.
   - Hasta: campo de tipo calendario, obligatorio, que solo permite fechas
     hasta el día de hoy y posteriores o iguales a "Desde". Valor por
     defecto: el día de hoy.
   - Mínimo de reclamos: campo numérico, obligatorio, entero entre 2 y 50,
     que solo se muestra si el tipo es "Reclamos recurrentes por
     ubicación". Valor por defecto: 3.
3. El administrador completa los campos y presiona "Generar".
4. El sistema valida que los campos cumplan con el formato requerido.
5. El sistema busca los reclamos registrados en el período indicado y
   genera el reporte según el tipo seleccionado:
   - **Reclamos por estado y rubro:** una tabla con un rubro por fila
     (más la fila "Sin categorizar") y un estado por columna, con la
     cantidad de reclamos en cada celda y los totales por fila y por
     columna.
   - **Tiempos de resolución:** para cada rubro, la cantidad de reclamos
     resueltos, el promedio y el máximo de días desde el registro hasta la
     resolución, el plazo objetivo del rubro y el porcentaje de
     reclamos resueltos fuera de plazo; y los mismos valores para el total.
   - **Reclamos recurrentes por ubicación:** las combinaciones de
     ubicación y rubro con una cantidad de reclamos mayor o igual al
     mínimo indicado, ordenadas por cantidad en forma descendente. Para
     cada una se muestra la ubicación, el rubro, la cantidad de reclamos
     y la fecha del último reclamo.

   Si no hay reclamos en el período, el sistema muestra el mensaje "No hay
   reclamos registrados en el período seleccionado".
   Debajo del reporte se muestra el botón "Descargar CSV".
6. El administrador puede presionar "Descargar CSV". El sistema genera un
   archivo CSV con los datos del reporte y lo descarga.
7. El administrador puede modificar los campos y presionar "Generar". El
   sistema vuelve al paso 4.

## Flujos alternativos

- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.

## Flujos de excepción

Ninguno.

## Observaciones

- Los reportes de tiempos usan la fecha en que el reclamo pasó a
  "Resuelto", ya sea por la administración (CU-032) o por su autor
  (CU-028).
- Un reclamo se considera resuelto fuera de plazo si pasó a "Resuelto"
  después de su fecha objetivo de resolución, que se
  fija al categorizarlo (CU-031). Los días hasta la resolución, en cambio,
  se cuentan desde la fecha de registro.
- El reporte de reclamos recurrentes apunta al problema económico
  planteado en el alcance: detectar reparaciones que se repiten sobre una
  misma unidad o instalación.
