# Anexo A — Decisiones para cerrar las preguntas abiertas

> **Qué es:** cada pregunta abierta de la sección 5 de [analisis-dominio.md](analisis-dominio.md) (P-1 a P-20), más tres que faltaban sobre tiempo y fechas (P-21 a P-23), con una **recomendación** para que Santi la confirme o la corrija.
> **Estado:** las 23 están **Decididas por Santi el 2026-11-04**, y también las 4 de la segunda vuelta (P-24 a P-27). En 17 aceptó la recomendación; en P-1, P-3, P-4, P-5, P-9 y P-11 la corrigió o la amplió, y esas filas muestran **lo que decidió él**. Mauro y el modelo de IA toman estas decisiones como regla. Falta copiarlas a `00-vision/decisiones.md` de la KB.
> **Nada es intocable.** Estas decisiones son lo que hoy creemos mejor. Se van a ajustar con la práctica, cuando salga el MVP y lo usen polistas reales (Santi, 2026-11-04).
> **Criterio de las recomendaciones:** respetar las reglas que no se discuten sin Santi (ante la duda pregunta; nunca preguntar el tipo de cambio de los pesos; todo total es la suma de lo que se ve; privacidad de la plata) y elegir lo más simple que sirva para la V1.

## Cómo se decidió

Santi contestó **OK** o **No** (con la corrección) en cada fila. La P-11 se volvió a explicar y se eligió la opción recomendada. Sobre P-3 hubo una repregunta: qué pasa con el mensaje de origen cuando se elimina un registro.

## Resumen

| Id | Tema | Recomendación en una línea | Bloquea V1 | Estado |
|---|---|---|---|---|
| P-1 | Cuándo y a quién responde el bot | Responde lo menos posible. Si tiene una duda, le pregunta a quien mandó el mensaje, sea quien sea. A quien registra un gasto o un ingreso **siempre** le contesta qué entendió y qué cargó. El resto, solo ✅ | Sí | Decidida (corregida) |
| P-2 | Quién puede cargar plata | Gastos: cualquier miembro. Ingresos: solo owners. Proveedores: nunca gastos | Sí | Decidida |
| P-3 | Acuerdos caídos y eliminar registros | Un acuerdo o una venta se pueden marcar como caídos. Además, **un owner puede eliminar cualquier registro**: desaparece de la app y de los totales; el mensaje de origen queda oculto | Sí | Decidida (ampliada) |
| P-4 | Qué es una temporada | La **estadía del polista en un lugar** durante un período. Puede incluir varios torneos, patrones e ingresos. En un año hay varias (EE.UU., Inglaterra, Sotogrande, Argentina) | Sí | Decidida (precisada) |
| P-5 | Resultado por temporada | Ingresos (acordados y ya cobrados) − gastos de ese destino. Ventas y compras de caballos aparte | Sí | Decidida (precisada) |
| P-5b | Pago a cuenta o reintegro | A cuenta del acuerdo, salvo que el mensaje diga que es un reintegro | Sí | Decidida |
| P-6 | Identidad del patrón | Contraparte con nombre y apodos dentro de la organización, sin acceso | Sí | Decidida |
| P-7 | Cuándo sale del plantel un caballo vendido | Al entregarlo (por defecto, el día de la venta) | No | Decidida |
| P-8 | "Lo pagué yo" y "queda a pagar" | Es gasto igual y suma; se marca quién pagó o "a pagar" | Sí | Decidida |
| P-9 | Gasto por caballo | **No** hay gasto por caballo. El gasto se vincula a los caballos; en la ficha de cada uno queda **qué se le hizo**, sin el monto | Sí | Decidida (corregida) |
| P-10 | Pregunta sin respuesta | Se repregunta una vez; después queda "sin terminar" en la app. No suma | Sí | Decidida |
| P-11 | Pendientes automáticos | En la V1 solo existen los pendientes que pide alguien | No | Decidida |
| P-12 | Estados del caballo | Separar situación y lugar; los filtros de la app se mantienen | Sí | Decidida |
| P-13 | Caballos que no son del polista | Fuera de la V1: todos son del polista | No | Decidida |
| P-14 | Cotización y redondeo | Cotización del día del gasto; US$ redondeado a entero al registrar | Sí | Decidida |
| P-15 | Falla la fuente del blue | Última cotización disponible (hasta 3 días), avisada en letra chica | Sí | Decidida |
| P-16 | Varios mensajes, una carga | Mismo emisor, mismo chat, dentro de 5 minutos y antes de confirmar | Sí | Decidida |
| P-17 | Consultas de plata en el grupo | Nunca se contestan en el grupo | Sí | Decidida |
| P-18 | Accesos parciales | Solo mirar; solo sus caballos; sin vencimiento en V1 | No | Decidida |
| P-19 | Manager vs owner | Manager es un rol; owner es un permiso; van por separado | Sí | Decidida |
| P-20 | Moneda de referencia | US$ para todas las organizaciones en V1 | No | Decidida |
| P-21 | Huso horario | Cada persona tiene su huso; por defecto, el de su lugar | Sí | Decidida |
| P-22 | Fecha del gasto | La que dice el mensaje; si no dice, el día local de quien lo manda | Sí | Decidida |
| P-23 | Consumo real de stock | Los conteos sugieren un ajuste; nunca cambian el consumo solos | No | Decidida |

---

## Detalle

### P-1 · Cuándo y a quién responde el bot

**Decisión de Santi (corrige la propuesta)**
- **El bot responde lo menos posible.**
- **Si tiene una duda, le pregunta a quien mandó el mensaje, sea quien sea:** polista, manager, piloto, petisero, familiar o proveedor. No deriva la duda a los owners.
- **A quien registra un gasto o un ingreso, siempre le contesta**, diciendo qué entendió y qué está cargando, aunque no tenga dudas. Ejemplo: «Herraje de 4 caballos, $ 180.000 → US$ 116 (blue de hoy). Anotado en Pilar». **Esa respuesta va siempre por privado** (P-27): si el gasto se mandó en el grupo, ahí solo aparece ✅.
- **Para el resto** (novedades, vareos, stock, visitas, tareas), si no hay dudas, solo reacciona con ✅.

**Lo que sigue yendo a los owners** (por decisiones anteriores de Santi, que esta no reemplaza):
- El **trabajo de un proveedor** que puede ser un gasto: los proveedores no registran gastos, así que el bot les pregunta a los owners si lo registran y por cuánto.
- La **pregunta del pago fijo** el día que vence. No es una respuesta a un mensaje: es un aviso saliente.
- Un **ingreso** que manda alguien sin permiso para cargarlo (P-2).

**Qué cambia en el modelo:** desaparece "recibe preguntas" de la `Membresia`. La aclaración **siempre** tiene como destinatario al emisor, salvo las tres excepciones de arriba. La regla de respuesta pasa a depender del **tipo de registro**: gasto o ingreso → texto siempre; el resto → ✅ si no hay dudas. Con P-27, en el grupo se mantiene la decisión de la sesión 9 («en los grupos, el bot confirma con una reacción»): la confirmación por escrito de un gasto o un ingreso va por privado a quien lo cargó.

### P-2 · Quién puede cargar plata por WhatsApp

**Recomendación por defecto (un owner la puede cambiar por persona):**

| Rol | Gastos | Ingresos (acuerdos, cobros, ventas) | Novedades, actividad, stock | Tareas y recordatorios |
|---|---|---|---|---|
| Polista, manager owner | Sí | Sí | Sí | Sí |
| Familiar o asistente | Sí | No | Sí | No |
| Piloto | Sí | No | Sí | Tacha las suyas |
| Petisero, puestero | Sí | No | Sí | No |
| Veterinario, herrero | **Nunca** (carga trabajo; ver P-1) | No | Sí, de su trabajo | No |

- Si alguien sin permiso manda un ingreso («me pagó Halvorsen»), el bot **no lo registra** y le avisa a los owners por privado: «Pedro dice que pagó Halvorsen. ¿Lo registro?».

**Por qué:** la KB muestra petiseros que cargan gastos (Juanca en Inglaterra) y un piloto que paga de su bolsillo. Los ingresos son lo más sensible y en los ejemplos solo los carga el polista.

**Qué cambia en el modelo:** el objeto de valor `Accesos` suma **permisos de carga**, separados de lo que la persona **ve**.

### P-3 · Acuerdos que se caen y eliminar registros

**Recomendación**
- Un owner puede decir «se cayó lo de Les Pins». El acuerdo pasa a **Caído**.
- **Lo ya cobrado queda como cobrado** (una seña no se devuelve en este modelo). **Por cobrar** del acuerdo pasa a **cero**.
- Si había **gastos cubiertos sin reintegrar**, el bot pregunta: «Les Pins tenía US$ 3.200 de gastos para reintegrarte. ¿Te los van a devolver igual?». Si la respuesta es **sí**, siguen pendientes. Si es **no**, se les saca la marca y pasan a ser gastos propios.
- **Venta caída:** si no hubo cobros, se anula y el caballo vuelve al plantel. Si hubo cobros, se pregunta; las devoluciones quedan fuera de la V1.

**Por qué:** pasa en la vida real y, si no se modela, el "Por cobrar" queda inflado para siempre.

**Ampliación de Santi: el owner puede eliminar cualquier registro**
- Un owner puede **eliminar** cualquier registro de la plataforma: un gasto, un ingreso, un acuerdo (caído o no), una venta, una novedad, un caballo, una tarea.
- Lo eliminado **desaparece de la app y de todos los totales**.
- Si era un **gasto cubierto** por un patrón, también sale de lo que le debe. Si era un **acuerdo con pagos**, se eliminan con él sus pagos y sus reintegros.
- El **mensaje de origen** (audio, foto, texto) **no se borra: queda oculto**, solo para auditoría y para medir la IA (decisión de Santi en la repregunta).
- **Caído ≠ eliminado.** Caído deja el acuerdo visible con lo que se cobró; eliminado lo saca de la plataforma.

**Qué cambia en el modelo:** estado **Caído** en `AcuerdoConPatron` y en `VentaDeCaballo`; los eventos *AcuerdoCaido* y *VentaCaida* dejan de ser hipotéticos. Cada contexto tiene un evento de **registro eliminado** (por ejemplo, *GastoEliminado*, *AcuerdoEliminado*), que reemplaza a *GastoAnulado*. El `MensajeDeOrigen` suma el estado **oculto**.

### P-4 · Qué es una temporada

**Decisión de Santi**
- **Temporada = la estadía del polista en un lugar durante un período.** Puede incluir **varios torneos, varios patrones y varios ingresos**.
- En un mismo año hay varias. En 2026, por ejemplo: EE.UU., Inglaterra, Sotogrande y Argentina.

**Cómo queda en el modelo** (lo que se había recomendado, ahora con esta definición)
- `Temporada` es un concepto propio de la organización: nombre («Inglaterra 2026»), **lugar o lugares** donde está el polista, y **fechas** (desde, hasta).
- Los acuerdos y las ventas se asignan a una temporada. El filtro "Temporada" de Gastos usa esos mismos lugares y fechas. Hay **una sola definición**.
- Al cerrar un acuerdo, el bot propone la temporada que corresponde o crea una nueva; si no puede deducir las fechas, las pregunta.
- Fechas del mockup: Inglaterra 2026 = abril a julio; Sotogrande 2026 = agosto.

**Quedan dos dudas nuevas** (ver las preguntas nuevas al final): si una temporada puede tener más de un lugar (en el mockup, "Argentina 2026" = Pilar y el campo), y qué pasa con los gastos de un lugar **fuera** de las fechas de su temporada (la invernada de Windsor de septiembre a marzo).

### P-5 · Qué muestra el resultado por temporada

**Decisión de Santi**
- **Resultado de la temporada = ingresos − gastos de ese destino.**
- Los ingresos se muestran **acordados y ya cobrados**.
- Las **ventas y las compras de caballos van aparte** y no entran en el resultado.

**Cómo queda en la app**
- **Ingresos acordados:** acuerdos con patrones de la temporada + gastos cubiertos que te reintegran.
- **Ya cobrado:** pagos y reintegros recibidos hasta hoy.
- **Gastos de ese destino:** gastos de los lugares de la temporada, en sus fechas, sin compras de caballos.
- **Resultado:** acordado − gastos, y debajo, «con lo cobrado hasta hoy: cobrado − gastos».
- Línea aparte: «Caballos: vendiste US$ X · compraste US$ Y».

**Por qué se muestran dos resultados:** "acordados y ya cobrados" puede leerse como dos números. Mostrar los dos responde "¿me conviene esta temporada?" y "¿cuánta plata tengo hoy de esta temporada?".

**Qué cambia en el modelo:** el servicio *Calculador de resultado de temporada* devuelve los dos resultados y deja las ventas fuera.

### P-5b · Un pago del patrón: ¿a cuenta o reintegro?

**Recomendación**
- Por defecto, el pago va **a cuenta del acuerdo**.
- Es **reintegro** solo si el mensaje lo dice («me devolvió el flete», «me reintegró los pasajes»).
- Si el monto coincide **exactamente** con un gasto pendiente de reintegro, el bot pregunta: «¿Es el reintegro del flete (US$ 38.000) o un pago del acuerdo?».

**Por qué:** el total "Te debe" da igual en los dos casos, pero el estado de cada gasto cubierto no.

### P-6 · Cómo se identifica al patrón (o al comprador)

**Recomendación**
- Cada organización tiene **contrapartes**, con nombre y **apodos** («Halvorsen», «Erik», «los de Northfield»).
- No son usuarios, no reciben nada y no tienen acceso. "El patrón no existe para la plataforma" sigue valiendo en ese sentido.
- Para imputar un cobro: si la contraparte tiene **un solo** acuerdo o venta abierto, va ahí. Si tiene varios, el bot pregunta con botones («¿Es de Northfield o de la venta de Halcona?»).

**Por qué:** con solo el nombre como texto, "Halvorsen" y "Erik Halvorsen" serían dos personas distintas y la imputación falla.

**Qué cambia en el modelo:** `Contraparte` pasa de objeto de valor a **entidad interna de Ingresos**. Se ajusta el supuesto S-6.

### P-7 · Cuándo sale del plantel un caballo vendido

**Recomendación:** al acordar la venta, el bot pregunta «¿Ya lo entregaste?». Si la respuesta es sí, o no se aclara nada, el caballo sale del plantel ese día. Si es no, sigue en su lugar con la línea «Vendido · se entrega el …» y sale ese día. Lo que falte cobrar no cambia nada en Caballos.

**Por qué:** lo que importa para el stock y la caballeriza es dónde está el caballo, no si está pago.

### P-8 · "Lo pagué yo" y "queda a pagar"

**Recomendación**
- El gasto **cuenta cuando ocurre** y **suma en los totales** aunque no esté pago.
- Cada gasto tiene **Pagado por**: la organización (por defecto), una persona («Pedro, en efectivo») o **A pagar**.
- La app muestra una lista simple, «Le debés a Pedro US$ 116» y «A pagar: herraje US$ 116», que se cierra con «ya se lo pagué».
- La cuenta corriente con comercios (la forrajería) queda **fuera de la V1**.

**Por qué:** si un gasto "a pagar" no sumara, el total de Gastos dependería de cuándo se paga, y el polista quiere saber cuánto gastó. La deuda con el piloto es un dolor real y sale casi gratis.

**Qué cambia en el modelo:** `Gasto` suma el estado de pago (Pagado / A pagar) y quién pagó. Nuevo evento *GastoSaldado*.

### P-9 · ¿El gasto va por caballo?

**Decisión de Santi (corrige la propuesta):** no se entra en el detalle del gasto por caballo.
- El gasto se registra con su **lugar** y, si es de caballos, **vinculado a los caballos** a los que se refiere (por ejemplo, «Herraje de 4 caballos»: Bruja, Gitana, Dinamita y Lucera).
- En la **ficha de cada caballo** queda **qué se le hizo**: lo herró el herrero, lo vacunaron, se le dio un medicamento. **Sin el monto.**
- **No existe el gasto de un caballo en particular**: no se reparte el monto entre caballos ni se calcula cuánto costó cada uno.
- ~~La pregunta del bot es por el **lugar**.~~ Reemplazado por P-29: el bot **no pregunta el lugar**; si no es explícito, el gasto va a General.

**Qué cambia en el modelo**
- El `Gasto` tiene una lista **opcional** de caballos vinculados. Esa lista no lleva montos.
- El **evento de actividad** del caballo (herrada, vacunación, medicamento) puede referenciar el gasto, pero la ficha nunca muestra plata.
- Un solo mensaje («Vino Cacho, herró a 4… son 180 lucas») genera **un gasto** (vinculado a 4 caballos) y **cuatro eventos de actividad** (uno por ficha).
- Coherente con que Gastos e Ingresos los ven solo los owners: alguien con acceso parcial a Caballos ve lo que se le hizo a cada caballo, nunca cuánto costó.

### P-10 · Una pregunta que nadie contesta

**Recomendación**
- Si nadie responde, el bot **repregunta una sola vez**: a las 9:00 del día siguiente, o en el cierre de las 20:00 si es antes.
- Si tampoco hay respuesta, la carga queda **sin terminar**: aparece en Inicio › "Necesita tu atención" como «2 gastos sin terminar» y se completa desde la app.
- **Nunca se descarta sola** y **no suma** en ningún total hasta que se completa.

**Por qué:** descartarla pierde gastos reales, y adivinar viola "ante la duda pregunta". Mostrarla como pendiente mantiene la regla de oro: lo que no está completo no es un gasto.

**Qué cambia en el modelo:** la aclaración pasa a tener los estados Abierta / Repreguntada / Vencida, y `Carga` el estado **Sin terminar** (visible en la app).

### P-11 · Pendientes automáticos (AIE por viaje, etc.)

**Decisión:** en la V1 **solo existen los pendientes que pide alguien** («hay que cambiarle la embocadura», «el lunes viene la Dra. Ibarra»). La app **no crea pendientes sola** a partir de reglas. Los automáticos (por ejemplo, AIE, vacunas y CVI antes de un viaje al exterior) se retoman con la ficha de documentación SENASA.

**Qué cambia:** se saca del mockup el pendiente «Sacar sangre para AIE · automático por el viaje»; el origen "automático" desaparece de los pendientes.

**Por qué:** cada regla sanitaria mal hecha avisa un trámite oficial equivocado.

### P-12 · Estados del caballo

**Recomendación**
- En el modelo, dos datos separados:
  - **Situación**: En trabajo · En descanso · En doma · En recuperación · Retirada (cría).
  - **Lugar**: el lugar de la organización donde está el caballo.
- En la app, **los filtros no cambian**: Jugando = en trabajo · Campo = lugar de tipo campo · Exterior = lugar en el exterior · Recuperación = situación en recuperación.
- Un caballo puede aparecer en dos filtros (en recuperación en Windsor) y eso está bien.

**Por qué:** "Exterior" es un lugar y "Recuperación" es una situación. Mezclarlos obliga a elegir mal en casos reales.

**Qué cambia en el modelo:** el objeto de valor Estado del caballo se separa en Situación y Lugar. Se ajusta el supuesto S-13.

### P-13 · Caballos que no son del polista

**Recomendación:** **fuera de la V1.** Todo caballo del plantel es del polista. Se registra como pregunta para las entrevistas: «¿Tenés caballos de un patrón o en sociedad? ¿Cómo dividís los gastos?».

### P-14 · Qué cotización se usa y cómo se redondea

**Recomendación**
- Se usa la cotización **del día del gasto** (ver P-22), no la del día en que llega el mensaje.
- Fin de semana o feriado: la **del último día hábil anterior**.
- Un owner puede **corregir la cotización** de un gasto desde la app; queda la fuente «corregida por Nacho».
- El **monto en US$ se redondea a entero al registrarse** y se guarda así. Los totales suman esos enteros.

**Por qué:** si se guardaran decimales y se redondeara al mostrar, tres gastos de US$ 115,6 se verían como 116 + 116 + 116 = 348, mientras el total diría 347. Eso rompe la regla de oro "todo total es la suma de lo que se ve". Perder centavos no le importa a nadie en este negocio.

**Ejemplo:** $ 180.000 ÷ 1.550 = 116,13 → **US$ 116**.

### P-15 · Si falla la fuente del dólar blue

**Recomendación**
- Se usa la **última cotización disponible de hasta 3 días** y se aclara en letra chica: «al blue del 20/10 ($ 1.545, última disponible)».
- Si no hay ninguna de los últimos 3 días, el gasto se registra con su monto en pesos y **la conversión queda pendiente**: se completa sola cuando vuelve la fuente. Mientras tanto aparece «≈» y no se le pregunta nada al usuario.
- Nunca se le pregunta al usuario el tipo de cambio del peso.

**Por qué:** respeta las dos reglas que chocaban: no preguntar el tipo de cambio de los pesos y no inventar un número.

**Qué cambia en el modelo:** `Conversion` suma el estado **Pendiente**. Hasta que se completa, el gasto suma con su valor estimado y se marca con «≈» en los totales.

### P-16 · Cuándo varios mensajes son una sola carga

**Recomendación**
- Es la misma carga si: el emisor y el chat son los mismos, pasaron **5 minutos o menos** y la carga todavía no se confirmó. Caso típico: audio y después la foto de la factura.
- Si la foto llega **después** de confirmar, el bot pregunta solo si hay más de un gasto posible: «¿Es la factura del herraje de las 11?». Si hay uno solo reciente, la adjunta y lo dice.

**Por qué:** si no, el audio y la foto generan dos gastos del mismo pago.

### P-17 · Consultas de plata en el grupo

**Recomendación:** **nunca se contestan en el grupo.** Si pregunta un owner, se le responde por privado: «Te contesto por acá: …». Si pregunta alguien que no es owner, no se le responde nada de plata.

**Por qué:** en el grupo están el veterinario, el herrero y los petiseros. La privacidad de la plata es un principio de producto.

### P-18 · Accesos parciales

**Recomendación (V1)**
- Quien tiene acceso parcial **solo mira**; carga por WhatsApp como cualquiera.
- En "Novedades del día" ve **solo las de sus caballos**.
- Los accesos **no vencen solos**: un owner los saca.

**Por qué:** es lo más simple que no filtra información de otros caballos. Los vencimientos se suman si aparece el caso del veterinario de reemplazo.

### P-19 · Manager y owner

**Recomendación**
- **Manager** es un **rol** de la organización. **Owner** es un **permiso**. Van por separado.
- Al invitar con rol manager, se preselecciona «Todo» (owner), pero se puede bajar.
- Siempre hay **al menos un owner**, y el último owner no se puede sacar.

**Por qué:** la KB dice a la vez "el manager ve lo mismo que el polista" y "los permisos se configuran por persona". Separar rol y permiso hace que las dos frases valgan.

### P-20 · Moneda de referencia

**Recomendación:** **US$ para todas las organizaciones en la V1.** Una moneda de referencia por organización (por ejemplo, libras para un polista que vive en Inglaterra) queda para más adelante.

---

## Decisiones que faltaban (tiempo y fechas)

### P-21 · Huso horario

**Recomendación**
- Cada **persona** tiene su huso horario. Por defecto, el de su lugar (el piloto de Pilar, Argentina; el petisero de Windsor, Inglaterra).
- El polista y el manager pueden cambiarlo («estoy en Inglaterra»). El bot lo propone cuando nota que los mensajes llegan en otro horario: «¿Estás en Inglaterra? Te paso los avisos en hora de Londres».
- Cada aviso sale **en la hora local de quien lo recibe**: tareas a las 7:00, cierre a las 20:00, recordatorios.
- "Hoy" y "mañana" se interpretan **en la hora local de quien manda el mensaje**.

**Por qué:** con un solo huso por organización, el petisero de Windsor recibe las tareas a las 11:00 de Londres y el polista en Sotogrande recibe el cierre a las 01:00.

### P-22 · Qué fecha tiene un gasto

**Recomendación**
- Si el mensaje dice la fecha («el viernes pagué…», «el 15»), es esa. «El viernes» es el **último viernes pasado**.
- Si no la dice, es el **día local** (P-21) de quien lo mandó, en el momento en que lo mandó. Un audio de las 00:30 que dice «hoy pagué» es de ese día nuevo.
- Si la fecha queda a **más de 30 días**, el bot la confirma: «¿Del 15 de septiembre, no?».
- La cotización sale de esa fecha (P-14).

**Por qué:** la KB dice "la cotización del día en que llega el gasto", pero eso falla con «el viernes pagué…». Hace falta una sola regla de fecha que use también la conversión.

### P-23 · Consumo real de stock

**Recomendación**
- Los conteos («quedan 18 bolsas», foto del depósito) actualizan el stock.
- Con al menos dos conteos sin ingresos de mercadería en el medio, se calcula el consumo real y se **sugiere** el ajuste («se están usando 3,4 por día, no 3»). El consumo **solo cambia si un owner acepta**.

**Por qué:** es lo que muestra el mockup. Un ajuste automático con un conteo mal dicho rompe los días que alcanza.

---

## Preguntas de la segunda vuelta (decididas por Santi el 2026-11-04)

| Id | Pregunta | Decisión | Qué cambia en el modelo |
|---|---|---|---|
| P-24 | ¿Una temporada puede tener **más de un lugar**? En el mockup, "Argentina 2026" junta Pilar y el campo. | **Sí:** una temporada tiene uno o más lugares. | Entidad `Temporada` con uno o más lugares. |
| P-25 | ¿Qué pasa con los gastos de un lugar **fuera de las fechas** de su temporada? Ejemplo: la invernada en Windsor de septiembre a marzo. | **Quedan asociados a ese destino, pero no a la temporada.** La temporada es el tiempo en que el polista **estuvo ahí** y tiene los gastos de vivir y jugar ahí. Durante el resto del año hay gastos de ese destino aunque él esté en otro lugar: se ven en Gastos con su lugar y no restan en ningún resultado de temporada. | Regla del *Calculador de resultado de temporada*: solo entran los gastos de los lugares de la temporada **dentro de sus fechas**. |
| P-26 | ¿Quién puede **eliminar**? Si un petisero dice «borrá el último», ¿se borra? | **También quien lo cargó:** cada persona puede eliminar lo que cargó ella; los owners pueden eliminar cualquier registro. | Permiso de eliminación en `Membresia`; invariante de `Gasto` y de los demás registros. |
| P-27 | Por P-1, un gasto mandado en el grupo se confirmaría por escrito **en el grupo**, con el monto. ¿Está bien? | **No: por privado a quien lo cargó.** En el grupo, el bot solo reacciona con ✅; la confirmación con el monto le llega por privado. | *Política de respuesta*: el texto con lo entendido de un gasto o un ingreso va siempre por privado al emisor. |

**Consecuencia de P-27 a confirmar (S-16 en el análisis de dominio):** a un petisero o un veterinario sumados **solo al grupo**, el bot igual les escribe por privado para confirmar un gasto o preguntar una duda de plata. Por coherencia, **las dudas sobre un gasto o un ingreso mandado en el grupo también se preguntan por privado**; las dudas sobre caballos y caballeriza se preguntan en el grupo.

## Tercera vuelta (decidida por Santi el 2026-11-04)

| Id | Tema | Decisión | Qué cambia en el modelo |
|---|---|---|---|
| P-28 | Reintegros con otra cotización | **Puede haber diferencias.** Se anota lo que se dice, textual (monto y moneda del mensaje), como gasto o como ingreso, valuado con la cotización de su día. Reemplaza la propuesta S-17 («el reintegro vale lo mismo que el gasto»). | El reintegro guarda el monto dicho y su valor en US$ del día del cobro. En el anexo C, Sotogrande 2026 gana US$ 90 por diferencia de cambio, y eso es correcto. |
| P-29 | Gastos generales | Hay gastos que **no van asociados a ninguna temporada ni destino**. **Salvo que el lugar sea explícito, se cargan como generales y después, en la app, el owner los puede asociar a una temporada.** El bot **no pregunta** el lugar en cada registro, porque se vuelve engorroso. | `Destino` = un lugar o **General**; el gasto puede tener una **temporada asociada a mano**; el resultado por temporada suma los gastos asociados a mano. Cambia la regla «ante la duda pregunta» **solo para el lugar**. |
| S-18 | Días de stock truncados | **OK**, a revisar con la práctica. | — |
| S-19 | Pagos que vienen: próximos 15 días | **OK**, a revisar con la práctica. | — |

**Supuestos nuevos a confirmar** (S-20 reemplazado por P-30; S-21 confirmado en la cuarta vuelta):
- ~~**S-20:** el lugar es "explícito" si el mensaje lo nombra o nombra caballos que están todos en un mismo lugar; el lugar de quien manda el mensaje no alcanza.~~
- **S-21:** si el patrón devuelve menos de lo pendiente, se anota lo dicho y el resto queda pendiente, sin preguntar.

## Cuarta vuelta (decidida por Santi el 2026-11-04)

### P-30 · De dónde sale el lugar de un gasto (reemplaza el supuesto S-20)

**Idea de Santi:** en la app, al estilo de un calendario, el polista carga las fechas en que va a estar en cada lugar. Así la app sabe que, si registra un gasto en esa fecha, está en ese lugar. Si el mensaje hace referencia a otro destino, se asocia a ese destino.

**Cómo queda en el modelo**
- El **calendario** es la lista de **temporadas** del polista, cargadas por adelantado: cada una con fechas, lugares y un **lugar principal** (donde vive y juega; en Argentina 2026, Pilar).
- El calendario se aplica a lo que cargan **los owners**. Para el resto vale el lugar fijo de la persona (decisión de Santi, para que la sal que compra Don Aníbal en el campo no vaya a Windsor).
- Si la temporada tiene varios lugares, el gasto va al **lugar principal** (decisión de Santi).

**Orden para resolver el lugar**

1. **Lugar nombrado** en el mensaje («para el campo», «en Windsor») → ese lugar. Siempre gana.
2. **Caballos nombrados** que están todos en un mismo lugar («herró a la Bruja y la Gitana») → ese lugar.
3. Si lo carga un **owner** (polista o manager) → el **calendario**: el **lugar principal** de la temporada vigente en la fecha del gasto.
4. Si lo carga otro miembro **con lugar fijo** (Don Aníbal → Campo, Juanca → Windsor) → su lugar.
5. Si lo carga un miembro **sin lugar fijo** (por ejemplo, Sofía) → el calendario, como en el paso 3.
6. Si nada de lo anterior da un lugar → **General**.

El bot **nunca pregunta** el lugar. Si quedó mal, un owner lo corrige o lo asocia a otra temporada desde la app.

**Efectos a tener en cuenta**
- **Hay menos gastos generales.** Un gasto queda en General solo si no hay temporada vigente y nadie nombró un lugar. Por ejemplo, el handicap cargado en octubre va a Pilar; si el owner lo quiere como general, lo cambia en la app.
- **Tensión con una regla anterior de la KB:** «se clasifica por destino, no por dónde estaba el polista». Se mantiene, porque el destino nombrado siempre gana (paso 1); el calendario solo completa lo que el mensaje no dice.

### S-21 · Reintegro parcial: confirmado

Si el patrón devuelve menos de lo pendiente, se anota lo dicho y **el resto queda pendiente**, sin preguntar. Un owner lo puede dar por cerrado desde la app.

### Supuestos nuevos a confirmar
- **S-22:** las temporadas del calendario **no se superponen en fechas** (el polista no está en dos lugares a la vez). Si va una semana a Chantilly en medio de Sotogrande, se cargan como tres tramos.
- **S-23:** el **lugar fijo** de un miembro que viaja con el polista (Juanca, de Windsor a Sotogrande) lo actualiza un owner desde Equipo. Mientras no se actualice, sus gastos sin lugar nombrado van a su lugar anterior.

## Cambios aplicados en `analisis-dominio.md` (2026-11-04)

| Decisión | Cambio |
|---|---|
| P-1 | Captura: la aclaración va siempre al emisor (salvo trabajo de proveedor, pago fijo e ingreso sin permiso); regla de respuesta por tipo de registro (gasto o ingreso → texto; resto → ✅) |
| P-2 | `Accesos`: permisos de carga separados de lo que se ve |
| P-3 | Estado Caído en Acuerdo y Venta; eventos de registro eliminado en cada contexto; mensaje de origen oculto |
| P-4 | Nueva entidad `Temporada` (Ingresos, publicada a Gastos). Se resuelve el homónimo "temporada" |
| P-5 | Resultado = ingresos (acordados y cobrados) − gastos del destino; ventas y compras aparte |
| P-9 | `Gasto` con caballos vinculados sin monto; la ficha muestra qué se le hizo, nunca la plata |
| P-11 | Sin pendientes automáticos; se saca el origen "automático" |
| P-6 | `Contraparte` pasa a entidad interna de Ingresos. Se ajusta S-6 |
| P-8 | `Gasto`: estado de pago y quién pagó; evento *GastoSaldado* |
| P-10 | Estados Repreguntada / Vencida de la aclaración; `Carga` Sin terminar |
| P-12 | Estado del caballo = Situación + Lugar. Se ajusta S-13 |
| P-14, P-15 | `Conversion`: redondeo a entero y estado Pendiente |
| P-21, P-22 | Nuevos objetos de valor: huso horario de la persona y regla de fecha del gasto |
| Resto | Pasan de "pregunta abierta" a "supuesto decidido" en la sección 5 |
