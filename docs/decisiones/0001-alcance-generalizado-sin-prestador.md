# 0001. Alcance generalizado a espacios de convivencia compartida, sin rol de prestador

Fecha: 2026-09-07
Estado: Aceptada

## Contexto

El planteo inicial del proyecto definía el alcance como "consorcios de
propiedad horizontal en Santa Fe", con un circuito de reclamos que incluía
un rol de "prestador externo" (plomero, electricista, etc.) con acceso al
sistema para gestionar la reparación derivada.

Al revisar el alcance con el equipo, surgieron dos cambios:

1. El sistema no está pensado únicamente para PH: aplica a cualquier
   espacio donde varias personas conviven bajo una administración común
   (barrios privados, residencias estudiantiles, etc.).
2. No existe, en la práctica, la necesidad de que el prestador externo
   tenga una cuenta dentro del sistema — el administrador ve el reclamo y
   coordina la reparación (con quién, cómo) por fuera del sistema.

## Opciones evaluadas

- **A. Mantener el alcance acotado a PH, con rol de prestador.** Más
  simple de relevar (ya hay contacto con una administración real), pero no
  refleja cómo el equipo quiere que funcione el sistema.
- **B. Generalizar el alcance y sacar el rol de prestador**, manteniendo
  el relevamiento concreto sobre PH como caso de estudio. El diseño del
  dominio busca minimizar los cambios necesarios para aplicarlo a otros
  contextos, sin comprometerse a relevarlos todos en esta instancia.
- **C. Generalizar sin ningún caso concreto de relevamiento.** Se descartó
  por falta de fuentes reales de relevamiento para los otros contextos
  (barrio privado, residencia estudiantil) — hubiera significado inventar
  datos.

## Decisión

Se adopta la opción B: el problema y el modelo de dominio se plantean en
términos generales (espacio compartido / unidad privada / ubicación
compartida vs. privada, en vez de edificio / unidad funcional / cosa común
vs. propia), pero el relevamiento y el prototipo concreto se desarrollan
sobre el caso de consorcios de propiedad horizontal de Santa Fe. No hay
rol de prestador externo dentro del sistema.

## Consecuencias

- El modelo de dominio no usa terminología exclusiva de la ley de
  propiedad horizontal (por ejemplo, "cosa común/propia" pasa a
  "ubicación compartida/privada"), lo que facilita generalizarlo más
  adelante sin reescribir el dominio.
- Se simplifican los roles del sistema a dos: residente y
  administrador/encargado.
- La "derivación" de un reclamo pasa a significar asignarle una
  categoría/rubro, no asignarlo a una persona/cuenta de prestador.
- Queda pendiente relevar formalmente otros contextos (barrio privado,
  residencia estudiantil) si el equipo decide extender el alcance en una
  entrega futura — por ahora son solo ejemplos ilustrativos, no fuente de
  requerimientos reales.
