# Bitácora de sesiones

Un archivo por sesión de trabajo, generado por la skill `cerrar-sesion`.

**Nombre de archivo**: `YYYY-MM-DD-HHmm-slug.md` (fecha y hora de inicio de
la sesión, `slug` corto derivado del objetivo). El orden alfabético de los
nombres de archivo coincide con el orden cronológico.

**Contenido de cada entrada**:

```markdown
# Sesión YYYY-MM-DD HH:mm

Integrantes: ...
Objetivo: ...

## Qué se hizo

## Decisiones

## Archivos tocados

## Pendientes
```

La skill `abrir-sesion` lee la entrada más reciente de esta carpeta al
empezar cada sesión para poner al día a quien arranca a trabajar.
