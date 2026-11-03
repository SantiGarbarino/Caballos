# Visión, problema y propuesta de valor

## En una frase

**El administrador de la organización de polo que vive en tu WhatsApp**: mandás un audio, una foto del ticket o un mensaje ("pagué 180 lucas de herraje, 12 caballos") y queda registrado, ordenado y visible en el celular.

## El problema

El polista profesional (y semi-profesional) maneja un **negocio** sin darse cuenta de que es un negocio: 15 a 60 caballos, varios petiseros, pensión, alfalfa, veterinario, herrero, transporte, inscripciones, viajes de temporada… y casi todo en **efectivo, en dos o tres monedas y sin registro**.

Dolores que detectamos **[HIPÓTESIS — validar en discovery]**:

1. **No sabe cuánto gasta ni en qué.** Los gastos están dispersos: efectivo al petisero, transferencia al vete, cuenta corriente en la forrajería, el herrero que cobra cada 5–6 semanas.
2. **No sabe cuánto le cuesta cada caballo** → no sabe si un caballo "se paga" o si conviene venderlo.
3. **Rendirle cuentas al patrón es un dolor.** Cuando el patrón paga los gastos de la organización (o de una parte de los caballos), el polista tiene que juntar tickets y armar una planilla a fin de mes. Discusiones y desconfianza.
4. **Ingresos desordenados**: lo que cobra por temporada, por torneo o por partido de distintos patrones, ventas y alquileres de caballos, clínicas. Cobros pendientes que se olvidan.
5. **Multimoneda**: pesos, dólares cash, y libras/euros/dólares en temporadas afuera (Inglaterra, Wellington, Sotogrande).
6. **El polista no usa la compu.** Vive en el celular y en WhatsApp. Las planillas de Excel no se mantienen. Las apps con formularios no se usan.

## La solución

Misma lógica que Queiros, aplicada al polo:

```
Polista / manager / petisero
   │  audio, foto de ticket, texto por WhatsApp
   ▼
IA estructura → gasto / ingreso / evento de caballo
   │  (categoría, monto, moneda, caballo(s), patrón/centro de costo, fecha)
   ▼
Confirmación por WhatsApp ("✅ Herraje $180.000 · 12 caballos · ¿OK?")
   ▼
Web app mobile-first: resumen del mes, gasto por caballo, por categoría,
por patrón, cobros pendientes, ficha de cada caballo
   ▼
Consultas en lenguaje natural por WhatsApp:
"¿cuánto gasté en vete en octubre?" · "¿cuándo herró por última vez la Pampa?"
```

### Principios de producto

1. **WhatsApp es la interfaz de carga.** Cero formularios. Si el polista tiene que abrir la app para cargar algo, perdimos.
2. **La app es para mirar, no para cargar.** Mobile-first (celular), nunca pensada para computadora.
3. **El módulo de gastos tiene que ser ridículamente simple.** Es el dolor #1 y el gancho de adopción.
4. **Hablamos como habla el polo.** Petisero, petiso, chukker, patrón, herraje, taqueo. Nada de "activos equinos" ni "recursos humanos".
5. **Confirmar siempre, preguntar poco.** La IA infiere todo lo que puede y solo pregunta lo imprescindible.

## Propuesta de valor por actor

| Actor | Qué gana |
|---|---|
| **Polista profesional** (comprador principal) | Saber cuánto gasta y cuánto gana, costo por caballo, rendición al patrón en un click, sin cargar nada en la compu |
| **Patrón** | Transparencia y control sobre lo que paga, sin pedir planillas |
| **Manager / capataz / jefe de petiseros** | Carga rápida desde el campo, menos discusiones por plata |
| **Haras / criador** (fase posterior) | Control de stock, reproducción, doma y costos por camada |

## Visión a largo plazo

Arrancar por **gastos del polista** → sumar **gestión de caballos** (stock, sanidad, herraje, movimientos) → **multiusuario** (organización completa: patrón, polista, manager, petiseros) → **haras y caballerizas** (cría, doma, pensión a terceros) → **second brain del mundo caballo**: todo el conocimiento operativo y económico de la organización, consultable por WhatsApp.

Y eventualmente, ser la capa de datos que conecta al ecosistema: veterinarios, herreros, transportistas, forrajerías, compra-venta de caballos.
