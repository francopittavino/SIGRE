# AGENTS.md

Instrucciones para agentes que trabajan en este repo (SIGRE).

## Skills de gestión de sesión

El equipo (3 integrantes) usa dos skills para estructurar cada sesión de
trabajo. Están versionadas en `.agents/skills/` y se invocan por nombre.

- **`abrir-sesion`** (`.agents/skills/abrir-sesion/SKILL.md`) — se invoca al
  empezar a trabajar. Verifica que no haya trabajo colgado de una sesión
  anterior, trae lo último del remoto, resume la última entrada de bitácora
  y los commits/ADRs nuevos, pregunta quién trabaja y con qué objetivo, y
  abre la nota de sesión.
- **`cerrar-sesion`** (`.agents/skills/cerrar-sesion/SKILL.md`) — se invoca
  al terminar. Revisa el diff, propone bitácora/ADR/CHANGELOG para
  aprobación, commitea en commits lógicos (Conventional Commits en español)
  y pushea recién al final.

**Regla que atraviesa toda la sesión**: generar y editar archivos
(documentos, código, carpetas) es libre, sin pedir aprobación previa — así
el equipo puede ir viendo el avance en las carpetas del repo a medida que
se trabaja. La única restricción dura es no pushear al remoto. Los commits
también quedan para `cerrar-sesion`, salvo pedido explícito del usuario.
`cerrar-sesion` es el único punto del flujo donde se toca git en serio.
Excepción: si el trabajo se vuelve muy voluminoso o se está por hacer algo
riesgoso, se puede *sugerir* (no ejecutar sin confirmación) un commit de
checkpoint intermedio.

## Convenciones que asumen estas skills

- **Ramas**: se trabaja siempre sobre `main`. El equipo es chico y coordina
  de palabra; no hay ramas por tarea. Si al abrir sesión el repo no está en
  `main`, es señal de algo pendiente — se avisa, no se resuelve solo.
- **Bitácora**: `docs/bitacora/YYYY-MM-DD-HHmm-slug.md`, un archivo por
  sesión. Ver `docs/bitacora/README.md`.
- **ADRs**: `docs/decisiones/NNNN-slug.md`, numeración secuencial. Ver
  `docs/decisiones/README.md`.
- **CHANGELOG**: `CHANGELOG.md`, formato Keep a Changelog.
- **Notas de sesión**: `.agents/session-notes/`, gitignoreado — nunca se
  versionan, son borradores de trabajo que alimentan la bitácora al cerrar.
- **Co-authored-by**: no hay roster versionado de integrantes; `cerrar-sesion`
  pregunta nombre y email de cada co-autor al momento de commitear, cuando
  corresponde.
- **Commits**: Conventional Commits, mensajes en español.

## Limitaciones conocidas (aceptadas deliberadamente)

- El aviso de "ADRs nuevos" en `abrir-sesion` no distingue si una persona en
  particular ya los vio — muestra todo lo nuevo desde la última entrada de
  bitácora, sin trackear estado por integrante.
- La revisión de secretos/datos sensibles en `cerrar-sesion` es heurística
  (lectura del diff por el agente), no un scanner dedicado tipo gitleaks. Si
  el proyecto crece, vale la pena sumar un hook de pre-commit dedicado.
