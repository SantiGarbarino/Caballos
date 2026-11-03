# PRD — PROGRAMON

**Estado:** v0.3 · 2026-11-03 (sesión 3: monedas, manager, grupos, integración con la app Polo Argentino, recordatorios) · Basado en el mockup final de las sesiones 22–27/10/2026 ([mockup](mockups/README.md)). La verdad de producto es el mockup y lo que dice este documento. Lo previo de la v0.1 que lo contradecía se reemplazó.

## Objetivo

Que un **polista profesional** (y su **manager**) tenga **toda su organización en el celular**, cargada por WhatsApp por él y su equipo:

- **Cuánto gastó** (en dólares), en qué y dónde.
- **Cuánto le deben** (patrones, ventas de caballos, reintegros).
- **Qué pasa con cada caballo** y qué tiene pendiente.
- **Para cuántos días alcanza el stock** y qué reporta el equipo.

Gastos es el centro: el dolor número uno y el gancho de adopción.

**Métrica norte [HIPÓTESIS]:** organizaciones que cargan gastos **4 de 4 semanas** del mes.

## Usuarios

> **Actualización (2026-11-03, sesión 10):** quien crea la organización (polista o manager) es **owner** y configura desde Equipo qué ve cada usuario: solo WhatsApp (por defecto para todos salvo owners) o una parte de la plataforma (ej. el veterinario ve Caballos y las novedades de la caballeriza, nunca Gastos ni Ingresos). Lo de abajo es el caso típico.

Hay **dos tipos de usuario**: los de la **app** (polista y manager) y los de **solo WhatsApp** (el resto de la organización y los proveedores: cargan por el bot, lo que mandan figura en la plataforma con su nombre, pero nunca entran a la app).

| Persona | Canal | Acceso a la app | Ve plata |
|---|---|---|---|
| **Polista** (dueño de la cuenta) | WhatsApp (grupo + privado) + app | Sí | Todo |
| **Manager** (mano derecha; en organizaciones grandes, el que más usa) | WhatsApp (grupo + privado) + app | Sí, **igual que el polista** | Todo |
| Otros de la organización (ej. un familiar o asistente que lo ayuda con gastos y compras) | Solo WhatsApp (privado o grupo) | No | No (carga, no ve) |
| Piloto | Solo WhatsApp (grupo y tareas por privado) | No | No |
| Petiseros y puestero | Solo WhatsApp (grupo) | No | No |
| Veterinario / herrero (varios clientes) | Solo WhatsApp (grupo de cada cliente; por privado el bot pregunta el cliente) | No | No |
| Contador | Recibe el export por mail | No | — |

El **patrón no existe para la plataforma**: solo aparece como contraparte de acuerdos, pagos y reintegros.

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
| W1b | **Conversión a US$**: si el gasto es en pesos, se convierte solo al **dólar blue del día** (**promedio entre compra y venta**, de Rava, DólarHoy u otra fuente), sin preguntar. Si es en euros u otra moneda, se usa una cotización online; si no hay fuente, el bot pregunta el tipo de cambio | Must |
| W2 | **Ante la duda, preguntar**: si no sabe el lugar, la categoría o los caballos, pregunta (ej. "¿Son para acá o para la temporada de Inglaterra?"). Nunca adivina. **Nunca** pregunta el tipo de cambio de los pesos | Must |
| W3 | Entender la jerga y los montos ("180 lucas", "40 mil", "un millón doscientos") y las monedas (dólares, pesos, euros, libras) | Must |
| W4 | Confirmar cada carga y permitir corregir respondiendo | Must |
| W5 | Cargar **acuerdos con patrones**, **pagos recibidos** ("Me pagó 40 mil Halvorsen") y **ventas de caballos** | Must |
| W6 | Marcar un gasto como **cubierto por un patrón** ("Lo cubre Halvorsen") y sumarlo a lo que debe | Must |
| W7 | **Pagos fijos**: el día que vence cada uno, preguntar "¿Lo pagaste?"; con un «sí» se carga; si es "mañana", volver a preguntar al día siguiente a las 9 | Should |
| W8 | Reportes del equipo: vareos, herrajes, novedades de caballos (con foto a la ficha), stock ("quedan 18 bolsas") | Must |
| W9 | **Alta de caballo** por audio, con lectura de los papeles por foto (microchip) | Should |
| W10 | **Recordatorios** por caballo y **visitas** (herrero, veterinaria) por mensaje; asignables al piloto | Should |
| W10b | **Recordatorios personales**: «Mañana haceme acordar tal cosa» → el bot se lo recuerda al polista o al manager en ese momento | Must |
| W11 | **Tareas del piloto**: mensaje a las 7:00 con la lista del día; avisos durante el día ("Tomás te avisó…", "No te olvides…"); tachar respondiendo "Listo, hecho" | Should |
| W12 | **Consultas** en lenguaje natural ("¿Cuánto gasté en Inglaterra este mes?", "¿Qué le falta a la Morena para viajar?") respondidas con los mismos datos de la app | Should |
| W13 | **Cierre del día** a las 20:00: vareos, herrajes, gastos, stock, lo que viene mañana | Could |
| W14 | Si un gasto lo pagó el piloto, preguntar "¿Lo pagaste vos o queda a pagar?" | Should |
| W15 | **Bot en el grupo de WhatsApp** de la organización (manager, polista, vete, herrero, petiseros): lo que se manda sobre caballos y caballeriza entra a la app | Must |
| W16 | **Chat privado** con el bot para gastos, ingresos y consultas de plata (lo que no tienen que ver el vete ni los petiseros). Si se habla de plata en el grupo, **se registra igual** | Must |
| W18 | **Miembros de solo WhatsApp**: cualquier persona de la organización registrada (ej. un familiar, petiseros) puede cargar por el bot; en la app figura "lo cargó X" | Must |
| W17 | **Proveedores con varios clientes** (vete, herrero): en el grupo de cada cliente se asigna solo; por privado, el bot pregunta para qué cliente es | Must |

### App mobile (PWA)

| ID | Requerimiento | Prioridad |
|---|---|---|
| A1 | **Inicio**: saludo, Gastado en el período y Por cobrar (en US$), "Necesita tu atención", Gastos, "Lo que viene", "Pagos que vienen" | Must |
| A2 | **Gastos**: período (mes, 30 días, temporadas, año, fechas), lugar, total en US$, "En qué se fue" (grupo › categoría › ítems por día), detalle con comprobante (foto, o si no hay, el audio o mensaje original) y, si se convirtió, el detalle de la conversión en letra chica; pagos fijos, exportar | Must |
| A3 | **Ingresos**: Por cobrar (acuerdos y ventas con pagos parciales y reintegros) y Por temporada (ingresos − gastos en US$) | Must |
| A4 | **Caballos**: lista con estado y filtros, búsqueda, ficha con novedad, pendientes, Actividad y Salud; agregar caballo **eligiéndolo del catálogo de la app Polo Argentino** (sangre, padre, madre, partidos) | Must (la app Polo Argentino: sujeto a la integración) |
| A5 | **Caballeriza**: stock por sede con días que alcanza, consumo configurable, equipo con sus mensajes | Should |
| A6 | **Equipo**: owners (polista y/o manager) invitan usuarios y configuran qué ve cada uno: solo WhatsApp o módulos de la app (Gastos e Ingresos, solo owners) | Must |
| A7 | Cada total es la suma de los ítems visibles (una sola fuente de verdad) | Must |
| A8 | Todo en US$, con la conversión explicada en cada gasto; sin "% vs mes anterior" | Must |
| A9 | Login sin contraseña (link de un solo uso por WhatsApp) | Must |
| A10 | **Sin tablas**: módulos con tableros, tarjetas y listas | Must |

## Fuera de alcance (por ahora)

- **Onboarding** (decisión: que vean directo la versión final).
- **Ficha con documentación oficial / SENASA** (libreta digital, pasaporte, microchip como trámite).
- **Vista web del piloto** (el piloto usa solo WhatsApp).
- **Costo por caballo** (se sacó la pestaña Costos).
- **Pedidos a proveedores** desde la app.
- Integraciones (bancos, Mercado Pago, ARCA).
- App nativa.
- Inglés (evaluar con los primeros usuarios que juegan afuera).

## Requerimientos no funcionales

- **Mobile-first**: pensado para ~390 px de ancho. Nunca pensado para desktop.
- **Velocidad**: confirmación por WhatsApp en menos de 10 s.
- **Privacidad**: los montos son sensibles. En la app solo los ven el polista y el manager. Lo que se registra desde el grupo lo ven, en el chat, los que están en el grupo.
- **Trazabilidad**: cada registro guarda el mensaje original (texto, audio con transcripción, foto) y quién lo cargó.
- **Funciona desde el exterior** (Inglaterra, España, EE.UU.) y acepta cualquier moneda (se muestra en US$).

## Criterios de éxito (validación y beta) [HIPÓTESIS]

- 15 entrevistas con polistas que no sean familia.
- Compromisos concretos (preventa, seña o fecha de arranque) de al menos 5.
- Concierge test: ≥ 60% sigue mandando gastos en la semana 3.
- ≥ 85% de las cargas sin corrección manual.
- ≥ 3 referidos orgánicos.
