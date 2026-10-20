# CU-015 — Modificar ubicación compartida

| Campo | Valor |
|---|---|
| **ID** | CU-015 |
| **Nombre** | Modificar ubicación compartida |
| **Breve descripción** | Permite al administrador corregir los datos de un área común o instalación compartida del espacio. |
| **Prioridad** | Media |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. <br> La ubicación compartida seleccionada está en estado "Activa". |
| **Postcondiciones** | **Éxito:** los datos modificados de la ubicación compartida quedan registrados. <br> **Fracaso:** no se modifica ningún dato de la ubicación compartida. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Modificar"
   sobre una ubicación compartida seleccionada.
2. El sistema muestra los datos actuales de la ubicación en los siguientes
   campos editables y, debajo, el botón "Guardar":
   - Nombre: campo de texto, obligatorio, entre 2 y 50 caracteres; solo
     letras, dígitos, espacios, guion y punto.
   - Tipo: lista desplegable, obligatoria, con las opciones "Área común" e
     "Instalación".
   - Descripción: área de texto, opcional, máximo 500 caracteres.
3. El administrador modifica los datos que desea y presiona "Guardar".
4. El sistema valida que los campos cumplan con el formato requerido.
5. Si se modificó el nombre, el sistema valida que no exista otra
   ubicación compartida activa con el mismo nombre, sin distinguir
   mayúsculas de minúsculas.
6. El sistema guarda los cambios y muestra el mensaje "La ubicación
   *nombre* fue actualizada".

## Flujos alternativos

- **3.a No se modificó ningún dato:**
  - 3.a.1 El sistema muestra el mensaje "No hay cambios para guardar" y
    vuelve al paso 2.
- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.
- **5.a Ya existe una ubicación compartida activa con ese nombre:**
  - 5.a.1 El sistema muestra el mensaje "Ya existe una ubicación
    compartida activa con el nombre *nombre*" y vuelve al paso 2 sin
    guardar ningún dato.

## Flujos de excepción

- En el paso 2 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema descarta los cambios y finaliza el caso de uso.

## Observaciones

- Los reclamos y el historial quedan asociados a la ubicación, no a su
  nombre: cambiar el nombre no afecta el historial.
