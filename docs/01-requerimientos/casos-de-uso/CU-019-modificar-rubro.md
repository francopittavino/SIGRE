# CU-019 — Modificar rubro

| Campo | Valor |
|---|---|
| **ID** | CU-019 |
| **Nombre** | Modificar rubro |
| **Breve descripción** | Permite al administrador corregir los datos de un rubro, incluido su plazo objetivo de resolución. |
| **Prioridad** | Media |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. <br> El rubro seleccionado está en estado "Activo". |
| **Postcondiciones** | **Éxito:** los datos modificados del rubro quedan registrados. <br> **Fracaso:** no se modifica ningún dato del rubro. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Modificar"
   sobre un rubro seleccionado.
2. El sistema muestra los datos actuales del rubro en los siguientes
   campos editables y, debajo, el botón "Guardar":
   - Nombre: campo de texto, obligatorio, entre 2 y 50 caracteres; solo
     letras, dígitos, espacios, guion y punto.
   - Tipo: lista desplegable, obligatoria, con las opciones
     "Mantenimiento" y "Convivencia".
   - Descripción: área de texto, obligatoria, entre 10 y 500 caracteres.
   - Plazo objetivo de resolución: campo numérico, obligatorio, entero
     entre 1 y 365, expresado en días.
3. El administrador modifica los datos que desea y presiona "Guardar".
4. El sistema valida que los campos cumplan con el formato requerido.
5. Si se modificó el nombre, el sistema valida que no exista otro rubro
   activo con el mismo nombre, sin distinguir mayúsculas de minúsculas.
6. Si se modificó el tipo, el sistema valida que el rubro no tenga
   reclamos abiertos.
7. El sistema guarda los cambios y muestra el mensaje "El rubro *nombre*
   fue actualizado".

## Flujos alternativos

- **3.a No se modificó ningún dato:**
  - 3.a.1 El sistema muestra el mensaje "No hay cambios para guardar" y
    vuelve al paso 2.
- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.
- **5.a Ya existe un rubro activo con ese nombre:**
  - 5.a.1 El sistema muestra el mensaje "Ya existe un rubro activo con el
    nombre *nombre*" y vuelve al paso 2 sin guardar ningún dato.
- **6.a El rubro tiene reclamos abiertos:**
  - 6.a.1 El sistema muestra el mensaje "No se puede cambiar el tipo del
    rubro *nombre* porque tiene *N* reclamo(s) abierto(s)" y vuelve al
    paso 2 sin guardar ningún dato.

## Flujos de excepción

- En el paso 2 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema descarta los cambios y finaliza el caso de uso.

## Observaciones

- Un cambio en el plazo objetivo solo se aplica a los reclamos que se
  categoricen a partir de ese momento; los reclamos ya categorizados
  conservan el plazo que se les asignó.
- El tipo no puede cambiarse con reclamos abiertos porque cambiaría el
  tratamiento de reclamos que ya están en curso.
