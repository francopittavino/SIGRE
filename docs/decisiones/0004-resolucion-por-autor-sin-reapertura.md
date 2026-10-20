# 0004. Resolución por el autor y eliminación de la reapertura

Fecha: 2026-10-20
Estado: Aceptada

## Contexto

El ADR [0003](0003-circuito-de-estados-del-reclamo.md) estableció que solo
el administrador marca un reclamo como "Resuelto" y que después el autor
confirma (→ Cerrado) o reabre (→ Reabierto), con cierre automático a los
7 días si no responde.

Al revisar los supuestos de los casos de uso, el equipo decidió
simplificar el circuito:

- Hay problemas que se resuelven sin la administración (el residente lo
  arregla por su cuenta, el problema desaparece). Obligar a esperar a que
  el administrador lo marque deja reclamos abiertos sin sentido.
- La reapertura agrega un estado, un caso de uso y complejidad en los
  reportes, a cambio de un beneficio que puede cubrirse registrando un
  reclamo nuevo, que además queda en el historial de la ubicación.

## Opciones evaluadas

- **A. Mantener el circuito del ADR 0003.**
- **B. "Resuelto" como estado final**, eliminando "Cerrado" y el cierre
  automático.
- **C. Resuelto lo marcan el autor o el administrador, sin reapertura, y
  pasa a "Cerrado" a los 7 días.** Mantiene un período en el que el
  reclamo sigue admitiendo comentarios antes de cerrarse definitivamente.

## Decisión

Se adopta la opción C:

| Estado actual | Estados posibles | Quién |
|---|---|---|
| Ingresado | Asignado (al categorizar), Rechazado | Administrador |
| Ingresado | Cancelado | Residente autor (sin adhesiones) o baja del usuario |
| Asignado | En curso, Resuelto, Rechazado | Administrador |
| En curso | Esperando repuesto/tercero, Resuelto | Administrador |
| Esperando repuesto/tercero | En curso, Resuelto | Administrador |
| Ingresado, Asignado, En curso, Esperando repuesto/tercero | Resuelto | Residente autor; en reclamos comunitarios, mayoría de autor y adherentes |
| Resuelto | Cerrado (a los 7 días) | Tiempo |

- Se elimina el estado "Reabierto" y el CU-029 (Reabrir reclamo).
- CU-028 pasa de "Confirmar resolución" a "Marcar reclamo como resuelto",
  con comentario obligatorio (opcional en el voto de un reclamo
  comunitario).
- Estados finales: Cerrado, Rechazado y Cancelado. "Resuelto" no admite
  cambios de estado salvo el cierre automático.
- Rechazar y resolver exigen un comentario, salvo el voto de resolución en
  un reclamo comunitario.
- Cada transición queda en el historial inmutable, como en el ADR 0003.

## Consecuencias

- El residente ya no puede objetar una resolución mal hecha dentro del
  mismo reclamo: debe registrar uno nuevo. La recurrencia se sigue
  detectando por ubicación y rubro (CU-034, CU-035).
- Desaparecen de los reportes la cantidad de reaperturas y el concepto de
  "primera resolución".
- En un reclamo comunitario, el lado de los residentes da el reclamo por
  resuelto por mayoría: votan el autor y los adherentes, y alcanza con más
  de la mitad (CU-028). El administrador puede resolverlo directamente.
- El administrador puede pasar un reclamo de "Asignado" a "Resuelto" sin
  pasar por "En curso", para arreglos rápidos.
- Cada cambio de estado notifica a los interesados del reclamo (definidos
  en CU-038).
