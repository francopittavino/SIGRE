# 3. Requerimientos No Funcionales

> Borrador de la sesión 2026-11-03, pendiente de revisión del equipo.
> Fuente para la sección 3 de la plantilla 02.
>
> Cada RNF indica cómo se verifica, para que el plan de pruebas
> (objetivo específico 5) pueda comprobarlo. Los RNF no fijan tecnologías
> (lenguaje, framework, base de datos, proveedor de IA): se definen en la
> etapa de diseño.

## RNF-01: Seguridad y control de acceso

- Todas las funcionalidades requieren una sesión iniciada, salvo iniciar
  sesión, recuperar la contraseña y completar el registro desde una
  invitación.
- Cada usuario accede solo a las funcionalidades de su rol y a los
  reclamos que le corresponden según su relación con cada unidad (ADR
  0002). Los permisos se verifican en el servidor en cada operación, no
  solo ocultando opciones en la interfaz.
- Las contraseñas tienen entre 8 y 64 caracteres, con al menos una letra
  y un número, y se almacenan con un algoritmo de hash con sal, de modo
  que no puedan recuperarse a partir de lo almacenado.
- Después de 3 intentos fallidos de inicio de sesión se impone una espera
  escalonada de 1, 5 y 15 minutos (CU-001).
- Los enlaces enviados por email son de un solo uso y vencen: 30 minutos
  los de recuperación de contraseña y 7 días los de invitación.
- La sesión se cierra automáticamente después de 2 horas sin actividad.
- Toda la comunicación entre el navegador y el servidor viaja cifrada
  (HTTPS).

**Verificación:** pruebas de acceso con cada rol a funcionalidades y
reclamos ajenos (deben rechazarse también llamando directamente al
servidor); revisión de que la base de datos no contiene contraseñas en
texto plano; pruebas de bloqueo, vencimiento de enlaces y de sesión.

## RNF-02: Integridad y trazabilidad del historial

- El historial de cada reclamo es de solo agregado: ningún usuario,
  incluido el administrador, puede modificar ni eliminar sus registros
  desde el sistema.
- Cada registro guarda la fecha y hora, el autor, el estado anterior, el
  nuevo y el motivo o comentario, si lo hay.
- Las entidades con reclamos asociados (usuarios, unidades, ubicaciones,
  rubros) no se eliminan: se dan de baja, y sus reclamos e historial se
  conservan.

**Verificación:** pruebas que intentan modificar o eliminar registros del
historial por todas las vías que ofrece el sistema; comprobación de que
cada cambio de estado del circuito genera exactamente un registro
completo.

## RNF-03: Usabilidad y compatibilidad

- El sistema es una aplicación web *responsive*: se usa desde la
  computadora y desde el navegador del celular, en pantallas desde 360 px
  de ancho, sin perder funcionalidades.
- Funciona en las dos últimas versiones estables de Chrome, Firefox, Edge
  y Safari, en escritorio y en celular (Chrome en Android, Safari en iOS).
- La interfaz está en español rioplatense; las fechas se muestran en
  formato dd/mm/aaaa y las horas en la zona horaria de Argentina.
- Los errores de validación se muestran junto al campo afectado e indican
  cómo corregirlo, sin borrar lo que el usuario ya completó.

**Verificación:** recorrido de los CU principales (registrar reclamo,
consultar, categorizar, cambiar estado) en cada navegador y en un celular
de 360 px de ancho.

## RNF-04: Rendimiento

- El 95 % de las operaciones (abrir pantallas, buscar, guardar) responde
  en menos de 3 segundos con hasta 50 usuarios usando el sistema al mismo
  tiempo.
- Quedan excluidas de esta medición la subida de fotos (hasta 5 archivos
  de 5 MB cada uno) y la espera de la sugerencia de rubro, que tiene su
  propio límite de 10 segundos (RNF-05).

**Verificación:** prueba de carga que simula 50 usuarios concurrentes
ejecutando las operaciones más frecuentes, midiendo el percentil 95 del
tiempo de respuesta.

## RNF-05: Confiabilidad ante fallas de servicios externos

- Si el servicio de IA no responde en 10 segundos o responde con un
  error, el reclamo se registra igual, sin rubro sugerido, y el error
  queda en el registro técnico del sistema (CU-037).
- Si falla el envío de un email, el sistema lo reintenta hasta 3 veces
  con 5 minutos de diferencia y, si sigue fallando, registra el fallo. La
  operación que originó el email no se revierte (CU-038).

**Verificación:** pruebas con el servicio de IA y el de email
deshabilitados o simulando demoras, comprobando que las operaciones se
completan y que las fallas quedan registradas.

## RNF-06: Privacidad de los datos personales

- El sistema trata datos personales de sus usuarios (tipo y número de
  documento, nombre, apellido, teléfono, email) y fotos de los reclamos,
  conforme a la Ley 25.326 de Protección de los Datos Personales.
- Los datos se usan solo para la gestión de reclamos del espacio. Los
  demás residentes ven únicamente el nombre y apellido de los autores,
  adherentes y comentaristas de los reclamos a los que tienen acceso; el
  documento, el teléfono y el email solo los ven el propio usuario y el
  administrador.
- Al completar su registro, el usuario debe aceptar una política de
  privacidad que informa qué datos se guardan, para qué y por cuánto
  tiempo (CU-004).
- Los datos personales se conservan mientras haya reclamos o historial
  asociados al usuario, aunque se lo dé de baja, porque el historial
  inmutable es la finalidad del sistema y sirve como respaldo ante
  discusiones de responsabilidad (ver ADR 0005).

**Verificación:** revisión de las pantallas a las que accede cada rol,
comprobando qué datos personales muestran; presencia y obligatoriedad de
la aceptación en el registro.

## Decisiones tomadas al redactar los RNF

Decididas por el equipo (Santiago Fumis, sesión 2026-11-03):

- Se incluyen seis RNF: los cinco básicos más privacidad de datos.
- Web *responsive* (computadora y navegador del celular).
- Navegadores: dos últimas versiones de Chrome, Firefox, Edge y Safari,
  desde 360 px de ancho.
- Rendimiento: 95 % de las operaciones en menos de 3 s con 50 usuarios
  concurrentes.
- Cierre de sesión por inactividad: 2 horas.
- Privacidad: conservar los datos mientras haya historial e informarlo en
  una política de privacidad aceptada al registrarse (ADR 0005).
- Las tecnologías quedan fuera de los RNF.

Tomados de las fichas ya aprobadas: largo y composición de la contraseña,
espera escalonada, vencimiento de enlaces, límite de fotos, límite de
10 s de la IA y reintentos de email.

Propuestos por Claude como práctica estándar, **a confirmar por el
equipo**: almacenamiento de contraseñas con hash con sal, verificación de
permisos en el servidor, HTTPS, idioma español rioplatense con fechas
dd/mm/aaaa y zona horaria de Argentina, y errores de validación junto al
campo.

Pendiente: redactar el texto de la política de privacidad (no forma parte
de la plantilla 02).
