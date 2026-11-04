# 2. Requerimientos Funcionales

> Borrador de la sesión 2026-11-03, pendiente de revisión del equipo.
> Fuente para la sección 2 de la plantilla 02.
>
> **Criterio (decidido el 2026-11-03):** un RF por funcionalidad,
> agrupando los casos de uso que la componen; cada RF indica entre
> paréntesis los CU que lo detallan. Las reglas finas (campos, límites,
> mensajes) están en las fichas y no se repiten acá. Todos los CU del
> inventario quedan cubiertos por al menos un RF.

## Acceso y cuenta

- **RF-01:** El sistema debe permitir a los usuarios registrados iniciar
  sesión con su email y contraseña, y darles acceso solo a las
  funcionalidades de su rol. Ante intentos fallidos repetidos, debe
  imponer una espera creciente antes de permitir un nuevo intento.
  (CU-001)
- **RF-02:** El sistema debe permitir a un usuario que olvidó su
  contraseña definir una nueva mediante un enlace de un solo uso enviado a
  su email. (CU-002)
- **RF-03:** El sistema debe permitir a cada usuario modificar sus datos
  personales y su contraseña, y cambiar su email previa confirmación desde
  la casilla nueva. (CU-003)

## Usuarios

- **RF-04:** El sistema debe permitir al administrador invitar por email
  a una persona a ocupar el rol de propietario o inquilino de una unidad,
  y a la persona invitada completar su registro con sus datos personales,
  una contraseña y la aceptación de la política de privacidad. Si el email
  ya tiene una cuenta, la unidad se asocia a esa cuenta. (CU-006, CU-004)
- **RF-05:** El sistema debe permitir al administrador consultar los
  usuarios y las invitaciones del espacio, modificar los datos de un
  usuario, desvincularlo de sus unidades, darlo de baja y reactivarlo.
  (CU-005, CU-007, CU-008, CU-039)

## Configuración del espacio

- **RF-06:** El sistema debe permitir al administrador consultar,
  agregar, modificar y dar de baja las unidades privadas del espacio, e
  indicar si el propietario reside en la unidad. (CU-009, CU-010, CU-011,
  CU-012)
- **RF-07:** El sistema debe permitir al administrador consultar,
  agregar, modificar y dar de baja las ubicaciones compartidas del espacio
  (áreas comunes e instalaciones). (CU-013, CU-014, CU-015, CU-016)
- **RF-08:** El sistema debe permitir al administrador consultar,
  agregar, modificar y dar de baja los rubros de mantenimiento y de
  convivencia, cada uno con su plazo objetivo de resolución. Al crearse el
  espacio, el sistema debe cargar un conjunto inicial de rubros. (CU-017,
  CU-018, CU-019, CU-020)

## Reclamos del residente

- **RF-09:** El sistema debe permitir a un residente registrar un reclamo
  de mantenimiento o de convivencia sobre una de sus unidades o sobre una
  ubicación compartida, con título, descripción y fotos. Los reclamos
  sobre ubicaciones compartidas son comunitarios. Si ya hay reclamos
  abiertos sobre la misma ubicación compartida, el sistema debe ofrecer
  adherir a uno de ellos. (CU-021, CU-027)
- **RF-10:** El sistema debe sugerir automáticamente, mediante un servicio
  de inteligencia artificial, el rubro de un reclamo a partir de su título
  y descripción, al registrarlo o modificarlo. (CU-037, CU-021, CU-025)
- **RF-11:** El sistema debe permitir a cada residente consultar los
  reclamos a los que tiene acceso y ver su detalle (datos, fotos,
  historial y comentarios): los que registró, los que adhirió, los
  comunitarios y, según su rol en cada unidad, los registrados sobre ella
  (ver ADR 0002). (CU-022, CU-023, CU-024)
- **RF-12:** El sistema debe permitir al autor de un reclamo modificarlo o
  cancelarlo mientras está en estado "Ingresado". (CU-025, CU-026)
- **RF-13:** El sistema debe permitir a un residente adherir a un reclamo
  comunitario, y elevar la prioridad del reclamo un nivel por cada 20 % de
  los residentes activos del espacio que adhirieron, hasta "Urgente".
  (CU-027)
- **RF-14:** El sistema debe permitir al autor de un reclamo marcarlo como
  resuelto desde cualquier estado abierto. En los reclamos comunitarios,
  el reclamo pasa a "Resuelto" cuando lo indica la mayoría del autor y los
  adherentes. (CU-028)

## Gestión de reclamos por el administrador

- **RF-15:** El sistema debe permitir al administrador consultar todos los
  reclamos del espacio, filtrando por estado, rubro, ubicación, prioridad
  y otros criterios, y ver su detalle. (CU-030, CU-024)
- **RF-16:** El sistema debe permitir al administrador categorizar un
  reclamo: confirmar o cambiar el rubro sugerido, asignarle una prioridad
  y ajustar su fecha objetivo de resolución. Al categorizar un reclamo
  ingresado, pasa a "Asignado". (CU-031)
- **RF-17:** El sistema debe permitir al administrador cambiar el estado
  de un reclamo según el circuito de estados definido (ver ADR 0004),
  exigiendo un comentario al rechazarlo o resolverlo. (CU-032)
- **RF-18:** El sistema debe permitir al administrador y a los residentes
  con acceso a un reclamo agregar comentarios. El administrador puede
  marcar un comentario como interno, que no lo ven los residentes.
  (CU-033)
- **RF-19:** El sistema debe cerrar automáticamente, todos los días, los
  reclamos que llevan más de 7 días en estado "Resuelto". (CU-036)

## Historial y reportes

- **RF-20:** El sistema debe registrar en el historial del reclamo cada
  cambio de estado y cada modificación, con la fecha y hora, el autor, el
  estado anterior y el nuevo y el motivo o comentario, si lo hay. El
  historial no puede modificarse ni eliminarse. (CU-021, CU-025, CU-026,
  CU-028, CU-031, CU-032, CU-036)
- **RF-21:** El sistema debe permitir al administrador, y al propietario
  sobre sus unidades, consultar todos los reclamos registrados a lo largo
  del tiempo sobre una unidad o ubicación compartida. (CU-034)
- **RF-22:** El sistema debe permitir al administrador generar reportes de
  los reclamos de un período (cantidad por estado y rubro, tiempos de
  resolución y reclamos recurrentes por ubicación) y descargarlos en
  formato CSV. (CU-035)

## Notificaciones

- **RF-23:** El sistema debe enviar notificaciones por email a los
  interesados de cada reclamo ante cada cambio de estado, comentario
  visible, cancelación o registro de un reclamo comunitario, y los correos
  de invitación, recuperación de contraseña y avisos de cuenta. (CU-038 y
  los CU que lo incluyen)

## Trazabilidad RF → CU

| RF | CU |
|---|---|
| RF-01 | CU-001 |
| RF-02 | CU-002 |
| RF-03 | CU-003 |
| RF-04 | CU-004, CU-006 |
| RF-05 | CU-005, CU-007, CU-008, CU-039 |
| RF-06 | CU-009 a CU-012 |
| RF-07 | CU-013 a CU-016 |
| RF-08 | CU-017 a CU-020 |
| RF-09 | CU-021, CU-027 |
| RF-10 | CU-021, CU-025, CU-037 |
| RF-11 | CU-022, CU-023, CU-024 |
| RF-12 | CU-025, CU-026 |
| RF-13 | CU-027 |
| RF-14 | CU-028 |
| RF-15 | CU-024, CU-030 |
| RF-16 | CU-031 |
| RF-17 | CU-032 |
| RF-18 | CU-033 |
| RF-19 | CU-036 |
| RF-20 | CU-021, CU-025, CU-026, CU-028, CU-031, CU-032, CU-036 |
| RF-21 | CU-034 |
| RF-22 | CU-035 |
| RF-23 | CU-038 (y los CU que lo incluyen) |
