# Visión, problema y propuesta de valor

> Actualizado 2026-11-03 con todo lo definido en las sesiones de producto del 22 al 27/10/2026 (mockup PROGRAMON). Lo que no está validado con usuarios reales sigue marcado **[HIPÓTESIS]**.

## Marca y relación con Queiros

- **PROGRAMON** es la **marca vertical** para el mundo de los caballos (antes se pensó como "Un Programón"; quedó **PROGRAMON**, en mayúsculas).
- **Queiros es el motor**: la plataforma WhatsApp → IA → datos estructurados → tablero que ya construimos. PROGRAMON es el producto de cara al polista, construido sobre ese motor. Ver [reuso de Queiros](../03-tecnico/reuso-queiros.md).
- Por qué un vertical: Queiros multi-industria complica lo comercial y el producto. Queremos un ICP concreto. Mati, Mauro y Santi están de acuerdo en anicharse en caballos.
- **Logo: pendiente.** En la app no se muestra la palabra PROGRAMON en el header (se probó en Lexend negrita y en Caveat y no gustó). Cuando haya logo, la palabra aparece solo en la pantalla de carga (*splash*, pieza de marketing futura).

## En una frase

**Toda la organización de polo en el celular, cargada por WhatsApp**: el polista, el piloto y los petiseros mandan audios, fotos y mensajes como ya lo hacen hoy, y PROGRAMON lo ordena en gastos, cobros, caballos y caballeriza.

## Tesis: el software del mundo del caballo

- **Visión = el mundo del caballo. Entrada = un subsector.** Arrancamos por el **polo** y después vamos a **haras / cría**, **carrera**, **criollos** y **salto**.
- Referencia: **Pensai** (Joaco, amigo de Santi) hace lo mismo para ganadería (vacas) con un bot de WhatsApp. Ver [análisis de viabilidad](analisis-viabilidad.md).
- **[HIPÓTESIS]** Haras y cría pueden ser un mercado más grande que el polo profesional (más caballos por establecimiento, más procesos: reproducción, ET, clonación, ICSI, doma, ventas, exportación).
- **Ángulo regulatorio:** SENASA está digitalizando la libreta sanitaria y el pasaporte equino y prevé "aplicaciones autorizadas" (Res. 831/2026). Ser la ficha digital oficial del caballo puede ser el foso del negocio. **Queda para más adelante**. Ver [regulación SENASA](../01-mercado/regulacion-senasa.md).

## El problema

El polista profesional maneja un **negocio** sin tratarlo como tal. Tiene decenas de caballos repartidos entre la caballeriza, el campo y otros países. Tiene petiseros, piloto, puestero, alquileres acá y afuera, fletes, temporadas y acuerdos con varios patrones. Paga casi todo en efectivo o transferencia, en varias monedas y sin registro.

El cliente objetivo lo describe así: un rubro que **mueve mucha plata y no tiene nada de tecnología**.

Dolores **[HIPÓTESIS, salvo que se indique]**:

1. **No sabe cuánto gasta ni en qué.** Es el dolor principal según Santi, y por eso **Gastos es el módulo central**. Tiene que ser súper claro: no puede haber lugar a dudas de cómo se forma cada número.
2. **Gasta en varias monedas y en varios lugares.** Paga en US$, $, € y £, en Pilar, en el campo, en Inglaterra y en España. La moneda **no** depende del país: puede pagar en dólares un gasto del campo mientras está en Sotogrande.
3. **No tiene claro qué le deben.** Hay acuerdos con patrones por temporada (montos grandes, pagos parciales), ventas de caballos cobradas en cuotas y gastos que el patrón cubre y hay que reintegrar.
4. **Muchos caballos en muchos lugares.** Hay que saber cuáles juegan, cuáles están en el campo, en el exterior o en recuperación, qué le pasa a cada uno y qué hay pendiente (herraje, veterinaria, vacunas).
5. **La caballeriza se queda sin insumos.** Avena, fardos, viruta y balanceado se terminan sin aviso.
6. **El equipo reporta por WhatsApp y la información se pierde.** El piloto, los petiseros y el puestero mandan audios todo el día; nadie los ordena.
7. **No usa la computadora.** Vive en el celular y en WhatsApp.

## La solución

```
Polista · piloto · petiseros · puestero · quien lleva las cuentas
   │  audio, foto (factura, remito, comprobante, papeles), mensaje
   ▼
IA estructura → gasto · pago de patrón · venta · novedad de caballo ·
                vareo/herraje · stock · recordatorio · visita · consulta
   │  (si tiene una duda, PREGUNTA: nunca adivina destino ni categoría)
   ▼
Confirmación por WhatsApp
   ▼
Web app mobile (PWA): Inicio · Caballos · Caballeriza · Gastos · Ingresos
   ▼
Avisos salientes por WhatsApp: tareas del piloto (7:00), pagos fijos el día
que vencen, recordatorios, cierre del día (20:00)
```

### Principios de producto (vigentes)

1. **WhatsApp es la interfaz de carga.** La app también permite cargar (botones Agregar, Nuevo, Agendar, Recordatorio), pero siempre muestra el atajo de WhatsApp primero.
2. **La app es para mirar y decidir.** Mobile-first, pensada para el celular. No hay versión de escritorio.
3. **Ante la duda, pregunta.** Si la IA no sabe el destino (lugar), la categoría o los caballos, **pregunta**. Nunca adivina. (Decisión explícita de Santi: "tal cual, ante la duda que pregunte".)
4. **Cada número se explica.** Todo total es la suma de los ítems que se ven debajo. Cada gasto muestra su comprobante (foto, audio con transcripción o mensaje) y quién lo cargó.
5. **Monedas separadas, siempre.** Nunca se convierte ni se suma US$ con $ o €. No hay totales combinados.
6. **Sin ruido.** Nada de KPIs decorativos, minutos de vareo, "% vs mes anterior" ni botones de acción en las alertas. UX limpia y simple (preferencia explícita de Santi).
7. **Hablamos como habla el polo.** Petisero, piloto, puestero, vareo, herraje, chukker, patrón, invernada.
8. **Privacidad de la plata.** Los montos los ven solo las personas que el dueño habilita. Los patrones nunca ven la cuenta. El piloto no ve plata.

## Propuesta de valor por actor

| Actor | Qué gana |
|---|---|
| **Polista profesional** (comprador y usuario principal) | Sabe cuánto gastó, en qué, dónde y en qué moneda; cuánto le deben y quién; qué pasa con cada caballo; para cuántos días le alcanza el stock; sin abrir una computadora |
| **Quien lleva las cuentas** (pareja, familiar, asistente) | Ve y carga gastos e ingresos sin pedirle tickets al polista |
| **Contador** | Recibe el export (Excel/PDF con fotos) por mail |
| **Piloto** (encargado de la caballeriza) | Recibe sus tareas y avisos por WhatsApp y las tacha respondiendo; no tiene que abrir ninguna app |
| **Petiseros / puestero** | Reportan por audio como hoy; se les reconoce lo que hacen |
| **Haras / criador** (fase posterior) | Stock por categoría, reproducción, doma, ventas, sanidad y documentación |

## Visión a largo plazo

1. **Polo profesional**: gastos, cobros, caballos, caballeriza (lo que muestra el mockup).
2. **Ficha digital del caballo** con documentación sanitaria (libreta sanitaria digital, pasaporte equino, microchip). Eventualmente **habilitación de SENASA** como "aplicación autorizada".
3. **Haras y cría**, después **carrera, criollos y salto**.
4. **La capa de datos del ecosistema**: veterinarios, herreros, transportistas, forrajerías, compraventa y exportación de caballos.
