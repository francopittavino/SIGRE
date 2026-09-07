---
name: abrir-sesion
description: Ritual de inicio de sesión de trabajo en SIGRE. Verifica el estado del repo, trae lo último del remoto, resume la sesión anterior (bitácora, commits nuevos, ADRs nuevos), pregunta quién trabaja y con qué objetivo, y abre la nota de sesión. Usar siempre al empezar a trabajar, antes de tocar código.
---

# abrir-sesion

Ritual de arranque de sesión para el equipo de SIGRE (3 integrantes). Ejecutar
los pasos en este orden exacto. No saltear pasos ni adelantar trabajo de
`cerrar-sesion`.

## Convenciones del proyecto que este skill asume

- **Rama de trabajo por defecto: `main`.** El equipo es chico y coordina de
  palabra; no se usan ramas por tarea. Si al arrancar la sesión el working
  directory no está en `main`, es una señal de que algo quedó a medio hacer:
  avisar y preguntar cómo seguir, no cambiar de rama por tu cuenta.
- **Bitácora**: `docs/bitacora/YYYY-MM-DD-HHmm-slug.md`, ordenable
  cronológicamente por nombre de archivo. La "última entrada" es el archivo
  con fecha/hora más reciente en esa carpeta.
- **ADRs**: `docs/decisiones/NNNN-slug.md` (numeración secuencial con cero a
  la izquierda).
- **Nota de sesión**: vive en `.agents/session-notes/`, que está en
  `.gitignore` — nunca se versiona. Es un borrador de trabajo, no un
  documento final.

## Pasos

### 1. Verificar el estado del repo antes de tocar nada

- Correr `git status`.
  - Si hay cambios sin commitear (staged o no) que no generaste vos en esta
    misma invocación, **FRENÁ**. No asumas que podés pisarlos ni
    descartarlos. Mostrale al usuario exactamente qué archivos están
    modificados/sin trackear y preguntá cómo proceder (¿es una sesión
    anterior que quedó colgada? ¿hay que rescatarla?). No sigas con los
    pasos siguientes hasta que el usuario decida.
- Correr `git branch --show-current`.
  - Si la rama actual no es `main`, avisar explícitamente ("estás en la rama
    X, no en main") y preguntar cómo seguir antes de continuar. No hagas
    `git checkout` por tu cuenta.

### 2. Traer lo último del remoto

- `git fetch`.
- `git pull --rebase`.
  - Si hay conflictos de rebase: **FRENÁ**. Mostrá la lista de archivos en
    conflicto (`git status` lo indica) y esperá indicaciones explícitas del
    usuario. No resuelvas conflictos por tu cuenta, no uses `--abort` ni
    `--continue` sin que te lo pidan.

### 3. Poner al usuario al día

Hacé esto en un solo resumen, breve y legible:

- **Última entrada de bitácora**: buscá el archivo más reciente en
  `docs/bitacora/` (por nombre, formato `YYYY-MM-DD-HHmm-slug.md`). Si la
  carpeta está vacía o no hay entradas todavía, decilo explícitamente (no
  hay sesión anterior que resumir). Si hay una, leela y resumí en pocas
  líneas: qué se hizo, quién la hizo (según la propia entrada o el commit
  que la agregó), y qué quedó pendiente.
- **Commits nuevos en el remoto**: `git log` acotado a los commits que
  entraron desde la fecha/commit de esa última entrada de bitácora (si no
  hay entrada previa, mostrá los últimos commits disponibles). Mostrá autor
  y fecha de cada uno para que el usuario sepa qué tocaron los otros dos
  integrantes.
- **ADRs nuevos**: listá los archivos en `docs/decisiones/` cuya fecha de
  creación (según git log de ese archivo) sea posterior a la fecha de la
  última entrada de bitácora. Aclaración: esto no distingue si *esta persona
  en particular* ya los vio, solo si son nuevos desde la última sesión
  registrada — decilo así de simple, no asumas que el usuario ya los leyó
  solo porque estaban ahí antes.

### 4. Preguntar quién trabaja y el objetivo

Preguntale directamente al usuario:

- Quién(es) participa(n) de esta sesión (nombre de los integrantes
  presentes).
- Cuál es el objetivo de la sesión.

No sigas sin esta info — es el encabezado de la nota de sesión y después de
la entrada de bitácora.

### 5. Abrir la nota de trabajo de la sesión

- Creá `.agents/session-notes/YYYY-MM-DD-HHmm-slug.md` (fecha/hora de inicio
  de esta sesión, slug corto derivado del objetivo).
- Encabezado inicial:

  ```markdown
  # Sesión YYYY-MM-DD HH:mm

  Integrantes: ...
  Objetivo: ...

  ## Registro
  ```

- A partir de acá, **mantené esta nota actualizada vos mismo, sin que el
  usuario te lo pida**, agregando entradas breves a medida que avanza la
  sesión: qué se hizo, decisiones tomadas (aunque no ameriten ADR), archivos
  tocados. Esta nota es el insumo directo de la entrada de bitácora que se
  redacta en `cerrar-sesion` — cuanto más completa quede, menos hay que
  reconstruir al cerrar.

## Regla que sigue durante toda la sesión

Desde acá hasta que se invoque `cerrar-sesion`, no hagas `git commit` ni
`git push` salvo que el usuario te lo pida explícitamente. Trabajá sobre el
working tree y registrá todo en la nota de sesión. Si el trabajo se vuelve
muy voluminoso, o estás por hacer algo riesgoso (refactor grande, cambio de
esquema de base), **sugerí** un punto de guardado intermedio (por ejemplo un
commit de checkpoint) — sugerilo nomás, no lo ejecutes sin confirmación.
