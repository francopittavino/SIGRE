# Propuesta de tema — SIGRE

**SIGRE** — Sistema Integral de Gestión de Reclamos Edilicios.

## Integrantes

- Fumis, Santiago
- Pittavino, Franco
- Valente, Thiago

## Carrera / cátedra

[PENDIENTE: completar carrera, cátedra y docente(s) a cargo]

## 1. Problema y contexto

En los espacios donde varias personas conviven bajo una administración
común —consorcios de propiedad horizontal, barrios privados, residencias
estudiantiles, entre otros— el circuito de reclamos de mantenimiento
suele recaer sobre una sola persona (administrador o encargado), que
recibe, categoriza y hace seguimiento de los reclamos de las unidades a
su cargo. Hoy estos reclamos llegan por canales informales y dispersos
—teléfono, WhatsApp, notas dejadas en portería— sin un registro único de
qué se reclamó, cuándo, en qué estado quedó ni cuánto tiempo demoró en
resolverse.

Esta falta de registro estructurado tiene tres consecuencias concretas:

- **Operativa**: reclamos que se pierden o se duplican, e imposibilidad de
  priorizar entre ellos con criterio.
- **Económica**: sin un historial asociado a cada unidad no se detecta
  cuando un mismo desperfecto se repite, y se termina pagando varias
  veces una reparación parcial que no resolvió la causa de fondo.
- **Probatoria**: ante un daño, la discusión de responsabilidades entre
  quien reside, quien administra y terceros se dirime sobre la palabra de
  las partes, sin respaldo documental. A esto se suma que en muchos de
  estos espacios existe una distinción entre lo que es de uso y
  responsabilidad compartida y lo que es privado de cada unidad —en
  propiedad horizontal, por ejemplo, esta distinción está regulada por la
  normativa de cosas comunes y propias— y hoy esa distinción no queda
  registrada en ningún lado.

Este trabajo toma como caso concreto de relevamiento los consorcios de
propiedad horizontal de la ciudad de Santa Fe, con entrevistas a una
administración real y a propietarios. El problema y el diseño del
sistema, sin embargo, se plantean en términos generales, pensando también
en otros contextos de convivencia compartida (barrios privados,
residencias estudiantiles, entre otros).

## 2. Objetivo general

Desarrollar un prototipo de sistema de información que centralice el
registro de reclamos de mantenimiento en espacios de convivencia
compartida, ordene su categorización y seguimiento, y conserve la
trazabilidad completa desde el alta hasta el cierre.

## 3. Objetivos específicos

1. Relevar y documentar los requerimientos funcionales y no funcionales
   del circuito de reclamos, mediante entrevistas a una administración
   real de consorcios de propiedad horizontal y a propietarios, como caso
   concreto de relevamiento.
2. Modelar el dominio del problema —espacio compartido, unidades
   privadas, áreas e instalaciones comunes, y la distinción entre
   ubicación compartida y privada— de modo que el historial quede
   asociado a la unidad o instalación afectada, y no a la persona que
   reportó el reclamo, con un modelo que pueda aplicarse a distintos
   contextos de convivencia compartida sin requerir cambios
   estructurales.
3. Desarrollar el prototipo: alta y consulta de reclamos por parte de los
   residentes, y categorización, gestión de plazos y resolución por
   parte del administrador.
4. Implementar un registro de auditoría inmutable del sistema: cada
   cambio de estado de un reclamo queda registrado con autor y fecha,
   sin posibilidad de edición posterior.
5. Verificar, mediante un plan de pruebas, que el circuito de estados y
   el registro de auditoría se comporten según lo especificado.

## 4. Alcance del prototipo

- **Unidad de trabajo**: una instancia por espacio compartido (edificio,
  barrio privado, residencia, etc.). El prototipo no centraliza la
  gestión de varios espacios en una misma vista; cada uno se administra
  de forma independiente.
- **Roles**: residente (propietario o inquilino) y administrador/encargado,
  ambos con login propio. **No hay rol de prestador externo dentro del
  sistema**: el administrador ve el reclamo y coordina la reparación
  (con quién, cómo) por fuera del sistema.
- **Funcionalidades núcleo previstas**:
  - Alta de reclamo con categoría/rubro, ubicación (unidad privada o
    área/instalación compartida), descripción y fotos.
  - Categorización manual y automática por rubro.
  - Circuito de estados: Ingresado → Asignado (con rubro) → En curso →
    Esperando repuesto/tercero → Resuelto → Cerrado / Rechazado /
    Reabierto.
  - Historial inmutable por reclamo y por unidad.
  - Comentarios internos (administración) y comentarios visibles para el
    residente.
  - Notificaciones por email en cada cambio de estado.
- **Diferenciales confirmados**:
  - **Reclamos comunitarios**: varios residentes pueden adherir a un
    mismo reclamo (misma ubicación/rubro), lo que aumenta su prioridad.
  - **Reclamos entre vecinos (versión simple)**: categoría de reclamo
    para conflictos entre residentes (ruidos, mascotas, etc.), sin
    mediación formal ni anonimato — se gestiona con el mismo circuito
    que cualquier otro reclamo.
- **Visibilidad**: cada residente ve sus propios reclamos y los reclamos
  comunitarios (para poder adherirse); no ve los reclamos privados de
  otros residentes.

## 5. Justificación / aporte esperado

El proyecto aporta valor en tres frentes: reduce la pérdida y duplicación
de reclamos al centralizar su registro; permite detectar reparaciones
recurrentes sobre una misma unidad o instalación gracias al historial
asociado; y deja un respaldo documental de cada reclamo —incluida la
distinción entre ubicación compartida y privada— que hoy no existe y que
resulta relevante ante discusiones de responsabilidad entre las partes,
en cualquier espacio donde convivan varias unidades bajo una
administración común.

## 6. Metodología de trabajo

El desarrollo se organiza en etapas secuenciales con solapamiento
parcial: relevamiento (entrevistas a administración y propietarios) →
especificación de requerimientos → modelado del dominio → desarrollo del
prototipo → verificación mediante plan de pruebas → documentación final.
El modelo de dominio se diseña buscando minimizar los cambios necesarios
para aplicarlo a distintos contextos de convivencia compartida, aunque el
relevamiento y el prototipo concreto se desarrollan sobre el caso de
consorcios de propiedad horizontal. El equipo trabaja de forma
colaborativa (sin roles fijos por persona) y deja registro de cada
sesión de trabajo y de las decisiones relevantes en una bitácora y un
registro de decisiones (ADR) internos al equipo, que sirven de respaldo
del proceso ante consultas de la cátedra.

## 7. Fuentes de relevamiento

Entrevistas a una administración de consorcios real, y a propietarios e
inquilinos de propiedad horizontal en la ciudad de Santa Fe.
