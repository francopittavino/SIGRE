# CU-028 — Marcar reclamo como resuelto

| Campo | Valor |
|---|---|
| **ID** | CU-028 |
| **Nombre** | Marcar reclamo como resuelto |
| **Breve descripción** | Permite al residente que registró un reclamo indicar que el problema ya fue resuelto, por ejemplo porque se solucionó por su cuenta, sin esperar a que lo haga la administración. En los reclamos comunitarios, el autor y los adherentes votan, y el reclamo se da por resuelto cuando lo indica la mayoría. |
| **Prioridad** | Alta |
| **Complejidad** | Media |
| **Actor principal** | Residente |
| **Actores secundarios** | — (el Servicio de Email participa a través de CU-038) |
| **Precondiciones** | El residente tiene una sesión iniciada en el sistema. <br> El residente es el autor del reclamo seleccionado o, si el reclamo es comunitario, uno de sus adherentes. |
| **Postcondiciones** | **Éxito:** si el reclamo no es comunitario, o si con este voto se alcanza la mayoría, el reclamo queda en estado "Resuelto" y el cambio queda registrado en el historial. Si es comunitario y todavía no se alcanza la mayoría, queda registrado el voto del residente. <br> **Fracaso:** el reclamo conserva su estado y no se registra ningún voto. |

## Flujo principal

1. El caso de uso comienza cuando el residente presiona "Marcar como
   resuelto" sobre un reclamo seleccionado.
2. El sistema valida que el reclamo esté en estado "Ingresado",
   "Asignado", "En curso" o "Esperando repuesto/tercero".
3. Si el reclamo es comunitario, el sistema valida que el residente no
   haya votado ya su resolución.
4. El sistema muestra el mensaje "¿Confirmás que el problema del reclamo
   N° *número* está resuelto? Una vez resuelto, el reclamo no puede
   volver a abrirse". Si el reclamo es comunitario, agrega: "Se dará por
   resuelto cuando lo indique más de la mitad de los residentes que lo
   registraron o adhirieron (*N* de *M* hasta ahora)". Debajo muestra el
   siguiente campo y los botones "Marcar como resuelto" y "Volver":
   - Comentario: área de texto, entre 10 y 1000 caracteres. Indica cómo se
     resolvió el problema. Es obligatorio si el reclamo no es comunitario
     y opcional si lo es.
5. El residente completa el comentario, si corresponde, y presiona
   "Marcar como resuelto".
6. El sistema valida que el comentario cumpla con el formato requerido.
7. Si el reclamo no es comunitario, el sistema:
   a. cambia el estado del reclamo a "Resuelto" y registra en el
      historial del reclamo el cambio, con la fecha y hora, el residente
      como autor, el estado anterior, el nuevo y el comentario.
   b. continúa en el paso 9.
8. Si el reclamo es comunitario, el sistema:
   a. registra el voto del residente con la fecha y hora, y lo registra
      en el historial del reclamo.
   b. cuenta los votos sobre el total de participantes (el autor más los
      adherentes).
   c. si los votos superan la mitad de los participantes, cambia el
      estado del reclamo a "Resuelto" y registra en el historial el
      cambio, con la fecha y hora, el autor "Residentes (mayoría *N* de
      *M*)", el estado anterior y el nuevo, y continúa en el paso 9.
   d. si no, muestra el mensaje "Registramos tu voto. Van *N* de *M*: el
      reclamo se dará por resuelto cuando lo indique más de la mitad" y
      finaliza el caso de uso.
9. Si se indicó un comentario, el sistema lo agrega a los comentarios
   visibles del reclamo.
10. include(Enviar notificación por email), con el aviso de resolución y,
    si lo hay, el comentario, dirigido al administrador y a los
    interesados del reclamo (ver CU-038).
11. El sistema muestra el mensaje "El reclamo N° *número* fue marcado como
    resuelto. Se cerrará automáticamente en 7 días".

## Flujos alternativos

- **2.a El reclamo no está en un estado que permita marcarlo como
  resuelto:**
  - 2.a.1 El sistema muestra el mensaje "El reclamo está en estado
    *estado* y no puede marcarse como resuelto".
  - 2.a.2 El residente presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.
- **3.a El residente ya votó la resolución:**
  - 3.a.1 El sistema muestra el mensaje "Ya indicaste que este reclamo
    está resuelto. Van *N* de *M*".
  - 3.a.2 El residente presiona "Aceptar".
  - 3.a.3 Finaliza el caso de uso.
- **6.a El comentario no cumple con el formato requerido:**
  - 6.a.1 El sistema vuelve al paso 4. Debajo del campo se muestra la
    regla que no se cumple.

## Flujos de excepción

- En el paso 4 el residente puede presionar "Volver". El sistema no
  realiza ningún cambio y finaliza el caso de uso.

## Observaciones

- En un reclamo que no es comunitario, solo el autor puede marcarlo como
  resuelto. El administrador lo hace desde "Cambiar estado de reclamo"
  (CU-032), sin necesidad de votación, también en los comunitarios.
- Mayoría: más de la mitad de los participantes. Por ejemplo, con el
  autor y 4 adherentes (5 participantes) hacen falta 3 votos. Si un
  reclamo comunitario no tiene adherentes, el voto del autor alcanza.
- Los votos no se retiran. La mayoría se recalcula cuando cambia la
  cantidad de participantes: una nueva adhesión (CU-027) la vuelve más
  exigente, y el retiro de adhesiones por baja de un usuario (CU-008), que
  también retira su voto, puede hacer que se alcance.
- "Resuelto" no admite reapertura. A los 7 días el sistema pasa el
  reclamo a "Cerrado" (CU-036). Si el problema vuelve a aparecer, se
  registra un reclamo nuevo.
- A diferencia de cancelar (CU-026), marcar como resuelto puede hacerse
  aunque el reclamo tenga adhesiones o ya haya sido tomado por la
  administración, y cuenta como resolución en los reportes (CU-035).
