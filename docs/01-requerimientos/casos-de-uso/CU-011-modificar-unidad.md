# CU-011 — Modificar unidad

| Campo | Valor |
|---|---|
| **ID** | CU-011 |
| **Nombre** | Modificar unidad |
| **Breve descripción** | Permite al administrador corregir los datos de una unidad e indicar si su propietario reside en ella. |
| **Prioridad** | Media |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. <br> La unidad seleccionada está en estado "Activa". |
| **Postcondiciones** | **Éxito:** los datos modificados de la unidad quedan registrados. <br> **Fracaso:** no se modifica ningún dato de la unidad. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Modificar"
   sobre una unidad seleccionada.
2. El sistema muestra los datos actuales de la unidad en los siguientes
   campos editables:
   - Identificador: campo de texto, obligatorio, entre 1 y 10 caracteres;
     solo letras, dígitos, espacios y guion.
   - Tipo: lista desplegable, obligatoria, con las opciones
     "Departamento", "Casa", "Habitación", "Local", "Cochera" y "Otro".
   - Piso/sector: campo de texto, opcional, máximo 30 caracteres.
   - Descripción: área de texto, opcional, máximo 500 caracteres.
   - El propietario reside en la unidad: casilla de verificación. Solo se
     habilita si la unidad tiene propietario (activo o con invitación
     pendiente).

   Debajo muestra en solo lectura el propietario y el inquilino actuales,
   y el botón "Guardar".
3. El administrador modifica los datos que desea y presiona "Guardar".
4. El sistema valida que los campos cumplan con el formato requerido.
5. Si se modificó el identificador, el sistema valida que no exista otra
   unidad activa con el mismo identificador, sin distinguir mayúsculas de
   minúsculas.
6. Si se marcó "El propietario reside en la unidad", el sistema valida que
   la unidad no tenga un inquilino vinculado ni una invitación pendiente de
   inquilino.
7. El sistema guarda los cambios y muestra el mensaje "La unidad
   *identificador* fue actualizada".

## Flujos alternativos

- **3.a No se modificó ningún dato:**
  - 3.a.1 El sistema muestra el mensaje "No hay cambios para guardar" y
    vuelve al paso 2.
- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.
- **5.a Ya existe una unidad activa con ese identificador:**
  - 5.a.1 El sistema muestra el mensaje "Ya existe una unidad activa con
    el identificador *identificador*" y vuelve al paso 2 sin guardar
    ningún dato.
- **6.a La unidad tiene inquilino:**
  - 6.a.1 El sistema muestra el mensaje "No se puede indicar que el
    propietario reside en la unidad porque tiene un inquilino vinculado o
    invitado. Desvinculá primero al inquilino" y vuelve al paso 2 sin
    guardar ningún dato.

## Flujos de excepción

- En el paso 2 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema descarta los cambios y finaliza el caso de uso.

## Observaciones

- El propietario y el inquilino no se modifican desde aquí: se asocian con
  "Invitar usuario" (CU-006) y se desvinculan con "Modificar usuario"
  (CU-007).
- Desmarcar "El propietario reside en la unidad" habilita la unidad para
  invitar a un inquilino.
- Los reclamos y el historial quedan asociados a la unidad, no a su
  identificador: cambiar el identificador no afecta el historial.
