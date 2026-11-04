# Anexo B — Escenarios de aceptación

> **Qué es:** casos concretos en formato **Dado / Cuando / Entonces** para cada regla del [análisis de dominio](analisis-dominio.md) y de las decisiones del [anexo A](anexo-a-decisiones.md). Cada escenario tiene un único resultado correcto. Mauro los convierte en tests; para el modelo de IA son el piso de lo que tiene que hacer bien.
> **Nada es intocable:** los resultados esperados siguen las reglas decididas hoy; si una regla cambia con el MVP, se cambian sus escenarios.
> **Punto de partida:** salvo que se diga otra cosa, **"dado el dataset C"** = la organización de Tomás del [anexo C](anexo-c-dataset.md), con hoy **jueves 22/10/2026** y blue $ 1.550 (euro US$ 1,09). Los gastos se citan por su id (G138 = herraje de 4 caballos del 22/10).
> **Lectura de la columna "Entonces":** lo que **tiene que** pasar. Si dice "no", el sistema **no debe** hacerlo aunque el modelo de IA lo proponga. Las reglas marcadas con 🔒 las hace cumplir el sistema, no el modelo.

**Personas del dataset:** Tomás (polista, owner) · Nacho (manager, owner) · Pedro (piloto) · Ramón y Lucho (petiseros, Pilar) · Juanca (petisero, Windsor) · Don Aníbal (puestero, campo) · Sofía (familiar o asistente) · Dra. Ibarra (veterinaria, también trabaja para Juan Pérez) · Cacho (herrero).

---

## 1. Conversión, redondeo y fechas

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-01 | Hoy, blue $ 1.550 | Pedro manda «Son 180 lucas el herraje» | Monto original $ 180.000; US$ **116** (180.000 ÷ 1.550 = 116,13, redondeado); cotización guardada: valor, fecha 22/10, fuente | P-14 🔒 |
| B-02 | Hoy | Tomás: «Cargué nafta, 85 lucas» | US$ **55**. El bot **no pregunta** el tipo de cambio | W2 🔒 |
| B-03 | Tres gastos de $ 179.180 el mismo día | Se miran los totales del día | Cada uno: US$ 116 (115,6 redondeado); total del día US$ **348** (= 116 × 3, no 347) | P-14 🔒 |
| B-04 | Sábado 17/10 | Pedro carga «comida de los petiseros, 160 mil» ese día | Cotización del viernes 16/10 (G130) | P-14 |
| B-05 | Sábado 1/8, euro de julio 1,07 y de agosto 1,08 | Tomás carga «caballeriza de Sotogrande, 5 mil euros» | Usa el euro del viernes 31/7 (1,07) → US$ **5.350** (G088) | P-14 |
| B-06 | Hoy es jueves 22/10 | Tomás: «El viernes pagué 2 mil dólares de la montura» | Fecha del gasto: **viernes 16/10** (el último viernes pasado), no el 23 | P-22 |
| B-07 | Hoy | Tomás: «El 15 de agosto pagué 900 euros al vete» | Fecha a más de 30 días → el bot confirma «¿Del 15 de agosto, no?» antes de registrar; cotización del 14/8 (viernes) | P-22, P-14 |
| B-08 | Tomás está en Sotogrande (huso de España) y son las 00:30 del 23/10 allá | Manda «hoy pagué el pastoreo, 1.800 euros» | Fecha del gasto **23/10** (día local de Tomás), aunque en Argentina sean las 19:30 del 22 | P-21, P-22 |
| B-09 | La fuente del blue no responde desde hace 2 días | Pedro carga «$ 280.000 de flete» | Usa la última cotización disponible; letra chica «al blue del 20/10 (última disponible)». **No pregunta** | P-15 🔒 |
| B-10 | La fuente del blue no responde desde hace 4 días | Pedro carga «$ 280.000 de flete» | Gasto registrado con conversión **pendiente**; se ve «≈ US$ 181» y suma con «≈»; se completa sola cuando vuelve la fuente. **No pregunta** | P-15 🔒 |
| B-11 | No hay fuente para la libra | Juanca: «pagué 300 libras de pastoreo» | El bot pregunta el tipo de cambio de la libra (solo para monedas que no son el peso) | W1b |
| B-12 | G135 registrado con blue 1.550 | Un owner corrige la cotización a 1.600 desde la app | US$ pasa a 200; fuente «corregida por Nacho»; queda el antes y el después | P-14 |
| B-13 | G138 registrado | Al día siguiente el blue sube a 1.600 | G138 **sigue** en US$ 116: la conversión no se recalcula sola | Invariante 3 de `Gasto` 🔒 |

## 2. Clasificación, lugar y caballos

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-14 | Hoy (22/10, Tomás en la temporada Argentina 2026, lugar principal Pilar) | Tomás: «Le pagué 600 dólares al veterinario» | **No pregunta el lugar.** Registra US$ 600, Caballos › Veterinario, destino **Pilar** (por el calendario), y le confirma por privado qué cargó. Si era del campo, Tomás lo corrige | P-30 |
| B-15 | Hoy | Tomás: «Le pagué 600 dólares al veterinario por las de doma del campo» | Lugar **explícito** → destino **Campo** (G140) | P-29, S-20 |
| B-16 | Hoy, Argentina 2026 | Tomás manda la foto de la factura de 3 tacos, US$ 540, sin decir el lugar | **No pregunta**: Equipo de polo › Tacos, destino **Pilar** (calendario), con la foto como comprobante (G136) | P-30 |
| B-17 | Tomás está en Sotogrande | «Mandé 2 mil dólares para el campo» | Lugar **Campo**, no Sotogrande | Destino |
| B-18 | Hoy | Tomás: «Pagué 2 mil al vete y al herrero por las de doma» | **Dos** gastos: Veterinario y Herrero. Si no dice cómo se reparte, pregunta cuánto es de cada uno | Un gasto, una categoría 🔒 |
| B-19 | Hoy | Pedro: «Vino Cacho, herró a la Bruja, la Gitana, la Dinamita y la Lucera. Son 180 lucas» | **Un** gasto (Herrero, **Pilar**, porque los 4 caballos están en Pilar [S-20], US$ 116) vinculado a los 4 caballos **sin repartir el monto**; **cuatro** eventos «herrada» en las fichas | P-9 |
| B-20 | B-19 | Alguien con acceso parcial a Caballos abre la ficha de Bruja | Ve «Herrada · 22/10 · Cacho»; **no ve** ningún monto | P-9, P-18 🔒 |
| B-21 | Hoy | Tomás: «Compré a Fortuna, 18 mil dólares, llega el sábado a Pilar» | Alta de Fortuna en Caballos **y** gasto Compra de caballos US$ 18.000 (G137); el gasto suma en el total de Gastos y **no** en el resultado por temporada | S-14, P-5 |
| B-22 | Hoy | Tomás: «Las gomas del trailer, 600 mil» | Traslados y viajes › Nafta y vehículos (trailer propio) | Taxonomía |
| B-23 | Hoy | Tomás: «Pagué el trailer de Gómez para llevar 4 al campo, 280 mil» | Traslados y viajes › **Fletes de caballos** (trailer contratado) | Taxonomía |

## 3. Cuándo y cómo responde el bot

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-24 | Grupo de la organización | Ramón manda un audio con 4 vareos sin dudas | Solo reacción ✅; **ningún** mensaje escrito | P-1 🔒 |
| B-25 | Grupo de la organización | Pedro manda «son 180 lucas el herraje» **en el grupo**, sin dudas | En el grupo: solo ✅. **Por privado a Pedro:** «Herraje de 4 caballos, $ 180.000 → US$ 116 (blue de hoy). Anotado en Pilar» | P-1, P-27 🔒 |
| B-26 | B-25, pero Pedro no dijo quién pagó | — | La pregunta «¿Lo pagaste vos o queda a pagar?» va **por privado** a Pedro, no al grupo | S-16 |
| B-27 | Grupo; Ramón: «la Morena o la Moro, no sé, renguea» | El bot no sabe qué caballo es | Pregunta **en el grupo, a Ramón**, con opciones | P-1 |
| B-28 | Privado; Tomás carga un acuerdo nuevo sin dudas | — | Responde siempre con lo que entendió: «Acuerdo nuevo: Palm Ridge (Daniel Whitmore), Wellington 2027, US$ 180.000. Seña cobrada: US$ 30.000» | P-1 |
| B-29 | Grupo | Lucho: «jaja qué partido el de ayer» | No reacciona, no registra, no contesta | Charla 🔒 |
| B-30 | Grupo | Pedro manda en el grupo un ingreso: «me dijo Halvorsen que ya transfirió» | No lo registra (Pedro no puede cargar ingresos); a los owners, **por privado**: «Pedro dice que pagó Halvorsen. ¿Lo registro?» | P-2, S-15 🔒 |
| B-31 | Sofía tiene una sola organización; la Dra. Ibarra, dos | Cada una carga algo por privado | A Sofía, la confirmación **no** menciona la organización. A la Dra. Ibarra, **sí**: «Anotado en la organización de Tomás» | Invariante 8 de `Carga` |

## 4. Carga o charla

| Id | Mensaje | Entonces | Regla |
|---|---|---|---|
| B-32 | Pedro, grupo: «el flete salió 2 mil» | Es un dato → carga (con las preguntas que falten) | Charla vs carga 🔒 |
| B-33 | Pedro, grupo: «¿el flete sale 2 mil?» | Es una pregunta → **no** se carga | 🔒 |
| B-34 | Tomás, grupo: «che, ¿cuánto te salió el flete a vos?» | **No** se carga | 🔒 |
| B-35 | Tomás, privado: «la semana que viene voy a pagar la inscripción, 3 mil» | Es un plan a futuro → **no** es gasto. Se puede ofrecer «¿Querés que te lo recuerde?» | 🔒 |
| B-36 | Tomás, privado: «gracias» | Respuesta corta o ninguna; nada registrado | — |
| B-37 | Ramón, grupo: «mañana viene Cacho a las 9» | No es gasto; es una **visita** (Agenda) con ✅ | — |

## 5. Duplicados y varios mensajes

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-38 | G138 (herraje US$ 116, cargado por Pedro hoy a las 11:02) | A las 21:00 Tomás, por privado: «Pagué 180 mil al herrero» | Antes de registrar: «¿Es el mismo que cargó Pedro hoy a las 11?». Con «sí» → **no** se registra nada (carga descartada). Con «no» → segundo gasto | Duplicados 🔒 |
| B-39 | B-38 | Tomás no contesta la pregunta del duplicado | El gasto **no** se registra; repregunta a las 9:00 del día siguiente; después queda **sin terminar** en Inicio | P-10 🔒 |
| B-40 | Hoy | Tomás manda «Te paso la factura de los tacos» y a los 2 minutos la foto | **Una sola** carga con la foto como comprobante | P-16 |
| B-41 | G136 confirmado a las 18:41 | A las 19:30 Tomás manda una foto de factura de tacos | Si es el único gasto reciente compatible, la adjunta a G136 y lo dice; si hay más de uno, pregunta a cuál | P-16 |
| B-42 | Pedro manda un audio de gasto y 8 minutos después una foto | — | Son **dos** cargas; la segunda pasa por el control de duplicados | P-16 |

## 6. Varias organizaciones y proveedores

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-43 | La Dra. Ibarra trabaja para Tomás y para Juan Pérez | Por privado: «Le di el alta a la yegua del tendón» (ningún caballo nombrado) | Pregunta «¿Para qué cliente es: Tomás o Juan Pérez?» con botones | Ruteo |
| B-44 | Solo Tomás tiene una yegua llamada Patria | Dra. Ibarra por privado: «Patria evoluciona bien» | Va a la organización de Tomás **sin preguntar**; la confirmación lo dice | Ruteo |
| B-45 | B-43, eligió Tomás hace 10 minutos | La Dra. Ibarra manda 4 audios más | **No** vuelve a preguntar (contexto de conversación vigente) | Ruteo |
| B-46 | B-43 | La Dra. Ibarra dice «no, era para Juan» | El registro pasa a la organización de Juan; en la de Tomás **no queda nada** | Ruteo 🔒 |
| B-47 | La Dra. Ibarra está en el grupo de Tomás | Escribe ahí «¿cómo viene la Patria de Juan?» | Nunca muestra datos de la organización de Juan en el grupo de Tomás | Privacidad 🔒 |
| B-48 | Hoy | Dra. Ibarra, grupo: «Vacuné a las 16 de Pilar, influenza y encefalomielitis» | Evento de vacunación en las 16 fichas. **No** hay gasto. A los owners, por privado: «La Dra. Ibarra vacunó a 16 caballos. ¿Lo registro como gasto? ¿Por cuánto?» | Proveedores 🔒 |
| B-49 | Hoy | Cacho: «son 180 mil el herraje de las 4» | **No** registra el gasto con Cacho como autor; pregunta a los owners si lo registran por $ 180.000 | Proveedores 🔒 |

## 7. Permisos, accesos y eliminación

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-50 | — | Sofía, por privado: «nafta de la camioneta, 85 mil» | Se registra (G139) con «lo cargó Sofía por WhatsApp» | P-2 |
| B-51 | — | Juanca: «pagué el pastoreo de Windsor, 1.500 dólares» | Se registra: un petisero puede cargar gastos | P-2 |
| B-52 | — | Sofía: «me pagó La Ensenada 30 mil» | **No** se registra (Sofía no carga ingresos); se avisa a los owners | P-2 🔒 |
| B-53 | La Dra. Ibarra tiene acceso parcial: Novedades, Caballos, Lo que viene, 4 caballos | Entra a la app | Ve **solo** esos 4 caballos y sus novedades; **no** ve Gastos ni Ingresos; no puede cargar desde la app | P-18 🔒 |
| B-54 | — | Un owner intenta darle «Todo» a Cacho | La opción **no existe** para proveedores | 🔒 |
| B-55 | Tomás y Nacho son owners | Nacho intenta sacarle el owner a Tomás y después a sí mismo | Lo primero se puede; lo segundo **no**: siempre queda al menos un owner | P-19 🔒 |
| B-56 | Pedro cargó G133 | Pedro: «borrá el último» | Se elimina G133 (lo cargó él): sale de los totales y su mensaje queda **oculto** | P-26, P-3 🔒 |
| B-57 | Tomás cargó G136 | Pedro: «borrá los tacos» | **No** se elimina (no lo cargó Pedro); se les pregunta a los owners | P-26 🔒 |
| B-58 | — | Nacho elimina G048 (flete aéreo cubierto por Northfield) | Sale de Gastos; en Northfield el por cobrar baja de US$ 151.200 a **US$ 113.200**; el mensaje de origen queda oculto, no borrado | P-3 🔒 |
| B-59 | Don Aníbal se va de la organización | Al día siguiente manda un audio | El bot **no** lo carga para esa organización; lo que cargó antes sigue con su nombre | Bajas 🔒 |

## 8. Pagos fijos y deudas

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-60 | Pago fijo «Sueldos de los petiseros», día 5, US$ 3.000, Pilar | Llega el 5/11 a las 9:00 (hora de Tomás) | Pregunta «Hoy vencen los sueldos de los petiseros: US$ 3.000. ¿Los pagaste?» | Pagos fijos |
| B-61 | B-60 | Tomás: «Sí» | **Un** gasto Personal › Petiseros, US$ 3.000, Pilar, 5/11 | 🔒 |
| B-62 | B-60 | Tomás: «Todavía no, mañana» | Ningún gasto; vuelve a preguntar el 6/11 a las 9:00 | W7 |
| B-63 | B-61 ya confirmado | Tomás contesta «sí» otra vez a un mensaje viejo | **No** se genera un segundo gasto (un vencimiento, un gasto) | 🔒 |
| B-64 | Dataset C | Se mira Inicio › Pagos que vienen | 4 pagos, US$ **8.000** (1/11 y 5/11); la invernada del 15/11 no aparece | Anexo C §9 |
| B-65 | B-19, Pedro pagó en efectivo | Se mira Gastos | El herraje **suma** en el total; aparece «Le debés a Pedro US$ 116» | P-8 |
| B-66 | B-65 | Tomás: «ya le pagué a Pedro el herraje» | Desaparece de «Le debés a Pedro»; el total de Gastos **no cambia** | P-8 |

## 9. Ingresos, cobros y reintegros

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-67 | Dataset C | Se mira Ingresos › Por cobrar | ≈ US$ **415.250** (US$ 366.200 + ≈ 49.050 de Les Pins) | Anexo C §6 |
| B-68 | Halvorsen tiene Northfield y la venta de Halcona abiertos | Tomás: «Me pagó 40 mil Halvorsen» | Pregunta «¿Es de Northfield o de la venta de Halcona?» | P-6 |
| B-69 | B-68 | Responde «Northfield» | Cobrado 180.000 de 250.000; Te debe **US$ 111.200** (70.000 + 41.200 de reintegros) | Por cobrar 🔒 |
| B-70 | La Ensenada es el único acuerdo de Pablo Ferrer | «Me pagó 30 mil Ferrer» | Va a La Ensenada **sin preguntar**; queda Cobrado (60.000 de 60.000) | P-6 |
| B-71 | Northfield con reintegros pendientes: flete US$ 38.000 y pasajes US$ 3.200 | «Halvorsen me devolvió el flete» | Reintegro del flete → reintegrado; Te debe baja 38.000; el pago **no** se imputa a cuenta del acuerdo | P-5b |
| B-72 | Northfield | «Me pagó 38 mil Halvorsen» (coincide exacto con el flete pendiente) | Pregunta «¿Es el reintegro del flete o un pago del acuerdo?» | P-5b |
| B-73 | Northfield ya cobró los 250.000 pero los reintegros siguen pendientes | — | Estado **Cobrando**, no Cobrado | S-9 |
| B-74 | La Ensenada, 30.000 de 60.000 | «Me pagó 40 mil Ferrer» | Supera lo acordado → pregunta antes de registrar | S-8 |
| B-75 | Les Pins, € 45.000, sin pagos | Se mira el detalle | «≈ US$ 49.050», con «€ 45.000 al euro de hoy (US$ 1,09)» | Euros |
| B-76 | Valle Alto: € 80.000 cobrados (10/8 y 31/8) | Se mira lo cobrado | US$ **86.400** (a la cotización de cada pago) y no cambia si mañana cambia el euro | Euros 🔒 |
| B-77 | — | Tomás: «Pagué el flete aéreo de 10 caballos a Inglaterra, 38 mil dólares. Lo cubre Halvorsen» | Gasto con «Lo cubre Northfield» y reintegro **a reintegrar** en Northfield; Te debe **sube** 38.000 | Reintegros |
| B-78 | — | Tomás intenta marcar G137 (compra de Fortuna) como cubierto por un patrón | **No** se puede | S-10 🔒 |

## 10. Acuerdos caídos

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-79 | Palm Ridge, seña US$ 30.000 cobrada | Tomás: «Se cayó lo de Whitmore» | Estado **Caído**; la seña queda como cobrada; Por cobrar de Palm Ridge pasa de 150.000 a **0** | P-3 |
| B-80 | Northfield con US$ 41.200 de reintegros pendientes | Se marca Caído | El bot pregunta por los reintegros: «¿Te los van a devolver igual?». Si es no → los gastos pierden la marca «lo cubre» y pasan a ser propios | P-3 |
| B-81 | Venta de Halcona con US$ 50.000 cobrados | «Se cayó la venta de Halcona» | Pregunta qué hacer (con cobros); las devoluciones quedan fuera de la V1 | P-3 |
| B-82 | B-79 | Se mira Ingresos | Palm Ridge **sigue visible** como Caído. Si un owner lo **elimina**, desaparece y la seña sale de lo cobrado | Caído ≠ eliminado |

## 11. Temporadas y resultado

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-83 | Dataset C | Resultado de Inglaterra 2026 | Ingresos acordados **291.200** · cobrado **140.000** · gastos **122.300** · resultado **+168.900** (con lo cobrado: +17.700). La venta de Halcona va aparte | P-5 |
| B-84 | Dataset C | Resultado de Sotogrande 2026 | Ingresos **96.120** (incluye el reintegro del flete a su día: US$ 9.720) · gastos **32.749** · resultado **+63.371** | P-5, P-28 |
| B-85 | Dataset C | Resultado de Argentina 2026 | Ingresos 60.000 · cobrado 30.000 · gastos 33.618 · resultado **+26.382** (con lo cobrado: −3.618) | P-5, P-24 |
| B-86 | Invernada de Windsor del 1/9 (US$ 4.250) | — | Se ve en Gastos con lugar Windsor; **no** resta en Inglaterra 2026 (terminó el 31/7) ni en ninguna temporada | P-25 |
| B-87 | Seña de Sotogrande 2027 del 16/10 | — | No resta en Sotogrande 2026 | P-25 |
| B-88 | Temporada Inglaterra 2026 con Windsor del 1/4 al 31/7 | Un owner intenta crear otra temporada con Windsor del 1/7 al 31/8 | **No** se puede: un lugar no puede estar en dos temporadas superpuestas | `Temporada` 🔒 |
| B-89 | — | Tomás: «Cerré con Whitmore para jugar Wellington el año que viene, 180 mil» | El bot propone la temporada «Wellington 2027» (la crea si no existe) y pregunta las fechas si no puede deducirlas | P-4 |

## 12. Caballos, caballeriza y agenda

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-90 | Dataset C | Filtros de Caballos | Todos 35 · Jugando 14 · Campo 15 · Exterior 4 · Recuperación 2 | P-12 |
| B-91 | Patria: en recuperación, Pilar | — | Aparece en **Recuperación**, no en Jugando | P-12 |
| B-92 | Avena en Pilar: 18 bolsas, 7,5 kg por caballo, 16 caballos, bolsas de 40 kg | — | 3 por día · **6 días** · alerta en Inicio | Anexo C §8 |
| B-93 | B-92 | Tormenta pasa al campo (15 caballos en Pilar) | Avena: 2,81 por día · **6 días** (6,4 truncado); rollos del campo: 45 días | Anexo C §8 |
| B-94 | Dos conteos de Pedro dan 3,4 bolsas por día | — | Sugerencia «se están usando 3,4 por día, no 3»; el consumo **no** cambia hasta que un owner acepta | P-23 🔒 |
| B-95 | Pedro está en Pilar; Juanca, en Windsor | Llegan las tareas del día | Pedro las recibe a las 7:00 de Argentina; Juanca, a las 7:00 de Inglaterra | P-21 |
| B-96 | — | Tomás: «A la Morena hay que cambiarle la embocadura, que lo haga Pedro mañana» | Pendiente en la ficha de Morena, asignado a Pedro; mañana a las 7:00 está en sus tareas | Agenda |
| B-97 | B-96 | Pedro: «Listo, hecho» | Tachado; el bot le dice cuántas tareas le quedan | Agenda |
| B-98 | Morena viaja a Inglaterra en marzo | — | **No** aparece ningún pendiente automático de AIE ni vacunas | P-11 🔒 |
| B-99 | — | Tomás, 21:10: «Mañana haceme acordar de llamar a Cacho» | Mañana a las 9:00 (hora de Tomás): «Te acuerdo: llamar a Cacho…» | Recordatorio personal |

## 13. Consultas

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-100 | Dataset C | Tomás, privado: «¿Cuánto gasté en Inglaterra este mes?» | US$ **7.300** en Windsor (invernada 4.250, saldo del flete 2.450, tacos 600): los mismos números que la app | Consultas |
| B-101 | Dataset C | Tomás, privado: «¿Cuánto llevo de veterinario este mes?» | US$ **2.006** (1.200 + 206 + 600) | Anexo C, O-3 |
| B-102 | Grupo | Tomás pregunta en el grupo «¿cuánto llevamos gastado este mes?» | **No** contesta en el grupo; le responde a Tomás por privado | P-17 🔒 |
| B-103 | Grupo o privado | Pedro: «¿cuánto le debe Halvorsen a Tomás?» | **No** responde nada de plata (Pedro no es owner) | P-17 🔒 |


## 14. Gastos generales y reintegros con diferencia (tercera vuelta)

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-104 | 15/1: no hay temporada en el calendario | Tomás: «Pagué el handicap de este año, 850 mil» | Destino **General**, sin preguntar; suma en el total de Gastos y en el renglón «General» del filtro de lugar | P-29, P-30 |
| B-105 | B-104 | Se mira el resultado de cada temporada | El handicap **no** resta en ninguna | P-29 🔒 |
| B-106 | Juanca tiene lugar fijo Windsor | Juanca: «pagué 300 dólares de mantas» (sin lugar ni caballos) | Destino **Windsor** (lugar fijo de quien carga; el calendario no aplica porque Juanca no es owner) | P-30 |
| B-107 | Juanca tiene lugar fijo Windsor | «pagué 300 dólares de mantas para las de Sotogrande» | Destino **Sotogrande**: el lugar nombrado gana | P-30 |
| B-108 | Pasajes de vuelta del 30/8 (G099 y G100, US$ 4.200, Pilar), fuera de toda temporada | Un owner, en la app, los asocia a Sotogrande 2026 | Pasan a restar en Sotogrande 2026: gastos US$ 36.949, resultado **+59.171**; el total de Gastos no cambia | P-29 |
| B-109 | B-108 | Otro owner intenta asociar el mismo gasto también a Argentina 2026 | **No** se puede: un gasto resta en a lo sumo un resultado | Invariante 10 de `Gasto` 🔒 |
| B-110 | Flete Windsor – Sotogrande pagado el 2/8: € 9.000 = US$ 9.630 | El 31/8 Tomás: «Ordóñez me devolvió los 9 mil euros del flete» | Reintegro anotado tal cual: **€ 9.000**, a 1,08 = **US$ 9.720**. La diferencia de US$ 90 queda en el resultado; no se fuerza a 9.630 | P-28 |
| B-111 | Northfield con el flete de US$ 38.000 a reintegrar | «Halvorsen me devolvió 35 mil del flete» | Se anota US$ 35.000 reintegrado; quedan **US$ 3.000 pendientes** del flete; **no** pregunta. Un owner lo puede dar por cerrado en la app | P-28, S-21 |
| B-112 | Dataset C | Tomás: «¿Cuánto gasté en Windsor este mes?» | US$ 7.300; los gastos **General** del mes **no** se suman a Windsor | P-29 |


## 15. De dónde sale el lugar: calendario y lugar fijo (cuarta vuelta)

| Id | Dado | Cuando | Entonces | Regla |
|---|---|---|---|---|
| B-113 | 15/5: Tomás en Inglaterra 2026 (Windsor) | Tomás: «pagué 200 dólares de nafta» | Destino **Windsor** (calendario); resta en Inglaterra 2026 | P-30 |
| B-114 | 15/5: Tomás en Inglaterra 2026 | Tomás: «mandé 2 mil dólares para el campo» | Destino **Campo** (lugar nombrado gana sobre el calendario). No resta en Inglaterra 2026 ni en Argentina 2026 (fuera de sus fechas) | P-30, P-25 |
| B-115 | 15/5: Tomás en Windsor; Don Aníbal, lugar fijo Campo | Don Aníbal: «compré 6 bolsas de sal, 90 mil» | Destino **Campo**, **no** Windsor: el calendario solo vale para lo que cargan los owners | P-30 🔒 |
| B-116 | 22/10: Argentina 2026; Sofía sin lugar fijo | Sofía: «nafta de la camioneta, 85 mil» | Destino **Pilar** (calendario, lugar principal) (G139) | P-30 |
| B-117 | 20/1: no hay temporada | Nacho (manager, owner): «pagué 300 dólares de bozales» | Destino **General** | P-30 |
| B-118 | 15/5: Tomás en Windsor | Tomás: «le pagué a Cacho por herrar a la Bruja y la Gitana, 150 mil» (las dos están en Pilar) | Destino **Pilar** por los caballos nombrados (paso 2, antes que el calendario) | P-30 |
| B-119 | Sotogrande 2026 del 1/8 al 31/8 en el calendario | Un owner intenta cargar Chantilly del 10/8 al 17/8 | **No** se puede (se superponen); la app sugiere partir Sotogrande en tramos | S-22 🔒 |
| B-120 | B-113 | Tomás abre el detalle del gasto | Ve de dónde salió el lugar: «Windsor · según tu calendario». Puede cambiarlo o pasarlo a General | P-30 |

---

## Cobertura

| Regla o decisión | Escenarios |
|---|---|
| Conversión, redondeo, fecha, huso | B-01 a B-13, B-95 |
| Ante la duda pregunta / lugar General sin preguntar | B-14 a B-18, B-27 |
| Respuesta del bot (P-1, P-27) | B-24 a B-31 |
| Charla vs carga | B-29, B-32 a B-37 |
| Duplicados y varios mensajes | B-38 a B-42 |
| Ruteo y proveedores | B-43 a B-49 |
| Permisos y eliminación | B-50 a B-59 |
| Pagos fijos y deudas | B-60 a B-66 |
| Ingresos, cobros y reintegros | B-67 a B-78 |
| Acuerdos caídos | B-79 a B-82 |
| Temporadas y resultado | B-83 a B-89 |
| Caballos, caballeriza, agenda | B-90 a B-99 |
| Consultas y privacidad | B-100 a B-103 |
| Gastos generales y reintegros con diferencia | B-104 a B-112 |
| Lugar por calendario y lugar fijo | B-14, B-16, B-113 a B-120 |

**Lo que este anexo no cubre** (va en los anexos G y H): la calidad del modelo con mensajes reales, como audios largos con ruido, jerga regional o fotos ilegibles. Acá cada escenario tiene un mensaje claro y un resultado único.
