# CU-029 — Reabrir reclamo

| Campo | Valor |
|---|---|
| **ID** | CU-029 |
| **Nombre** | Reabrir reclamo |
| **Breve descripción** | Permite al residente que registró un reclamo indicar que el problema no fue resuelto, para que la administración vuelva a gestionarlo. |
| **Prioridad** | Alta |
| **Complejidad** | Baja |
| **Actor principal** | Residente |
| **Actores secundarios** | — (el Servicio de Email participa a través de CU-038) |
| **Precondiciones** | El residente tiene una sesión iniciada en el sistema. <br> El residente es el autor del reclamo seleccionado. |
| **Postcondiciones** | **Éxito:** el reclamo queda en estado "Reabierto" y la reapertura queda registrada en el historial del reclamo con la fecha y hora, el autor y el motivo. <br> **Fracaso:** el reclamo conserva su estado. |

## Flujo principal

1. El caso de uso comienza cuando el residente presiona "Reabrir" sobre un
   reclamo seleccionado.
2. El sistema valida que el reclamo esté en estado "Resuelto".
3. El sistema muestra el mensaje "Contanos por qué el problema no fue
   resuelto" y, debajo, el siguiente campo y los botones "Reabrir" y
   "Volver":
   - Motivo: área de texto, obligatoria, entre 10 y 1000 caracteres.
4. El residente completa el motivo y presiona "Reabrir".
5. El sistema valida que el motivo cumpla con el formato requerido.
6. El sistema cambia el estado del reclamo a "Reabierto" y registra en el
   historial del reclamo la reapertura, con la fecha y hora, el autor y el
   motivo.
7. include(Enviar notificación por email), con el aviso de reapertura y el
   motivo, dirigido al administrador y a los adherentes del reclamo.
8. El sistema muestra el mensaje "El reclamo N° *número* fue reabierto. La
   administración volverá a gestionarlo".

## Flujos alternativos

- **2.a El reclamo no está en estado "Resuelto":**
  - 2.a.1 El sistema muestra el mensaje "Solo se puede reabrir un reclamo
    marcado como resuelto que todavía no fue cerrado".
  - 2.a.2 El residente presiona "Aceptar".
  - 2.a.3 Finaliza el caso de uso.
- **5.a El motivo no cumple con el formato requerido:**
  - 5.a.1 El sistema vuelve al paso 3. Debajo del campo se muestra la
    regla que no se cumple.

## Flujos de excepción

- En el paso 3 el residente puede presionar "Volver". El sistema no
  realiza ningún cambio y finaliza el caso de uso.

## Observaciones

- El reclamo reabierto conserva su número, rubro, prioridad, adhesiones e
  historial. El administrador lo sigue gestionando con "Cambiar estado de
  reclamo" (CU-032).
- Un reclamo puede reabrirse más de una vez; cada reapertura queda en el
  historial, lo que permite detectar reparaciones que no resolvieron la
  causa del problema.
