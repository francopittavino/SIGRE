# 0005. Conservación de datos personales y política de privacidad

Fecha: 2026-11-03
Estado: Aceptada

## Contexto

Al redactar los requerimientos no funcionales se sumó uno de privacidad
(RNF-06), porque el sistema guarda datos personales de sus usuarios (tipo
y número de documento, nombre, apellido, teléfono, email) y fotos de los
reclamos. La Ley 25.326 de Protección de los Datos Personales da a sus
titulares, entre otros, el derecho a pedir la supresión de sus datos.

Esto choca con dos definiciones previas:

- El historial de cada reclamo es inmutable (objetivo específico 4).
- Al dar de baja a un usuario, sus reclamos e historial se conservan
  (CU-008), y la baja puede revertirse (CU-039).

## Opciones evaluadas

- **A. Conservar los datos e informarlo.** Los datos personales se
  conservan mientras haya reclamos o historial asociados al usuario, y el
  usuario lo acepta en una política de privacidad al registrarse.
- **B. Anonimizar al dar de baja.** Al dar de baja a un usuario se
  eliminan su documento, teléfono y email, y en el historial queda solo su
  nombre. Obliga a cambiar CU-008 y CU-039: un usuario anonimizado no
  podría reactivarse con sus datos.
- **C. Dejarlo pendiente** y marcar el punto como a definir.

## Decisión

Se adopta la opción A (decidida por Santiago Fumis en la sesión
2026-11-03):

- Los datos personales se conservan mientras haya reclamos o historial
  asociados al usuario, aunque se lo dé de baja. La finalidad del sistema
  es justamente conservar ese historial como respaldo ante discusiones de
  responsabilidad.
- Al completar su registro (CU-004), el usuario debe aceptar una política
  de privacidad que informa qué datos se guardan, para qué y por cuánto
  tiempo. El sistema registra la aceptación con fecha y hora.

## Consecuencias

- CU-004 suma la casilla obligatoria "Leí y acepto la política de
  privacidad" y el registro de la aceptación.
- CU-008 y CU-039 no cambian.
- Queda pendiente redactar el texto de la política de privacidad.
- Si la cátedra o el relevamiento indican que hace falta atender pedidos
  de supresión, la opción B queda como alternativa; este ADR se
  reemplazaría.
