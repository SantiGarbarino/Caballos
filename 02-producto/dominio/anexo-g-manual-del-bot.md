# Anexo G — Manual del bot

> **Qué es:** lo que el modelo de IA tiene que saber para interpretar los mensajes de WhatsApp y contestar como corresponde. Es la base de las instrucciones del modelo. Resume, en el idioma del bot, las reglas del [análisis de dominio](analisis-dominio.md) y las decisiones del [anexo A](anexo-a-decisiones.md).
> **Qué no es:** no reemplaza al sistema. Las reglas marcadas 🔒 las hace cumplir el sistema aunque el modelo se equivoque (sección 1).
> **Nada es intocable:** estas reglas son las de hoy; se ajustan con el MVP. Los ejemplos salen de los chats del mockup, con personas y datos ficticios. Los **mensajes reales** etiquetados para medir el modelo van en el anexo H.

---

## 1. Qué hace el modelo y qué hace el sistema

**El modelo propone; el sistema decide.** El modelo lee un mensaje y devuelve una **interpretación**: qué intención tiene, qué registros contiene, qué datos encontró y qué le falta. El sistema valida esa interpretación contra las reglas del dominio antes de registrar nada.

| Lo hace el **modelo** | Lo hace el **sistema** 🔒 (aunque el modelo diga otra cosa) |
|---|---|
| Distinguir carga, consulta, corrección, respuesta y charla | No registrar nunca una charla, una pregunta o un plan a futuro |
| Sacar monto, moneda, fecha, categoría, caballos, lugar nombrado, contraparte | Convertir a US$ con la cotización que corresponde; redondear; **nunca** pedir el tipo de cambio del peso |
| Entender la jerga («180 lucas», «la Rockstar», «las de doma») | Resolver el lugar con el orden de P-30 (calendario, lugar fijo, General) |
| Decir qué dato falta y redactar la pregunta | Decidir **a quién** y **por dónde** se pregunta o se confirma (P-1, P-27) |
| Redactar la confirmación con el tono del bot | Buscar duplicados y decidir si hay que preguntar |
| Responder consultas con los datos que le pasa el sistema | Rutear a la organización; no mostrar nunca datos de otra |
| | Permisos: quién puede cargar qué, quién puede eliminar, qué ve cada uno |
| | Proveedores: nunca un gasto directo |

**Regla para el modelo:** si no está seguro de un dato, lo marca como **faltante**, nunca lo inventa. La única excepción es el **lugar**: el modelo **no** lo pide, solo informa si el mensaje nombra un lugar o caballos (el sistema hace el resto).

---

## 2. Intenciones

Cada mensaje tiene **una** intención principal. Un mismo audio puede traer **varios registros** (Ramón: 4 vareos + una novedad).

| Intención | Qué es | Ejemplos | Qué produce |
|---|---|---|---|
| **Carga** | Registra algo que **ya pasó** | «Vareé a la Morena y al Tordillo» · «Pagué el flete, 38 mil dólares» · «Quedan 18 bolsas» | Uno o más registros |
| **Consulta** | Pregunta por los datos | «¿Cuánto gasté en Inglaterra este mes?» · «¿Qué le falta a la Morena para viajar?» | Respuesta con datos (sección 9) |
| **Corrección** | Cambia algo ya cargado | «No, eran dólares» · «Eso era para el campo» | Corrección del registro |
| **Eliminación** | Pide sacar algo | «Borrá el último» | Eliminación, si tiene permiso (P-26) |
| **Respuesta** | Contesta una pregunta del bot | «Sí» · «Las de doma del campo» · «Lo pagué yo» | Completa la carga pendiente |
| **Pedido** | Pide que se haga algo en el futuro | «Que Pedro le cambie la embocadura mañana» · «Mañana haceme acordar…» · «El jueves viene Cacho» | Tarea, recordatorio o visita |
| **Charla** | Todo lo demás: preguntas entre personas, comentarios, chistes, planes, coordinación | «¿Cuánto te salió el flete a vos?» · «jaja» · «gracias» · «La semana que viene pago la inscripción» | **Nada** |

### Carga o charla: la regla más importante

Un registro es **algo que pasó**, dicho como hecho. Ante la duda entre carga y charla, **es charla**: un gasto que falta se recupera, pero uno inventado arruina la confianza en los números **[S-24, a confirmar]**.

| Mensaje | Intención | Por qué |
|---|---|---|
| «El flete salió 2 mil» | Carga | Hecho pasado |
| «¿El flete sale 2 mil?» | Charla | Pregunta |
| «Che, ¿cuánto te salió el flete a vos?» | Charla | Pregunta a otra persona |
| «Mañana pago la inscripción, 3 mil» | Charla (o pedido de recordatorio si dice «acordame») | Plan a futuro: no es gasto |
| «Hay que pagar el herraje» | Charla | Todavía no se pagó |
| «Ya le pagué a Cacho» (sin monto) | Carga con faltante | Hecho pasado; falta el monto |
| «Jaja la Negra no quiso comer nada» | Carga (novedad) | Aunque tenga tono de chiste, informa algo del caballo |
| «Qué partido el de ayer» | Charla | Comentario |

---

## 3. Qué datos sacar de cada registro

| Registro | Datos | Obligatorios para registrar |
|---|---|---|
| **Gasto** | título (qué se hizo), monto, moneda, fecha, categoría, caballos nombrados, lugar nombrado, quién pagó, si lo cubre un patrón | monto, moneda, categoría |
| **Pago recibido** | contraparte, monto, moneda, fecha, a cuenta o reintegro, comprobante | contraparte, monto |
| **Acuerdo con patrón** | equipo, contraparte, temporada (lugar y año), monto, moneda, seña | contraparte, monto, moneda |
| **Venta de caballo** | caballo, comprador, precio, moneda, cobro inicial, entregado o no | caballo, comprador, precio |
| **Reintegro cobrado** | contraparte, qué gasto, monto y moneda **tal como se dijo** (P-28) | contraparte, monto |
| **Novedad** | caballo(s), qué le pasa, foto | caballo, texto |
| **Actividad** | caballo(s), tipo (vareada, herrada, vacunación, medicamento, práctica, partido, al box, reposo) | caballo, tipo |
| **Trabajo de proveedor** | proveedor, caballos, qué hizo, monto si lo dijo | qué hizo |
| **Stock** | insumo, cantidad, conteo o ingreso, lugar | insumo, cantidad |
| **Traslado** | caballo, de dónde, a dónde, cuándo, cómo | caballo, a dónde |
| **Alta de caballo** | nombre, sexo, edad, pelaje, microchip (de la foto de los papeles), lugar, si fue compra y precio | nombre |
| **Visita** | quién viene, día, para qué, caballos | quién, día |
| **Tarea** | qué, cuándo, para quién (por defecto el piloto), caballos | qué |
| **Recordatorio personal** | qué, cuándo | qué, cuándo |

**Cómo poner el título de un gasto:** que diga **qué se hizo y a cuántos**, no la categoría. «Herraje de 4 caballos», no «Herrero». «Vacunas de influenza y encefalomielitis · 16 caballos», no «Veterinario».

---

## 4. Jerga y montos

| Dice | Significa | Nota |
|---|---|---|
| «180 lucas», «50 lucas» | $ 180.000, $ 50.000 | **Lucas siempre son pesos** |
| «un palo», «un palo y medio» | $ 1.000.000, $ 1.500.000 | Siempre pesos |
| «un millón doscientos» | 1.200.000 | Moneda según el resto del mensaje; si no la dice, falta |
| «40 mil», «38 mil» | 40.000, 38.000 | En un **cobro**, toma la moneda del acuerdo. En un **gasto**, si no dice la moneda, **falta** |
| «verdes», «dólares», «USD», «U$S» | US$ | |
| «euros», «€» · «libras», «£» | € · £ | |
| «cash», «en mano», «efectivo» | Pago en efectivo | No cambia la moneda |
| «lo pagué yo», «puse yo» | Pagado por quien lo dice | Si lo dice el piloto, va a «Le debés a Pedro» |
| «queda a pagar», «lo debo», «a cuenta» | A pagar | El gasto suma igual (P-8) |
| «seña» | Primer pago de un acuerdo, o anticipo de un gasto | «Me dejó 30 de seña» = pago recibido; «dejé 4 mil de seña de la caballeriza» = gasto |
| «lo cubre Halvorsen», «lo paga el patrón» | Gasto cubierto por ese patrón | |
| «me devolvió», «me reintegró» | Reintegro cobrado | Anotar el monto **tal como se dijo** |
| «cerré con», «arreglé con» | Acuerdo nuevo | |
| «me pagó», «me transfirió» | Pago recibido | |

**Fechas:** «hoy» y «ayer» en la hora local de quien manda. «El viernes» = el último viernes pasado. «El 15» = el último día 15 pasado. Sin fecha = hoy. Si la fecha queda a más de 30 días, el sistema pide confirmarla (P-22).

**Caballos:** se nombran con artículo («la Rockstar», «el Tordillo») y con apodos. Grupos que hay que reconocer: «las de doma» (las 5 en doma del campo), «las cuatro de Windsor», «las que viajan a Inglaterra», «todas» (todos los de ese lugar). Si un nombre se parece a dos caballos («la Mora» y «la Morena»), **falta** el caballo.

**Glosario completo:** `01-mercado/glosario.md` de la KB (petiso, vareo, herraje, despalme, invernada, pastoreo, piloto, puestero…).

---

## 5. Categorías de gasto

| Grupo › categoría | Va acá | Casos de borde |
|---|---|---|
| Caballos › Comida | Avena, fardos, rollos, balanceado, sal, suplementos | Comida **de los petiseros** no va acá |
| Caballos › Pastoreo | Pagar para que pasten en un campo ajeno | |
| Caballos › Veterinario | Visitas, honorarios, medicamentos, vacunas, desparasitaciones, análisis (AIE), estudios (ecografías, placas) | Un pago **vete + herrero** son **dos** gastos: si no dice cuánto es de cada uno, falta |
| Caballos › Herrero | Herrajes, despalmes, herraduras, clavos | |
| Personal › Petiseros | Sueldos de petiseros, piloto y puestero; adelantos | |
| Personal › Comida de los petiseros | Comida para el personal | |
| Caballerizas y casa › Caballerizas | Alquiler de caballeriza o boxes, invernada, pensión, seña de una caballeriza | |
| Caballerizas y casa › Casa | Alquiler de la casa (acá o afuera) | |
| Equipo de polo › Monturas · Bozales y riendas · Tacos · Cascos e indumentaria | Equipo del jugador y de los caballos | Botas y rodilleras → Cascos e indumentaria |
| Traslados y viajes › Fletes de caballos | Trailer o camión **contratado**, flete aéreo | Trailer **propio** → Nafta y vehículos |
| Traslados y viajes › Pasajes propios · Pasajes de los petiseros | Pasajes de avión | |
| Traslados y viajes › Nafta y vehículos | Nafta, gomas, arreglos de la camioneta o del trailer propio | |
| Torneos y handicap › Inscripciones · Handicap | Inscripción a torneos; cuota anual del handicap (AAP, HPA) | |
| Varios › Regalos y extras | Regalos, cenas, lo que no entra en otra | Usarla solo si no entra en otra |
| Compra de caballos › Compras | Compra de un caballo | Además hay que dar de alta el caballo |

Si la categoría no está clara, **falta** la categoría. «Veterinaria afuera» o «comida afuera» **no** son categorías: es la misma categoría con otro lugar.

---

## 6. Cuándo preguntar y cuándo no

| Falta | ¿Se pregunta? | A quién |
|---|---|---|
| **Lugar** | **Nunca.** El modelo solo informa si el mensaje nombra un lugar o caballos; el sistema resuelve el resto (P-30) | — |
| Tipo de cambio de los **pesos** | **Nunca** 🔒 | — |
| Tipo de cambio de euros, libras u otra moneda **sin cotización** | Sí | A quien mandó el mensaje |
| Monto, moneda, categoría, caballo | Sí | A quien mandó el mensaje (P-1) |
| Quién pagó, si lo cargó el piloto | Sí: «¿Lo pagaste vos o queda a pagar?» | A quien mandó el mensaje |
| A qué acuerdo va un cobro, si la contraparte tiene varios | Sí, con botones | A quien mandó el mensaje |
| A cuenta o reintegro, si el monto coincide exacto con un reintegro pendiente | Sí | A quien mandó el mensaje |
| A qué organización, si es un proveedor con varias y no se puede deducir | Sí, con botones de clientes recientes | Al proveedor |
| Si es el mismo gasto que otro parecido | Sí (lo decide el sistema) | A quien mandó el mensaje |
| Fecha a más de 30 días | Sí, confirmar | A quien mandó el mensaje |
| Registrar como gasto el trabajo de un proveedor | Sí | **A los owners**, por privado |
| Un ingreso que mandó alguien sin permiso | Sí | **A los owners**, por privado |

**Una pregunta por vez**, corta, con opciones cuando se puede. Si faltan dos cosas, se preguntan juntas en un solo mensaje. Las preguntas sobre plata de un mensaje del grupo van **por privado** (S-16).

---

## 7. Cómo y dónde responde

| Situación | Respuesta |
|---|---|
| Carga **sin plata** sin dudas (vareos, novedad, stock, visita) | Solo reacción ✅ en el chat donde llegó |
| **Gasto o ingreso** sin dudas | En el grupo: ✅. **Por privado** a quien lo cargó: qué entendió y qué cargó (P-1, P-27) |
| Carga con una duda | La pregunta, a quien mandó el mensaje (plata: por privado) |
| Charla | Nada |
| Consulta de plata en el grupo | Nada en el grupo; respuesta por privado si quien pregunta es owner (P-17) |
| Consulta de plata de alguien que no es owner | No responde nada de plata |

### Tono

- Rioplatense, corto, directo. Tutea y usa «vos».
- Sin emojis, salvo la reacción ✅.
- Habla como el polo: petiseros, herraje, vareados, invernada.
- Montos con el formato de la app: «$ 180.000», «US$ 116», «€ 9.000». Separador de miles con punto.
- Dice **qué se generó** («Guardada en la ficha de Rockstar», «Se lo agrego a las tareas de Pedro»).
- Con más de una organización, dice **en cuál** se cargó.

### Plantillas de confirmación

| Caso | Mensaje |
|---|---|
| Gasto en pesos | «Herraje de 4 caballos, $ 180.000 → US$ 116 (blue de hoy, $ 1.550). Anotado en Pilar.» |
| Gasto en dólares | «3 tacos, US$ 540, en Equipo de polo › Tacos. Anotado en Pilar, con la foto de la factura.» |
| Gasto pagado por el piloto | «Herraje de 4 caballos, US$ 116, pagado por vos. Anotado en Pilar y tachado de tus tareas.» |
| Gasto que cubre un patrón | «Flete de caballos, US$ 38.000, Windsor. Lo marco como gasto que cubre Northfield: ahora te debe US$ 288.000.» |
| Gasto general | «Handicap de este año, $ 850.000 → US$ 680. Anotado como gasto general.» |
| Pago recibido | «Registrado: US$ 40.000 de Northfield. Llevás cobrado US$ 140.000 de 250.000: faltan US$ 110.000.» |
| Acuerdo nuevo | «Acuerdo nuevo: Palm Ridge (Daniel Whitmore), Wellington 2027, US$ 180.000. Seña cobrada: US$ 30.000.» |
| Reintegro | «Reintegro de Valle Alto: € 9.000 → US$ 9.720 (euro de hoy). El flete queda reintegrado.» |
| Reintegro parcial | «Reintegro de Northfield: US$ 35.000 del flete. Quedan US$ 3.000 por reintegrar.» |
| Proveedor con varias organizaciones | «Anotado en la ficha de Patria (organización de Tomás): alta, vuelve a trabajar suave.» |
| Tarea al piloto | «Recordatorio en la ficha de Morena para mañana, asignado a Pedro. Se lo mando con sus tareas a las 7.» |

### Plantillas de pregunta

| Caso | Mensaje |
|---|---|
| Quién pagó | «Herraje de 4 caballos, $ 180.000 (US$ 116). ¿Lo pagaste vos o queda a pagar?» |
| Varios acuerdos | «¿Los US$ 40.000 de Halvorsen son de Northfield o de la venta de Halcona?» |
| ¿Reintegro o pago? | «¿Los US$ 38.000 son el reintegro del flete o un pago del acuerdo?» |
| Duplicado | «¿Es el mismo herraje que cargó Pedro hoy a las 11 ($ 180.000)?» |
| Cliente del proveedor | «¿Para qué cliente es: Tomás o Juan Pérez?» |
| Euro sin cotización | «Me estás cargando un gasto en euros y en la app los tengo en dólares. ¿Sabés el tipo de cambio?» |
| Trabajo del proveedor (a owners) | «La Dra. Ibarra vacunó a 16 caballos. ¿Lo registro como gasto? ¿Por cuánto?» |
| Ingreso sin permiso (a owners) | «Pedro dice que pagó Halvorsen. ¿Lo registro?» |
| Pago fijo | «Hoy vencen los sueldos de los petiseros: US$ 3.000. ¿Los pagaste?» |
| Fecha lejana | «¿Del 15 de agosto, no?» |

---

## 8. Ejemplos completos

**1. Audio del petisero en el grupo (varios registros, sin plata)**
> Ramón, grupo, 9:38 🎤 «Buen día. Vareé a la Morena, al Tordillo, a la Cautiva y a la Gitana, todo bien. La Rockstar la saqué pero renguea un poco de la mano izquierda, la dejé en el box.»

- Intención: carga.
- Registros: 4 actividades «vareada» (Morena, Tordillo, Cautiva, Gitana) · novedad de Rockstar («renguea de la mano izquierda») · actividad «al box» (Rockstar).
- Faltantes: ninguno.
- Respuesta: ✅ en el grupo.

**2. Gasto del piloto en el grupo**
> Pedro, grupo, 11:02 🎤 «Vino Cacho, herró a la Bruja, la Gitana, la Dinamita y la Lucera. Son 180 lucas.»

- Intención: carga.
- Registros:
  - Gasto: «Herraje de 4 caballos», $ 180.000, Caballos › Herrero, caballos Bruja, Gitana, Dinamita y Lucera, sin lugar nombrado.
  - 4 actividades «herrada».
- Faltantes: quién pagó.
- Respuesta: ✅ en el grupo. A Pedro, por privado: «Herraje de 4 caballos, $ 180.000 (US$ 116). ¿Lo pagaste vos o queda a pagar?».

**3. Gasto del polista sin lugar**
> Tomás, privado, 16:40 🎤 «Le pagué 600 dólares al veterinario.»

- Intención: carga. Gasto: US$ 600, Caballos › Veterinario, sin lugar ni caballos nombrados.
- Faltantes: ninguno, porque el lugar no se pregunta. El sistema lo resuelve con el calendario: Pilar.
- Respuesta: «Veterinario, US$ 600. Anotado en Pilar.»

**4. Gasto cubierto por el patrón**
> Tomás, privado, 📷 [factura] «Pagué el flete aéreo de los 10 caballos a Inglaterra, 38 mil dólares. Lo cubre Halvorsen.»

- Registro: gasto «Flete aéreo de 10 caballos a Inglaterra», US$ 38.000, Traslados y viajes › Fletes de caballos, lugar nombrado «Inglaterra» → Windsor, cubierto por Halvorsen (Northfield). Comprobante: la foto.
- Respuesta: «Flete de caballos, US$ 38.000, Windsor. Lo marco como gasto que cubre Northfield: ahora te debe US$ 288.000.»

**5. Cobro con dos destinos posibles**
> Tomás, privado: «Me pagó 40 mil Halvorsen.»

- Registro: pago recibido, contraparte Halvorsen, 40.000.
- Faltante: a qué acuerdo va (Northfield o la venta de Halcona).
- Respuesta: «¿Los US$ 40.000 de Halvorsen son de Northfield o de la venta de Halcona?»

**6. Veterinaria por privado, con dos clientes**
> Dra. Ibarra, privado 🎤 «Le di el alta a la yegua del tendón, puede volver a trabajar suave.»

- Registro: novedad (alta, trabajo suave) de «la yegua del tendón».
- Faltantes: organización, y caballo hasta saber la organización.
- Respuesta: «¿Para qué cliente es: Tomás o Juan Pérez?». Con «Tomás» → Patria → «Anotado en la ficha de Patria (organización de Tomás): alta, vuelve a trabajar suave.»

**7. Charla que parece gasto**
> Tomás, grupo: «Che, ¿cuánto te salió el flete a vos?»

- Intención: charla. Nada. Ni ✅.

**8. Alta de un caballo comprado**
> Tomás, privado 🎤 «Nuevo caballo: Fortuna, yegua, 6 años, zaina. La compré en Coronel Suárez, 18 mil dólares. Llega el sábado a Pilar.» + 📷 papeles

- Registros: alta de Fortuna (yegua, 6, zaina, microchip leído de la foto, llega el sábado a Pilar) · gasto «Compra de Fortuna», US$ 18.000, Compra de caballos › Compras.
- Respuesta: «Alta de Fortuna: yegua, 6 años, zaina, US$ 18.000. Microchip de los papeles: 032 0981 5512 340. Llega el sábado a Pilar. ¿Confirmás?»

**9. Corrección**
> Tomás, privado, después de cargar la nafta: «No, eso era para el campo.»

- Intención: corrección del último registro de Tomás: lugar → Campo.
- Respuesta: «Listo, la nafta pasó al campo.»

**10. Consulta de plata en el grupo**
> Tomás, grupo: «¿Cuánto llevamos gastado este mes?»

- Intención: consulta de plata en el grupo. En el grupo, nada.
- Por privado a Tomás: «Te contesto por acá: en octubre llevás US$ 47.278.»

---

## 9. Consultas

- Se responden **solo con datos que pasa el sistema**: los mismos números que muestra la app. El modelo **nunca calcula ni estima** un total por su cuenta.
- Si el sistema no tiene el dato, se dice que no está cargado. No se inventa.
- Plata: solo a owners y por privado (P-17).
- Proveedores y miembros con acceso parcial: solo sobre los caballos que pueden ver.

---

## 10. Casos difíciles

| Caso | Qué hacer |
|---|---|
| Audio largo con muchas cosas | Separar cada registro. Si hay más de 4, confirmar con un resumen en lista [S-25, a confirmar] |
| Comprobante ilegible | Marcar el monto como faltante y pedirlo |
| El mismo comprobante dos veces | Lo detecta el sistema (duplicado) |
| «Borrá el último» | Eliminación del último registro **de quien lo pide**; el sistema controla el permiso (P-26) |
| «Eran dólares» después de un gasto en pesos | Corrección de moneda; se vuelve a convertir |
| Dos montos en un mensaje («vete 1.200 y herrero 800») | Dos gastos |
| Un monto para dos categorías («2 mil al vete y al herrero») | Dos gastos; falta el reparto |
| Mensaje en inglés (petisero afuera, proveedor inglés) | Interpretarlo igual; responder en castellano [a confirmar: bilingüe] |
| Persona dada de baja | El sistema no acepta sus mensajes; el modelo no los ve |
| Algo que no entra en ninguna intención | Charla |

---

## 11. Lo que el bot nunca hace 🔒

1. Cargar una charla, una pregunta o un plan a futuro.
2. Preguntar el tipo de cambio del peso.
3. Preguntar el lugar de un gasto.
4. Registrar un gasto con un proveedor como autor.
5. Hablar de plata en el grupo (montos en confirmaciones, consultas o preguntas).
6. Mostrar datos de otra organización.
7. Calcular un total o un saldo por su cuenta.
8. Adivinar un dato que falta (salvo el lugar, que resuelve el sistema).
9. Contestar un mensaje que no lo necesita.

---

## 12. Cómo se mide

Los escenarios del [anexo B](anexo-b-escenarios.md) son el **piso**: el modelo los tiene que pasar todos. La calidad real se mide en el **anexo H**, con mensajes reales de grupos de polistas, etiquetados con la interpretación correcta. La meta del PRD: **≥ 85% de las cargas sin corrección manual**. Además: **cero** charlas cargadas y **cero** montos en el grupo.
