# 0002. Roles de propietario e inquilino por unidad

Fecha: 2026-10-20
Estado: Aceptada

## Contexto

La propuesta de tema definía los roles "propietario" e "inquilino" como si
fueran atributos fijos de cada usuario. Al especificar los casos de uso de
alta de usuarios (CU-004, CU-006) aparecieron situaciones que ese modelo no
cubre:

- Un propietario puede tener varias unidades.
- Una misma persona puede ser propietaria de una unidad e inquilina de
  otra dentro del mismo espacio.
- El propietario puede vivir en su unidad (no hay inquilino) o alquilarla.
- El propietario necesita ver los reclamos que su inquilino hace sobre la
  unidad.

## Opciones evaluadas

- **A. Rol fijo por usuario** (cada usuario es propietario o inquilino).
  Simple, pero no admite que una persona tenga roles distintos en unidades
  distintas.
- **B. Relación muchos a muchos libre** entre usuarios y unidades, con
  varios propietarios (cotitulares) e inquilinos (convivientes) por
  unidad. Más realista en algunos casos, pero complica la visibilidad de
  reclamos y las notificaciones, y el equipo no lo necesita.
- **C. Rol por unidad con cupo**: el rol es una relación usuario–unidad;
  cada unidad tiene a lo sumo un propietario y un inquilino, y un
  indicador "el propietario reside en la unidad".

## Decisión

Se adopta la opción C:

- El rol (propietario o inquilino) es una relación entre el usuario y cada
  unidad, no un atributo del usuario.
- Cada unidad tiene a lo sumo un propietario y un inquilino. Un
  propietario puede tener varias unidades.
- Si el propietario vive en la unidad, se marca "el propietario reside en
  la unidad" y no se puede invitar inquilino. El propietario no puede ser
  además inquilino de su propia unidad.
- Para invitar un inquilino, la unidad debe tener propietario (activo o
  con invitación pendiente) que no resida en ella.
- Hay un único administrador por espacio.

## Consecuencias

- Invitar usuario (CU-006) asocia una unidad por vez; si el email ya tiene
  cuenta, la unidad se asocia a esa cuenta sin un registro nuevo. Una
  invitación pendiente reserva el rol de la unidad.
- Desvincular (CU-007) y dar de baja (CU-008) no pueden dejar a un
  inquilino sin propietario: primero hay que desvincular al inquilino.
- Visibilidad: el propietario ve los reclamos de su unidad mientras sea su
  propietario; al desvincularse, cada usuario conserva solo los reclamos
  que registró, y el nuevo ocupante no ve los de los anteriores. El
  historial por ubicación (CU-034) sí muestra al propietario todos los
  reclamos de su unidad, pero sin acceso al detalle de los ajenos.
- Un usuario puede quedar sin unidades y seguir entrando para consultar
  sus reclamos anteriores, pero no puede registrar reclamos nuevos.
