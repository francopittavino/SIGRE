# Sesión 2026-10-20 11:56

Integrantes: Fumis, Santiago; Pittavino, Franco; Valente, Thiago (con Claude Code)
Objetivo: realizar la entrega 2 para la cátedra (plantilla 02, Especificación
de Requerimientos).

## Qué se hizo

- Se incorporaron la plantilla `02_Especificación de Requerimientos.docx` y
  el material de cátedra `EspecificacionesCU FRSF-UTN.pdf` (template de
  fichas de CU).
- Se redactó la sección 1 de la plantilla (alcance) en
  `docs/01-requerimientos/01-alcance.md`.
- Se armó el inventario de casos de uso (actores, 39 CU, relaciones
  include/extend y decisiones de modelado) en `casos-de-uso/00-inventario.md`.
- Se redactaron las 39 fichas de CU (CU-001 a CU-039), un archivo .md por
  CU, con el template de la cátedra. Los primeros CU se definieron uno por
  uno con el equipo; a partir de CU-009 se redactaron con supuestos
  propuestos por Claude y revisados por el equipo.

## Decisiones

- Formato de trabajo: un .md por CU; al final se vuelca todo a la
  plantilla .docx y se exporta a PDF. IDs CU-001 / RF-01 / RNF-01.
  Diagrama en PlantUML.
- La cátedra aprobó el tema sin observaciones; no hubo entrevistas todavía.
- Roles por unidad: propietario/inquilino es una relación usuario–unidad;
  a lo sumo un propietario y un inquilino por unidad; "propietario reside"
  como indicador; un solo administrador por espacio. Ver ADR
  [0002](../decisiones/0002-roles-por-unidad.md).
- Alta de usuarios por invitación del admin (7 días). Login con email y
  contraseña, con espera escalonada de 1/5/15 min cada 3 fallos por email y
  dispositivo (se descartó bloquear la cuenta para que nadie pueda
  bloquear una cuenta ajena). Recuperación por enlace (30 min), máximo 5
  solicitudes por mes calendario, reiniciables por el admin. Tipo de
  documento DNI o Pasaporte.
- La baja de usuario es reversible (CU-039 Reactivar usuario); la de
  unidades, ubicaciones compartidas y rubros es definitiva.
- Circuito de estados del reclamo: se agrega el estado "Cancelado"; el
  residente confirma o reabre, y si no responde en 7 días se cierra
  automáticamente. Ver ADR
  [0003](../decisiones/0003-circuito-de-estados-del-reclamo.md).
- Rubros con tipo (Mantenimiento / Convivencia) y plazo objetivo de
  resolución. Prioridad Baja/Media/Alta/Urgente, fijada por el admin y
  aumentada un nivel cada 3 adhesiones.
- Categorización: la IA sugiere el rubro al registrar el reclamo (solo
  con título y descripción, sin datos personales); el admin confirma o
  cambia.
- Los reclamos sobre ubicaciones compartidas son comunitarios (salvo los
  de convivencia); al registrar se ofrece adherir a reclamos abiertos de
  la misma ubicación.
- Reportes básicos dentro del alcance; fuera: expensas/pagos, app nativa,
  mediación de conflictos.

## Archivos tocados

- `docs/00-gestion/02_Especificación de Requerimientos.docx`,
  `docs/00-gestion/EspecificacionesCU FRSF-UTN.pdf`
- `docs/01-requerimientos/01-alcance.md`
- `docs/01-requerimientos/casos-de-uso/00-inventario.md`,
  `CU-001-….md` a `CU-039-….md`
- `docs/decisiones/0002-roles-por-unidad.md`,
  `docs/decisiones/0003-circuito-de-estados-del-reclamo.md`
- `.gitignore`, `CHANGELOG.md`

## Pendientes

- Revisar los supuestos tomados por Claude en CU-009 a CU-038, en especial
  el alcance del historial para el propietario (CU-034).
- Diagrama de casos de uso en PlantUML a partir del inventario.
- Redactar RF (derivados de las fichas) y RNF (sección 3 de la plantilla).
- Volcar todo en la plantilla 02 .docx y exportar a PDF. La plantilla no
  lleva fecha de presentación.
