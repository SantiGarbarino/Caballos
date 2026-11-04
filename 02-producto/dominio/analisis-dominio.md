# Análisis de dominio — Asistencia financiera y operativa para polistas

> **Producto:** PROGRAMON (nombre provisorio). **Fuente:** knowledge base del repositorio `SantiGarbarino/Caballos` (visión, decisiones, PRD v0.3, módulos, flujos de WhatsApp, modelo de datos v0.3, glosario), vigente al 2026-11-03.
> **Alcance de este documento:** vocabulario, fronteras, modelo interno y hechos del negocio. No incluye código, esquemas de datos, contratos de API, tecnologías ni despliegue.
> **Idioma del modelo:** los términos del dominio se escriben en **castellano rioplatense**, con la jerga del polo del glosario de la KB (petisero, piloto, patrón, vareo, herraje). Los nombres de agregados y eventos siguen esa misma lengua (`Gasto`, `AcuerdoConPatron`, `GastoRegistrado`).
> **Convención:** cuando el documento funcional no define algo, se marca **[SUPUESTO S-n]** o **[PREGUNTA P-n]** y se desarrolla en la sección 5.
> **Nada es intocable.** Estas decisiones son lo que hoy creemos mejor. Se van a ajustar con la práctica, cuando salga el MVP y lo usen polistas reales (Santi, 2026-11-04).
> **Anexos:** [A — decisiones](anexo-a-decisiones.md) · [B — escenarios de aceptación](anexo-b-escenarios.md) · [C — dataset de referencia con resultados esperados](anexo-c-dataset.md) · [G — manual del bot](anexo-g-manual-del-bot.md).
> **Decisiones incorporadas:** las 23 preguntas que dejó abiertas la primera versión, y las 4 que surgieron de esas respuestas, las decidió Santi el 2026-11-04 (detalle en [anexo-a-decisiones.md](anexo-a-decisiones.md)). Las referencias **[P-n]** del texto apuntan a esas decisiones, resumidas en la sección 5.2.

---

## 1. Lenguaje Ubicuo

El producto le sirve a un **polista profesional** (y a su **manager**) que maneja un negocio informal: muchos caballos en varios lugares, gente que reporta por WhatsApp, gastos en varias monedas y cobros parciales de varios patrones. El lenguaje que sigue es el que tienen que compartir el equipo, el bot y la app.

### Términos centrales

#### Entidades del dominio

| Término | Definición | Notas de contexto |
|---|---|---|
| **Organización** | La "empresa" de un polista: su gente, sus caballos, sus lugares y su plata. Es la unidad que contrata el producto y dentro de la cual vive todo dato. | En el glosario del polo, "organización" es el equipo-empresa del jugador. En la plataforma es además el **límite de privacidad**: nada cruza de una organización a otra. La KB la llama también "Cuenta"; en este modelo se usa solo **Organización**. |
| **Polista** | Jugador profesional, dueño de la organización. Comprador y usuario. | No confundir con "polista de Wellington" que aparece como **comprador** de un caballo: ahí es una contraparte, no un usuario. |
| **Manager** | Mano derecha del polista en organizaciones grandes; registra el día a día. Cuando es owner, ve exactamente lo mismo que el polista. | Puede ser quien crea la organización. En muchas organizaciones es quien más usa el producto. |
| **Owner** | Persona con todos los accesos de una organización: ve Gastos e Ingresos, invita gente, define qué ve cada uno y recibe las preguntas del bot. | Es un **atributo de la membresía**, no un rol del polo. Lo es quien crea la organización y a quien un owner le dé "Todo". Un proveedor nunca puede ser owner. |
| **Miembro** | Persona que pertenece a una organización con un rol (piloto, petisero, puestero, familiar o asistente, manager, polista). | Por defecto es **de solo WhatsApp**: carga por el bot, nunca entra a la app, y lo que manda figura con su nombre. |
| **Proveedor** | Veterinario o herrero que trabaja para **varias** organizaciones y carga **trabajo**, no gastos. | Dos acepciones. En **Organización y accesos**: miembro con muchas membresías. En el habla del polo, "proveedor" es también el **corralón o la forrajería** que vende insumos; ese **no** es miembro y en el modelo se llama **Comercio**. |
| **Piloto** | El mayor de los petiseros, encargado de la caballeriza; recibe tareas y avisos por WhatsApp y los tacha respondiendo. | Sinónimos en el campo: encargado, capataz, jefe de petiseros. En el modelo se usa solo **piloto**. |
| **Petisero / Puestero** | Petisero: cuida, alimenta y varea los caballos. Puestero: vive en el campo y cuida los caballos que están ahí. | Siempre de **una sola** organización. |
| **Patrón** | Dueño o financista de un equipo que contrata al polista para una temporada. | **No existe como usuario ni actor de la plataforma.** Aparece solo como **contraparte** de acuerdos, pagos y reintegros (ver **Contraparte**). |
| **Contraparte** | Quien le debe plata al polista: el patrón de un acuerdo o el comprador de un caballo. | Tiene nombre y apodos dentro de la organización, pero no es usuario ni recibe nada [P-6]. La misma contraparte puede ser patrón en un acuerdo y comprador en una venta (Halvorsen en el mockup). |
| **Contador** | Persona que recibe el export de gastos por mail. | No es usuario ni miembro: es solo un **destinatario**. |
| **Lugar** | Sitio físico de la organización donde hay caballos o se gasta plata: caballeriza, campo, invernada en el exterior, caballeriza de temporada. | Un gasto puede no tener lugar: es **General** [P-29]. Se usa con tres funciones que hay que distinguir: **destino** de un gasto (Gastos), **ubicación** de un caballo (Caballos) y **sede** con stock propio (Caballeriza). El "dónde" de un acuerdo ("Francia · Chantilly 2026") lo da la **Temporada** a la que pertenece. |
| **Caballo (petiso)** | Animal del plantel, con su ficha: estado, ubicación, novedades, pendientes, actividad y salud. | "Petiso" es caballo de polo aunque no sea chico. Los datos de registro (sangre, padre, madre, partidos) pueden venir de la **app Polo Argentino**, que es de terceros; "Polo Argentino" es también el nombre de la **raza**. |
| **Gasto** | Salida de plata de la organización, con su destino, su clasificación, su monto original, su monto en dólares y lo que lo originó. | Es la unidad de la "**una sola lista**": todo total es la suma de gastos. Un pago que mezcla veterinario y herrero son **dos** gastos. Puede estar vinculado a caballos, pero **no existe el gasto de un caballo en particular** [P-9]. |
| **Pago fijo** | Gasto que se repite todos los meses (sueldos, alquileres, invernada) y que el bot pregunta el día que vence. | No es un gasto: es una **plantilla** que, confirmada, genera un gasto por mes. |
| **Acuerdo con patrón** | Lo que el polista arregló cobrar por jugar una temporada para un equipo, y los pagos que van entrando. | El acuerdo lleva el nombre del **equipo del patrón** (Northfield), no del patrón. |
| **Venta de caballo** | Precio pactado por un caballo vendido y sus cobros parciales. | Es un **ingreso**. Su opuesto, la **compra de caballo**, es un gasto que **no** entra en el resultado por temporada. |
| **Pago recibido** | Plata que entra a cuenta de un acuerdo o de una venta (seña, transferencia, efectivo). | Ver homónimo **Pago** en 1.3. |
| **Gasto cubierto / Reintegro** | Gasto que pagó el polista y que el patrón se comprometió a devolver; mientras no lo devuelve, suma a lo que debe. | En Gastos es una **marca** sobre el gasto ("Lo cubre Northfield"). En Ingresos es una **deuda** con estado (a reintegrar / reintegrado). |
| **Mensaje de origen** | El audio, la foto o el texto tal como llegó por WhatsApp, con quién lo mandó y por dónde. | Nunca se borra ni se modifica. Es la prueba de "cada número se explica". |
| **Carga** | Lo que el bot entiende de uno o varios mensajes que **registran algo que pasó**, y que espera confirmación o aclaración antes de impactar en la app. | Un solo audio puede producir varias cargas o una carga con varios registros (Ramón: 4 vareos + una novedad). "Carga" del camión (Tormenta al campo) es otra cosa: un **traslado**. |
| **Comprobante** | Documento que respalda un gasto o un pago: foto de factura, remito, ticket o comprobante de transferencia. | La KB usa "comprobante" también para el audio o el texto cuando no hay foto. En el modelo se separan: **Comprobante** = documento; **Origen** = mensaje que generó el registro (siempre existe). |
| **Novedad** | Algo que le pasa a un caballo y que alguien reporta ("renguea de la mano izquierda"). | "Novedades del día" en la pantalla de permisos es una **sección de la app**, no una novedad. |
| **Evento de actividad** | Algo que se hizo con un caballo: vareada, montada, práctica, partido, herrada, vacunación, medicamento, veterinaria, al box, entrada en reposo. | Se registra con quién lo reportó y cómo. Puede referenciar el gasto que lo pagó, pero la ficha **nunca muestra el monto** [P-9]. |
| **Trabajo de proveedor** | Lo que un veterinario o herrero dice que hizo (vacunó, herró, revisó). | No es un gasto: puede **dar lugar** a una pregunta a los owners para registrarlo como gasto. |
| **Insumo** | Lo que consume una sede: avena, fardos, rollos, viruta, balanceado, suplementos. | Cada sede tiene su stock y su consumo. |
| **Visita** | Venida agendada de un proveedor (herrero, veterinaria u otro) para ciertos caballos. | Aparece en "Lo que viene". |
| **Tarea** | Algo que el polista o el manager le pide al piloto; le llega por WhatsApp y se tacha respondiendo. | |
| **Recordatorio** | Algo a recordar en un momento dado. | Tres acepciones, ver 1.3. |
| **Grupo de WhatsApp** | Conversación grupal donde está el bot; pertenece a **una** organización, que puede tener varios. | Homónimo de **grupo de gastos** (ver 1.3). |
| **Temporada** | La **estadía del polista** en uno o más lugares durante un período: el tiempo en que **estuvo ahí** viviendo y jugando. Puede incluir varios torneos, patrones e ingresos; en un mismo año hay varias (EE.UU., Inglaterra, Sotogrande, Argentina) [P-4, P-24]. | Es la misma para Ingresos (a qué temporada pertenece un acuerdo) y para Gastos (qué gastos entran en su resultado). Un gasto de ese lugar **fuera** de esas fechas (la invernada de Windsor entre temporadas) sigue siendo de ese **destino**, pero no de la temporada [P-25]. |

#### Estados

| Término | Definición | Notas de contexto |
|---|---|---|
| **Situación del caballo** | En trabajo · En descanso · En doma · En recuperación · Retirada (cría). Es independiente del **lugar** donde está [P-12]. | Los filtros de la app se mantienen y combinan los dos datos: **Jugando** = en trabajo; **Campo** = lugar de tipo campo; **Exterior** = lugar en el exterior; **Recuperación** = en recuperación. Un caballo puede aparecer en dos filtros. |
| **Sin pagos / Cobrando / Cobrado / Caído** | Estado de un acuerdo o de una venta según lo cobrado; Caído si no se concretó [P-3]. | "Cobrado" exige además que no queden reintegros pendientes [S-9]. **Caído** no es **eliminado**: el acuerdo caído sigue visible con lo cobrado. |
| **A reintegrar / Reintegrado** | Estado de un gasto cubierto por un patrón. | Lo decide **Ingresos**; Gastos solo lo muestra. |
| **Al día / Vencido (N semanas) / Pendiente** | Estado de un ítem de salud de un caballo (herraje, vacunas, desparasitación, control veterinario). | "Herraje" es a la vez evento, ítem de salud y categoría de gasto. |
| **Pendiente de aclaración / Sin terminar / Confirmada / Aplicada / Descartada** | Ciclo de vida de una carga. | **Sin terminar**: nadie respondió la pregunta ni la repregunta; se ve en la app y no suma [P-10]. Ver agregado `Carga`. |
| **Pagado por / A pagar** | Si el gasto ya lo pagó alguien (la organización o una persona) o si quedó como deuda. | En los dos casos el gasto **suma** [P-8]. De ahí sale «Le debés a Pedro US$ 116». |
| **Eliminado** | Registro que quien lo cargó o un owner sacó de la plataforma: desaparece de la app y de todos los totales [P-3, P-26]. | Su mensaje de origen queda **oculto**, no se borra. |
| **Owner / Acceso parcial / Solo WhatsApp** | Lo que una persona puede ver de la app: Todo, Una parte (secciones y qué caballos) o Nada. | |
| **Activa / Inactiva (membresía)** | Si la persona sigue en la organización. | Al darla de baja, el bot deja de aceptarle mensajes para esa organización; lo que cargó queda con su nombre. |

#### Conceptos de soporte

| Término | Definición | Notas de contexto |
|---|---|---|
| **Moneda de referencia (US$)** | Todo se muestra y se suma en dólares. | Se guardan siempre el monto y la moneda **originales**. |
| **Dólar blue del día** | Cotización informal del dólar en Argentina; promedio entre compra y venta, **del día del gasto** (fin de semana o feriado: último día hábil anterior) [P-14]. | El bot **nunca** pregunta el tipo de cambio de los pesos. Si la fuente falla, se usa la última de hasta 3 días [P-15]. |
| **Cotización** | Valor, fecha, tipo y fuente usados para pasar un monto a dólares. | Si es euro sin fuente, la da el usuario y queda como fuente "la dio el usuario". |
| **Conversión** | El registro de cómo un monto original se pasó a US$, **redondeado a dólares enteros** [P-14]. | Se ve en letra chica: «$ 800.000 al dólar blue del 22/10 ($ 1.550) = US$ 516». No se recalcula sola. |
| **Fecha del gasto** | La que dice el mensaje («el viernes»); si no dice nada, el día local de quien lo manda [P-22]. | De ella salen la cotización y el período en que suma. |
| **Huso horario de la persona** | La hora local de cada persona; por defecto, la de su lugar [P-21]. | Define "hoy" y "mañana" en sus mensajes y la hora a la que le llegan los avisos. |
| **Grupo › categoría** | Taxonomía de gastos (Caballos › Veterinario, Traslados y viajes › Fletes de caballos…). | Ocho grupos. "Compra de caballos" es inversión. |
| **Destino** | El lugar **al que corresponde** un gasto, no donde estaba el polista al pagar; o **General** si no corresponde a ningún lugar [P-29]. | US$ 2.000 para el campo pagados desde Sotogrande → Campo. La moneda no depende del lugar. El lugar **nunca se pregunta**: sale del mensaje, de los caballos nombrados, del **calendario** (si carga un owner) o del lugar fijo de quien carga; si nada lo da, es **General** [P-30]. Un owner lo puede corregir o asociar a otra temporada desde la app. |
| **Calendario** | Las temporadas del polista cargadas por adelantado en la app: dónde va a estar y en qué fechas, con un **lugar principal** por temporada [P-30]. | Le dice a la app dónde está el polista en la fecha de un gasto que carga un owner sin decir el lugar. Las temporadas no se superponen [S-22]. |
| **Gasto general** | Gasto que no va asociado a ningún lugar ni temporada: el mensaje no nombró un lugar, no hay temporada vigente en el calendario y quien lo cargó no tiene lugar fijo; o un owner lo pasó a General [P-29, P-30]. | Suma en los totales de Gastos (renglón «General» en el filtro de lugar) y **no** resta en ningún resultado de temporada hasta que un owner lo asocia. |
| **Período** | Ventana de fechas para mirar gastos: este mes, últimos 30 días, temporada, todo el año o un rango. | |
| **Por cobrar / Te debe** | Acordado − cobrado + gastos cubiertos pendientes de reintegro. | Se calcula, no se guarda. |
| **Resultado por temporada** | Ingresos de la temporada (acordados y ya cobrados) menos los gastos de su destino en sus fechas y los gastos que un owner **asoció a mano** a esa temporada [P-5, P-29]. | Ventas y compras de caballos se muestran aparte y no entran. |
| **Días que alcanza** | Stock ÷ (consumo por caballo por día × caballos que lo consumen ÷ tamaño del envase). | Por sede e insumo. |
| **Consumo** | Cuánto come o usa cada caballo por día de un insumo. | Dos acepciones: **consumo cargado** (configurado) y **consumo real** (inferido de conteos). El real solo **sugiere** un ajuste [P-23]. |
| **Lo cargó** | Persona y canal por el que entró un registro ("Pedro por WhatsApp"). | Distinto de **pagado por**. |
| **Canal** | Grupo de WhatsApp de la organización o chat privado con el bot. | La plata va en general por privado, pero si se habla en el grupo **se registra igual**. |
| **Contexto de conversación** | Organización que eligió un proveedor por privado, vigente por un rato, para no repreguntar. | |
| **Charla** | Mensaje que no registra algo que pasó: pregunta, comentario, plan, chiste, coordinación. | **Nunca** se carga. «¿el flete sale 2 mil?» es charla; «el flete salió 2 mil» es dato. |
| **Duplicado sospechado** | Gasto parecido a otro ya registrado (monto, categoría, fecha cercana), de cualquier canal o persona. | Antes de registrar se pregunta si es el mismo. |
| **Aviso saliente** | Mensaje que el bot manda por iniciativa propia: tareas de las 7:00, pagos fijos, recordatorios, cierre del día de las 20:00. | |

### Acciones y procesos

| Término | Definición |
|---|---|
| **Cargar (por WhatsApp)** | Mandar un audio, una foto o un mensaje al bot, en el grupo o por privado, para registrar algo que pasó. |
| **Interpretar** | Entender qué dice un mensaje: si es carga o charla, qué registros contiene (gasto, pago, novedad, vareo, stock…) y qué datos faltan. |
| **Rutear a una organización** | Decidir a qué organización pertenece un mensaje: la del grupo; la única del remitente; o, si es un proveedor con varias, deducirla por caballo o cliente nombrado, o preguntarla. |
| **Preguntar ante la duda (aclarar)** | Antes de registrar, pedir lo que falta (categoría, caballos, cliente, tipo de cambio de euros). Nunca adivinar. **Excepción: el lugar no se pregunta**; se resuelve con la regla de P-30 y, si no sale, el gasto va a General. |
| **Confirmar** | Cerrar una carga. Si es un **gasto o un ingreso**, siempre con un mensaje **por privado** a quien lo cargó, que dice qué entendió y qué cargó; si llegó por el grupo, en el grupo solo hay ✅ [P-1, P-27]. Para el resto, solo con ✅ si no hubo dudas. Con más de una organización, dice en cuál se cargó. |
| **Corregir** | Cambiar un registro ya hecho respondiendo ("no, eran dólares", "eso era para el campo"). Queda el antes y el después. |
| **Eliminar** | Sacar un registro de la plataforma ("borrá el último", o desde la app). Puede hacerlo **quien lo cargó** (lo suyo) o **un owner** (cualquier registro) [P-3, P-26]. |
| **Marcar como caído** | Indicar que un acuerdo o una venta no se concretó; lo cobrado queda y se deja de esperar el resto [P-3]. |
| **Descartar** | Dar por no registrada una carga (charla, duplicado confirmado, el usuario lo cancela). |
| **Registrar un gasto** | Agregar un gasto a la lista única con destino, clasificación, monto original, conversión y origen. |
| **Convertir a dólares** | Pasar un monto original a US$ con la cotización del día que corresponde. |
| **Clasificar** | Asignar grupo › categoría y destino (un lugar o General) a un gasto. |
| **Asociar a una temporada** | Que un owner, desde la app, asigne un gasto (general o de otro lugar o fecha) a una temporada, para que reste en su resultado [P-29]. |
| **Separar un gasto** | Partir un pago mixto (veterinario + herrero) en dos gastos. |
| **Marcar como cubierto ("lo cubre el patrón")** | Indicar que un gasto lo va a reintegrar el patrón de un acuerdo; pasa a sumar en lo que debe. |
| **Reintegrar** | Que el patrón devuelva un gasto cubierto. |
| **Cerrar un acuerdo** | Registrar lo arreglado con un patrón para una temporada (con o sin seña). |
| **Cobrar / Registrar un pago** | Anotar plata recibida a cuenta de un acuerdo o una venta. |
| **Vender un caballo / Comprar un caballo** | Pactar el precio de un caballo propio con un comprador (ingreso) / incorporar un caballo pagando por él (gasto de inversión). |
| **Dar de alta un caballo** | Sumar un caballo al plantel: elegirlo del catálogo de la app Polo Argentino o mandarlo por WhatsApp (nombre, sexo, edad, pelaje; microchip leído de los papeles). |
| **Trasladar** | Cambiar un caballo de lugar (Pilar → campo, al exterior). |
| **Varear** | Ejercitar a un caballo. |
| **Herrar / Despalmar** | Poner herraduras / emparejar el casco. |
| **Reportar una novedad** | Avisar algo que le pasa a un caballo; queda en su ficha y puede generar una alerta. |
| **Agendar una visita** | Fijar día, proveedor, motivo y caballos de una venida. |
| **Asignar una tarea al piloto / Tachar** | Pedirle algo al piloto / darlo por hecho respondiendo "Listo, hecho". |
| **Recordar** | Avisar en el momento indicado algo pedido ("mañana haceme acordar"). |
| **Contar stock / Ingresar insumo** | Informar cuánto queda ("quedan 18 bolsas") / informar que entró mercadería. |
| **Ajustar consumo** | Cambiar el consumo cargado, a mano o aceptando la sugerencia según los conteos reales. |
| **Invitar / Dar de baja** | Sumar a alguien a la organización eligiendo rol, cómo se suma (grupo y/o privado) y qué ve / sacarlo. |
| **Configurar accesos** | Elegir qué ve alguien: Nada, Todo o Una parte (secciones y qué caballos). |
| **Consultar** | Preguntarle al bot algo de los datos ("¿cuánto gasté en Inglaterra este mes?"); se responde con los mismos datos de la app. |
| **Exportar al contador** | Mandar por mail los gastos de un período y lugar, con fotos, monto original, cotización y monto en US$. |
| **Cerrar el día** | Resumen de las 20:00: vareos, herrajes, gastos, stock y lo que viene mañana. |

### Homónimos resueltos

Un mismo nombre para dos conceptos distintos es un error del modelo. Estos son los casos detectados en la KB y cómo se nombran en este modelo.

| Palabra en la KB | Acepciones | Nombre en el modelo |
|---|---|---|
| **Equipo** | (a) la gente de la organización (pantalla Equipo); (b) el equipo de polo de un patrón (Northfield); (c) el grupo de gastos "Equipo de polo" (tacos, monturas). | (a) **Miembros**; (b) **Equipo del patrón**; (c) grupo de gastos **Equipo de polo** (siempre con "de polo"). |
| **Grupo** | (a) grupo de WhatsApp; (b) primer nivel de la taxonomía de gastos. | **Grupo de WhatsApp** / **Grupo de gastos**. Nunca "grupo" a secas. |
| **Temporada** | La KB la usaba como: (a) período de juego en un lugar del mundo; (b) atributo de un acuerdo ("Wellington 2027"); (c) período de filtro en Gastos ("Temporada Inglaterra: mayo a julio"). | **Resuelto [P-4]:** una sola **Temporada** (estadía en uno o más lugares, con fechas). El acuerdo se asigna a una temporada y Gastos filtra con sus lugares y fechas. |
| **Pago** | (a) plata que entra (Ingresos); (b) pago fijo (egreso recurrente); (c) "quién lo pagó" de un gasto. | **Pago recibido** / **Pago fijo** / **Pagado por**. |
| **Recordatorio** | (a) personal del polista o manager; (b) pendiente en la ficha de un caballo, asignable al piloto. (El "automático por el viaje" del mockup sale de la V1 [P-11].) | **Recordatorio personal** / **Pendiente del caballo**. |
| **Caballeriza** | (a) la instalación (Pilar); (b) el módulo de stock; (c) la categoría de gasto Caballerizas y casa › Caballerizas (alquiler). | **Sede** (cuando tiene stock) o **Lugar**; módulo **Caballeriza**; categoría **Caballerizas**. |
| **Proveedor** | (a) veterinario o herrero multi-organización; (b) corralón o forrajería. | **Proveedor** / **Comercio**. |
| **Comprobante** | (a) foto del documento; (b) audio o texto cuando no hay foto. | **Comprobante** / **Origen**. |
| **Dueño** | (a) dueño de la cuenta (polista); (b) patrón = dueño del equipo; (c) propietario de un caballo (propio, de un patrón, en sociedad). | **Owner** / **Patrón** / **Propietario** (fuera del modelo actual, [P-13]). |
| **Lugar / Dónde** | (a) destino de un gasto; (b) ubicación de un caballo; (c) "dónde" de un acuerdo (país, torneo). | (a) y (b) **Lugar** de la organización; (c) lo da la **Temporada** a la que se asigna el acuerdo. |

---

## 2. Mapeo estratégico

### Subdominios

| Subdominio | Tipo | Contextos acotados que lo implementan |
|---|---|---|
| **Finanzas de la organización** | Núcleo | Gastos · Ingresos y cobros |
| **Captura conversacional** | Núcleo | Captura |
| **Operación del plantel** | Soporte | Caballos · Caballeriza · Agenda y tareas |
| **Organización y accesos** | Soporte | Organización |
| **Cotizaciones de moneda** | Genérico | Cotizaciones |
| **Mensajería y transcripción** | Genérico | Canal de mensajería |
| **Identificación de usuarios** | Genérico | Acceso (link de un solo uso) |
| **Reportes a terceros** | Genérico | Exportación |

**Por qué estos son el núcleo.** Es una decisión del equipo y se argumenta así:

- **Finanzas** es el dolor número uno ("no sabe cuánto gasta ni en qué") y el gancho de adopción. Lo que el producto sabe hacer y nadie más hace para un polista es: una sola lista de gastos clasificada por **destino** (o general) y no por moneda ni por país, todo en dólares con la conversión explicada, y lo que le deben **mezclando** acuerdos, ventas y gastos que cubre el patrón. Estas reglas son propias del polo profesional; no existen en un software contable genérico y son las que hay que hacer mejor que nadie.
- **Captura conversacional** es la otra mitad de la ventaja: el polista no usa computadora. El modelo de "ante la duda pregunta, nunca adivina", distinguir carga de charla, rutear mensajes de proveedores con varias organizaciones y detectar duplicados entre el grupo y el privado es lo que hace que los números sean confiables **sin formularios**. Si la captura falla, Finanzas muestra números falsos. No es "integrar WhatsApp" (eso es genérico): es la **política de negocio** sobre qué entra al libro y cómo se aclara.
- **Operación del plantel** (caballos, stock, agenda) agrega valor y retiene, pero sus reglas son conocidas en la industria y la KB las trata como secundarias (Caballeriza es "Should"; la ficha oficial SENASA se posterga). Es soporte: hecho a medida, sin ser el diferencial.
- **Organización y accesos** es necesario y específico (owners, solo WhatsApp, proveedores multi-organización), pero no es lo que el cliente paga. Es soporte.
- Cotizaciones, mensajería, transcripción de audio, lectura de imágenes, login y exportación a Excel/PDF son problemas resueltos fuera del polo: genéricos.

### 2.1 Contextos acotados

| Contexto | Tipo | Responsabilidades | Fuera de su responsabilidad |
|---|---|---|---|
| **Gastos** | Núcleo | Es dueño de la **lista única de gastos**. Registra, corrige, elimina (a pedido de un owner) y separa gastos; aplica la taxonomía grupo › categoría; asigna destino (un lugar, o General si el mensaje no lo dice) y permite asociar un gasto a una temporada; guarda monto y moneda originales y la conversión a US$; mantiene los **pagos fijos** y sus vencimientos mensuales; marca un gasto como cubierto por un acuerdo; calcula totales por período, lugar, grupo y categoría; responde si existe un gasto parecido (para duplicados). | Interpretar mensajes o hablar con el usuario. Obtener cotizaciones. El estado del reintegro (lo decide Ingresos). Lo que se le debe a quien pagó de su bolsillo [P-8]. Generar el archivo para el contador. |
| **Ingresos y cobros** | Núcleo | Es dueño de los **acuerdos con patrones** y las **ventas de caballos**: monto acordado o precio, moneda, temporada del acuerdo, pagos recibidos, gastos cubiertos y su estado de reintegro. Es dueño de las **temporadas** (nombre, lugares, fechas) y de las **contrapartes**. Calcula **por cobrar** por acuerdo y total, y el **resultado por temporada** (consumiendo totales de Gastos). Valúa en US$ lo cobrado (al día del pago) y lo pendiente (a hoy, con «≈»). | Registrar el gasto cubierto (lo hace Gastos). Gestionar al patrón como persona o usuario (no existe). Dar de baja el caballo vendido (lo hace Caballos al enterarse). |
| **Captura** | Núcleo | Recibe cada **mensaje de origen**, lo rutea a una organización, decide si es carga o charla, lo interpreta en **registros propuestos**, **aclara** lo que falta (siempre con quien mandó el mensaje), sospecha **duplicados**, confirma (texto para gastos e ingresos; ✅ para el resto) y entrega cada registro al contexto dueño. Atiende **correcciones** y **consultas** en lenguaje natural respetando la privacidad (plata solo a owners). Convierte el trabajo de un proveedor y el vencimiento de un pago fijo en **preguntas a los owners**. | Las reglas de cada registro (qué es un gasto válido lo decide Gastos; qué es un caballo válido, Caballos). Guardar los registros. Transportar mensajes, transcribir audio o leer imágenes (Canal). Definir quién es owner (Organización). |
| **Caballos** | Soporte | Plantel y **ficha** de cada caballo: datos de registro, estado, ubicación, novedad vigente, eventos de actividad, ítems de salud, trabajos de proveedor. Altas, traslados, bajas. Traduce el catálogo de la app Polo Argentino. | Pendientes y visitas (Agenda; Caballos solo los muestra). Lo que cuesta cada caballo (fuera de alcance). Documentación oficial SENASA (más adelante). |
| **Caballeriza** | Soporte | Stock por **sede** e insumo: envase, consumo cargado por caballo por día, caballos que lo consumen, conteos e ingresos; calcula **días que alcanza**, alerta stock bajo y sugiere ajuste de consumo según conteos reales. | Comprar o pedir a comercios (se sacó). El gasto de la compra de insumos (Gastos). Qué caballos hay en cada lugar (lo publica Caballos). |
| **Agenda y tareas** | Soporte | **Visitas**, **tareas del piloto**, **pendientes del caballo** (solo los que pide alguien [P-11]) y **recordatorios personales**; arma los avisos salientes del día (7:00), los recordatorios y el **cierre del día** (20:00), cada uno en la hora local de quien lo recibe [P-21]. | Ejecutar el envío (Canal). Registrar lo que se hizo en la ficha (Caballos). |
| **Organización** | Soporte | Organizaciones, **membresías** (rol, owner sí/no, canales, accesos: Nada / Todo / Una parte con secciones y alcance de caballos), invitaciones, altas y bajas, **grupos de WhatsApp** vinculados, **lugares** de la organización. Garantiza el límite de privacidad. | Autenticar (Acceso). Interpretar mensajes. Decidir qué dato es sensible dentro de cada contexto (cada contexto lo marca; Organización dice quién puede ver qué sección). |
| **Cotizaciones** | Genérico | Cotización del día por moneda (blue compra, venta y promedio; euro, libra) con fuente; informa si no hay. | Decidir qué cotización usar para un gasto (lo decide Gastos o Ingresos). Preguntar al usuario (Captura). |
| **Canal de mensajería** | Genérico | Recibir y entregar mensajes de grupo y privados, reacciones, plantillas de avisos salientes; transcribir audios y leer imágenes y papeles (texto, montos, microchip). | Entender la intención o el negocio. |
| **Acceso** | Genérico | Identificar a la persona que entra a la app (link de un solo uso por WhatsApp). | Qué puede ver (Organización). |
| **Exportación** | Genérico | Armar el Excel o PDF de gastos de un período y lugar, con fotos, y mandarlo al mail del contador. | Calcular totales (los toma de Gastos). |

**Externos (fuera del sistema):** la **app Polo Argentino** (catálogo de caballos registrados, de terceros), las **fuentes de cotización** (Rava, DólarHoy u otra) y la **plataforma de WhatsApp** de Meta.

### 2.2 Mapa de contextos

*Canal de mensajería -> Captura*
- Relación: **Capa anticorrupción (ACL)** en Captura.
- Dirección: Canal upstream, Captura downstream.
- Integración: cruzan los mensajes entrantes (remitente por teléfono, grupo o privado, tipo, contenido, transcripción, lectura de imagen) y Captura los traduce a su **Mensaje de origen**. En sentido inverso, Captura le pide al Canal confirmar (reacción ✅ o texto) y preguntar (con botones). Las particularidades de la plataforma (ventanas de 24 h, plantillas, límites de grupo) no entran al modelo de Captura.

*Organización -> Captura*
- Relación: **Servicio de host abierto / lenguaje publicado** (Organización); Captura **conformista**.
- Dirección: Organización upstream, Captura downstream.
- Integración: Captura consulta las **membresías** de un teléfono (organizaciones, rol, owner, canales, activa, huso horario), a qué organización pertenece un grupo, quiénes son los owners y qué permisos de carga tiene esa persona [P-2]. Captura adopta ese lenguaje sin traducirlo. Eventos `MiembroDadoDeBaja` y `AccesosDelMiembroCambiados` le llegan para dejar de aceptar o de responder.

*Captura -> Gastos*
- Relación: **Cliente-proveedor**. Gastos es el **proveedor** y publica un **lenguaje publicado** para registrar, corregir, eliminar y marcar gastos y para buscar gastos parecidos; Captura es el **cliente** y lo usa tal cual.
- Dirección: Gastos upstream (define qué es un gasto válido), Captura downstream.
- Integración: Captura entrega **registros confirmados** (monto original, moneda, fecha, título, destino, clasificación, quién cargó, pagado por, origen, acuerdo que lo cubre). Gastos responde con el gasto registrado y su conversión, o lo rechaza si falta destino o clasificación. Gastos publica `PagoFijoVencido`, que Captura transforma en pregunta a los owners.

*Captura -> Ingresos y cobros*
- Relación: **Cliente-proveedor**, Ingresos como proveedor con lenguaje publicado.
- Dirección: Ingresos upstream, Captura downstream.
- Integración: Captura entrega acuerdos nuevos, pagos recibidos ("Me pagó 40 mil Halvorsen"), ventas y reintegros cobrados. Para rutear "Halvorsen" a un acuerdo, Captura consulta los acuerdos y ventas abiertos por contraparte.

*Captura -> Caballos / Caballeriza / Agenda y tareas*
- Relación: **Cliente-proveedor** con cada uno (cada contexto publica su lenguaje).
- Dirección: los tres upstream, Captura downstream.
- Integración: novedades, eventos de actividad, trabajos de proveedor, altas y traslados (Caballos); conteos e ingresos de stock (Caballeriza); visitas, tareas, recordatorios y "listo, hecho" (Agenda). Captura consulta los **nombres de caballos** de cada organización para interpretar y rutear.

*Gastos -> Ingresos y cobros*
- Relación: **Cliente-proveedor** (Gastos proveedor, Ingresos cliente) mediante eventos.
- Dirección: Gastos upstream, Ingresos downstream.
- Integración: `GastoMarcadoComoCubierto`, `CoberturaRetirada`, `GastoCorregido` y `GastoEliminado` (de gastos cubiertos) → Ingresos crea, ajusta o elimina el reintegro. Para el resultado por temporada, Ingresos publica cada **Temporada** (lugares y fechas) y consulta **totales de gastos de esos lugares y fechas, sin compra de caballos**. En sentido inverso, Ingresos publica `ReintegroCobrado` y Gastos lo **muestra** (no lo guarda como propio).

*Gastos y Ingresos y cobros (núcleo compartido)*
- Relación: **Núcleo compartido (shared kernel)** pequeño y explícito.
- Dirección: bidireccional; cambiarlo requiere acuerdo de ambos.
- Integración: comparten los objetos de valor **Dinero**, **Moneda**, **Cotización**, **Conversión** y la regla "todo en US$ con monto original guardado". Se justifica porque las dos mitades de Finanzas tienen que convertir igual o el resultado por temporada no cierra.

*Cotizaciones -> Gastos / Ingresos y cobros*
- Relación: **Servicio de host abierto** (Cotizaciones); Gastos e Ingresos **conformistas**.
- Dirección: Cotizaciones upstream.
- Integración: piden la cotización de una moneda para una fecha; reciben valor, compra, venta, tipo y fuente, o "no disponible". Quien la pide guarda una **copia** (la cotización usada no cambia si la fuente cambia).

*Fuentes de cotización (externas) -> Cotizaciones*
- Relación: **ACL** en Cotizaciones.
- Integración: cada fuente publica a su manera; Cotizaciones normaliza a "promedio compra/venta del día".

*App Polo Argentino (externa) -> Caballos*
- Relación: **ACL** en Caballos.
- Dirección: externa upstream.
- Integración: búsqueda en el catálogo y datos de registro (nombre, sexo, nacimiento, pelaje, padre, madre, criador, partidos). Caballos los traduce a sus **Datos de registro** y guarda la referencia. Es una integración **a explorar**: si no existe, el ACL queda vacío y el alta es por WhatsApp o manual.

*Caballos -> Caballeriza*
- Relación: **Cliente-proveedor** (Caballos proveedor).
- Dirección: Caballos upstream.
- Integración: `CaballoDadoDeAlta`, `CaballoTrasladado`, `CaballoDadoDeBaja` → Caballeriza recalcula cuántos caballos hay en cada sede y los días que alcanza.

*Caballos -> Agenda y tareas*
- Relación: **Conformista** (Agenda usa la identidad y el nombre del caballo tal como los publica Caballos).
- Dirección: Caballos upstream.
- Integración: identidades de caballos para visitas, tareas y pendientes. No hay pendientes automáticos en la V1 [P-11]. En sentido inverso, Agenda publica `TareaCompletada` y `VisitaRealizada`; Caballos no los consume directamente: lo que se hizo entra como evento de actividad por Captura.

*Caballos -> Ingresos y cobros / Gastos*
- Relación: **Cliente-proveedor** por eventos, en los dos sentidos de negocio.
- Integración: una venta referencia un caballo del plantel (Ingresos consulta su identidad); `VentaDeCaballoAcordada` → Caballos lo saca del plantel el día de la entrega [P-7]. Una compra se registra como gasto de Compra de caballos con referencia al caballo dado de alta (Captura arma los dos registros a partir de un mismo mensaje).

*Gastos -> Exportación*
- Relación: **Conformista** (Exportación toma el lenguaje de Gastos tal cual).
- Integración: lista de gastos del período y lugar con monto original, cotización, monto en US$ y comprobantes.

*Agenda y tareas -> Canal de mensajería*
- Relación: **Cliente-proveedor** (Canal proveedor genérico).
- Integración: avisos salientes con destinatario, momento y contenido; Canal informa si no se pudo entregar.

*Organización -> Todos los contextos de la app*
- Relación: **Servicio de host abierto**.
- Integración: "¿qué ve esta persona?" (secciones y alcance de caballos). Gastos e Ingresos aceptan lectura solo de owners. Organización también dice qué tipos de registro puede **cargar** cada persona [P-2].

### 2.3 Diagrama del mapa de contextos

```
EXTERNOS   [Fuentes de cotización]        [App Polo Argentino]          [Plataforma WhatsApp]
                  |                               |                              |
                 ACL                             ACL                            ACL
                  v                               v                              v
           (Cotizaciones)G                  (Caballos)S ---C/P---> (Caballeriza)S   (Canal de mensajería)G
             |OHS     |OHS                   |   |   \                             |        ^
             |conf.   |conf.            C/P  |   |    \--conformista--> (Agenda)S  |        | C/P
             v        v              (venta) |   |                        |  ^     |        | (avisos
     +-------------------------------+       |   |                        |  |     |        |  salientes)
     | [[GASTOS]]N <==SK==> [[INGRESOS]]N <--+   |                        |  +-----|--------+
     |      |                    ^    |          |                        |        |
     |      +--C/P (cobertura)---+    |          |                        |        |
     +------|------------------|------+          |                        |        |
            |  PL               |  PL            |  PL                    | PL     | ACL
            v                   v                v                        v        v
     ===================================================================================
                                        [[ CAPTURA ]]N
                 (cliente de todos los contextos de registro; downstream del Canal)
     ===================================================================================
            ^
            | OHS / Captura conformista
     (Organización)S --OHS--> (todos los contextos de la app y Acceso)G: qué ve cada persona

     (Gastos) --conformista--> (Exportación)G      (Caballeriza) --PL--> Captura (no dibujada)

Leyenda: [[X]]N núcleo · (X)S soporte · (X)G genérico · [X] externo
         Las flechas van de upstream a downstream.
         SK núcleo compartido · OHS servicio de host abierto · PL lenguaje publicado
         C/P cliente-proveedor · ACL capa anticorrupción (del lado downstream)
         conformista / conf.: el downstream adopta el modelo del upstream
```

Vista resumida en una línea por relación:

```
[Canal de mensajería]  --[U]--ACL-->        [Captura]
[Organización]         --[U]--OHS/PL-->     [Captura] (conformista)
[Gastos]               --[U]--C/P, PL-->    [Captura]
[Ingresos y cobros]    --[U]--C/P, PL-->    [Captura]
[Caballos]             --[U]--C/P, PL-->    [Captura]
[Caballeriza]          --[U]--C/P, PL-->    [Captura]
[Agenda y tareas]      --[U]--C/P, PL-->    [Captura]
[Gastos]               <==SK==>             [Ingresos y cobros]
[Gastos]               --[U]--C/P (eventos)--> [Ingresos y cobros]
[Cotizaciones]         --[U]--OHS-->        [Gastos], [Ingresos y cobros] (conformistas)
[Fuentes de cotización]--[U]--ACL-->        [Cotizaciones]
[App Polo Argentino]   --[U]--ACL-->        [Caballos]
[Caballos]             --[U]--C/P-->        [Caballeriza]
[Caballos]             --[U]--conformista-->[Agenda y tareas]
[Caballos]             <--C/P (eventos)-->  [Ingresos y cobros] (venta) / [Gastos] (compra)
[Gastos]               --[U]--conformista-->[Exportación]
[Canal de mensajería]  --[U]--C/P-->        [Agenda y tareas] (avisos salientes)
[Organización]         --[U]--OHS-->        [todos] (qué ve cada persona)
[Organización]         --[U]--OHS-->        [Acceso] (a quién identifica y qué puede ver)
```

---

## 3. Diseño táctico

Los tres contextos núcleo (**Gastos**, **Ingresos y cobros**, **Captura**) se desarrollan en profundidad. Los de soporte y genéricos tienen un tratamiento breve al final de cada apartado.

### 3.1 Entidades

#### Gastos (núcleo)

**Gasto**
- Identidad: propia, estable durante toda su vida (se corrige, no se reemplaza).
- Atributos clave: organización, **fecha del gasto** [P-22], título que dice qué se hizo ("Herraje de 4 caballos"), **destino** (un lugar o General) [P-29], **temporada asociada a mano** (opcional) [P-29], **clasificación** (grupo › categoría), **monto original** (Dinero), **conversión** a US$, **origen** (referencia al mensaje de origen) y comprobante opcional, **lo cargó**, **estado de pago** (pagado por la organización, pagado por una persona, o a pagar) [P-8], **cubierto por** (referencia a un acuerdo, opcional), **caballos vinculados** (opcional, sin montos) [P-9], historial de correcciones.
- Comportamiento: registrarse; corregir destino, clasificación, monto o fecha (cada corrección deja antes y después; si cambia el monto o la fecha, se vuelve a convertir con la cotización de la nueva fecha); **eliminarse** (quien lo cargó o un owner) [P-3, P-26]; separarse en dos; marcarse como cubierto por un acuerdo y retirar esa marca; saldarse ("ya se lo pagué a Pedro").
- Reglas: no existe un gasto sin clasificación (la duda se resuelve antes, en Captura); el destino siempre tiene valor (un lugar o General) [P-29]; el monto original y su moneda no se pisan nunca; un gasto de Compra de caballos no puede marcarse como cubierto [S-10]; un gasto tiene **una sola** categoría.

**Pago fijo**
- Identidad: propia (el "sueldo de los petiseros" es el mismo pago fijo mes a mes).
- Atributos: título, monto original, día del mes en que vence, destino, clasificación, vigencia (desde, hasta opcional), destinatarios de la pregunta (owners).
- Comportamiento: darse de alta; cambiar monto o día; darse de baja; abrir el **vencimiento** de cada mes.

**Vencimiento de pago fijo** (entidad interna del agregado Pago fijo)
- Identidad: local (pago fijo + mes).
- Atributos: fecha de vencimiento, estado (Pendiente / Postergado hasta tal día / Confirmado / Omitido), gasto generado (referencia).
- Reglas: un solo vencimiento por mes y pago fijo; confirmado genera **exactamente un** gasto; "mañana" lo posterga al día siguiente a las 9.

#### Ingresos y cobros (núcleo)

**Acuerdo con patrón**
- Identidad: propia.
- Atributos: equipo del patrón (Northfield), contraparte (referencia a Erik Halvorsen), **temporada** (referencia), monto acordado (Dinero), pagos recibidos, gastos cubiertos, estado (Sin pagos / Cobrando / Cobrado, derivado; o Caído).
- Comportamiento: cerrarse (con o sin seña); recibir un pago; incorporar un gasto cubierto; marcar un reintegro como cobrado; anular la cobertura de un gasto; corregir el monto acordado; **caerse** (lo cobrado queda, por cobrar pasa a cero; por cada reintegro pendiente se pregunta si igual se devuelve) [P-3]; **eliminarse** (quien lo cargó o un owner, con sus pagos y reintegros) [P-3, P-26].

**Venta de caballo**
- Identidad: propia.
- Atributos: caballo (referencia a Caballos), comprador (contraparte), dónde y cuándo, precio (Dinero), pagos recibidos, estado derivado.
- Comportamiento: acordarse, recibir pagos, caerse (sin cobros: se anula y el caballo vuelve al plantel; con cobros: se pregunta) y eliminarse [P-3].

**Temporada**
- Identidad: propia ("Inglaterra 2026" es la misma temporada para todos sus acuerdos).
- Atributos: nombre, **uno o más lugares** de la organización [P-24], **lugar principal** (donde vive y juega el polista) [P-30], desde, hasta. Puede ser futura: el conjunto de temporadas es el **calendario** del polista.
- Comportamiento: crearse (en el calendario de la app, o propuesta por el bot al cerrar un acuerdo), corregir fechas o lugares.
- Reglas: desde ≤ hasta; el lugar principal es uno de sus lugares; **dos temporadas no se superponen en fechas** [S-22] (el polista no está en dos lugares a la vez, y así un gasto no suma en dos resultados). Los gastos de sus lugares fuera de sus fechas no son de la temporada [P-25].

**Contraparte**
- Identidad: propia dentro de la organización; **no es usuario** ni recibe nada [P-6].
- Atributos: nombre, apodos ("Halvorsen", "Erik", "los de Northfield").
- Regla: los acuerdos y las ventas la referencian; con un solo acuerdo o venta abiertos, un cobro se imputa ahí; con varios, se pregunta.

**Pago recibido** (entidad interna de Acuerdo y de Venta)
- Identidad local; atributos: fecha, Dinero, **valor en US$ al día del pago** (fijo), origen (mensaje o comprobante), concepto (a cuenta del acuerdo, por defecto, o reintegro de un gasto si el mensaje lo dice) [P-5b].
- Regla: una vez registrado, su valor en US$ no cambia aunque cambie la cotización.

**Gasto cubierto / Reintegro** (entidad interna de Acuerdo)
- Identidad local, vinculada al gasto de Gastos por referencia.
- Atributos: referencia al gasto, monto pendiente (copia del original y de US$ del gasto), fecha, estado (A reintegrar / Reintegrado), **monto reintegrado tal como se dijo** (moneda y monto del mensaje), su valor en US$ al día del cobro, fecha de reintegro [P-28].
- Regla: su monto se actualiza solo por eventos de Gastos (`GastoCorregido`); si el gasto se elimina, el reintegro se elimina.

#### Captura (núcleo)

**Mensaje de origen**
- Identidad: propia; inmutable desde que llega.
- Atributos: organización (una vez ruteado), emisor (teléfono + membresía), canal (grupo de WhatsApp o privado), tipo (texto, audio, foto), contenido, duración, transcripción, lectura de imagen, recibido en (con la hora local del emisor [P-21]), registros que generó, **oculto** (sí/no).
- Regla: nunca se borra; es la trazabilidad de todo registro. Si un owner elimina el registro que generó, el mensaje queda **oculto**: no se ve en la app, pero se conserva para auditoría y para medir la IA [P-3].

**Carga**
- Identidad: propia, desde que se detecta intención de registrar hasta que se aplica o se descarta.
- Atributos: organización, emisor, mensajes de origen (uno o varios: el audio y luego la foto), **registros propuestos**, aclaraciones, sospechas de duplicado, estado, organización informada en la confirmación.
- Comportamiento: interpretarse; pedir aclaración; recibir respuesta; confirmarse; aplicarse (entregar cada registro a su contexto); descartarse; corregirse después de aplicada.

**Aclaración** (entidad interna de Carga)
- Identidad local; atributos: qué falta (lugar, categoría, cliente, tipo de cambio de una moneda sin fuente, fecha a más de 30 días, "¿es el mismo gasto?", "¿lo pagaste vos o queda a pagar?", "¿lo registro como gasto y por cuánto?"), destinatario, canal donde se pregunta, opciones, respuesta, estado (Abierta / Repreguntada / Respondida / Vencida) [P-10].
- Destinatario [P-1]: **siempre quien mandó el mensaje**, sea quien sea. Solo van a los **owners**: el trabajo de un proveedor que puede ser gasto, la pregunta del pago fijo y un ingreso mandado por alguien sin permiso para cargarlo [P-2].

**Contexto de conversación**
- Identidad: emisor multi-organización por privado.
- Atributos: última organización elegida, vigente hasta.
- Regla: se usa solo si el mensaje no permite deducir la organización por caballo o cliente.

#### Soporte y genéricos (breve)

- **Caballos — Caballo**: identidad propia (y referencia opcional al catálogo externo). Atributos: nombre, sexo, edad, pelaje, datos de registro, **situación** y **lugar** (por separado [P-12]), línea de estado, novedad vigente, ítems de salud. Todo caballo del plantel es del polista [P-13]. Entidades internas: **Evento de actividad**, **Novedad**, **Trabajo de proveedor**.
- **Caballeriza — Insumo de sede**: identidad sede + insumo; stock, envase, consumo cargado, caballos que lo consumen (todos o un subconjunto: "solo las 5 de doma"), conteos, ingresos.
- **Agenda — Visita, Tarea, Pendiente del caballo, Recordatorio personal**: cada uno con identidad propia, momento, responsable, origen y estado (hecho / no hecho).
- **Organización — Organización, Membresía, Grupo de WhatsApp, Lugar, Invitación**. La membresía separa el **rol** (manager, piloto…) del permiso de **owner** [P-19] e incluye el huso horario de la persona [P-21] y, si corresponde, su **lugar fijo** (Pedro → Pilar, Don Aníbal → Campo), que usa el *Resolutor de destino* [P-30].
- **Cotizaciones — Cotización del día** (moneda + fecha + fuente). **Exportación — Envío al contador**.

### 3.2 Objetos de valor

| Objeto de valor | Contexto | Atributos | Reglas |
|---|---|---|---|
| **Moneda** | Núcleo compartido Finanzas | US$, $, €, £ | Conjunto cerrado; ampliarlo es una decisión de negocio. |
| **Dinero** | Núcleo compartido Finanzas | importe, moneda | Importe positivo; no se suman dineros de monedas distintas sin conversión. |
| **Cotización** | Núcleo compartido Finanzas | moneda origen, valor, compra y venta (si aplica), fecha, tipo (blue promedio, oficial online, dada por el usuario), fuente | Para pesos, valor = (compra + venta) ÷ 2. Inmutable: una cotización usada es una foto del momento. |
| **Conversión** | Núcleo compartido Finanzas | dinero original, cotización, monto en US$, estado (Hecha / Pendiente) | La cotización dice en qué sentido se lee (pesos por dólar: se divide; dólares por euro o libra: se multiplica). El monto en US$ se **redondea a entero al registrarse** y los totales suman esos enteros [P-14]. Si no hay cotización de los últimos 3 días, queda **Pendiente**, se muestra con «≈» y se completa sola [P-15]. Si la moneda original es US$, no hay cotización. No se recalcula sola. |
| **Valuación estimada** | Ingresos | dinero pendiente, cotización de hoy, monto ≈ US$ | Siempre se muestra con «≈»; no se guarda, se calcula al mirar. |
| **Clasificación** | Gastos | grupo de gastos, categoría | La categoría pertenece al grupo; "Compra de caballos" lleva la marca **inversión**. |
| **Destino** | Gastos | un lugar de la organización, o **General** | Siempre tiene valor; se resuelve con la regla de P-30 (mensaje → caballos → calendario o lugar fijo → General). No deriva de la moneda. |
| **Período** | Gastos | desde, hasta, nombre (este mes, últimos 30 días, temporada, año, rango) | desde ≤ hasta; "al día N" cuando el período no terminó. El período "temporada" toma los lugares y fechas de la Temporada de Ingresos [P-4]. |
| **Estado de pago** | Gastos | pagado por la organización, pagado por una persona (quién, cómo), a pagar | El gasto suma en los totales cualquiera sea su estado de pago [P-8]. |
| **Caballos vinculados** | Gastos | lista de referencias a caballos | Sin montos; no hay reparto del gasto entre caballos [P-9]. |
| **Fecha del gasto** | Gastos | día | La que dice el mensaje («el viernes» = el último viernes pasado); si no dice, el día local del emisor; a más de 30 días, se confirma [P-22]. |
| **Origen** | Gastos, Ingresos, Caballos | referencia a mensaje de origen, tipo, quién lo cargó, canal | Todo registro que entra por WhatsApp tiene uno. |
| **Comprobante** | Gastos, Ingresos | tipo (factura, remito, ticket, comprobante de transferencia), imagen | Opcional; si no hay, se muestra el Origen. |
| **Quién lo cargó** | Todos los de registro | persona (membresía), canal | Se conserva aunque la persona se dé de baja. |
| **Por cobrar** | Ingresos | acordado, cobrado, reintegros pendientes, resultado | Resultado = acordado − cobrado + reintegros pendientes; siempre derivado. |
| **Resultado de temporada** | Ingresos | ingresos acordados, ya cobrado, gastos del destino (más los asociados a mano), resultado sobre lo acordado y sobre lo cobrado, todo en US$ | Excluye ventas y compras de caballos, que se muestran aparte [P-5]. |
| **Registro propuesto** | Captura | tipo (gasto, pago recibido, acuerdo, venta, reintegro, novedad, vareo, herraje, stock, visita, tarea, recordatorio, alta de caballo, traslado, trabajo de proveedor), datos interpretados, datos faltantes | Un registro con datos faltantes no se puede aplicar. |
| **Intención** | Captura | carga, consulta, corrección, respuesta a una aclaración, charla | Solo "carga" y "corrección" pueden producir registros. |
| **Monto hablado** | Captura | expresión ("180 lucas", "un palo", "40 mil"), interpretación | "Lucas" y "palo" son siempre pesos; "40 mil" toma la moneda del acuerdo al que se imputa. |
| **Canal** | Captura, Organización | grupo de WhatsApp (id) o privado | |
| **Accesos** | Organización | tipo (Nada, Todo, Una parte), secciones, alcance de caballos (todos, de lugares, algunos) | Gastos e Ingresos solo con "Todo"; "Todo" no se ofrece a proveedores. |
| **Situación / Línea de estado** | Caballos | En trabajo, En descanso, En doma, En recuperación, Retirada; texto libre | La situación no dice dónde está el caballo: eso es el Lugar [P-12]. |
| **Envase / Consumo por caballo** | Caballeriza | tamaño y unidad / cantidad diaria | Días que alcanza = stock ÷ (consumo × caballos ÷ envase); "Sin consumo cargado" si falta. |
| **Momento** | Agenda | fecha y hora, o "hoy / mañana / esta semana" | Los "mañana" se resuelven con hora por defecto 9:00, en la hora local de quien recibe [P-21]. |
| **Huso horario** | Organización | zona horaria de la persona | Por defecto, la de su lugar; el polista y el manager la cambian al viajar [P-21]. |
| **Permisos de carga** | Organización | qué tipos de registro puede cargar por WhatsApp | Por defecto: gastos cualquier miembro; ingresos solo owners; proveedores nunca gastos [P-2]. |

### 3.3 Agregados

#### Gastos

**Agregado `Gasto`** (raíz: Gasto)
- Contiene: Gasto, su Conversión, Clasificación, Destino, Origen, Comprobante, historial de correcciones, marca de cobertura.
- Invariantes:
  1. Tiene clasificación válida siempre, y destino (un lugar o General) siempre [P-29].
  10. Si tiene una temporada asociada a mano, esa temporada es de la misma organización; un gasto suma en **a lo sumo un** resultado de temporada [P-29].
  2. Monto original y moneda original son inmutables desde el registro; una corrección del monto crea una nueva versión con historial, no pisa el original.
  3. El monto en US$ es el que resulta de su conversión guardada; nunca cambia por un cambio de cotización posterior.
  4. Una sola categoría por gasto.
  5. A lo sumo un acuerdo lo cubre; un gasto de grupo "Compra de caballos" no puede estar cubierto [S-10].
  6. Un gasto eliminado desaparece de todo total y de toda lista; solo pueden eliminarlo quien lo cargó o un owner [P-3, P-26].
  7. Siempre tiene un origen.
  8. Su monto en US$ es un entero [P-14]; si la conversión está pendiente, suma su estimado y se marca con «≈» [P-15].
  9. Los caballos vinculados no llevan monto [P-9].
- **Por qué no hay un agregado "Libro de gastos".** La regla de oro "todo total es la suma de los gastos visibles" se cumple porque los totales **no se guardan**: se derivan siempre de los gastos vigentes. Hacer del libro un agregado obligaría a bloquear toda la organización en cada carga, y no hay ningún invariante que exija consistencia inmediata entre dos gastos. La detección de duplicados es una **política** con consistencia eventual y confirmación humana (servicio de dominio).

**Agregado `PagoFijo`** (raíz: Pago fijo)
- Contiene: el pago fijo y sus vencimientos.
- Invariantes: un vencimiento por mes; un vencimiento confirmado referencia exactamente un gasto; no se abren vencimientos fuera de la vigencia; un vencimiento postergado tiene fecha de próxima pregunta.

#### Ingresos y cobros

**Agregado `AcuerdoConPatron`** (raíz: Acuerdo con patrón)
- Contiene: pagos recibidos y gastos cubiertos (reintegros).
- Invariantes:
  1. Por cobrar = acordado − Σ pagos a cuenta + Σ reintegros pendientes, en todo momento.
  2. Los pagos a cuenta no superan el monto acordado sin una aclaración explícita [S-8].
  3. Estado = Sin pagos si no hay pagos; Cobrado si lo cobrado cubre lo acordado y no hay reintegros pendientes; Cobrando en cualquier otro caso; **Caído** si se marcó así (entonces por cobrar del acuerdo = reintegros que igual se van a devolver) [P-3].
  4. Cada reintegro referencia un gasto distinto (un gasto no se reintegra dos veces).
  5. Un pago en una moneda distinta a la del acuerdo se registra con su conversión del día [S-7].
  6. El valor en US$ de lo ya cobrado queda fijo; lo pendiente solo se valúa al mirar.
  7. Pertenece a una temporada de la misma organización [P-4].

**Agregado `VentaDeCaballo`** (raíz: Venta de caballo)
- Invariantes: referencia a un caballo de la misma organización; cobrado ≤ precio; estado derivado igual que el acuerdo (sin reintegros).
- **Agregado `Temporada`** (raíz: Temporada). Invariantes: desde ≤ hasta; lugar principal dentro de sus lugares. **Política entre agregados:** ninguna temporada se superpone en fechas con otra de la organización [S-22]; se valida al crear o mover una temporada, con consistencia inmediata.
- **Agregado `Contraparte`** (raíz: Contraparte). Invariante: nombre y apodos únicos dentro de la organización, para que la imputación de cobros no sea ambigua. No es un usuario ni un "patrón" de la plataforma [P-6].

#### Captura

**Agregado `Carga`** (raíz: Carga)
- Contiene: registros propuestos, aclaraciones, sospechas de duplicado, referencias a mensajes de origen.
- Invariantes:
  1. Una carga cuya intención es charla o consulta **nunca** se aplica.
  2. No se aplica mientras haya aclaraciones abiertas o duplicados sin respuesta.
  3. Nunca se abre una aclaración sobre el tipo de cambio del peso.
  4. La organización está resuelta antes de interpretar datos que dependen de ella (caballos, lugares, acuerdos) y antes de responder nada.
  5. Una carga de un **proveedor** nunca produce un gasto directo: produce un trabajo de proveedor y, si corresponde, una aclaración dirigida a los owners.
  6. Regla de respuesta [P-1, P-27]: si hay una duda, se le pregunta a **quien mandó el mensaje**. Un **gasto o un ingreso** se confirma **siempre** con un texto **por privado** a quien lo cargó, que dice qué se entendió y qué se cargó; en el grupo solo queda ✅. Las dudas sobre plata también van por privado [S-16]; las de caballos y caballeriza, en el chat donde llegó el mensaje. El resto se confirma solo con ✅. Las preguntas que van a owners (trabajo de proveedor, pago fijo, ingreso sin permiso) van por privado.
  7. Una vez aplicada, solo cambia por corrección o eliminación (hacia los contextos dueños), nunca se reabre.
  8. Toda confirmación dice en qué organización se cargó cuando el emisor tiene más de una.
  9. Con la pregunta y la repregunta sin respuesta, la carga pasa a **Sin terminar**: se ve en la app de los owners y no entra a ningún contexto hasta completarse [P-10].
  10. Varios mensajes del mismo emisor en el mismo chat, dentro de 5 minutos y antes de confirmar, son la misma carga [P-16].

**Agregado `ContextoDeConversacion`** (raíz: Contexto de conversación). Invariante: una sola organización vigente por emisor y vencimiento explícito.

**Agregado `MensajeDeOrigen`** (raíz: Mensaje de origen). Invariante: inmutable; agregar transcripción o lectura de imagen es completar, no modificar.

#### Soporte y genéricos (breve)

| Agregado | Contexto | Invariantes principales |
|---|---|---|
| `Caballo` | Caballos | Una situación y un lugar de la organización; los eventos se ordenan por fecha y conservan quién los reportó; un caballo dado de baja no recibe eventos. |
| `InsumoDeSede` | Caballeriza | Stock ≥ 0; consumo y envase en unidades compatibles; los caballos consumidores son de esa sede. |
| `Visita`, `Tarea`, `Pendiente`, `RecordatorioPersonal` | Agenda | Momento y responsable definidos; una tarea solo la tacha el piloto o un owner; un recordatorio personal solo lo ve su dueño. |
| `Organizacion` | Organización | Al menos un owner siempre (el último no se puede sacar) [P-19]; cada grupo de WhatsApp pertenece a una sola organización; moneda de referencia US$ [P-20]. |
| `Membresia` | Organización | Cada persona puede eliminar lo que cargó; un owner, cualquier registro [P-26]. Piloto, petisero, puestero y familiar tienen una sola membresía activa; un proveedor no puede tener "Todo" ni cargar gastos; Gastos e Ingresos solo con "Todo"; el acceso parcial es solo para mirar y solo de sus caballos [P-18]; rol y owner van por separado [P-19]. |
| `CotizacionDelDia` | Cotizaciones | Una por moneda, fecha y fuente; promedio entre compra y venta para el blue. |

### 3.4 Servicios de dominio

| Servicio | Contexto | Propósito | Entradas | Salidas | Por qué no vive en una entidad |
|---|---|---|---|---|---|
| **Conversor a US$** | Gastos (y núcleo compartido) | Obtener la cotización que corresponde (del día del gasto, o la última hábil, o la última de hasta 3 días) y producir la conversión redondeada [P-14, P-15]. | Dinero original, fecha del gasto | Conversión hecha o pendiente; para euros sin fuente, "no hay cotización" para que Captura pregunte | Depende de un contexto externo (Cotizaciones) y de una regla que comparten Gastos e Ingresos; el gasto no debe conocer fuentes. |
| **Totalizador de gastos** | Gastos | Sumar gastos vigentes por período, lugar, grupo y categoría; con o sin inversión. | Organización, período, lugar, filtros | Total en US$, cantidad, desglose | Opera sobre muchos agregados; garantiza la regla de oro sin crear un agregado gigante. |
| **Buscador de gastos parecidos** | Gastos | Encontrar gastos que podrían ser el mismo. | Organización, Dinero, categoría, fecha, ventana de días | Lista de candidatos con quién los cargó | Compara contra todo el libro de la organización; ningún gasto se conoce a sí mismo en relación con los demás. |
| **Generador de vencimientos** | Gastos | Abrir el vencimiento del día de cada pago fijo vigente y publicar `PagoFijoVencido`. | Fecha de hoy | Vencimientos abiertos | Es un proceso del calendario sobre todos los pagos fijos. |
| **Calculador de por cobrar** | Ingresos | Sumar el por cobrar de todos los acuerdos y ventas abiertos, con valuación de hoy. | Organización, fecha | Total en US$ (≈ para lo pendiente en otra moneda), detalle | Agrega varios agregados y depende de cotizaciones del día. |
| **Calculador de resultado de temporada** | Ingresos | Enfrentar los ingresos de una temporada (acordados y ya cobrados) con los gastos de sus lugares **dentro de sus fechas** más los gastos que un owner **asoció a mano** a la temporada [P-5, P-25, P-29]; los generales no asociados no entran; los gastos de esos lugares fuera de las fechas quedan del destino, no de la temporada. | Temporada (lugares y fechas) | Ingresos acordados, cobrado, gastos, dos resultados en US$; ventas y compras aparte | Cruza dos contextos (Ingresos y Gastos) y la regla de dejar afuera los caballos. |
| **Imputador de cobros** | Ingresos | Decidir a qué acuerdo o venta, y a qué concepto (a cuenta o reintegro), va un pago dicho por una contraparte. | Contraparte, Dinero, texto | Acuerdo o venta y concepto, o ambigüedad | Una misma contraparte puede tener varios acuerdos y ventas (Halvorsen: Northfield y Halcona). |
| **Resolutor de destino** | Captura | Darle lugar a un gasto sin preguntar, en este orden: lugar nombrado → caballos nombrados en un mismo lugar → calendario (si carga un owner, o alguien sin lugar fijo) → lugar fijo de quien carga → General [P-30]. | Registro propuesto, emisor, fecha del gasto | Destino y de dónde salió (para mostrarlo en el detalle) | Cruza tres contextos: Caballos (ubicación), Ingresos (calendario de temporadas) y Organización (lugar fijo del miembro). |
| **Ruteador de organización** | Captura | Resolver la organización de un mensaje. | Emisor, canal, contenido interpretado, contexto de conversación | Organización, o aclaración con botones de clientes recientes | Necesita membresías (Organización), nombres de caballos (Caballos) y el contexto; no es responsabilidad del mensaje ni de la carga. |
| **Clasificador de intención** | Captura | Distinguir carga de charla, consulta, corrección o respuesta. | Mensaje (y los anteriores) | Intención | Es una política sobre la conversación, no sobre un registro. |
| **Intérprete de registros** | Captura | Convertir un mensaje en registros propuestos con datos faltantes marcados. | Mensaje, organización, vocabulario (caballos, lugares, acuerdos, taxonomía) | Registros propuestos | Usa el lenguaje de varios contextos a la vez. |
| **Detector de duplicados** | Captura | Antes de confirmar un gasto, preguntar si es el mismo que uno ya registrado. | Registro propuesto de gasto | Sospecha de duplicado (o ninguna) | Combina el buscador de Gastos con la política de cuándo preguntar y a quién. |
| **Política de respuesta** | Captura | Decidir si el bot contesta, cómo, a quién y por dónde: duda → al emisor (plata, por privado); gasto o ingreso → texto por privado con lo entendido, ✅ en el grupo; resto → ✅; tres casos van a owners por privado [P-1, P-27]. | Tipo de registro, dudas, emisor, canal | Respuesta (texto, ✅ o nada) y destinatario | Es una regla sobre la conversación entera, no sobre un registro. |
| **Respondedor de consultas** | Captura | Contestar en lenguaje natural con los mismos datos de la app, respetando privacidad. | Pregunta, emisor, canal | Respuesta o derivación al privado | Lee de varios contextos y aplica reglas de acceso de Organización. |
| **Calculador de días que alcanza** | Caballeriza | Días de stock por insumo y sede, y sugerencia de consumo real. | Insumo, caballos de la sede, conteos | Días, alerta, sugerencia | Necesita la cantidad de caballos por sede, que publica Caballos. |
| **Planificador de avisos** | Agenda | Armar las tareas de las 7:00, los recordatorios y el cierre de las 20:00. | Tareas, visitas, pendientes, resumen del día | Avisos salientes | Recorre varios agregados y contextos. |

---

## 4. Eventos de dominio

Los eventos marcados **Cruza frontera: Sí** forman parte del lenguaje publicado de su contexto. Los marcados **No** son hechos internos útiles para el propio contexto (y para la trazabilidad).

### Eventos de Captura

*MensajeRecibido*
- Disparador: llega un audio, foto o texto por un grupo de WhatsApp o por privado (traducido por el ACL del Canal).
- Payload: mensaje de origen, emisor, canal, grupo de WhatsApp, recibido en.
- Consumidores: Captura (ruteo e intención).
- Cruza frontera: No.

*OrganizacionDelMensajeResuelta*
- Disparador: el ruteador asigna una organización (por grupo, por membresía única, por caballo o cliente nombrado, o por respuesta del emisor).
- Payload: mensaje, organización, forma de resolución.
- Consumidores: Captura (actualiza el contexto de conversación).
- Cruza frontera: No.

*MensajeTomadoComoCharla*
- Disparador: el clasificador decide que no es una carga.
- Payload: mensaje, intención detectada.
- Consumidores: ninguno fuera; queda para evaluar la precisión del bot.
- Cruza frontera: No.

*CargaInterpretada*
- Disparador: un mensaje con intención de carga se traduce en registros propuestos.
- Payload: carga, organización, registros propuestos, datos faltantes.
- Consumidores: Captura.
- Cruza frontera: No.

*AclaracionSolicitada*
- Disparador: falta categoría, caballos, cliente, tipo de cambio de una moneda sin fuente, quién pagó, o hay que preguntar a owners por un trabajo de proveedor o un pago fijo.
- Payload: carga, qué falta, destinatario, canal, opciones.
- Consumidores: Canal de mensajería (la envía).
- Cruza frontera: Sí (hacia Canal).

*AclaracionRespondida*
- Disparador: el destinatario contesta.
- Payload: carga, aclaración, respuesta, quién respondió.
- Consumidores: Captura.
- Cruza frontera: No.

*PosibleDuplicadoDetectado*
- Disparador: el buscador de Gastos devuelve un gasto parecido.
- Payload: carga, gasto candidato, quién lo cargó y cuándo.
- Consumidores: Captura (abre aclaración "¿Es el mismo que cargó Pedro el martes?").
- Cruza frontera: No.

*CargaConfirmada*
- Disparador: no quedan aclaraciones abiertas y la carga se aplica a los contextos dueños.
- Payload: carga, organización, registros por tipo, emisor, mensajes de origen.
- Consumidores: Gastos, Ingresos y cobros, Caballos, Caballeriza, Agenda (cada uno toma los registros de su lenguaje); Canal (confirmación ✅ o texto).
- Cruza frontera: Sí.

*CargaDescartada*
- Disparador: el emisor la cancela, se confirma que era duplicado, se confirma que no era un registro, o una aclaración vence sin respuesta [P-10].
- Payload: carga, motivo, mensajes de origen.
- Consumidores: Canal (avisar si corresponde); métricas de calidad.
- Cruza frontera: Sí (hacia Canal).

*CorreccionSolicitada*
- Disparador: "no, eran dólares", "eso era para el campo", "borrá el último".
- Payload: carga original, registro afectado, cambio pedido, quién lo pidió.
- Consumidores: el contexto dueño del registro (Gastos, Ingresos, Caballos…).
- Cruza frontera: Sí.

### Eventos de Gastos

*GastoRegistrado*
- Disparador: Gastos acepta un registro confirmado de gasto (o la confirmación de un vencimiento de pago fijo).
- Payload: gasto, organización, fecha, destino, clasificación, monto original, conversión, monto en US$, lo cargó, pagado por, origen, cubierto por (si lo dice el mismo mensaje).
- Consumidores: Ingresos (si viene cubierto), Agenda (cierre del día), Exportación (lectura), Inicio de la app.
- Cruza frontera: Sí.

*GastoMarcadoComoCubierto*
- Disparador: "Lo cubre Halvorsen" al registrar o después.
- Payload: gasto, acuerdo, monto original y en US$, fecha.
- Consumidores: Ingresos y cobros (crea el reintegro pendiente).
- Cruza frontera: Sí.

*CoberturaRetirada*
- Disparador: corrección: el gasto no lo cubre el patrón.
- Payload: gasto, acuerdo.
- Consumidores: Ingresos (anula el reintegro).
- Cruza frontera: Sí.

*GastoCorregido*
- Disparador: cambio de monto, fecha, destino, temporada asociada o clasificación.
- Payload: gasto, antes, después, nueva conversión si aplica, quién corrigió.
- Consumidores: Ingresos (si estaba cubierto), métricas de calidad de la IA.
- Cruza frontera: Sí.

*GastoEliminado*
- Disparador: quien lo cargó o un owner lo elimina ("borrá el último" o desde la app), por ejemplo, porque era un duplicado detectado después de registrado [P-3].
- Payload: gasto, motivo, quién.
- Consumidores: Ingresos (si estaba cubierto: elimina el reintegro), Captura (oculta el mensaje de origen).
- Cruza frontera: Sí.

*GastoSaldado*
- Disparador: un gasto "a pagar" o pagado por una persona se termina de pagar ("ya se lo pagué a Pedro") [P-8].
- Payload: gasto, quién lo saldó, fecha.
- Consumidores: Gastos (lista "Le debés a…"), Inicio.
- Cruza frontera: No.

*GastoSeparado*
- Disparador: un pago mixto se parte en dos.
- Payload: gasto original, gastos resultantes.
- Consumidores: Gastos.
- Cruza frontera: No.

*PagoFijoDadoDeAlta / PagoFijoModificado / PagoFijoDadoDeBaja*
- Disparador: un owner lo configura por WhatsApp o en la app.
- Payload: pago fijo, monto, día, destino, clasificación.
- Consumidores: Agenda ("Pagos que vienen").
- Cruza frontera: Sí.

*PagoFijoVencido*
- Disparador: llega el día de vencimiento (o el día de la postergación).
- Payload: pago fijo, vencimiento, monto, destinatarios.
- Consumidores: Captura (abre la pregunta "¿Lo pagaste?").
- Cruza frontera: Sí.

*VencimientoDePagoFijoConfirmado*
- Disparador: la respuesta "sí" llega como registro confirmado.
- Payload: vencimiento, gasto generado.
- Consumidores: Gastos (dispara `GastoRegistrado`).
- Cruza frontera: No.

*VencimientoDePagoFijoPostergado*
- Disparador: "Todavía no, mañana".
- Payload: vencimiento, nueva fecha de pregunta (día siguiente, 9:00).
- Consumidores: Gastos (Generador de vencimientos).
- Cruza frontera: No.

### Eventos de Ingresos y cobros

*AcuerdoCerrado*
- Disparador: "Cerré con Whitmore para jugar Wellington, 180 mil dólares".
- Payload: acuerdo, equipo del patrón, contraparte, temporada, monto acordado.
- Consumidores: Inicio (por cobrar), Captura (vocabulario para imputar cobros).
- Cruza frontera: Sí.

*PagoDeAcuerdoRecibido*
- Disparador: "Me pagó 40 mil Halvorsen", seña al cerrar, transferencia con foto.
- Payload: acuerdo, Dinero, valor en US$ al día, origen, cobrado acumulado, por cobrar.
- Consumidores: Captura (respuesta "Llevás cobrado… faltan…"), Agenda (cierre del día).
- Cruza frontera: Sí.

*ReintegroPendienteRegistrado*
- Disparador: reacción a `GastoMarcadoComoCubierto`.
- Payload: acuerdo, gasto, monto, nuevo por cobrar.
- Consumidores: Gastos (muestra "Está sumado a lo que te debe").
- Cruza frontera: Sí.

*ReintegroCobrado*
- Disparador: el patrón devuelve un gasto cubierto.
- Payload: acuerdo, gasto, Dinero, fecha.
- Consumidores: Gastos (muestra el gasto como reintegrado).
- Cruza frontera: Sí.

*AcuerdoCobradoEnTotal*
- Disparador: lo cobrado cubre lo acordado y no quedan reintegros pendientes.
- Payload: acuerdo, total cobrado en US$.
- Consumidores: Inicio, resultado por temporada.
- Cruza frontera: Sí.

*VentaDeCaballoAcordada*
- Disparador: "Vendí a Halcona a Halvorsen, 85 mil dólares".
- Payload: venta, caballo, comprador, precio.
- Consumidores: Caballos (lo marca como vendido o lo da de baja, [P-7]).
- Cruza frontera: Sí.

*CobroDeVentaRecibido / VentaCobradaEnTotal*
- Disparador: pago parcial o total del comprador.
- Payload: venta, Dinero, cobrado acumulado.
- Consumidores: Inicio, Caballos (si la baja se da al cobro total, [P-7]).
- Cruza frontera: Sí.

*AcuerdoCaido / VentaCaida*
- Disparador: un owner indica que el acuerdo o la venta no se concretó [P-3].
- Payload: acuerdo o venta, lo cobrado hasta el momento, reintegros pendientes.
- Consumidores: Captura (pregunta si los reintegros pendientes se devuelven igual), Gastos (*CoberturaRetirada* en los que no), Caballos (en una venta sin cobros, el caballo vuelve al plantel).
- Cruza frontera: Sí.

*AcuerdoEliminado / VentaEliminada*
- Disparador: un owner elimina el registro [P-3].
- Payload: acuerdo o venta, pagos y reintegros que se eliminan con él.
- Consumidores: Gastos (se les saca la marca "lo cubre" a sus gastos cubiertos), Captura (oculta los mensajes de origen).
- Cruza frontera: Sí.

*TemporadaCreada / TemporadaModificada*
- Disparador: el bot la propone al cerrar un acuerdo y un owner la confirma, o un owner corrige lugares o fechas [P-4].
- Payload: temporada, lugares, desde, hasta.
- Consumidores: Gastos (período "temporada"), Ingresos (resultado).
- Cruza frontera: Sí.

### Eventos de Caballos

| Evento | Disparador | Payload | Consumidores | Cruza frontera |
|---|---|---|---|---|
| *CaballoDadoDeAlta* | Elegido del catálogo o mandado por WhatsApp | caballo, datos, lugar, referencia externa, compra (si la hubo) | Caballeriza, Agenda, Captura (vocabulario) | Sí |
| *CaballoTrasladado* | "La Tormenta se va al campo mañana" | caballo, lugar de origen y destino, fecha | Caballeriza, Agenda (tarea al piloto) | Sí |
| *EstadoDelCaballoCambiado* | Pasa a recuperación, vuelve a jugar, sale al exterior | caballo, estado anterior y nuevo | Inicio, Agenda | Sí |
| *NovedadReportada* | "La Rockstar renguea", "la Negra no comió" | caballo, texto, quién, foto, origen | Inicio ("Necesita tu atención"), Agenda (cierre del día) | Sí |
| *ActividadRegistrada* | Vareo, herraje, práctica, partido, al box | caballo(s), tipo, fecha, quién | Agenda (tacha tareas, cierre del día), Caballos (salud) | Sí |
| *TrabajoDeProveedorRegistrado* | El veterinario o el herrero carga lo que hizo | proveedor, caballos, qué hizo, monto si lo dijo | Captura (pregunta a owners si lo registra como gasto) | Sí |
| *HerrajeVencido* | Pasan más semanas que las previstas desde el último herraje | caballo, semanas | Inicio, Agenda | Sí |
| *CaballoDadoDeBaja* | Venta, muerte, retiro del plantel | caballo, motivo | Caballeriza, Agenda | Sí |

### Eventos de Caballeriza

| Evento | Disparador | Payload | Consumidores | Cruza frontera |
|---|---|---|---|---|
| *StockContado* | "Quedan 18 bolsas", foto del depósito | sede, insumo, cantidad, quién | Caballeriza | No |
| *InsumoIngresado* | "Entraron 30 bolsas" | sede, insumo, cantidad, quién | Caballeriza | No |
| *StockBajoDetectado* | Días que alcanza < 8 | sede, insumo, días | Inicio, Agenda (cierre del día), Canal (aviso a owners) | Sí |
| *ConsumoAjustado* | Cambio manual o aceptación de la sugerencia | sede, insumo, antes, después | Caballeriza | No |

### Eventos de Agenda y tareas

| Evento | Disparador | Payload | Consumidores | Cruza frontera |
|---|---|---|---|---|
| *VisitaAgendada* | "El jueves viene Cacho a herrar a…" | proveedor, día, motivo, caballos | Caballos (pendientes de la ficha), Canal (aviso al piloto el día antes) | Sí |
| *CargaSinTerminar* (Captura) | Pregunta y repregunta sin respuesta [P-10] | carga, qué falta | Inicio ("Necesita tu atención") | Sí |
| *TareaAsignadaAlPiloto* | Pedido del polista o manager, o derivado de un traslado | tarea, piloto, momento, caballos | Canal (tareas de las 7:00) | Sí |
| *TareaCompletada* | "Listo, hecho" | tarea, quién, cuándo | Inicio, cierre del día | Sí |
| *RecordatorioProgramado / RecordatorioCumplido* | "Mañana haceme acordar…" | recordatorio, dueño, momento | Canal | Sí |
| *CierreDelDiaGenerado* | 20:00 | resumen | Canal | Sí |

### Eventos de Organización

| Evento | Disparador | Payload | Consumidores | Cruza frontera |
|---|---|---|---|---|
| *OrganizacionCreada* | Un polista o un manager la crea | organización, owner inicial | Todos | Sí |
| *MiembroInvitado / MiembroSeSumo* | Invitación / responde "Sí" | membresía, rol, canales, accesos | Captura, Canal | Sí |
| *AccesosDelMiembroCambiados* | Un owner cambia qué ve | membresía, accesos anteriores y nuevos | Todos los de la app, Captura (consultas) | Sí |
| *MiembroDadoDeBaja* | Se va un petisero, cambia el veterinario | membresía | Captura (deja de aceptar sus mensajes) | Sí |
| *GrupoDeWhatsAppVinculado* | Se suma el bot a un grupo de la organización | grupo, organización | Captura | Sí |
| *LugarAgregado* | Nueva caballeriza de temporada | lugar | Gastos, Caballos, Caballeriza | Sí |

### Eventos de Cotizaciones

| Evento | Disparador | Payload | Consumidores | Cruza frontera |
|---|---|---|---|---|
| *CotizacionDelDiaPublicada* | Lectura diaria de la fuente | moneda, compra, venta, promedio, fecha, fuente | Gastos, Ingresos | Sí |
| *CotizacionNoDisponible* | La fuente no responde o no hay fuente para esa moneda | moneda, fecha | Gastos (pesos: usa la última de hasta 3 días o deja la conversión pendiente [P-15]); Captura (euros u otra moneda sin fuente: pregunta) | Sí |

### Encadenamiento de eventos

La consigna pide los flujos de **apertura de sobre**, **intercambio completado** e **intercambio no concretado**. Esos nombres no existen en este dominio. Siguiendo lo acordado con el equipo, se mapean a los flujos equivalentes del producto y el mapeo queda explícito en [S-0].

| Nombre de la consigna | Flujo equivalente en el dominio | Por qué es el equivalente |
|---|---|---|
| **Apertura de sobre** | **Apertura de un mensaje entrante**: un audio o foto que se "abre" y del que salen varios registros. | Como un sobre con varias figuritas, un audio de un petisero trae varios registros a la vez (4 vareos + una novedad + una foto), y no se sabe qué contiene hasta abrirlo. |
| **Intercambio completado** | **Intercambio polista–patrón cerrado**: el polista juega y adelanta gastos; el patrón paga lo acordado y reintegra; se llega a *AcuerdoCobradoEnTotal*. (Variante: venta de caballo cobrada.) | Es la única relación de dar y recibir entre dos partes que modela el producto. |
| **Intercambio no concretado** | **Carga que no llega a registrarse** (charla, duplicado, cancelada, sin terminar), **pago fijo postergado** y **acuerdo o venta caída** [P-3]. | Son los casos en que una de las partes propone y la otra no confirma. |

#### Flujo 1 · Apertura de un mensaje entrante (audio del petisero en el grupo)

| # | Contexto | Evento | Reacción |
|---|---|---|---|
| 1 | Canal → Captura | *MensajeRecibido* | Audio de Ramón en el grupo de la organización. |
| 2 | Captura | *OrganizacionDelMensajeResuelta* | Por grupo: sin preguntas. |
| 3 | Captura | *CargaInterpretada* | 4 vareos (Morena, Tordillo, Cautiva, Gitana) + novedad de Rockstar (renguera, al box). |
| 4 | Captura | *CargaConfirmada* | Sin dudas y sin plata: solo una reacción ✅ en el grupo [P-1]. |
| 5 | Caballos | *ActividadRegistrada* ×4, *NovedadReportada*, *EstadoDelCaballoCambiado* (Rockstar → al box) | Fichas actualizadas. |
| 6 | Agenda | (reacciona a la novedad) | Suma a "Necesita tu atención" y al cierre del día. |
| 7 | Canal → Captura | *MensajeRecibido* (foto de la mano) | Se adjunta a la misma carga o a una nueva [P-16]; *NovedadReportada* actualizada con foto. |

Variante con plata (audio del piloto "Vino Cacho, herró a 4… son 180 lucas"):
*MensajeRecibido* → *CargaInterpretada* (herraje ×4 + gasto $ 180.000) → Cotizaciones da el blue → *AclaracionSolicitada* a Pedro, que es quien mandó el mensaje ("¿Lo pagaste vos o queda a pagar?") → *AclaracionRespondida* → Gastos busca parecidos (ninguno) → *CargaConfirmada* con texto por privado, porque hay un gasto («Herraje de 4 caballos, US$ 116, pagado por vos. Anotado en Pilar») → **Gastos** *GastoRegistrado* (Caballos › Herrero, Pilar, US$ 116, pagado por el piloto, vinculado a Bruja, Gitana, Dinamita y Lucera) · **Caballos** *ActividadRegistrada* ×4 ("herrada", sin monto en la ficha) · **Agenda** *TareaCompletada* (herraje de las 4).

Variante proveedor por privado: *MensajeRecibido* (Dra. Ibarra) → ruteador no puede deducir → *AclaracionSolicitada* (botones: Tomás / Juan Pérez) → *AclaracionRespondida* → *OrganizacionDelMensajeResuelta* → *CargaConfirmada* → **Caballos** *TrabajoDeProveedorRegistrado* y *EstadoDelCaballoCambiado* (Patria: alta, vuelve a trabajar) → **Captura** abre *AclaracionSolicitada* a los owners ("¿Lo registro como gasto y por cuánto?") → si responden, *GastoRegistrado*.

#### Flujo 2 · Intercambio polista–patrón completado

| # | Contexto | Evento | Efecto |
|---|---|---|---|
| 1 | Captura → Ingresos | *CargaConfirmada* → *AcuerdoCerrado* | Northfield, US$ 250.000, Inglaterra 2026. Por cobrar = 250.000. |
| 2 | Captura → Gastos | *CargaConfirmada* → *GastoRegistrado* + *GastoMarcadoComoCubierto* | Flete aéreo US$ 38.000, destino Windsor, lo cubre Northfield. |
| 3 | Ingresos | *ReintegroPendienteRegistrado* | Por cobrar = 288.000. Gastos muestra "Está sumado a lo que te debe". |
| 4 | Captura → Ingresos | *PagoDeAcuerdoRecibido* (15/5 US$ 100.000; 20/6 US$ 40.000) | Por cobrar baja; estado Cobrando. |
| 5 | Captura → Ingresos | *ReintegroCobrado* (flete, pasajes) | Gastos muestra el gasto como reintegrado. |
| 6 | Ingresos | *PagoDeAcuerdoRecibido* (saldo) → *AcuerdoCobradoEnTotal* | Estado Cobrado. |
| 7 | Ingresos (lectura de Gastos) | (cálculo del resultado de temporada) | Inglaterra 2026 (Windsor, abril a julio): ingresos acordados (acuerdo + reintegros) y ya cobrados, menos los gastos de Windsor en esas fechas. La venta de Halcona se muestra aparte [P-5]. |

Variante venta: *VentaDeCaballoAcordada* → **Caballos** marca el caballo como vendido → *CobroDeVentaRecibido* → *VentaCobradaEnTotal* → (si la baja es al cobro total) *CaballoDadoDeBaja* → **Caballeriza** recalcula días de stock.

#### Flujo 3 · Intercambio no concretado

| Caso | Cadena |
|---|---|
| **Charla en el grupo** | *MensajeRecibido* ("che, ¿cuánto te salió el flete?") → *MensajeTomadoComoCharla*. Nada cruza la frontera; el bot no toca el mensaje. |
| **Duplicado** | *MensajeRecibido* (polista por privado: "pagué 180 mil al herrero") → *CargaInterpretada* → *PosibleDuplicadoDetectado* (lo cargó Pedro en el grupo) → *AclaracionSolicitada* ("¿Es el mismo?") → "sí" → *CargaDescartada* (motivo: duplicado). Gastos no recibe nada; los totales no se inflan. |
| **Duplicado detectado tarde** | Si ya se registraron los dos, quien cargó el repetido o un owner elimina uno: *GastoEliminado* → (si estaba cubierto) Ingresos elimina el reintegro → Captura oculta el mensaje de origen [P-3]. |
| **Sin respuesta** | *AclaracionSolicitada* (¿lo pagaste vos o queda a pagar?, a Pedro) → sin respuesta → repregunta a las 9:00 del día siguiente → sin respuesta → *CargaSinTerminar*: aparece en "Necesita tu atención" y no suma hasta que se completa [P-10]. |
| **Pago fijo postergado** | *PagoFijoVencido* → Captura *AclaracionSolicitada* ("¿Lo pagaste?") → "mañana" → Gastos *VencimientoDePagoFijoPostergado* → al día siguiente 9:00 *PagoFijoVencido* de nuevo. Mientras tanto no hay gasto. |
| **Trabajo de proveedor no registrado como gasto** | *TrabajoDeProveedorRegistrado* → Captura pregunta a owners → "no" → la actividad queda en la ficha, sin gasto. |
| **Acuerdo caído** | *AcuerdoCaido* → lo cobrado queda y el por cobrar del acuerdo pasa a cero → Captura pregunta por cada reintegro pendiente si igual se devuelve → si es no, Gastos *CoberturaRetirada* y el gasto pasa a ser propio [P-3]. |
| **Venta caída** | *VentaCaida* sin cobros → la venta se anula → Caballos devuelve el caballo al plantel. Con cobros, se pregunta (las devoluciones quedan fuera de la V1). |
| **Registro eliminado** | Un owner elimina el acuerdo → *AcuerdoEliminado* → Gastos saca la marca "lo cubre" de sus gastos → Captura oculta los mensajes de origen [P-3]. |

---

## 5. Supuestos y preguntas abiertas

La primera versión de este documento dejó 20 preguntas abiertas. Se sumaron 3 sobre tiempo y fechas, y Santi decidió las 23 el **2026-11-04** (detalle y justificación en [anexo-a-decisiones.md](anexo-a-decisiones.md)). Se dejan a la vista, con su resolución, porque cada una era una ambigüedad real del documento funcional. Esas respuestas dejaron cuatro preguntas nuevas (P-24 a P-27), que Santi también decidió el mismo día.

### 5.1 Supuestos

| Id | Supuesto | Justificación |
|---|---|---|
| **S-0** | Los flujos "apertura de sobre", "intercambio completado" e "intercambio no concretado" de la consigna se interpretan como: apertura de un mensaje entrante, intercambio polista–patrón cobrado, y carga o acuerdo que no se concreta. | Los términos no existen en la KB ni en el polo; parecen venir de otra consigna. Se acordó con el equipo mapearlos en vez de ignorarlos (ver 4). |
| ~~S-1~~ | ~~En el grupo, el bot confirma con ✅ y solo escribe si duda.~~ **Reemplazado por P-1 y P-27.** | Un gasto o un ingreso se confirma siempre por escrito, por privado a quien lo cargó; en el grupo, solo ✅. |
| **S-2** | Gastos e Ingresos son **dos contextos** dentro de un mismo subdominio núcleo, con un núcleo compartido de dinero y conversión. | Decisión del equipo. Cada uno tiene su ciclo de vida (gasto vs acuerdo con pagos) y la única unión es el reintegro, que se resuelve con eventos. |
| **S-3** | El **libro de gastos no es un agregado**; los totales se derivan siempre. | La regla "todo total es la suma de los ítems visibles" se cumple por construcción y no hay invariante transaccional entre gastos. |
| **S-4** | El **estado del reintegro** es de Ingresos; Gastos solo guarda la marca "lo cubre X". | El modelo de datos lo pone en el gasto; tener el estado en los dos lados abre la puerta a que no coincidan. Una sola fuente de verdad. |
| **S-5** | Un registro que el bot **no** puede completar no entra a ningún contexto: queda en Captura como carga pendiente o **sin terminar** [P-10]. | "Ante la duda pregunta, nunca adivina" implica que no existe un gasto "sin destino" ni "sin categoría". |
| ~~S-6~~ | ~~El patrón es un objeto de valor identificado solo por nombre.~~ **Reemplazado por P-6.** | La contraparte pasa a tener identidad interna, sin ser usuario. |
| **S-7** | Un pago recibido en una moneda distinta a la del acuerdo se convierte a la del acuerdo con la cotización del día del pago. | La KB define cómo valuar en US$ lo cobrado en € pero no el caso de monedas cruzadas. |
| **S-8** | Un pago que haría superar lo acordado se aclara antes de registrarse. | Es el patrón "ante la duda pregunta" aplicado a cobros; puede ser un error de interpretación o un reintegro. |
| **S-9** | Un acuerdo está "Cobrado" solo si no quedan reintegros pendientes. | El ejemplo de Valle Alto ("Cobrado, flete reintegrado") sugiere que el estado mira ambas cosas. |
| **S-10** | Un gasto de Compra de caballos no puede marcarse como cubierto por un patrón. | Es inversión y no entra en el resultado; si un patrón pagara un caballo, cambiaría la propiedad, que está fuera de la V1 [P-13]. |
| **S-11** | Los "mañana" sin hora se resuelven a las 9:00 (recordatorios, postergaciones), en la hora local de quien recibe [P-21]. | Es lo que muestran los chats de ejemplo. |
| **S-12** | "Lucas" y "palo" siempre son pesos; "40 mil" toma la moneda del acuerdo al que se imputa; un número sin moneda en un gasto se aclara. | Glosario y chat de cobros. |
| ~~S-13~~ | ~~Los cuatro estados del caballo son exhaustivos.~~ **Reemplazado por P-12.** | Situación y lugar pasan a ser dos datos separados. |
| **S-14** | La compra de un caballo se modela como **dos registros** de un mismo mensaje: alta en Caballos y gasto en Gastos. | El chat de alta lo muestra así y mantiene cada regla en su contexto. |
| **S-16** | Como la confirmación de un gasto o un ingreso va por privado [P-27], el bot le escribe por privado también a quien está sumado **solo al grupo** (petiseros, veterinario), y las **dudas sobre plata** de un mensaje del grupo se preguntan por privado. | Es la consecuencia directa de P-27 y evita discutir montos en el grupo. Choca con «Cómo lo sumás: solo el grupo» de la invitación: a confirmar con Santi. |
| ~~S-17~~ | ~~Un reintegro vale en US$ lo mismo que el gasto que devuelve.~~ **Reemplazado por P-28.** | Santi: puede haber diferencias; se anota lo que se dice, textual, como gasto o como ingreso. |
| **S-18** | Los **días que alcanza** un insumo se truncan a días enteros (6,4 → 6). | Es lo que muestra el mockup en todos sus insumos (anexo C, sección 8). **Confirmado por Santi** (2026-11-04), a revisar con el MVP. |
| **S-19** | **Pagos que vienen** muestra los pagos fijos que vencen en los próximos **15 días**. | Con esa ventana, el ejemplo del mockup da exactamente sus 4 pagos y US$ 8.000. **Confirmado por Santi** (2026-11-04), a revisar con el MVP. |
| ~~S-20~~ | ~~Un lugar es **explícito** cuando el mensaje lo nombra («para el campo», «en Windsor») o nombra caballos que están todos en un mismo lugar. El lugar de quien manda el mensaje (Juanca vive en Windsor) **no** alcanza: sin otra señal, el gasto va a General. | Es la lectura literal de "a no ser que sea explícito" [P-29]. Si en la práctica deja demasiados gastos en General, se puede sumar el lugar del emisor como señal.~~ **Reemplazado por P-30** (calendario). | |
| **S-21** | Si el patrón devuelve **menos** de lo pendiente («me devolvió 8 mil del flete» sobre € 9.000), se anota lo dicho y el resto **queda pendiente**; un owner lo puede dar por cerrado desde la app. El bot no pregunta. | Combina "se anota lo que se dice, textual" [P-28] con "que no pregunte para cada registro" [P-29]. **Confirmado por Santi** (2026-11-04). |
| **S-22** | Las temporadas del calendario **no se superponen en fechas**. Si el polista va una semana a Chantilly en medio de Sotogrande, se cargan tres tramos. | La temporada es la estadía del polista y no puede estar en dos lugares a la vez; si se superponen, el calendario no sabe dónde está. A confirmar. |
| **S-23** | El **lugar fijo** de un miembro que viaja con el polista (Juanca, de Windsor a Sotogrande) lo actualiza un owner desde Equipo; hasta entonces, sus gastos sin lugar nombrado van a su lugar anterior. | Sin esto, la comida de los petiseros en Sotogrande quedaría en Windsor. A confirmar. |
| **S-24** | Si el modelo duda entre **carga y charla**, es charla: no se registra. | "El bot nunca carga una charla" es una regla explícita de Santi; un gasto que falta se recupera, uno inventado rompe la confianza en los totales. A confirmar (anexo G). |
| **S-25** | Un audio con **más de 4 registros** se confirma con un resumen en lista. | La KB pide "resumir y pedir confirmación" en audios largos sin decir desde cuántos. A confirmar (anexo G). |
| **S-15** | Las preguntas que van a owners (trabajo de proveedor, pago fijo, ingreso sin permiso) siguen yendo por privado aunque la regla general de P-1 sea responder al emisor. | Son decisiones previas de Santi que P-1 no menciona, y responder en el grupo una pregunta de plata contradice la privacidad de la plata. A confirmar en la próxima revisión. |

### 5.2 Preguntas resueltas (Santi, 2026-11-04)

| Id | Pregunta | Decisión | Qué cambió en el modelo |
|---|---|---|---|
| **P-1** | ¿A quién le pregunta el bot y cuándo responde? | Responde lo menos posible. Si tiene una duda, le pregunta a **quien mandó el mensaje**, sea quien sea. A quien registra un **gasto o un ingreso**, siempre le contesta qué entendió y qué cargó. El resto, solo ✅. | *Política de respuesta* en Captura; invariante 6 de `Carga`; destinatario de la Aclaración. |
| **P-2** | ¿Quién puede cargar plata? | Gastos: cualquier miembro. Ingresos: solo owners. Proveedores: nunca gastos. Configurable por persona. | Permisos de carga en `Membresia`, separados de lo que se ve. |
| **P-3** | ¿Un acuerdo puede caerse? | Sí: queda **Caído**, lo cobrado se mantiene. Además, **un owner puede eliminar cualquier registro**: desaparece de la app y de los totales, y su mensaje de origen queda oculto. | Estado Caído; eventos *AcuerdoCaido*, *VentaCaida* y de registro eliminado; `MensajeDeOrigen` oculto. |
| **P-4** | ¿Qué es una temporada? | La **estadía del polista en un lugar** durante un período; puede tener varios torneos, patrones e ingresos; en un año hay varias. | Nueva entidad `Temporada` (Ingresos, publicada a Gastos). |
| **P-5** | ¿Qué es el resultado por temporada? | Ingresos (acordados y ya cobrados) − gastos de ese destino. Ventas y compras de caballos aparte. | *Calculador de resultado de temporada* con dos resultados. |
| **P-5b** | ¿Pago a cuenta o reintegro? | A cuenta, salvo que el mensaje diga que es un reintegro; si el monto coincide exacto con un reintegro pendiente, se pregunta. | *Imputador de cobros*. |
| **P-6** | ¿Cómo se identifica al patrón? | Contraparte con nombre y apodos dentro de la organización, sin acceso. | `Contraparte` pasa a entidad de Ingresos. |
| **P-7** | ¿Cuándo sale del plantel un caballo vendido? | Al entregarlo (por defecto, el día de la venta). | Reacción de Caballos a *VentaDeCaballoAcordada*. |
| **P-8** | ¿"Lo pagué yo" y "queda a pagar"? | Es gasto y suma; se marca quién pagó o "a pagar"; se ve «Le debés a Pedro». Sin cuenta corriente con comercios en la V1. | Estado de pago en `Gasto`; *GastoSaldado*. |
| **P-9** | ¿Gasto por caballo? | **No.** El gasto se vincula a los caballos; en la ficha queda **qué se le hizo**, sin el monto. | Caballos vinculados sin monto; la ficha nunca muestra plata. |
| **P-10** | ¿Pregunta sin respuesta? | Se repregunta una vez; después queda **sin terminar** en la app y no suma. | Estado Sin terminar en `Carga`; *CargaSinTerminar*. |
| **P-11** | ¿Pendientes automáticos? | En la V1 solo existen los que pide alguien. | Sale el origen "automático" de Agenda. |
| **P-12** | ¿Estados del caballo? | Situación y lugar por separado; los filtros de la app se mantienen. | Objeto de valor Situación. |
| **P-13** | ¿Caballos que no son del polista? | Fuera de la V1: todos son del polista. | — |
| **P-14** | ¿Cotización y redondeo? | Del día del gasto (feriado: último hábil); corregible por un owner; US$ redondeado a entero al registrar. | `Conversion`; *Conversor a US$*. |
| **P-15** | ¿Si falla la fuente del blue? | Última cotización de hasta 3 días, avisada; si no hay, conversión pendiente con «≈». Nunca se pregunta. | Estado Pendiente de `Conversion`. |
| **P-16** | ¿Varios mensajes, una carga? | Mismo emisor y chat, hasta 5 minutos y antes de confirmar. | Invariante 10 de `Carga`. |
| **P-17** | ¿Consultas de plata en el grupo? | Nunca se contestan ahí; al owner, por privado. | *Respondedor de consultas*. |
| **P-18** | ¿Accesos parciales? | Solo mirar; solo sus caballos; sin vencimiento en la V1. | Invariantes de `Membresia`. |
| **P-19** | ¿Manager vs owner? | Rol y permiso van por separado; siempre al menos un owner. | `Membresia`, `Organizacion`. |
| **P-20** | ¿Moneda de referencia? | US$ para todas en la V1. | `Organizacion`. |
| **P-21** | ¿Huso horario? | Por persona; por defecto, el de su lugar; los avisos salen en la hora local de quien los recibe. | Objeto de valor Huso horario; *Planificador de avisos*. |
| **P-22** | ¿Fecha del gasto? | La que dice el mensaje; si no, el día local del emisor; a más de 30 días se confirma. | Objeto de valor Fecha del gasto. |
| **P-23** | ¿Consumo real de stock? | Los conteos solo sugieren el ajuste; un owner lo acepta. | *Calculador de días que alcanza*. |

### 5.3 Preguntas de la segunda vuelta (Santi, 2026-11-04)

| Id | Pregunta | Decisión | Qué cambió en el modelo |
|---|---|---|---|
| **P-24** | ¿Una temporada puede tener más de un lugar? | Sí, uno o más. | `Temporada` con uno o más lugares. |
| **P-25** | ¿Qué pasa con los gastos de un lugar fuera de las fechas de su temporada? | Quedan asociados a ese **destino**, no a la temporada. La temporada es el tiempo en que el polista estuvo ahí; durante el resto del año hay gastos de ese destino aunque él esté en otro lugar. | *Calculador de resultado de temporada*: solo gastos dentro de las fechas. |
| **P-26** | ¿Quién puede eliminar? | Quien lo cargó (lo suyo) y los owners (cualquier registro). | Permiso en `Membresia`; invariante 6 de `Gasto`. |
| **P-27** | ¿La confirmación con monto de un gasto mandado en el grupo va en el grupo? | No: por privado a quien lo cargó; en el grupo, solo ✅. | *Política de respuesta*; S-16. |

### 5.3b Tercera vuelta (Santi, 2026-11-04)

| Id | Pregunta | Decisión | Qué cambió en el modelo |
|---|---|---|---|
| **P-28** | Un reintegro cobrado otro día, con otra cotización, ¿vale lo mismo que el gasto? | **No necesariamente: puede haber diferencias.** Se anota lo que se dice, textual (monto y moneda del mensaje), como gasto o como ingreso, y se valúa con la cotización de su propio día. | Reintegro con monto dicho y su valor en US$ al día del cobro; reemplaza S-17. |
| **P-29** | ¿Todo gasto tiene un lugar? | **No.** Hay gastos **generales**, sin temporada ni destino. Si el mensaje no dice el lugar de forma explícita, el gasto va a General **sin preguntar** («que no le pregunte para cada registro porque se vuelve engorroso»); después, en la app, un owner lo puede asociar a una temporada. | `Destino` = lugar o General; temporada asociada a mano; el bot deja de preguntar el lugar; S-20. |

### 5.3c Cuarta vuelta (Santi, 2026-11-04)

| Id | Pregunta | Decisión | Qué cambió en el modelo |
|---|---|---|---|
| **P-30** | ¿Cuándo es "explícito" el lugar de un gasto? | Idea de Santi: un **calendario** en la app con las fechas en que el polista va a estar en cada lugar. Con eso, un gasto que carga un owner va adonde está el polista ese día, salvo que el mensaje nombre otro destino. El calendario aplica solo a lo que cargan los owners; el resto usa el lugar fijo de quien carga. Con varios lugares, va al **lugar principal**. | Temporada con lugar principal; servicio *Resolutor de destino*; reemplaza S-20. |
| **S-21** | ¿Reintegro parcial? | Confirmado: el resto queda pendiente. | — |

### 5.4 Preguntas abiertas

No quedan preguntas abiertas que bloqueen el modelo. Quedan para validar:

| Id | Pregunta | Qué parte del modelo depende de la respuesta |
|---|---|---|
| **S-15, S-16, S-22 a S-25** | Confirmar con Santi que las temporadas no se superponen (S-22), cómo se actualiza el lugar de quien viaja (S-23), las dos reglas del bot del anexo G (S-24, S-25) y los dos supuestos de privacidad: las preguntas a owners van siempre por privado, y el bot escribe por privado a quien está sumado solo al grupo. | *Política de respuesta*; invitación «Cómo lo sumás». |
| **Validación** | La taxonomía de gastos, los estados del caballo y el glosario salen del mockup y del entorno de Santi; siguen marcados como [HIPÓTESIS] en la KB hasta las entrevistas con polistas. | Lenguaje ubicuo (sección 1); `Clasificación`; Situación del caballo. |
