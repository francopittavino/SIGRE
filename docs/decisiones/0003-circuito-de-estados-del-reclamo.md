# 0003. Circuito de estados del reclamo y cierre por confirmación del residente

Fecha: 2026-10-20
Estado: Aceptada

## Contexto

La propuesta de tema enumeraba los estados del reclamo (Ingresado,
Asignado, En curso, Esperando repuesto/tercero, Resuelto, Cerrado,
Rechazado, Reabierto) pero no definía las transiciones ni quién realiza
cada una. Al especificar los casos de uso surgieron además la cancelación
por parte del residente (CU-026) y la cancelación en cascada por la baja de
un usuario (CU-008), que no tenían estado propio.

El circuito de estados es la base del historial inmutable (objetivo
específico 4) y de los reportes de tiempos de resolución, por lo que
cambiarlo más adelante afecta datos ya registrados.

## Opciones evaluadas

- **A. El administrador maneja todos los estados**, incluidos Cerrado y
  Reabierto. Simple, pero el residente no puede objetar una resolución
  mal hecha.
- **B. El residente confirma o reabre**, sin límite de tiempo. Deja
  reclamos indefinidamente en "Resuelto" si el residente no responde.
- **C. El residente confirma o reabre, con cierre automático** si no
  responde en un plazo.

## Decisión

Se adopta la opción C, con el siguiente circuito:

| Estado actual | Estados posibles | Quién |
|---|---|---|
| Ingresado | Asignado (al categorizar), Rechazado | Administrador |
| Ingresado | Cancelado | Residente autor (sin adhesiones) o baja del usuario |
| Asignado | En curso, Rechazado | Administrador |
| En curso | Esperando repuesto/tercero, Resuelto | Administrador |
| Esperando repuesto/tercero | En curso, Resuelto | Administrador |
| Reabierto | En curso, Resuelto | Administrador |
| Resuelto | Cerrado, Reabierto | Residente autor |
| Resuelto | Cerrado (a los 7 días sin respuesta) | Tiempo |

- Estados finales: Cerrado, Rechazado y Cancelado.
- Rechazar y resolver exigen un comentario para el residente.
- Reabrir exige un motivo y puede repetirse.
- Cada transición queda en un historial inmutable, con fecha y hora,
  autor (o "Sistema"), estado anterior, nuevo y motivo.

## Consecuencias

- Aparece el actor Tiempo y el CU-036 (cierre automático diario).
- Se agrega el estado "Cancelado" al alcance.
- Los reportes de tiempos de resolución usan la primera vez que el reclamo
  pasó a "Resuelto"; las reaperturas se cuentan aparte, lo que permite
  detectar reparaciones que no resolvieron la causa de fondo.
- Cada cambio de estado notifica por email al autor, a los adherentes y al
  propietario de la unidad, si no es el autor.
