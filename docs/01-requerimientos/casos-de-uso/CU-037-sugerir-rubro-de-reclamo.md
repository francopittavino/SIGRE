# CU-037 — Sugerir rubro de reclamo

| Campo | Valor |
|---|---|
| **ID** | CU-037 |
| **Nombre** | Sugerir rubro de reclamo |
| **Breve descripción** | Obtiene, mediante un servicio de inteligencia artificial, el rubro activo más adecuado para un reclamo a partir de su título y descripción. |
| **Prioridad** | Media |
| **Complejidad** | Alta |
| **Actor principal** | — (caso de uso incluido) |
| **Actores secundarios** | Servicio de IA |
| **Precondiciones** | — |
| **Postcondiciones** | **Éxito:** se devuelve un rubro sugerido, que es uno de los rubros activos del tipo indicado. <br> **Fracaso:** no se devuelve ningún rubro sugerido. |

## Flujo principal

1. El caso de uso comienza cuando es incluido por otro caso de uso, que le
   indica el título y la descripción del reclamo y el tipo de rubro
   ("Mantenimiento" o "Convivencia").
2. El sistema obtiene los rubros activos del tipo indicado, con su nombre y
   descripción.
3. El sistema envía al Servicio de IA el título y la descripción del
   reclamo y la lista de rubros obtenida, y le solicita que indique el
   rubro más adecuado.
4. El Servicio de IA responde con un rubro.
5. El sistema valida que el rubro recibido sea uno de los rubros enviados.
6. El sistema devuelve el rubro como rubro sugerido.

## Flujos alternativos

- **2.a No hay rubros activos del tipo indicado:**
  - 2.a.1 El sistema no devuelve ningún rubro sugerido.
  - 2.a.2 Finaliza el caso de uso.
- **4.a El Servicio de IA no responde en 10 segundos o responde con un
  error:**
  - 4.a.1 El sistema registra el error en el registro técnico del sistema.
  - 4.a.2 El sistema no devuelve ningún rubro sugerido.
  - 4.a.3 Finaliza el caso de uso.
- **5.a El rubro recibido no es uno de los rubros enviados:**
  - 5.a.1 El sistema no devuelve ningún rubro sugerido.
  - 5.a.2 Finaliza el caso de uso.

## Flujos de excepción

Ninguno.

## Observaciones

- La falta de sugerencia no impide registrar ni modificar el reclamo: el
  caso de uso que lo incluye continúa normalmente y el administrador elige
  el rubro al categorizar (CU-031).
- Al Servicio de IA solo se le envían el título y la descripción del
  reclamo y los rubros. No se envían datos personales del residente, la
  ubicación ni las fotos.
- La sugerencia es una ayuda: la decisión final sobre el rubro siempre la
  toma el administrador.
