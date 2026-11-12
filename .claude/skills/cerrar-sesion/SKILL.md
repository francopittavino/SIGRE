---
name: cerrar-sesion
description: Ritual de cierre de sesión de trabajo en SIGRE. Muestra el resumen de cambios, revisa el diff en busca de secretos o archivos que no deberían commitearse, redacta bitácora/ADR/CHANGELOG para aprobación, commitea en commits lógicos con Conventional Commits en español, y pushea tras rebasar contra el remoto. Usar siempre al terminar de trabajar, es el único momento en que se commitea y pushea.
---

# cerrar-sesion

Ritual de cierre de sesión para el equipo de SIGRE (3 integrantes). Es el
único momento del flujo en que se commitea y se pushea. Ejecutar los pasos en
orden; ninguno se salta ni se adelanta sin aprobación explícita del usuario en
los puntos marcados como tal.

## Convenciones del proyecto que este skill asume

- **Bitácora**: `docs/bitacora/YYYY-MM-DD-HHmm-slug.md`.
- **ADRs**: `docs/decisiones/NNNN-slug.md`, numeración secuencial. Formato
  sugerido: Título, Fecha, Estado (Propuesta/Aceptada/Rechazada/Reemplazada),
  Contexto, Decisión, Consecuencias.
- **CHANGELOG**: `CHANGELOG.md` en formato Keep a Changelog, sección
  `[Unreleased]` para cambios sin versión todavía asignada.
- **Nota de sesión**: la que abrió `abrir-sesion` en
  `.agents/session-notes/` (no versionada). Es el insumo principal de la
  entrada de bitácora de este cierre. Una vez que la bitácora quedó escrita y
  aprobada, la nota puede borrarse (no hace falta conservarla, no está
  versionada).
- **Co-authored-by**: no hay un roster versionado de integrantes. Si en la
  sesión participó más de una persona, preguntar en este paso nombre y email
  de cada co-autor para armar los trailers.

## Pasos

### 1. Mostrar el resumen de lo trabajado

- `git status`.
- `git diff --stat` (y `git diff --stat --cached` si ya hay algo en stage).
- Mostrar el contenido de la nota de sesión de `.agents/session-notes/`.

### 2. Revisar el diff en busca de cosas que no deberían commitearse

Recorré el diff completo (no solo el `--stat`) buscando, como mínimo:

- Credenciales/claves: patrones tipo API key, tokens, `AWS_SECRET`,
  `-----BEGIN PRIVATE KEY-----`, contraseñas en texto plano, connection
  strings con usuario/password embebido.
- Archivos de entorno: `.env`, `.env.*`, `*.pem`, `*.key`,
  `credentials.json` o similares.
- Datos personales reales de entrevistas (nombres, contactos, transcripciones
  con información identificable de personas reales, no anonimizada).
- Binarios pesados que no deberían vivir en git (dumps de base de datos,
  videos, zips grandes, exports).
- Archivos temporales/basura de editor u OS (`*.tmp`, `*.bak`, `.DS_Store`,
  `Thumbs.db`, carpetas de build).

Si encontrás algo de esto: **FRENÁ**, mostrale al usuario qué encontraste y
en qué archivo, y proponé la entrada de `.gitignore` correspondiente (o sacar
el archivo del stage) antes de seguir a redactar nada. No seas exhaustivo
como un scanner dedicado — esto es una revisión heurística, decilo si tenés
dudas en vez de asumir que algo es seguro.

### 3. Redactar y proponer para aprobación (todavía sin escribir nada)

Presentale al usuario, para que apruebe o corrija antes de que escribas
ningún archivo:

- **Entrada de bitácora** (`docs/bitacora/YYYY-MM-DD-HHmm-slug.md`): fecha,
  integrantes, objetivo, qué se hizo, decisiones tomadas, archivos tocados,
  pendientes. Basate en la nota de sesión, no la reescribas desde cero.
- **ADR** si hubo alguna decisión de peso durante la sesión (arquitectura,
  esquema de datos, elección de librería/servicio con impacto difícil de
  revertir). Si no hubo ninguna, decilo explícitamente y no inventes una.
- **Actualización de CHANGELOG.md** si corresponde (cambios visibles para
  quien usa el sistema, no housekeeping interno).

Esperá confirmación explícita antes de pasar al punto 4. Si el usuario pide
cambios al texto, iterá antes de escribir.

### 4. Recién ahí, escribir los archivos y commitear

- Escribí bitácora / ADR / CHANGELOG ya aprobados.
- Agrupá el resto de los cambios (código, docs, config) junto con estos en
  **commits lógicos y coherentes** — nunca un commit único con todo
  mezclado. Un criterio razonable: un commit por unidad de cambio con sentido
  propio (ej. una feature, un fix, la actualización de docs/bitácora como
  commit aparte si no está atada 1:1 a un cambio de código).
- Mensajes en formato Conventional Commits, en español (`feat:`, `fix:`,
  `docs:`, `refactor:`, `chore:`, etc.).
- Si trabajó más de una persona en la sesión, preguntá los datos de
  co-autoría que falten y agregá al final del mensaje:

  ```
  Co-authored-by: Nombre Apellido <email@ejemplo.com>
  ```

- **Mostrale al usuario los mensajes de commit propuestos (agrupados) antes
  de ejecutar `git commit`.** Esperá confirmación.

### 5. Antes de pushear, verificar que el remoto no avanzó

- `git fetch`.
- Si el remoto avanzó desde que arrancó la sesión: `git pull --rebase`.
  - Si hay conflictos: **FRENÁ**, mostrá los archivos en conflicto y esperá
    indicaciones del usuario. No los resuelvas por tu cuenta.

### 6. Push

- `git push`.
- Confirmá que salió bien y mostrale al usuario el hash de los commits
  pusheados (`git log --oneline -n <cantidad>`).

### Después de pushear

- Si la nota de sesión en `.agents/session-notes/` ya no hace falta (su
  contenido pasó a la bitácora), podés borrarla. No es obligatorio: al no
  estar versionada, no ensucia el repo si queda.
