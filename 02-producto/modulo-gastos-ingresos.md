# Gastos e Ingresos — el corazón del producto

> **Gastos es el módulo principal.** Tiene que ser súper claro y fácil de leer: **no puede haber lugar a dudas** de cómo se forma cada número (pedido de Santi). Se rediseñó dos veces porque "quedó un lío" y "no quedó limpio". Lo que sigue es la versión final del mockup.

---

# Gastos

## Reglas de oro

1. **Una sola lista de gastos** (en el mockup, `LEDGER`, de enero al 22/10/2026). **Todo total que se muestra es la suma de los gastos de esa lista** que caen en el período y el lugar elegidos. Nunca hay datos separados para los totales.
2. **Monedas separadas**: US$, $ y € (y £ en Ingresos). Nunca se convierte, nunca hay un total combinado y **no hay "+X% vs mes anterior"**.
3. **La moneda no depende del lugar.** Un gasto del campo se puede pagar en dólares estando en Sotogrande.
4. **Se clasifica por destino (lugar)**, no por dónde estaba el polista cuando pagó. US$ 2.000 para el campo pagados en Sotogrande → **Campo**.
5. **Ante la duda, el bot pregunta** el lugar, la categoría o los caballos. Nunca adivina.
6. Cada gasto muestra **de dónde salió**: foto, audio con transcripción o mensaje, y **quién lo cargó**.

## Dimensiones de un gasto

| Dimensión | Valores |
|---|---|
| **Grupo › categoría** | Ver taxonomía |
| **Lugar (destino)** | Caballeriza Pilar · Campo, Cnel. Suárez · Windsor, Inglaterra · Sotogrande, España |
| **Moneda** | US$ · $ · € |
| **Fecha** | Día y mes |
| **Comprobante** | Foto (factura, remito o ticket), audio (con transcripción) o mensaje |
| **Lo cargó** | Tomás, Sofía, Pedro, Juanca, Don Aníbal, Dra. Ibarra… "por WhatsApp" |
| **Lo cubre** (opcional) | Acuerdo con un patrón + estado del reintegro (a reintegrar / reintegrado) |

## Taxonomía (grupo › categoría)

Armada con la lista de gastos que dio Santi. Veterinaria y comida **"afuera" no son categorías**: se resuelven con el **lugar**.

| Grupo | Bajada | Categorías |
|---|---|---|
| **Caballos** | Comida, pastoreo, veterinario y herrero | Comida · Pastoreo · Veterinario · Herrero |
| **Personal** | Petiseros y su comida | Petiseros · Comida de los petiseros |
| **Caballerizas y casa** | Acá y afuera | Caballerizas · Casa |
| **Equipo de polo** | Monturas, bozales, tacos y cascos | Monturas · Bozales y riendas · Tacos · Cascos e indumentaria |
| **Traslados y viajes** | Fletes de caballos, pasajes y nafta | Fletes de caballos (incluye **trailer y camión contratados**) · Pasajes propios · Pasajes de los petiseros · Nafta y vehículos |
| **Torneos y handicap** | Inscripciones y pago del handicap | Inscripciones · Handicap |
| **Varios** | Regalos y gastos extra | Regalos y extras |
| **Compra de caballos** | Inversión: caballos que compraste | Compras |

Notas:
- Sueldo del puestero va en Personal › Petiseros (lugar Campo).
- Gomas del trailer propio, nafta de la camioneta → Traslados y viajes › Nafta y vehículos.
- Seña de una caballeriza de la próxima temporada → Caballerizas y casa › Caballerizas (lugar de esa caballeriza).
- **Compra de caballos** se ve en Gastos como grupo aparte, pero **no entra en el resultado por temporada** (es inversión).

## Pantalla Gastos

1. **Encabezado**: "Gastos" y botón **Exportar**.
2. **Botón de período**. Hoja "Ver gastos de…":
   - Este mes (Octubre, al día 22)
   - Últimos 30 días (del 23/9 al 22/10)
   - Temporada Argentina (septiembre a diciembre · al 22/10)
   - Temporada Inglaterra (mayo a julio 2026)
   - Temporada Sotogrande (agosto 2026)
   - Todo 2026 (del 1/1 al 22/10)
   - "O elegí las fechas": Desde / Hasta → "Ver este rango"
3. **Botón de lugar**. Hoja "Ver gastos de…": Todos los lugares (Argentina, Inglaterra y España) · Caballeriza Pilar (16 caballos · Argentina) · Campo, Cnel. Suárez (15 caballos · Argentina) · Windsor, Inglaterra (4 caballos en invernada) · Sotogrande, España (sin caballos ahora · caballeriza de temporada).
4. **Tarjeta de total** (degradado): "Total gastado · N gastos" y un renglón por moneda. Este mes: **24 gastos · US$ 38.690 · $ 5.625.000 · € 4.000**.
5. **Pagos fijos**: "5 pagos · US$ 12.250 por mes" → vista Pagos fijos.
6. **En qué se fue**: un renglón por grupo, con cantidad de gastos y total por moneda. Tocar un grupo → total del grupo y **Por categoría** → tocar una categoría → total y los gastos **agrupados por día** (Hoy, Ayer, "Jueves 8 de octubre"…).
7. **Últimos gastos** (5) y **Ver los N** → lista completa por día.

Ejemplo, este mes por grupo:

| Grupo | Gastos | Totales |
|---|---|---|
| Caballos | 6 | US$ 2.000 · $ 4.380.000 |
| Personal | 4 | US$ 3.800 · $ 160.000 |
| Caballerizas y casa | 4 | US$ 8.650 · € 4.000 |
| Equipo de polo | 4 | US$ 3.790 |
| Traslados y viajes | 4 | US$ 2.450 · $ 965.000 |
| Varios | 1 | $ 120.000 |
| Compra de caballos | 1 | US$ 18.000 |

## Detalle de un gasto (hoja)

- Monto grande y título.
- Si lo cubre un patrón: banner "Lo cubre Northfield (Erik Halvorsen). Está sumado a lo que te debe en Ingresos."
- **Fecha** ("Hoy, 22/10", "Lunes 20 de abril"), **Categoría** (grupo › categoría), **Lugar**, **Lo cargó** ("Pedro por WhatsApp").
- **Comprobante**: "Foto de la factura / del remito / del ticket · Tocá para ampliar", o **Audio original** con la transcripción entre comillas, o el mensaje.
- **Ver la conversación de WhatsApp** (en algunos gastos).

## Pagos fijos

Se cargan una vez. El día que vence cada uno, PROGRAMON pregunta por WhatsApp si lo pagaste; respondés «sí» y queda en Gastos.

| Pago | Día | Lugar | Monto |
|---|---|---|---|
| Sueldos de los petiseros | 5 | Pilar | US$ 3.000 |
| Sueldo del puestero | 5 | Campo | US$ 600 |
| Alquiler caballeriza Pilar | 1 | Pilar | US$ 1.900 |
| Alquiler de la casa en Pilar | 1 | Pilar | US$ 2.500 |
| Invernada en Windsor | 15 | Windsor | US$ 4.250 |

Botón **Agregar** (hoja para un pago fijo nuevo) y **Ver cómo se confirma por WhatsApp**. Inicio muestra los que vencen pronto en "Pagos que vienen".

## Exportar

Hoja "Exportar gastos": período y lugar actuales ("Octubre, al día 22 · Todos los lugares · 24 gastos · 10 con foto"), **Formato** Excel / PDF, **Incluir las fotos de los comprobantes**, **Mail de tu contador** (contador@estudioruiz.com.ar) → **Mandar a mi contador** → confirmación.

---

# Ingresos

## Qué incluye

- **Acuerdos con patrones**: lo que se arregló cobrar por jugar una temporada y los pagos que van entrando (seña, transferencias).
- **Ventas de caballos**: precio y cobros parciales.
- **Gastos que cubre el patrón**: se suman a lo que debe hasta que los reintegra.

**Por cobrar = acordado − cobrado + gastos que cubre el patrón pendientes de reintegro.**

Se puede cargar por WhatsApp ("Me pagó 40 mil Halvorsen", "Cerré con Whitmore para jugar Wellington, 180 mil dólares, me dejó 30 de seña") o desde la app.

## Pantalla Ingresos

- Encabezado "Ingresos" y botón **Nuevo** (hoja con pestañas **Patrón** / **Venta de caballo**).
- Selector **Por cobrar** / **Por temporada**.

### Por cobrar

- **Tarjeta**: "Por cobrar · 5 pendientes": **US$ 366.200 · € 45.000**.
- "Ya cobraste US$ 290.000 · € 80.000".
- Filtros: Todos · Por cobrar · Cobrados.
- Secciones **Patrones** y **Venta de caballos**. Cada tarjeta muestra: nombre, patrón/comprador · lugar · temporada, estado (**Sin pagos** / **Cobrando** / **Cobrado**), barra de progreso, "Cobrado X de Y · Faltan Z" y, si corresponde, "+ US$ 41.200 de gastos que cubre y no reintegró".

| Acuerdo | Patrón | Dónde | Acordado | Pagos | Estado |
|---|---|---|---|---|---|
| Northfield | Erik Halvorsen | Inglaterra · temporada 2026 | US$ 250.000 | 15/5 US$ 100.000 · 20/6 US$ 40.000 | Cobrando · faltan 110.000 + 41.200 de reintegros |
| Palm Ridge | Daniel Whitmore | Estados Unidos · Wellington 2027 | US$ 180.000 | 10/10 seña US$ 30.000 | Cobrando · faltan 150.000 |
| La Ensenada | Pablo Ferrer | Argentina · temporada 2026 | US$ 60.000 | 1/10 US$ 30.000 | Cobrando · faltan 30.000 |
| Les Pins | Antoine Moreau | Francia · Chantilly 2026 | € 45.000 | — | Sin pagos |
| Valle Alto | Javier Ordóñez | España · Sotogrande 2026 | € 80.000 | 10/8 € 50.000 · 31/8 € 30.000 | Cobrado (flete € 9.000 reintegrado) |
| Venta de Halcona | Erik Halvorsen | Inglaterra · julio 2026 | US$ 85.000 | 25/7 US$ 50.000 | Cobrando · faltan 35.000 |
| Venta de Trueno | Un polista de Wellington | EE.UU. · septiembre 2026 | US$ 40.000 | Total | Cobrado |

### Detalle de un acuerdo

- Acordado (o Precio de venta) · Cobrado · **Gastos a reintegrar** · **Te debe**. Northfield: 250.000 · 140.000 · 41.200 · **151.200**.
- **Pagos recibidos** (fecha, origen: "Transferencia · foto del comprobante", "mensaje de Tomás", monto).
- **Gastos que cubre el patrón** con estado: Northfield → Pasajes de 2 petiseros a Londres (28/4, a reintegrar, US$ 3.200) y Flete aéreo de 10 caballos a Inglaterra (20/4, a reintegrar, US$ 38.000). Valle Alto → Flete Windsor – Sotogrande (2/8, reintegrado, € 9.000).
- **Registrar pago** (hoja: "Te debe US$ 151.200 · Cuánto te pagó") y atajo de WhatsApp.

### Nuevo

- **Patrón**: Equipo, Patrón, Dónde y cuándo, Lo que arreglaron + moneda (US$ / € / £) → Guardar. Atajo: «Cerré con Halvorsen para jugar Inglaterra, 250 mil dólares.»
- **Venta de caballo**: Caballo, Comprador, Dónde y cuándo, Precio + moneda → Guardar. Atajo: «Vendí a Halcona a Halvorsen, 85 mil dólares.»

### Por temporada (resultado)

"Lo que arreglaste con patrones y ventas (más los gastos que te reintegran), contra lo que gastaste en ese lugar y esas fechas. Cada moneda por separado. No incluye compras de caballos."

| Temporada | Lugar y fechas | Incluye | Moneda | Ingresos | Gastos | Resultado |
|---|---|---|---|---|---|---|
| Inglaterra 2026 | Windsor · abril a julio | Northfield + venta de Halcona | US$ | 376.200 | −122.300 | **+253.900** |
| Sotogrande 2026 | España · julio y agosto | Valle Alto | € | 89.000 | −30.500 | **+58.500** |
| Argentina 2026 | Pilar y campo · septiembre a hoy | La Ensenada + venta de Trueno | US$ | 100.000 | −24.770 | **+75.230** |
| | | | $ | — | −12.555.000 | −12.555.000 |

Los ingresos incluyen los reintegros (Inglaterra: 250.000 + 85.000 + 41.200; Sotogrande: 80.000 + 9.000).
