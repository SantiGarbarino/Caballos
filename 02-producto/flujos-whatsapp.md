# Flujos de WhatsApp

> Los 9 chats de demo del mockup (vista WhatsApp) son la referencia de tono y comportamiento. El remitente del bot es **PROGRAMON**.

## Principios

1. **Ante la duda, preguntar.** Nunca adivinar destino, categoría ni caballos. Ej.: "US$ 600 de veterinaria. ¿Para qué caballos es: Pilar, el campo o Windsor?"
2. **Confirmar corto y con el dato clave.** "Listo Ramón, 4 vareos cargados."
3. **Decir qué se generó** ("Guardada en la ficha de Rockstar", "Se lo agrego a las tareas de Pedro").
4. **Montos como los dice el polo**: "180 lucas" → $ 180.000; "40 mil" → 40.000 en la moneda del acuerdo; "un millón doscientos" → $ 1.200.000.
5. **Tono**: rioplatense, breve, sin emojis de más (el mockup no usa emojis).
6. **Mensajes salientes** (fuera de la ventana de 24 h) necesitan **plantillas aprobadas por Meta** y se pagan por mensaje: tareas del piloto a las 7:00, pagos fijos, recordatorios, avisos al piloto, cierre del día a las 20:00. Ver [arquitectura](../03-tecnico/arquitectura.md).
7. Cada chat de la demo cierra con **qué se ve en la app** (efecto), y algunos tienen botón "Ver en Ingresos" o "Ver este gasto en la app".

## 1. Ramón · petisero (vareos y novedad)

```
Ramón 🎤 0:31  9:38  «Buen día. Vareé a la Morena, al Tordillo, a la Cautiva y a la Gitana,
                     todo bien. La Rockstar la saqué pero renguea un poco de la mano izquierda,
                     la dejé en el box.»
PROGRAMON      9:38  Listo Ramón, 4 vareos cargados. Rockstar queda en el box con novedad,
                     le aviso a Tomás.
Ramón 📷       9:40  [Foto de la mano de Rockstar] Así tiene la mano
PROGRAMON      9:40  Guardada en la ficha de Rockstar.
Ramón 🎤 0:06 12:05  «También la Malcriada y la Chiquita.»
PROGRAMON     12:05  Sumadas. Van 12 de 14 hoy: faltan Rubia y Rockstar.
```
Efecto: vareos en las fichas, alerta de Rockstar en Inicio, la foto en su ficha. *(El texto del mockup todavía dice "6 vareos en «Día»": hay que corregirlo, Día ya no existe.)*

## 2. Pedro · piloto (tareas y avisos)

```
PROGRAMON  7:00  Buen día Pedro. Tus tareas de hoy:
                 1. Controlar si la Negra come la ración de la noche
                 2. Hielo en la mano de Rockstar, mañana y tarde
                 3. Herraje con Cacho: Bruja, Gitana, Dinamita y Lucera
                 Cuando termines una, avisame y la tacho.
Pedro      7:05  Dale
Pedro 🎤  11:02  «Vino Cacho, herró a la Bruja, la Gitana, la Dinamita y la Lucera. Son 180 lucas.»
PROGRAMON 11:02  Herraje de 4 caballos, $ 180.000. ¿Lo pagaste vos o queda a pagar?
Pedro     11:03  Lo pagué yo en efectivo
PROGRAMON 11:03  Anotado como pagado por vos y tachado de tus tareas. Próximo herraje de las 4:
                 fines de noviembre.
Pedro 📷  12:18  [Foto del depósito de avena] Se está terminando la avena
PROGRAMON 12:18  Conté 18 bolsas: alcanzan 6 días. Le aviso a Tomás para pedir.
PROGRAMON 14:16  Tomás te avisó: mañana a las 7 sale Tormenta al campo en el camión.
                 Ya está en tus tareas.
PROGRAMON 17:45  No te olvides: hielo en la mano de Rockstar antes de las 18.
Pedro     18:02  Listo, hecho
PROGRAMON 18:02  Tachado. Te quedan 2 tareas de hoy: la ración de la Negra y la práctica.
```
Efecto: al piloto le llegan tareas y avisos por WhatsApp y las tacha respondiendo. En la app: gasto en Herrero, herraje en cada ficha y alerta de avena.

## 3. Tomás · consultas (y cierre del día)

```
Tomás     14:10  ¿Cuánto llevo gastado en veterinario este mes?
PROGRAMON 14:10  En octubre, $ 1.950.000 en veterinaria. La mitad fue por Rockstar y Patria.
Tomás     14:11  ¿Cuánto gasté en Inglaterra este mes?
PROGRAMON 14:11  US$ 6.700 en Windsor: US$ 4.250 de la invernada y US$ 2.450 del saldo del flete.
Tomás     14:12  ¿Qué le falta a la Morena para viajar a Inglaterra?
PROGRAMON 14:12  Microchip y vacunas, al día. Falta el AIE (en febrero), la cuarentena desde
                 el 1/3 y el CVI de SENASA.
Tomás 🎤  14:15  «La Tormenta se va al campo mañana.»
PROGRAMON 14:15  Anotado: Tormenta pasa de Pilar al campo mañana. ¿Va en el camión de las 7 con Pedro?
Tomás     14:15  Sí
PROGRAMON 14:15  Listo. Se lo agrego a las tareas de Pedro.
Tomás 🎤  16:40  «Le pagué 600 dólares al veterinario.»
PROGRAMON 16:40  US$ 600 de veterinaria. ¿Para qué caballos es: Pilar, el campo o Windsor?
Tomás     16:41  Las de doma del campo
PROGRAMON 16:41  Anotado: US$ 600, veterinaria, destino Campo.
PROGRAMON 20:00  Cierre de hoy:
                 • 12 de 14 vareados (falta Rubia, Rockstar en el box con hielo)
                 • Herraje de 4 caballos: $ 180.000
                 • Avena para 6 días: ya le pediste 40 bolsas al corralón
                 • Mañana 7:00: Tormenta al campo
                 • Sábado: Morena llega a 6 chukkers en la semana
```
Efecto: las respuestas salen de los mismos datos de la app. Cada gasto se clasifica solo por categoría; si no sabe el destino, pregunta. A las 20:00 llega el cierre del día. *(Inconsistencias a corregir en el mockup: "$ 1.950.000 en veterinaria" no coincide con la lista de octubre; "40 bolsas al corralón" y "6 chukkers" refieren a funciones que se sacaron.)*

## 4. Recordatorios y visitas

```
Tomás 🎤 18:20  «A la Morena hay que cambiarle la embocadura, probar la de goma. Que lo haga Pedro mañana.»
PROGRAMON 18:20 Recordatorio en la ficha de Morena para mañana, asignado a Pedro. Se lo mando con
                sus tareas a las 7.
Tomás    18:24  El jueves que viene viene Cacho a herrar a la Chiquita, la Rubia y la Malcriada
PROGRAMON 18:24 Agendado: jueves 29, Cacho, herrero, 3 caballos. Le aviso a Pedro el día antes.
Tomás    18:25  Y el lunes la Dra. Ibarra a ver a la Rockstar
PROGRAMON 18:25 Agendado: lunes 26, Dra. Ibarra, control de Rockstar. Queda también como pendiente
                en su ficha.
```
Efecto: el recordatorio aparece en los pendientes de Morena y las visitas en "Lo que viene" (Inicio) y en las tareas del piloto.

## 5. Acuerdos y cobros

```
Tomás 🎤 10:15  «Me pagó 40 mil Halvorsen.»
PROGRAMON 10:15 Registrado: US$ 40.000 de Northfield (Erik Halvorsen). Llevás cobrado US$ 140.000
                de 250.000: faltan US$ 110.000.
Tomás    10:20  Cerré con Whitmore para jugar Wellington el año que viene, 180 mil dólares.
                Me dejó 30 de seña.
PROGRAMON 10:20 Acuerdo nuevo: Palm Ridge (Daniel Whitmore), Estados Unidos · Wellington 2027,
                US$ 180.000. Seña cobrada: US$ 30.000. ¿Confirmás?
Tomás    10:21  Sí
PROGRAMON 10:21 Listo. En total te deben US$ 366.200 y € 45.000, contando los gastos que te tienen
                que reintegrar.
```
Efecto: acuerdos y pagos en Ingresos, con lo que falta cobrar de cada patrón. Botón "Ver en Ingresos".

## 6. Gasto que cubre el patrón

```
Tomás 📷 12:10  [Foto de la factura del flete] Pagué el flete aéreo de los 10 caballos a Inglaterra,
                38 mil dólares. Lo cubre Halvorsen.
PROGRAMON 12:10 Anotado: flete de caballos, US$ 38.000, destino Windsor. Lo marco como gasto que
                cubre Northfield (Erik Halvorsen) y lo sumo a lo que te debe.
Tomás    12:11  Perfecto
PROGRAMON 12:11 Northfield te debe ahora US$ 288.000: US$ 250.000 del acuerdo y US$ 38.000 del flete.
```
(Fecha del chat: 20 de abril.) Efecto: el flete aparece en Gastos con la marca «Lo cubre Northfield» y en Ingresos se suma a lo que debe ese patrón.

## 7. Pagos fijos

```
PROGRAMON  9:00  Hoy vencen los sueldos de los petiseros: US$ 3.000. ¿Los pagaste?
Tomás      9:40  Sí
PROGRAMON  9:40  Listo, cargado en Gastos › Personal › Petiseros.
PROGRAMON  9:41  También vence hoy el sueldo de Don Aníbal: US$ 600. ¿Lo pagaste?
Tomás     11:02  Todavía no, mañana
PROGRAMON 11:02  Dale, te lo vuelvo a preguntar mañana a las 9.
```
(Fecha: 5 de octubre.) Efecto: los pagos fijos se cargan una vez; cada mes, el día que vencen, PROGRAMON pregunta y con un «sí» quedan en Gastos.

## 8. Carga de un gasto (con foto)

```
Tomás 📷 18:40  [Foto de la factura de los tacos] Te paso la factura de los tacos
PROGRAMON 18:40 3 tacos, US$ 540. Lo anoto en Equipo de polo › Tacos. ¿Son para acá o para la
                temporada de Inglaterra?
Tomás    18:41  Para acá
PROGRAMON 18:41 Listo, anotado en Pilar con la foto de la factura.
```
Efecto: aparece en Gastos › Equipo de polo › Tacos y al abrirlo se ve la foto. Botón "Ver este gasto en la app".

## 9. Alta de un caballo

```
Tomás 🎤 19:40  «Nuevo caballo: Fortuna, yegua, 6 años, zaina. La compré en Coronel Suárez,
                18 mil dólares. Llega el sábado a Pilar.»
Tomás 📷 19:41  [Foto de los papeles de Fortuna]
PROGRAMON 19:41 Alta de Fortuna: yegua, 6 años, zaina, US$ 18.000. Microchip de los papeles:
                032 0981 5512 340. Llega el sábado a Pilar. ¿Confirmás?
Tomás    19:42  Dale
PROGRAMON 19:42 Lista. Ya son 36 caballos. Te aviso el sábado si no me confirman que llegó.
```
Efecto: Fortuna aparece en Caballos con su ficha y la compra queda aparte de los gastos del mes (Compra de caballos).

## Otros casos que el bot tiene que resolver

- Mensajes que no son cargas ("gracias", "jaja") → respuesta corta, no registrar.
- Fecha pasada ("el viernes pagué…").
- Audio largo con varias cosas → resumir y pedir confirmación.
- Comprobante ilegible → pedir el monto.
- Mismo comprobante dos veces → avisar duplicado.
- Correcciones ("no, eran dólares", "borrá el último", "eso era para el campo").
- Persona del equipo que deja de reportar (ej. Don Aníbal, 2 días sin mensajes) → destacarlo en la app.
