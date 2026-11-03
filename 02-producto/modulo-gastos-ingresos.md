# Módulo de gastos e ingresos — el corazón del MVP

> **Regla de oro:** registrar un gasto tiene que ser más rápido que mandárselo al patrón por WhatsApp. Un mensaje → un registro → una confirmación.

## Taxonomía de categorías (v0)

Las categorías son las que usa el polista, no las de un contador. La IA asigna automáticamente; el usuario puede corregir.

### Gastos

| Categoría | Subcategorías | Palabras que la disparan |
|---|---|---|
| 🧑‍🌾 **Petiseros** | Sueldo, adelanto, aguinaldo, premio, cargas sociales | petisero, sueldo, adelanto, "le pagué al Chino" |
| 🍖 **Comida petiseros** | Mercadería, asado, viandas | comida, súper, asado, carne, mercadería |
| 🌾 **Alimentación** | Alfalfa, fardos/rollos, avena, maíz, balanceado, suplementos, sal | alfalfa, fardo, rollo, avena, balanceado, forrajería |
| 🛏️ **Cama** | Viruta, paja | viruta, cama |
| 🏠 **Caballeriza / pensión** | Alquiler de boxes, pensión, potrero, servicios | pensión, box, alquiler, campo, luz |
| 💉 **Veterinaria** | Consulta, medicamentos, vacunas, análisis (AIE), estudios, cirugía | vete, veterinario, vacuna, AIE, ecografía, remedio |
| 🔨 **Herrería** | Herraje, despalme | herrero, herraje, herrar |
| 🚚 **Transporte** | Flete, combustible, peajes, mantenimiento camión | flete, camión, gasoil, nafta, peaje, transporte |
| 🏆 **Torneos** | Inscripción, cuota, alquiler de cancha | inscripción, torneo, cancha |
| 🎽 **Equipamiento** | Talabartería, tacos, bochas, cascos, botas, vendas | montura, cabezada, taco, bochas, casco |
| 🐎 **Doma / entrenamiento** | Domador, entrenamiento | doma, domador |
| 💰 **Compra de caballos** | Compra, comisión, revisación | compré, compra |
| 🧬 **Cría** | Servicio, transferencia embrionaria, receptora | servicio, embrión, receptora, padrillo |
| ✈️ **Viajes / temporada** | Pasajes, alojamiento, exportación temporal | pasaje, vuelo, hotel, Inglaterra |
| 📄 **Administrativo** | Seguros, cuotas AAP/club, SENASA, contador | seguro, cuota, SENASA |
| ❓ **Otros** | — | (fallback) |

### Ingresos

| Categoría | Ejemplos |
|---|---|
| 🏇 **Jugar (patrón)** | Pago por temporada, torneo o partido; premio |
| 🔁 **Reintegro de gastos** | El patrón devuelve gastos rendidos |
| 💵 **Venta de caballos** | Venta total o parcial |
| 📆 **Alquiler de caballos** | Por torneo / temporada |
| 🎓 **Clínicas / clases** | |
| 🏠 **Pensión / doma a terceros** | |
| 🏆 **Premios** | |
| ❓ **Otros** | |

## Campos de un movimiento

| Campo | Obligatorio | Cómo se obtiene |
|---|---|---|
| Tipo (gasto/ingreso) | ✅ | Inferido ("pagué" vs "cobré/me pagó") |
| Monto | ✅ | Texto/audio/OCR. Normaliza "50 lucas" → 50.000 |
| Moneda | ✅ | Inferida (default: moneda habitual del usuario; "verdes/USD" → USD) |
| Categoría / subcategoría | ✅ | Inferida |
| Fecha | ✅ | Default hoy; entiende "ayer", "el viernes" |
| Proveedor / persona | ⬜ | "al herrero", "al Chino", "forrajería Don Pedro" |
| Caballo(s) | ⬜ | "a la Pampa", "a los 12", "a todos" |
| Patrón / centro de costo | ⬜ | Default configurable ("propio" o patrón principal) |
| Medio de pago | ⬜ | efectivo / transferencia / cuenta corriente |
| Comprobante | ⬜ | Foto adjunta guardada |
| Nota libre | ⬜ | El texto original siempre se guarda (trazabilidad) |

## Reglas de negocio

1. **Siempre se guarda el mensaje original** (texto, audio, foto) vinculado al registro → trazabilidad, igual que Queiros.
2. **Moneda original inmutable**. Los reportes muestran totales por moneda. (Conversión: ver preguntas abiertas.)
3. **Prorrateo**: "herraje 180 lucas, 12 caballos" → 15.000 por caballo si se identifican los caballos; si no, queda como gasto general.
4. **Gasto general vs. por caballo**: alimento, sueldos y pensión son generales por defecto; vete y herrero por caballo si se menciona.
5. **Patrón**: cada movimiento puede imputarse a un patrón. La rendición = gastos imputados − reintegros recibidos.
6. **Duplicados**: si llega el mismo comprobante dos veces, avisar.
7. **Edición**: "borrá el último", "no, eran dólares", "ese era para Martín" → modifica el último movimiento.

## Ejemplos de mensajes que el MVP tiene que entender

| Mensaje | Resultado |
|---|---|
| "Pagué 180 lucas de herraje" | Gasto · Herrería · ARS 180.000 · hoy |
| 🎤 "Le di 300 mil al Chino del sueldo y 40 para la comida de los chicos" | 2 gastos: Petiseros ARS 300.000 + Comida petiseros ARS 40.000 |
| 📷 foto de factura de forrajería | Gasto · Alimentación · monto/fecha/proveedor por OCR |
| "Vete a la Pampa y a la Tormenta, 2 mil verdes, lo paga Martín" | Gasto · Veterinaria · USD 2.000 · 2 caballos · patrón Martín |
| "Me pagó Martín 5 mil dólares del torneo de Hurlingham" | Ingreso · Jugar (patrón) · USD 5.000 · patrón Martín |
| "Vendí la Morocha en 25 mil verdes" | Ingreso · Venta de caballos · USD 25.000 · caballo Morocha (marcar como vendida) |
| "Flete a Tortugas 450 lucas" | Gasto · Transporte · ARS 450.000 |
| "Inscripción 500 libras" | Gasto · Torneos · GBP 500 |
| "¿Cuánto llevo gastado en vete este mes?" | Consulta → respuesta con total y link al detalle |
