# Sesión 2026-09-07 08:40

Integrantes: Pittavino, Franco (con Claude Code)
Objetivo: arrancar el repositorio del proyecto SIGRE — dejar la gestión de
sesión del equipo lista, y producir la primera entrega para la cátedra
(propuesta de tema).

## Qué se hizo

- Se crearon las skills `abrir-sesion` y `cerrar-sesion` en
  `.agents/skills/`, con las convenciones de bitácora, ADRs, ramas y commits
  documentadas en `AGENTS.md`.
- Se relevó el contexto completo del proyecto (problema, objetivos,
  alcance) a partir de la consigna dada por el usuario, con varias rondas
  de preguntas para afinar el alcance real.
- Se redactó `docs/00-gestion/propuesta-tema.md` (y su versión con marca
  SIGRE en `.html`/`.pdf`) como primer documento de contextualización para
  que la cátedra apruebe el tema.
- Se completó la plantilla oficial de la cátedra
  (`docs/00-gestion/01_Presentación Idea-Proyecto.docx`) con los datos del
  proyecto, preservando el formato original (header UTN FRSF, tablas,
  estilos).
- Se incorporaron los assets de marca (`docs/branding/`: logo y paleta de
  colores SIGRE).

## Decisiones

- **Alcance del prototipo generalizado**: en vez de acotarse solo a
  consorcios de propiedad horizontal, el sistema se diseña para cualquier
  espacio de convivencia compartida (edificio, barrio privado, residencia
  estudiantil), tomando PH en Santa Fe como caso concreto de relevamiento.
  Ver ADR [0001](../decisiones/0001-alcance-generalizado-sin-prestador.md).
- **Sin rol de prestador externo** dentro del sistema: el administrador
  coordina la reparación por fuera del sistema. Ver mismo ADR.
- **Diferenciales confirmados**: reclamos comunitarios (adhesión, sube
  prioridad) y reclamos entre residentes/inquilinos (versión simple, sin
  mediación ni anonimato).
- Convención de trabajo: generar/editar archivos libremente durante la
  sesión, sin pedir aprobación previa; la única restricción dura es no
  pushear al remoto hasta el cierre (ya reflejado en `AGENTS.md`).

## Archivos tocados

- `.agents/skills/abrir-sesion/SKILL.md`, `.agents/skills/cerrar-sesion/SKILL.md`
- `AGENTS.md`, `.gitignore`, `CHANGELOG.md`
- `docs/bitacora/README.md`, `docs/decisiones/README.md`
- `docs/branding/logo.png`, `docs/branding/logo-small.png`, `docs/branding/paleta-colores.md`
- `docs/00-gestion/propuesta-tema.md`, `.html`, `.pdf`
- `docs/00-gestion/01_Presentación Idea-Proyecto.docx`, `.pdf`
- `01_Presentación Idea-Proyecto.docx` (plantilla original, sin completar, provista por la cátedra)

## Pendientes

- Completar "Carrera / cátedra" con datos exactos si faltara algo (ya
  cargado: UTN FRSF, Ingeniería en Sistemas de Información, docente
  Vallejos, Luciana).
- Avanzar con el relevamiento real (entrevistas a administración y
  propietarios) una vez aprobado el tema.
- Definir stack técnico del prototipo (todavía abierto, ver conversación
  previa).
