# CU-031 — Categorizar reclamo

| Campo | Valor |
|---|---|
| **ID** | CU-031 |
| **Nombre** | Categorizar reclamo |
| **Breve descripción** | Permite al administrador confirmar o cambiar el rubro sugerido de un reclamo, asignarle una prioridad y ajustar su fecha objetivo de resolución. Al categorizar un reclamo ingresado, este pasa a estado "Asignado". |
| **Prioridad** | Alta |
| **Complejidad** | Media |
| **Actor principal** | Administrador |
| **Actores secundarios** | — (el Servicio de Email participa a través de CU-038) |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** el reclamo queda con el rubro, la prioridad asignada y la fecha objetivo de resolución indicados; si estaba en "Ingresado", pasa a "Asignado". Los cambios quedan registrados en el historial del reclamo. <br> **Fracaso:** el reclamo conserva su categorización y su estado. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Categorizar"
   sobre un reclamo seleccionado.
2. El sistema valida que el reclamo esté en estado "Ingresado",
   "Asignado", "En curso", "Esperando repuesto/tercero" o "Reabierto".
3. El sistema muestra el número, el título, la descripción y la ubicación
   del reclamo, y los siguientes campos y, debajo, el botón "Guardar":
   - Rubro: lista desplegable, obligatoria, que contiene los rubros
     activos del tipo del reclamo ("Mantenimiento" o "Convivencia"),
     ordenados alfabéticamente; de cada uno se muestra el nombre. Si el
     reclamo no fue categorizado todavía, aparece preseleccionado el rubro
     sugerido, con la indicación "Sugerido automáticamente".
   - Prioridad asignada: lista desplegable, obligatoria, con las opciones
     "Baja", "Media", "Alta" y "Urgente". Valor por defecto: la prioridad
     asignada actual ("Media" si no fue categorizado).
   - Fecha objetivo de resolución: campo de tipo calendario, obligatorio,
     que solo permite fechas a partir del día de hoy. Si el reclamo no fue
     categorizado, se completa con la fecha de hoy más el plazo objetivo
     del rubro seleccionado, y se recalcula al cambiar de rubro.

   Debajo de la prioridad se muestra la cantidad de adhesiones y la
   prioridad resultante (asignada más un nivel cada 3 adhesiones, con tope
   "Urgente").
4. El administrador confirma o modifica los datos y presiona "Guardar".
5. El sistema valida que los campos cumplan con el formato requerido.
6. El sistema guarda el rubro, la prioridad asignada y la fecha objetivo, y
   registra en el historial del reclamo los datos modificados, con la
   fecha y hora y el autor.
7. Si el reclamo estaba en estado "Ingresado", el sistema:
   a. cambia el estado a "Asignado" y lo registra en el historial.
   b. include(Enviar notificación por email), con el aviso del cambio de
      estado y el rubro asignado, dirigido al autor del reclamo, a sus
      adherentes y, si el autor no es el propietario de la unidad, al
      propietario.
8. El sistema muestra el mensaje "El reclamo N° *número* fue
   categorizado".

## Flujos alternativos

- **2.a El reclamo no está en un estado que permita categorizarlo:**
  - 2.a.1 El sistema muestra el mensaje "El reclamo está en estado
    *estado* y no puede categorizarse".
  - 2.a.2 El administrador presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.
- **4.a El administrador no modificó ningún dato en un reclamo ya
  categorizado:**
  - 4.a.1 El sistema muestra el mensaje "No hay cambios para guardar" y
    vuelve al paso 3.
- **5.a La validación de formato falla:**
  - 5.a.1 El sistema vuelve al paso 3. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.

## Flujos de excepción

- En el paso 3 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema descarta los cambios y finaliza el caso de uso.

## Observaciones

- La primera categorización es la que hace pasar el reclamo de
  "Ingresado" a "Asignado". En los demás estados abiertos el administrador
  puede recategorizar el reclamo sin cambiar su estado.
- Cuando el administrador recategoriza un reclamo ya categorizado, la
  fecha objetivo no se recalcula sola: se mantiene la vigente y el
  administrador puede ajustarla.
- Si el administrador elige un rubro distinto del sugerido, el historial
  registra ambos, lo que permite evaluar la calidad de la sugerencia
  automática.
