# Revisión de supuestos — CU-009 a CU-038

Documento de trabajo de la sesión 2026-10-20 13:27 (Pittavino, Valente).
Las fichas no marcan los supuestos explícitamente; acá se relevan los que
tomó Claude al redactarlas, para confirmarlos o cambiarlos. Una vez
resueltos, se aplican los cambios en las fichas y este archivo puede
eliminarse.

Marcar cada ítem con: ✅ se mantiene · ✏️ se cambia (anotar cómo) · ❓ consultar.

## A. Inconsistencias entre fichas (hay que resolverlas sí o sí)

| # | CU | Problema | Propuesta |
|---|---|---|---|
| A1 ✏️ **Resuelto: opción 1** (aplicado en CU-007, 022, 024, 033, 034 y ADR 0002) | 022, 024, 034, ADR 0002 | **Qué reclamos de su unidad ve el propietario.** CU-022 lista solo los registrados *mientras* es propietario; CU-024 le da acceso al detalle de *cualquier* reclamo de la unidad mientras sea propietario; CU-034 le muestra en el historial *todos* (título, rubro, estado), incluso los anteriores a ser propietario, pero sin detalle. | Unificar con una sola regla. Opción 1: el propietario actual ve todo el historial de la unidad (lista y detalle) — es la unidad la que tiene historia. Opción 2: solo ve desde que es propietario, y en CU-034 los anteriores aparecen solo en los contadores del resumen. |
| A2 ✅ **Falsa alarma**: CU-023 ya exige unidad vinculada | 023 vs 024 | CU-023 (consultar comunitarios) no exige unidad vinculada; CU-024 solo da acceso a comunitarios a residentes *con* unidades vinculadas. Un usuario sin unidades vería el listado pero no podría abrir el detalle. | Agregar a CU-023 la precondición "tiene al menos una unidad vinculada". |
| A3 ✏️ **Resuelto** (CU-028, 029, 036) | 028 vs 036 vs ADR 0003 | Avisos de cierre: CU-028 (cierre por confirmación) avisa al admin y adherentes; CU-036 (cierre automático) avisa al autor y adherentes, no al admin; ninguno avisa al propietario, aunque ADR 0003 dice que cada cambio de estado lo notifica. | Regla única para "Cerrado": autor (si no fue él), adherentes, propietario si no es el autor, y admin. |
| A4 ✅ **Se mantiene**, aclarado en CU-031 y 035 | 031, 035 | La fecha objetivo se calcula desde la **categorización** (hoy + plazo), pero los tiempos de resolución del reporte se miden desde el **registro**. El "% fuera de plazo" puede dar distinto según cuál se use. | Definir: fuera de plazo = primera resolución posterior a la fecha objetivo (así lo dejan las fichas). O bien calcular la fecha objetivo desde el registro. |
| A5 ✅ **Se mantiene**, aclarado en CU-033 | 033 vs 038 | Un comentario visible del admin solo se notifica al autor; la regla general de CU-038 menciona además adherentes y propietario (para cambios de estado). | Confirmar que los comentarios solo van al autor (no es cambio de estado, así que no hay contradicción formal, pero conviene decidirlo). |

## B. Supuestos de negocio a confirmar

### Unidades, ubicaciones y rubros (CU-009 a CU-020)

> ✅ B1–B5 se mantienen. ✏️ B6: se precargan rubros (CU-017, inventario).
> ✏️ Extra: cancelar reclamo (CU-026) notifica al administrador.

- B1. Tipos de unidad: Departamento, Casa, Habitación, Local, Cochera, Otro.
- B2. Tipos de ubicación compartida: solo "Área común" e "Instalación".
- B3. Baja de unidad exige que no tenga usuarios vinculados ni invitaciones
  pendientes **ni reclamos abiertos** (CU-012). Mismo criterio de reclamos
  abiertos para ubicaciones y rubros (CU-016, CU-020).
- B4. Identificador / nombre únicos solo entre activos; se pueden reutilizar
  los de dados de baja.
- B5. Rubro: descripción **obligatoria** (la usa la IA); plazo objetivo de
  1 a 365 días; el tipo no se puede cambiar con reclamos abiertos; un
  cambio de plazo solo afecta categorizaciones futuras.
- B6. **No hay rubros precargados**: el espacio arranca sin rubros y el
  admin los crea. Mientras no haya rubros no hay sugerencia de IA. ¿Se
  quiere un set inicial por defecto (Plomería, Electricidad, Ascensores,
  Ruidos molestos…)?

### Reclamos — residente (CU-021 a CU-029)

> ✅ B7, B8, B11, B13. ✏️ B9: convivencia sobre unidad la ven autor, admin
> y la unidad involucrada (sin anonimato); sobre ubicación compartida es
> comunitario. ✏️ B10: el inquilino ve los reclamos de su unidad mientras
> vive ahí. ✏️ B12: +1 nivel por cada 20 % de residentes activos
> adheridos. ✏️ B14: Resuelto lo marca autor o admin, sin reapertura,
> Cerrado a los 7 días (ADR 0004; CU-028 reescrito, CU-029 eliminado).

- B7. Prioridad base "Media" al registrar, hasta que el admin categoriza.
- B8. Cada reclamo nuevo notifica por email al admin (uno por reclamo, sin
  resumen diario).
- B9. Reclamo de convivencia: la unidad involucrada es opcional y **no ve
  el reclamo**; los de convivencia nunca son comunitarios.
- B10. El **inquilino no ve** los reclamos que el propietario registra
  sobre la unidad donde vive (no hay regla de acceso que lo cubra).
- B11. Modificar y cancelar solo en "Ingresado" y sin adhesiones; después,
  solo se puede comentar. La ubicación nunca se modifica (se cancela y se
  registra de nuevo).
- B12. Adherir solo en estados abiertos y no en "Resuelto"; las adhesiones
  no se pueden retirar; +1 nivel de prioridad cada 3 adhesiones, tope
  "Urgente".
- B13. Solo el **autor** confirma o reabre; ni adherentes ni propietario.
  Si el autor fue dado de baja, se espera el cierre automático.
- B14. Reabrir solo mientras está "Resuelto" (ventana de 7 días); después,
  reclamo nuevo. Se puede reabrir varias veces.

### Reclamos — administrador (CU-030 a CU-036)

> ✅ B15, B17, B19–B24. ✏️ B16: el admin puede pasar Asignado → Resuelto.
> ✏️ B18: sin anonimato (autor, adherentes y comentarios con nombre); se
> mantienen los comentarios internos. ✏️ Extra: en comunitarios, Resuelto
> del lado residente requiere mayoría de autor + adherentes (CU-028).

- B15. Orden por defecto del listado: prioridad desc., luego antigüedad.
- B16. Transiciones (ADR 0003): desde "Asignado" no se puede pasar
  directo a "Resuelto" (hay que pasar por "En curso"); desde "En curso" ya
  no se puede rechazar.
- B17. Recategorizar no recalcula la fecha objetivo sola.
- B18. Comentarios internos del admin, invisibles para residentes. En
  comunitarios, los comentarios de residentes aparecen como "Residente"
  (anónimos) para los demás.
- B19. Se puede comentar en "Resuelto"; no en estados finales.
- B20. **CU-034**: solo admin y propietario consultan el historial (el
  inquilino no). "Problema recurrente" = 3+ reclamos del mismo rubro en
  los últimos 12 meses, **independiente del período filtrado**. Los
  reclamos de convivencia donde la unidad es la *involucrada* no cuentan.
- B21. Reportes: tres tipos fijos (estado×rubro, tiempos, recurrentes) con
  exportación CSV; sin gráficos ni PDF.
- B22. Cierre automático corre a las 00:00 y cierra los "Resuelto" con más
  de 7 días.

### Servicios externos (CU-037, CU-038)

- B23. IA: timeout de 10 s; si falla o devuelve algo fuera de la lista, no
  hay sugerencia. Solo se envían título, descripción y rubros.
- B24. Email en segundo plano: 3 reintentos cada 5 min; a usuarios dados
  de baja no se les envía nada (salvo el aviso de baja).

## C. Valores de detalle (confirmar en bloque)

> ✅ Aprobados sin cambios. ✏️ Extra: un reclamo comunitario nuevo se
> notifica a todos los residentes activos (CU-021).

- Listados paginados de 20, ordenables por columna.
- Identificador de unidad: 1–10 caracteres (letras, dígitos, espacio,
  guion). Piso/sector hasta 30. Nombres de ubicación y rubro: 2–50.
  Descripciones de ABM hasta 500.
- Reclamo: título 5–100, descripción 20–2000, hasta 5 fotos JPG/PNG de
  5 MB c/u.
- Motivo de cancelación opcional hasta 500; motivo de reapertura 10–1000;
  comentario del admin hasta 1000 (mín. 10 al rechazar/resolver);
  comentarios 1–2000.
- Reporte: período por defecto últimos 12 meses; mínimo de recurrencia
  2–50, por defecto 3.
