# CU-010 — Agregar unidad

| Campo | Valor |
|---|---|
| **ID** | CU-010 |
| **Nombre** | Agregar unidad |
| **Breve descripción** | Permite al administrador registrar una nueva unidad privada del espacio, para que luego se le puedan asociar propietario e inquilino y registrar reclamos sobre ella. |
| **Prioridad** | Alta |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** la nueva unidad queda registrada en estado "Activa", sin propietario ni inquilino. <br> **Fracaso:** no se registra la unidad. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Agregar
   unidad".
2. El sistema muestra los siguientes campos a completar y, debajo, el
   botón "Guardar":
   - Identificador: campo de texto, obligatorio, entre 1 y 10 caracteres;
     solo letras, dígitos, espacios y guion (por ejemplo, "3B", "Casa 12",
     "PB-1").
   - Tipo: lista desplegable, obligatoria, con las opciones
     "Departamento", "Casa", "Habitación", "Local", "Cochera" y "Otro".
   - Piso/sector: campo de texto, opcional, máximo 30 caracteres (por
     ejemplo, "Piso 3", "Manzana B").
   - Descripción: área de texto, opcional, máximo 500 caracteres.
3. El administrador completa los campos y presiona "Guardar".
4. El sistema valida que los campos cumplan con el formato requerido.
5. El sistema valida que no exista otra unidad activa con el mismo
   identificador, sin distinguir mayúsculas de minúsculas.
6. El sistema registra la unidad en estado "Activa" y muestra el mensaje
   "La unidad *identificador* fue agregada".

## Flujos alternativos

- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.
- **5.a Ya existe una unidad activa con ese identificador:**
  - 5.a.1 El sistema muestra el mensaje "Ya existe una unidad activa con
    el identificador *identificador*" y vuelve al paso 2.

## Flujos de excepción

- En el paso 2 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema descarta los datos ingresados y finaliza el caso
  de uso.

## Observaciones

- El propietario y el inquilino de la unidad se asocian desde "Invitar
  usuario" (CU-006).
- El identificador es único solo entre unidades activas: como la baja de
  una unidad es definitiva, puede volver a usarse el identificador de una
  unidad dada de baja.
