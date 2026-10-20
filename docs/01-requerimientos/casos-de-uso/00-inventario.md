# Inventario de casos de uso

> Aprobado en sesión 2026-10-20. Es la fuente del diagrama de casos de uso
> (`diagrama-cu.puml`) y de las fichas `CU-NNN-slug.md`. Si se agrega,
> saca o renombra un CU, actualizar acá primero.

## Actores

**Principales**

- **Usuario** (abstracto): generaliza a Administrador y Residente. Se usa
  en los CU de acceso y cuenta.
- **Administrador**: administra el espacio compartido (equivale también al
  encargado; es un único rol).
- **Residente** (abstracto): generaliza a Propietario e Inquilino.
- **Propietario**: puede ser residente o no residente. Ve además los
  reclamos que el inquilino de su unidad haga sobre ella y el historial de
  su unidad.
- **Inquilino**.
- **Tiempo**: activa el cierre automático de reclamos resueltos.

**Secundarios**

- **Servicio de IA**: sugiere el rubro de un reclamo a partir de su
  descripción.
- **Servicio de Email**: envía los correos (invitaciones, recuperación de
  contraseña, notificaciones de cambio de estado).

## Casos de uso

| ID | Caso de uso | Actor principal | Relaciones |
|---|---|---|---|
| **Acceso y cuenta** | | | |
| CU-001 | Iniciar sesión | Usuario | |
| CU-002 | Recuperar contraseña | Usuario | include CU-038 |
| CU-003 | Modificar datos de perfil | Usuario | |
| CU-004 | Completar registro | Residente invitado | |
| **Usuarios** | | | |
| CU-005 | Consultar usuarios | Administrador | punto de extensión |
| CU-006 | Invitar usuario | Administrador | include CU-038 |
| CU-007 | Modificar usuario | Administrador | extend CU-005 |
| CU-008 | Dar de baja usuario | Administrador | extend CU-005 |
| **Unidades** | | | |
| CU-009 | Consultar unidades | Administrador | punto de extensión |
| CU-010 | Agregar unidad | Administrador | |
| CU-011 | Modificar unidad | Administrador | extend CU-009 |
| CU-012 | Dar de baja unidad | Administrador | extend CU-009 |
| **Ubicaciones compartidas** | | | |
| CU-013 | Consultar ubicaciones compartidas | Administrador | punto de extensión |
| CU-014 | Agregar ubicación compartida | Administrador | |
| CU-015 | Modificar ubicación compartida | Administrador | extend CU-013 |
| CU-016 | Dar de baja ubicación compartida | Administrador | extend CU-013 |
| **Rubros** | | | |
| CU-017 | Consultar rubros | Administrador | punto de extensión |
| CU-018 | Agregar rubro | Administrador | |
| CU-019 | Modificar rubro | Administrador | extend CU-017 |
| CU-020 | Dar de baja rubro | Administrador | extend CU-017 |
| **Reclamos del residente** | | | |
| CU-021 | Registrar reclamo | Residente | include CU-037, CU-038; punto de extensión |
| CU-022 | Consultar mis reclamos | Residente | punto de extensión |
| CU-023 | Consultar reclamos comunitarios | Residente | punto de extensión |
| CU-024 | Ver detalle de reclamo | Residente, Administrador | extend CU-022, CU-023, CU-030, CU-034; punto de extensión |
| CU-025 | Modificar reclamo | Residente | extend CU-024; include CU-037 |
| CU-026 | Cancelar reclamo | Residente | extend CU-024; include CU-038 |
| CU-027 | Adherir a reclamo comunitario | Residente | extend CU-021, CU-023 |
| CU-028 | Marcar reclamo como resuelto | Residente | extend CU-024; include CU-038 |
| ~~CU-029~~ | ~~Reabrir reclamo~~ — eliminado en la revisión del 2026-10-20 (ver ADR 0004); el número no se reutiliza | | |
| **Reclamos del administrador** | | | |
| CU-030 | Consultar reclamos | Administrador | punto de extensión |
| CU-031 | Categorizar reclamo | Administrador | extend CU-030; include CU-038 |
| CU-032 | Cambiar estado de reclamo | Administrador | extend CU-030; include CU-038 |
| CU-033 | Agregar comentario a reclamo | Residente, Administrador | extend CU-024; include CU-038 |
| **Historial y reportes** | | | |
| CU-034 | Consultar historial de ubicación | Administrador, Propietario | punto de extensión |
| CU-035 | Generar reporte de reclamos | Administrador | |
| **Automáticos e incluidos** | | | |
| CU-036 | Cerrar reclamos resueltos automáticamente | Tiempo | include CU-038 |
| CU-037 | Sugerir rubro de reclamo | — (incluido) | secundario: Servicio de IA |
| CU-038 | Enviar notificación por email | — (incluido) | secundario: Servicio de Email |
| **Agregados después de aprobar el inventario** | | | |
| CU-039 | Reactivar usuario | Administrador | extend CU-005 |

## Decisiones de modelado

- ABM al estilo del material de cátedra: "Consultar X" con punto de
  extensión, extendido por Modificar y Dar de baja; "Agregar X" queda
  independiente.
- "Dar de baja" en lugar de "Eliminar": el historial es inmutable, por lo
  que una entidad con reclamos asociados se desactiva, no se borra.
- Rechazar un reclamo es parte de CU-032 (Cambiar estado), con motivo
  obligatorio.
- CU-022 es único para ambos tipos de residente: si el actor es
  propietario, también ve los reclamos del inquilino sobre su unidad.
- CU-035 es un solo CU con selección del tipo de reporte (por estado y
  rubro, tiempos de resolución, recurrentes por ubicación).
- CU-034 no extiende las consultas de unidades/ubicaciones porque el
  propietario no tiene acceso a ellas; es un CU independiente con dos
  actores.
- La sugerencia de rubro por IA (CU-037) se ejecuta al registrar el
  reclamo; el administrador confirma o cambia el rubro en CU-031.
- Un reclamo es comunitario automáticamente si su ubicación es compartida.
- El residente puede modificar o cancelar un reclamo solo mientras está en
  estado Ingresado.
- Roles por unidad: el rol de propietario o inquilino es una relación
  entre el usuario y cada unidad, no un atributo fijo del usuario. Una
  unidad tiene a lo sumo un propietario y un inquilino. Un propietario
  puede tener varias unidades, y una misma persona puede ser propietaria de
  una unidad e inquilina de otra. Si el propietario vive en la unidad, se
  marca "el propietario reside en la unidad" y no hay inquilino.
- La baja de usuario no es definitiva: puede revertirse con CU-039. La
  reactivación no restituye unidades, reclamos cancelados ni adhesiones.
- Estado "Cancelado" del reclamo: lo usan CU-026 (cancelación por el
  residente) y CU-008 (baja del usuario).
- Prioridad del reclamo: niveles Baja / Media / Alta / Urgente. Base
  "Media" al registrarse; el administrador la fija al categorizar
  (CU-031). Las adhesiones suben un nivel por cada 20 % de los residentes
  activos del espacio que adhirieron, con tope "Urgente".
- Sin anonimato: quien tiene acceso a un reclamo ve su autor, sus
  adherentes y el nombre de quien escribió cada comentario. Solo los
  comentarios internos del administrador quedan ocultos a los residentes.
- Reclamos de convivencia: el residente marca "Es un problema de
  convivencia" y puede indicar la unidad involucrada. Si se registran
  sobre una ubicación compartida son comunitarios, como cualquier otro.
  Si se registran sobre una unidad, los ven el autor, la administración y
  el propietario y el inquilino actuales de la unidad involucrada, que ven
  quién lo registró (sin anonimato) y pueden comentar. La IA sugiere solo
  rubros del tipo correspondiente.
- Al registrar un reclamo sobre una ubicación compartida con reclamos
  abiertos, el sistema ofrece adherir (CU-027 extiende CU-021).
- Un usuario sin unidades vinculadas no puede registrar reclamos.
- Circuito de estados (CU-028, CU-031, CU-032, ADR 0004): Ingresado →
  Asignado (al categorizar) o Rechazado; Asignado → En curso, Resuelto o
  Rechazado;
  En curso → Esperando repuesto/tercero o Resuelto; Esperando → En curso o
  Resuelto. Además, el autor puede pasar su reclamo a Resuelto desde
  cualquier estado abierto; si es comunitario, hace falta la mayoría de
  autor y adherentes (CU-028). Resuelto → Cerrado a los 7 días
  (CU-036); no hay reapertura. Finales: Cerrado, Rechazado, Cancelado.
  Rechazar y Resolver exigen comentario.
- Notificaciones de cambio de estado: a los interesados del reclamo
  (autor, adherentes, propietario de la unidad si no es el autor y, en
  convivencia, propietario e inquilino de la unidad involucrada; ver
  CU-038).
- Visibilidad por unidad: el propietario actual ve todos los reclamos de
  su unidad, incluidos los anteriores a que lo fuera; el inquilino actual
  ve los registrados mientras vive en ella (ADR 0002).
- Hay un único administrador por espacio; no se invitan administradores.
- Rubros precargados: al crearse el espacio se carga un conjunto inicial
  de rubros de mantenimiento y de convivencia (detalle en CU-017), que el
  administrador puede modificar o dar de baja.
- La cancelación de un reclamo (CU-026) se notifica al administrador.
- Un reclamo comunitario nuevo (CU-021) se notifica a todos los residentes
  activos del espacio, además del administrador.
- Si se invita a un email que ya tiene cuenta, la nueva unidad se asocia a
  esa cuenta (con aviso por email), sin un registro nuevo. No se puede
  invitar a una unidad cuyo rol ya está ocupado.
- Cierre: el admin (CU-032) o el autor (CU-028) marcan Resuelto; a los
  7 días CU-036 lo pasa a Cerrado (todos los días a las 00:00 hs).
