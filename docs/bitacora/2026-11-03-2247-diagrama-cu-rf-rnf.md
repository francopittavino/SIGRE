# Sesión 2026-11-03 22:47

Integrantes: Fumis, Santiago (con Claude Code)
Objetivo: diagrama de casos de uso en PlantUML y, después, redacción de los
requerimientos funcionales y no funcionales (pendientes de la sesión
anterior).

## Qué se hizo

- Se revisó qué piden la plantilla 02 (un "Diagrama de Casos de Uso",
  consistente con las fichas) y el material de cátedra (notación de
  puntos de extensión y «extend» con condición). El enunciado del TP no
  está en el repo.
- Diagrama de casos de uso en PlantUML: un diagrama general para la
  sección 4 y cuatro vistas por área con la notación completa de cátedra,
  con PNG y SVG generados. Un único diagrama con toda la notación
  quedaba ilegible.
- Se verificó por script que las vistas cubren exactamente las relaciones
  del general (38 CU, 15 include, 21 extend) y que los puntos de extensión
  coinciden con las fichas.
- Requerimientos funcionales RF-01 a RF-23, con trazabilidad a los CU
  (todos los CU quedan cubiertos).
- Requerimientos no funcionales RNF-01 a RNF-06, cada uno con su forma de
  verificación.

## Decisiones

- Diagrama general + vistas por área; el actor se asocia solo al CU base
  (como en el material de cátedra); CU-004 se representa con el actor
  Residente.
- RF agrupados por funcionalidad, cada uno con los CU que lo detallan.
- RNF: seguridad, integridad del historial, usabilidad y compatibilidad,
  rendimiento, confiabilidad ante servicios externos y privacidad. Web
  responsive; dos últimas versiones de Chrome, Firefox, Edge y Safari
  desde 360 px; 95 % de las operaciones en menos de 3 s con 50 usuarios
  concurrentes; cierre de sesión tras 2 h de inactividad; las tecnologías
  quedan fuera de los RNF.
- Privacidad: los datos personales se conservan mientras haya historial
  y se informa en una política de privacidad aceptada al registrarse
  (ADR [0005](../decisiones/0005-conservacion-de-datos-personales.md)).
  CU-004 suma la casilla de aceptación.
- Se corrigió el inventario: CU-003, CU-007, CU-008 y CU-039 incluyen
  CU-038, como ya decían sus fichas.

## Archivos tocados

- `docs/01-requerimientos/casos-de-uso/diagrama-cu*.puml|png|svg` y
  `estilo-cu.iuml` (nuevos)
- `docs/01-requerimientos/02-requerimientos-funcionales.md`,
  `03-requerimientos-no-funcionales.md` (nuevos)
- `docs/01-requerimientos/casos-de-uso/00-inventario.md`, `CU-004-…`
- `docs/decisiones/0005-…` (nuevo)

## Pendientes

- Que el equipo revise los RF y RNF; en particular, confirmar los puntos
  que propuso Claude como práctica estándar (hash con sal, permisos en el
  servidor, HTTPS, idioma y formato de fechas, errores junto al campo).
- Redactar el texto de la política de privacidad.
- Volcar todo en la plantilla 02 .docx (sección 4: general + vistas) y
  exportar a PDF.
- Generar las imágenes requiere Graphviz y PlantUML instalados
  (`scoop install graphviz extras/plantuml`).
