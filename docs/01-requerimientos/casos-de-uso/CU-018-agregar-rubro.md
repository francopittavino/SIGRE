# CU-018 — Agregar rubro

| Campo | Valor |
|---|---|
| **ID** | CU-018 |
| **Nombre** | Agregar rubro |
| **Breve descripción** | Permite al administrador registrar un nuevo rubro para categorizar reclamos, de mantenimiento o de convivencia, con su plazo objetivo de resolución. |
| **Prioridad** | Alta |
| **Complejidad** | Baja |
| **Actor principal** | Administrador |
| **Actores secundarios** | — |
| **Precondiciones** | El administrador tiene una sesión iniciada en el sistema. |
| **Postcondiciones** | **Éxito:** el nuevo rubro queda registrado en estado "Activo" y disponible para categorizar reclamos. <br> **Fracaso:** no se registra el rubro. |

## Flujo principal

1. El caso de uso comienza cuando el administrador presiona "Agregar
   rubro".
2. El sistema muestra los siguientes campos a completar y, debajo, el
   botón "Guardar":
   - Nombre: campo de texto, obligatorio, entre 2 y 50 caracteres; solo
     letras, dígitos, espacios, guion y punto (por ejemplo, "Plomería",
     "Electricidad", "Ruidos molestos").
   - Tipo: lista desplegable, obligatoria, con las opciones
     "Mantenimiento" y "Convivencia".
   - Descripción: área de texto, obligatoria, entre 10 y 500 caracteres.
     Describe qué problemas abarca el rubro (por ejemplo, "Pérdidas de
     agua, cañerías, desagües, canillas y tanques").
   - Plazo objetivo de resolución: campo numérico, obligatorio, entero
     entre 1 y 365, expresado en días.
3. El administrador completa los campos y presiona "Guardar".
4. El sistema valida que los campos cumplan con el formato requerido.
5. El sistema valida que no exista otro rubro activo con el mismo nombre,
   sin distinguir mayúsculas de minúsculas.
6. El sistema registra el rubro en estado "Activo" y muestra el mensaje
   "El rubro *nombre* fue agregado".

## Flujos alternativos

- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2. Debajo de cada campo erróneo se
    muestra la regla que no se cumple.
- **5.a Ya existe un rubro activo con ese nombre:**
  - 5.a.1 El sistema muestra el mensaje "Ya existe un rubro activo con el
    nombre *nombre*" y vuelve al paso 2.

## Flujos de excepción

- En el paso 2 el administrador puede cancelar la operación presionando
  "Cancelar". El sistema descarta los datos ingresados y finaliza el caso
  de uso.

## Observaciones

- La descripción es obligatoria porque, junto con el nombre, es la
  referencia que usa la sugerencia automática de rubro (CU-037) para
  elegir el rubro más adecuado a un reclamo.
- El plazo objetivo se aplica a los reclamos al categorizarlos (CU-031) y
  permite identificar reclamos vencidos y medir tiempos en los reportes
  (CU-035).
- Los rubros de tipo "Convivencia" se usan para los reclamos entre vecinos
  (ruidos, mascotas, etc.).
