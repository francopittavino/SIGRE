# CU-025 — Modificar reclamo

| Campo | Valor |
|---|---|
| **ID** | CU-025 |
| **Nombre** | Modificar reclamo |
| **Breve descripción** | Permite al residente que registró un reclamo corregir su título, descripción, fotos y datos de convivencia mientras el reclamo todavía no fue tomado por la administración. |
| **Prioridad** | Media |
| **Complejidad** | Media |
| **Actor principal** | Residente |
| **Actores secundarios** | — (el Servicio de IA participa a través de CU-037) |
| **Precondiciones** | El residente tiene una sesión iniciada en el sistema. <br> El residente es el autor del reclamo seleccionado. |
| **Postcondiciones** | **Éxito:** los datos modificados del reclamo quedan registrados y la modificación queda registrada en el historial del reclamo. <br> **Fracaso:** no se modifica ningún dato del reclamo. |

## Flujo principal

1. El caso de uso comienza cuando el residente presiona "Modificar" sobre
   un reclamo seleccionado.
2. El sistema valida que el reclamo esté en estado "Ingresado".
3. El sistema valida que el reclamo no tenga adhesiones.
4. El sistema muestra en solo lectura la ubicación del reclamo, y los
   siguientes campos editables con sus datos actuales y, debajo, el botón
   "Guardar":
   - Es un problema de convivencia: casilla de verificación.
   - Unidad involucrada: lista desplegable, opcional, que solo se muestra
     si está marcada "Es un problema de convivencia". Contiene las
     unidades activas del espacio, excepto las vinculadas al residente; de
     cada una se muestra el identificador.
   - Título: campo de texto, obligatorio, entre 5 y 100 caracteres.
   - Descripción: área de texto, obligatoria, entre 20 y 2000 caracteres.
   - Fotos: se muestran las fotos actuales, cada una con la opción
     "Quitar", y la carga de archivos para agregar nuevas. En total, hasta
     5 archivos en formato JPG o PNG, de hasta 5 MB cada uno.
5. El residente modifica los datos que desea y presiona "Guardar".
6. El sistema valida que los campos cumplan con el formato requerido.
7. Si se modificó el título, la descripción o la indicación de
   convivencia, include(Sugerir rubro de reclamo), con los nuevos datos.
8. El sistema guarda los cambios y registra en el historial del reclamo
   la modificación, con la fecha y hora y el autor.
9. El sistema muestra el mensaje "Tu reclamo N° *número* fue actualizado".

## Flujos alternativos

- **2.a El reclamo no está en estado "Ingresado":**
  - 2.a.1 El sistema muestra el mensaje "El reclamo ya fue tomado por la
    administración y no puede modificarse. Podés agregar un comentario
    con la información adicional".
  - 2.a.2 El residente presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.
- **3.a El reclamo tiene adhesiones:**
  - 3.a.1 El sistema muestra el mensaje "El reclamo tiene adhesiones de
    otros residentes y no puede modificarse. Podés agregar un comentario
    con la información adicional".
  - 3.a.2 El residente presiona "Aceptar".
  - 3.a.3 Finaliza el caso de uso.
- **5.a El residente no modificó ningún dato:**
  - 5.a.1 El sistema muestra el mensaje "No hay cambios para guardar" y
    vuelve al paso 4.
- **6.a La validación de formato falla:**
  - 6.a.1 El sistema vuelve al paso 4. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.

## Flujos de excepción

- En el paso 4 el residente puede cancelar la operación presionando
  "Cancelar". El sistema descarta los cambios y finaliza el caso de uso.

## Observaciones

- La ubicación no se puede modificar: si el reclamo se registró sobre una
  ubicación equivocada, el residente lo cancela (CU-026) y registra uno
  nuevo.
- Un reclamo con adhesiones no se modifica porque los adherentes se
  sumaron al reclamo tal como estaba descripto.
