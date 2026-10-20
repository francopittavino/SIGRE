# CU-021 — Registrar reclamo

| Campo | Valor |
|---|---|
| **ID** | CU-021 |
| **Nombre** | Registrar reclamo |
| **Breve descripción** | Permite a un residente registrar un reclamo de mantenimiento o de convivencia sobre una de sus unidades o sobre una ubicación compartida, con descripción y fotos. El sistema sugiere automáticamente el rubro. |
| **Prioridad** | Alta |
| **Complejidad** | Alta |
| **Actor principal** | Residente |
| **Actores secundarios** | — (el Servicio de IA participa a través de CU-037 y el Servicio de Email a través de CU-038) |
| **Precondiciones** | El residente tiene una sesión iniciada en el sistema. <br> El residente tiene al menos una unidad vinculada. |
| **Postcondiciones** | **Éxito:** el reclamo queda registrado en estado "Ingresado", con número, fecha y hora, autor, ubicación, prioridad base "Media" y, si fue posible obtenerlo, rubro sugerido. El alta queda registrada en el historial del reclamo y el administrador es notificado. <br> **Fracaso:** no se registra el reclamo. |

## Flujo principal

1. El caso de uso comienza cuando el residente presiona "Nuevo reclamo".
2. El sistema muestra los siguientes campos a completar y, debajo, el
   botón "Registrar":
   - Ubicación: selección de una opción, obligatoria, entre "Mi unidad" y
     "Ubicación compartida".
   - Unidad: lista desplegable, obligatoria si la ubicación es "Mi
     unidad". Contiene las unidades activas vinculadas al residente; de
     cada una se muestra su identificador. Si tiene una sola, aparece
     preseleccionada.
   - Ubicación compartida: lista desplegable, obligatoria si la ubicación
     es "Ubicación compartida". Contiene todas las ubicaciones compartidas
     activas del espacio, ordenadas alfabéticamente; de cada una se
     muestra su nombre.
   - Es un problema de convivencia: casilla de verificación, opcional,
     desmarcada por defecto.
   - Unidad involucrada: lista desplegable, opcional, que solo se muestra
     si se marcó "Es un problema de convivencia". Contiene las unidades
     activas del espacio, excepto las vinculadas al residente; de cada una
     se muestra su identificador.
   - Título: campo de texto, obligatorio, entre 5 y 100 caracteres.
   - Descripción: área de texto, obligatoria, entre 20 y 2000 caracteres.
   - Fotos: carga de archivos, opcional, hasta 5 archivos en formato JPG
     o PNG, de hasta 5 MB cada uno.
3. El residente completa los campos y presiona "Registrar".
4. El sistema valida que los campos cumplan con el formato requerido.
5. Si la ubicación es una ubicación compartida, el sistema busca los reclamos abiertos sobre
   esa ubicación.
   - Si hay resultados, muestra el mensaje "Ya hay reclamos abiertos sobre
     *nombre de la ubicación*. Si es el mismo problema, podés adherir en
     lugar de registrar uno nuevo" y, para cada reclamo, su número,
     título, estado, fecha de registro y cantidad de adhesiones, con el
     botón "Adherir".
     Punto de extensión: "ReclamoSimilarExistente".
     Debajo se muestra el botón "Registrar de todos modos". El residente
     presiona "Registrar de todos modos".
   - Si no hay resultados, continúa en el paso 6.
6. include(Sugerir rubro de reclamo), con el título y la descripción
   ingresados y el tipo de rubro que corresponde ("Convivencia" si se
   marcó "Es un problema de convivencia"; "Mantenimiento" en caso
   contrario).
7. El sistema registra el reclamo con:
   - un número correlativo único.
   - estado "Ingresado".
   - fecha y hora de registro.
   - el residente como autor.
   - la ubicación, la indicación de convivencia y la unidad involucrada, si
     corresponde.
   - la indicación de comunitario, si la ubicación es compartida.
   - prioridad base "Media".
   - el rubro sugerido, si se obtuvo.
   - el título, la descripción y las fotos.

   Además, registra en el historial del reclamo el alta con estado
   "Ingresado", la fecha y hora y el autor.
8. include(Enviar notificación por email), con el aviso de nuevo reclamo,
   dirigido al administrador. Si el reclamo es comunitario, también se
   envía, con un enlace al reclamo para ver el detalle o adherir, a todos
   los residentes activos del espacio (usuarios en estado "Activo" con al
   menos una unidad vinculada), excepto al autor.
9. El sistema muestra el mensaje "Tu reclamo N° *número* fue registrado.
   Te avisaremos por email cada vez que cambie de estado".

## Flujos alternativos

- **4.a La validación de formato falla:**
  - 4.a.1 El sistema vuelve al paso 2, conservando los datos ingresados.
    Debajo de cada campo erróneo se muestra la regla que no se cumple (por
    ejemplo, "Cada foto debe ser JPG o PNG y pesar hasta 5 MB").

## Flujos de excepción

- En los pasos 2 y 5 el residente puede cancelar la operación presionando
  "Cancelar". El sistema descarta los datos ingresados y finaliza el caso
  de uso.

## Observaciones

- Los reclamos sobre una ubicación compartida son comunitarios, también
  los de convivencia: todos los propietarios e inquilinos del espacio
  pueden verlos y adherir a ellos. Por eso, al registrarse uno, se avisa
  a todos los residentes activos.
- Un reclamo de convivencia sobre una unidad no es comunitario: lo ven el
  autor, la administración y el propietario y el inquilino actuales de la
  unidad involucrada, que ven también quién lo registró (ver CU-024).
- El rubro sugerido no es definitivo: el administrador lo confirma o lo
  cambia al categorizar el reclamo (CU-031). Si la sugerencia no puede
  obtenerse, el reclamo se registra sin rubro sugerido.
- La prioridad base "Media" es provisoria hasta que el administrador
  categoriza el reclamo. Las adhesiones suben la prioridad un nivel por
  cada 20 % de los residentes activos que adhirieron (ver CU-027).
- Un usuario sin unidades vinculadas no puede registrar reclamos; solo
  consulta los que registró anteriormente.
- Si la unidad involucrada en un problema de convivencia no figura en el
  sistema, el residente puede describirla en la descripción.
