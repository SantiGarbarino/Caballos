# PRD — PROGRAMON

**Estado:** v0.2 · 2026-11-03 · Basado en el mockup final de las sesiones 22–27/10/2026 ([mockup](mockups/README.md)). La verdad de producto es el mockup y lo que dice este documento. Lo previo de la v0.1 que lo contradecía se reemplazó.

## Objetivo

Que un **polista profesional** tenga **toda su organización en el celular**, cargada por WhatsApp por él y su equipo:

- **Cuánto gastó**, en qué, dónde y en qué moneda.
- **Cuánto le deben** (patrones, ventas de caballos, reintegros).
- **Qué pasa con cada caballo** y qué tiene pendiente.
- **Para cuántos días alcanza el stock** y qué reporta el equipo.

Gastos es el centro: el dolor número uno y el gancho de adopción.

**Métrica norte [HIPÓTESIS]:** organizaciones que cargan gastos **4 de 4 semanas** del mes.

## Usuarios

| Usuario | Canal | Ve plata |
|---|---|---|
| Polista (dueño de la cuenta) | WhatsApp + app | Todo |
| Quien lleva las cuentas (Sofía) | WhatsApp + app | Gastos e ingresos: ve y carga |
| Contador (Estudio Ruiz) | App / export | Solo gastos, para exportar |
| Piloto (Pedro) | **Solo WhatsApp** | No |
| Petiseros y puestero | Solo WhatsApp | No |
| Patrones | No tienen acceso | No |

## Estructura de la app

Barra inferior con cinco pestañas: **Inicio · Caballos · Caballeriza · Gastos · Ingresos**. Ver el detalle de cada una:

- [App mobile: principios, diseño, navegación, Inicio y accesos](app-mobile.md)
- [Caballos](modulo-caballos.md)
- [Caballeriza](modulo-caballeriza.md)
- [Gastos e Ingresos](modulo-gastos-ingresos.md)
- [Flujos de WhatsApp](flujos-whatsapp.md)
- [Modelo de datos](modelo-de-datos.md)

## Requerimientos funcionales

### WhatsApp (carga, consultas y avisos)

| ID | Requerimiento | Prioridad |
|---|---|---|
| W1 | Cargar un **gasto** por mensaje, audio o foto (factura, remito, ticket, comprobante). La IA detecta monto, moneda, grupo › categoría, **lugar** y fecha | Must |
| W2 | **Ante la duda, preguntar**: si no sabe el lugar, la categoría o los caballos, pregunta (ej. "¿Son para acá o para la temporada de Inglaterra?"). Nunca adivina | Must |
| W3 | Entender la jerga y los montos ("180 lucas", "40 mil", "un millón doscientos") y las monedas (dólares, pesos, euros, libras) | Must |
| W4 | Confirmar cada carga y permitir corregir respondiendo | Must |
| W5 | Cargar **acuerdos con patrones**, **pagos recibidos** ("Me pagó 40 mil Halvorsen") y **ventas de caballos** | Must |
| W6 | Marcar un gasto como **cubierto por un patrón** ("Lo cubre Halvorsen") y sumarlo a lo que debe | Must |
| W7 | **Pagos fijos**: el día que vence cada uno, preguntar "¿Lo pagaste?"; con un «sí» se carga; si es "mañana", volver a preguntar al día siguiente a las 9 | Should |
| W8 | Reportes del equipo: vareos, herrajes, novedades de caballos (con foto a la ficha), stock ("quedan 18 bolsas") | Must |
| W9 | **Alta de caballo** por audio, con lectura de los papeles por foto (microchip) | Should |
| W10 | **Recordatorios** por caballo y **visitas** (herrero, veterinaria) por mensaje; asignables al piloto | Should |
| W11 | **Tareas del piloto**: mensaje a las 7:00 con la lista del día; avisos durante el día ("Tomás te avisó…", "No te olvides…"); tachar respondiendo "Listo, hecho" | Should |
| W12 | **Consultas** en lenguaje natural ("¿Cuánto gasté en Inglaterra este mes?", "¿Qué le falta a la Morena para viajar?") respondidas con los mismos datos de la app | Should |
| W13 | **Cierre del día** a las 20:00: vareos, herrajes, gastos, stock, lo que viene mañana | Could |
| W14 | Si un gasto lo pagó el piloto, preguntar "¿Lo pagaste vos o queda a pagar?" | Should |

### App mobile (PWA)

| ID | Requerimiento | Prioridad |
|---|---|---|
| A1 | **Inicio**: saludo, Gastado en el período y Por cobrar (por moneda), "Necesita tu atención", Gastos, "Lo que viene", "Pagos que vienen" | Must |
| A2 | **Gastos**: período (mes, 30 días, temporadas, año, fechas), lugar, total por moneda, "En qué se fue" (grupo › categoría › ítems por día), detalle con comprobante, pagos fijos, exportar | Must |
| A3 | **Ingresos**: Por cobrar (acuerdos y ventas con pagos parciales y reintegros) y Por temporada (ingresos − gastos por moneda) | Must |
| A4 | **Caballos**: lista con estado y filtros, búsqueda, ficha con novedad, pendientes, Actividad y Salud; agregar caballo | Must |
| A5 | **Caballeriza**: stock por sede con días que alcanza, consumo configurable, equipo con sus mensajes | Should |
| A6 | **Quién ve tu cuenta**: accesos por persona y nota de privacidad | Must |
| A7 | Cada total es la suma de los ítems visibles (una sola fuente de verdad) | Must |
| A8 | Monedas siempre separadas; sin conversiones ni totales combinados; sin "% vs mes anterior" | Must |
| A9 | Login sin contraseña (link de un solo uso por WhatsApp, como Queiros) | Must |

## Fuera de alcance (por ahora)

- **Onboarding** (decisión: que vean directo la versión final).
- **Ficha con documentación oficial / SENASA** (libreta digital, pasaporte, microchip como trámite).
- **Vista web del piloto** (el piloto usa solo WhatsApp).
- **Costo por caballo** (se sacó la pestaña Costos).
- **Pedidos a proveedores** desde la app.
- Conversión de monedas.
- Integraciones (bancos, Mercado Pago, ARCA).
- App nativa.
- Inglés (evaluar con los primeros usuarios que juegan afuera).

## Requerimientos no funcionales

- **Mobile-first**: pensado para ~390 px de ancho. Nunca pensado para desktop.
- **Velocidad**: confirmación por WhatsApp en menos de 10 s.
- **Privacidad**: los montos son sensibles. Solo los ven las personas habilitadas; los patrones nunca.
- **Trazabilidad**: cada registro guarda el mensaje original (texto, audio con transcripción, foto) y quién lo cargó.
- **Funciona desde el exterior** (Inglaterra, España, EE.UU.) y en cualquier moneda.

## Criterios de éxito (validación y beta) [HIPÓTESIS]

- 15 entrevistas con polistas que no sean familia.
- Compromisos concretos (preventa, seña o fecha de arranque) de al menos 5.
- Concierge test: ≥ 60% sigue mandando gastos en la semana 3.
- ≥ 85% de las cargas sin corrección manual.
- ≥ 3 referidos orgánicos.
