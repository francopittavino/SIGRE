# CU-014 — Agregar ubicación compartida

| Campo | Valor |
|---|---|
| **ID** | CU-014 |
| **Nombre** | Agregar ubicación compartida |
| **Breve descripción** | Permite al administrador registrar una nueva área común o instalación compartida del espacio, para que los residentes puedan registrar reclamos sobre ella. |
| **Prioridad** | Alta |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** la nueva ubicación compartida queda registrada en estado "Activa". <br> **Fracaso:** no se registra la ubicación compartida. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Agregar
   ubicación compartida".
2. El sistema muestra los siguientes campos a completar y, debajo, el
   botón "Guardar":
   - Nombre: campo de texto, obligatorio, entre 2 y 50 caracteres; solo
     letras, dígitos, espacios, guion y punto (por ejemplo, "Ascensor 1",
     "Terraza", "Bomba de agua").
   - Tipo: lista desplegable, obligatoria, con las opciones "Área común"
     (por ejemplo, hall, terraza, pileta) e "Instalación" (por ejemplo,
     ascensor, bomba, portón).
   - Descripción: área de texto, opcional, máximo 500 caracteres.
3. El administrador completa los campos y presiona "Guardar".
4. El sistema valida que los campos cumplan con el formato requerido.
5. El sistema valida que no exista otra ubicación compartida activa con el
   mismo nombre, sin distinguir mayúsculas de minúsculas.
6. El sistema registra la ubicación compartida en estado "Activa" y
   muestra el mensaje "La ubicación *nombre* fue agregada".

## Flujos alternativos

- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.
- **5.a Ya existe una ubicación compartida activa con ese nombre:**
  - 5.a.1 El sistema muestra el mensaje "Ya existe una ubicación
    compartida activa con el nombre *nombre*" y vuelve al paso 2.

## Flujos de excepción

- En el paso 2 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema descarta los datos ingresados y finaliza el caso
  de uso.

## Observaciones

- Los reclamos registrados sobre una ubicación compartida son
  automáticamente comunitarios: todos los propietarios e inquilinos del
  espacio pueden verlos y adherir a ellos.
- El nombre es único solo entre ubicaciones activas: como la baja es
  definitiva, puede reutilizarse el nombre de una ubicación dada de baja.
