# 1. Descripción del Alcance del Problema

> Borrador aprobado en sesión 2026-10-20. Fuente para la sección 1 de la
> plantilla 02.

SIGRE (Sistema Integral de Gestión de Reclamos Edilicios) es un prototipo
de sistema web que centraliza el registro, la categorización y el
seguimiento de los reclamos de mantenimiento en espacios de convivencia
compartida, es decir, lugares donde varias unidades conviven bajo una
administración común. Para el relevamiento se toman como caso concreto los
consorcios de propiedad horizontal de la ciudad de Santa Fe, pero el modelo
se plantea en términos generales para poder aplicarlo a otros contextos,
como barrios privados o residencias estudiantiles.

Cada instancia del sistema gestiona un único espacio compartido, con sus
unidades privadas y sus áreas e instalaciones compartidas. El sistema
contempla tres roles:

- **Administrador**: administra el espacio. Invita a los usuarios,
  configura unidades, ubicaciones y rubros, categoriza los reclamos,
  gestiona sus estados y coordina la reparación por fuera del sistema.
- **Propietario**: registra y sigue reclamos sobre su unidad y sobre las
  ubicaciones compartidas, y ve los reclamos que el inquilino de su unidad
  haga sobre ella. Puede ser residente o no residente.
- **Inquilino**: registra y sigue reclamos sobre la unidad que habita y
  sobre las ubicaciones compartidas.

Propietarios e inquilinos pueden ver los reclamos comunitarios del espacio
y adherir a ellos.

**Dentro del alcance:**

- Alta de usuarios por invitación del administrador.
- Alta de reclamos con ubicación (unidad privada o ubicación compartida),
  descripción y fotos.
- Categorización por rubro: el sistema sugiere el rubro con un servicio de
  IA y el administrador lo confirma o lo modifica.
- Circuito de estados del reclamo: Ingresado → Asignado → En curso →
  Esperando repuesto/tercero → Resuelto → Cerrado, con las variantes
  Rechazado y Cancelado. El autor también puede dar su reclamo por
  resuelto.
- Historial inmutable de cada cambio de estado, con autor y fecha,
  consultable por reclamo y por unidad o instalación.
- Comentarios internos de la administración y comentarios visibles para el
  residente.
- Notificaciones por email ante cada cambio de estado.
- Reclamos comunitarios, a los que propietarios e inquilinos pueden
  adherir, lo que aumenta su prioridad.
- Reclamos entre vecinos, gestionados con el mismo circuito que los demás.
- Reportes básicos: reclamos por estado y por rubro, tiempos de resolución
  y reclamos recurrentes por unidad o instalación.

**Fuera del alcance:**

- Rol de prestador externo: la reparación se coordina por fuera del
  sistema.
- Gestión de varios espacios desde una misma instancia.
- Expensas, pagos y costos de reparación.
- Aplicación móvil nativa: el sistema es web.
- Mediación formal o anonimato en los reclamos entre vecinos.
