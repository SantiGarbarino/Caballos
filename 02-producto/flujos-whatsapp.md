# Flujos de WhatsApp

> Tono del bot: corto, canchero, rioplatense, con la jerga del polo. Emojis con moderación. Nunca más de 3 líneas salvo en resúmenes.

## 1. Onboarding (< 2 minutos)

```
Usuario: Hola
Bot:     ¡Buenas! Soy [nombre], tu administrador por WhatsApp 🐴
         Mandame cualquier gasto o ingreso de tu organización como se lo
         mandarías a tu patrón: texto, audio o foto del ticket.
         Antes, 2 preguntas rápidas:
         1) ¿Cómo te llamás?
Usuario: Juan
Bot:     2) ¿Más o menos cuántos caballos tenés? (después los cargamos)
Usuario: 25
Bot:     Listo Juan. Probá ahora: mandame el último gasto que hiciste 👇
```

Opcional después (no bloquea): patrones con los que juega, moneda principal, nombres de los caballos ("mandame una lista o un audio con los nombres").

## 2. Registrar un gasto (camino feliz)

```
Usuario: Pagué 180 lucas de herraje
Bot:     ✅ Gasto registrado
         🔨 Herrería · $180.000 · hoy
         ¿Lo imputo a algún patrón o caballo? Si no, queda como propio.
```

## 3. Audio con varios movimientos

```
Usuario: 🎤 "Le di 300 mil al Chino del sueldo, 40 para la comida de los
         chicos y 2 mil verdes al vete por la Pampa"
Bot:     ✅ Registré 3 movimientos:
         🧑‍🌾 Petiseros · $300.000 (Chino)
         🍖 Comida petiseros · $40.000
         💉 Veterinaria · USD 2.000 · la Pampa
         ¿Está todo bien? Si algo está mal decime qué.
```

## 4. Foto de comprobante

```
Usuario: 📷 [foto de transferencia]
Bot:     ✅ Transferencia de $520.000 a Forrajería San José (02/11)
         🌾 Lo puse en Alimentación. ¿Correcto?
```

## 5. Corrección

```
Usuario: No, eran dólares
Bot:     Corregido ✏️ USD 180 · Herrería
```

## 6. Ingreso

```
Usuario: Me pagó Martín 5 mil dólares por Hurlingham
Bot:     💵 Ingreso registrado
         🏇 Jugar · USD 5.000 · patrón Martín · torneo Hurlingham
```

## 7. Consulta

```
Usuario: ¿Cuánto gasté este mes?
Bot:     Noviembre (hasta hoy):
         $ 2.340.000 + USD 3.500
         Top 3: 🌾 Alimentación 38% · 🧑‍🌾 Petiseros 31% · 💉 Vete 14%
         Ver detalle 👉 [link]
```

## 8. Rendición al patrón

```
Usuario: Armame la rendición de Martín de octubre
Bot:     📄 Rendición octubre — Martín
         Gastos imputados: $1.850.000 + USD 2.000
         Reintegros recibidos: $1.000.000
         Saldo a cobrar: $850.000 + USD 2.000
         Link para mandarle 👉 [link] (o te paso el PDF)
```

## 9. Resumen automático (domingo a la noche / día 1 del mes)

```
Bot:     📊 Tu semana: gastaste $640.000 + USD 200 en 14 movimientos.
         Lo más grande: 🌾 alfalfa $260.000.
         Martín te debe $850.000 + USD 2.000.
```

## 10. Cuando falta info crítica

```
Usuario: Pagué al herrero
Bot:     ¿Cuánto le pagaste? 🔨
```

(Solo se repregunta el **monto**. Todo lo demás se infiere o queda vacío.)

## Casos borde a contemplar
- Mensajes que no son movimientos ("gracias", "jaja") → respuesta corta, no registrar.
- Mensaje ambiguo gasto/ingreso → preguntar con botones.
- Fecha pasada ("el viernes pagué…").
- Audio largo con muchos movimientos → resumir y pedir confirmación.
- Comprobante ilegible → pedir el monto.
- Usuario manda lo mismo dos veces → detectar duplicado.
