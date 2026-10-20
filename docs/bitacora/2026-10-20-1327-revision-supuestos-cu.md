# Sesión 2026-10-20 13:27

Integrantes: Pittavino, Franco; Valente, Thiago (con Claude Code)
Objetivo: revisar los supuestos tomados por Claude en las fichas CU-009 a
CU-038 (pendiente de la sesión anterior).

## Qué se hizo

- Se relevaron los supuestos de las fichas CU-009 a CU-038 en
  `docs/01-requerimientos/revision-supuestos-cu.md` (inconsistencias entre
  fichas, supuestos de negocio y valores de detalle) y se revisaron uno
  por uno con el equipo.
- Se aplicaron las decisiones en las fichas, el inventario, el alcance y
  los ADRs 0002 y 0003; se redactó el ADR 0004.
- CU-028 se reescribió como "Marcar reclamo como resuelto" y se eliminó
  CU-029 "Reabrir reclamo" (el número no se reutiliza).

## Decisiones

- Visibilidad por unidad: el propietario actual ve todos los reclamos de
  su unidad (incluidos los anteriores a serlo); el inquilino actual ve los
  registrados mientras vive en ella. Ajustado en ADR
  [0002](../decisiones/0002-roles-por-unidad.md).
- Convivencia: sobre una unidad, lo ven autor, admin y propietario e
  inquilino de la unidad involucrada (que pueden comentar); sobre una
  ubicación compartida es comunitario.
- Sin anonimato: se ven autor, adherentes y nombre en los comentarios. Se
  mantienen los comentarios internos del admin.
- Prioridad por adhesiones: +1 nivel por cada 20 % de residentes activos
  adheridos (antes: cada 3 adhesiones).
- Circuito de estados (ADR
  [0004](../decisiones/0004-resolucion-por-autor-sin-reapertura.md),
  reemplaza al 0003): sin reapertura; Resuelto lo marca el admin (también
  desde Asignado) o el autor desde cualquier estado abierto; en
  comunitarios, por mayoría de autor + adherentes. Resuelto → Cerrado a
  los 7 días.
- Notificaciones: se definen los "interesados del reclamo" en CU-038; se
  avisa al admin al cancelar un reclamo y a todos los residentes activos
  cuando se registra un reclamo comunitario; los cierres avisan a todos
  los interesados.
- Rubros precargados al crear el espacio (7 de mantenimiento, 3 de
  convivencia), editables.
- El resto de los supuestos (ABM, límites de campos, reportes, servicios
  externos) se confirmó sin cambios.

## Archivos tocados

- `docs/01-requerimientos/01-alcance.md`, `casos-de-uso/00-inventario.md`
- Fichas CU-007, 008, 017, 021–028, 030–036, 038; CU-029 eliminada
- `docs/decisiones/0002-…`, `0003-…` (reemplazado), `0004-…` (nuevo)
- `docs/01-requerimientos/revision-supuestos-cu.md` (nuevo)

## Pendientes

- Diagrama de casos de uso en PlantUML (ya sin CU-029).
- Redactar RF y RNF (sección 3 de la plantilla).
- Volcar todo en la plantilla 02 .docx y exportar a PDF.
