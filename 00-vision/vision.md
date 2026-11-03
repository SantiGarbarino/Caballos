# Visión, problema y propuesta de valor

> Actualizado 2026-11-03 con todo lo definido en las sesiones de producto del 22 al 27/10/2026 (mockup PROGRAMON). Lo que no está validado con usuarios reales sigue marcado **[HIPÓTESIS]**.

## Nombre y relación con Queiros

- **Nombre: no definido.** PROGRAMON es el **nombre provisorio** que usa el mockup.
- **Es un producto totalmente nuevo.** No es Queiros ni una marca de Queiros, y no se mezcla **nada** de Queiros (código, marca, producto ni restricciones). Lo que traemos es el **know-how** de haberlo construido y el mismo equipo: Santi, Mati y Mauro. Ver [aprendizajes de Queiros](../03-tecnico/aprendizajes-queiros.md).
- Se parecen en la idea (WhatsApp como interfaz, IA y una web app mobile-first con módulos), pero son productos distintos.
- Es un **proyecto paralelo**: si el mercado responde, se encara de lleno.
- **Logo: pendiente.** En la app no se muestra la palabra PROGRAMON en el header (se probó en Lexend negrita y en Caveat y no gustó). Cuando haya logo, la palabra aparece solo en la pantalla de carga (*splash*, pieza de marketing futura).

## En una frase

**Toda la organización de polo en el celular, cargada por WhatsApp**: el polista, su manager, el piloto, los petiseros y los proveedores (vete, herrero) mandan audios, fotos y mensajes como ya lo hacen hoy (en el grupo de la organización o por privado al bot), y PROGRAMON lo ordena en gastos, cobros, caballos y caballeriza.

## Tesis: el software del mundo del caballo

- **Visión = el mundo del caballo. Entrada = un subsector.** Arrancamos por el **polo** y después vamos a **haras / cría**, **carrera**, **criollos** y **salto**.
- **[HIPÓTESIS]** Haras y cría pueden ser un mercado más grande que el polo profesional (más caballos por establecimiento, más procesos: reproducción, ET, clonación, ICSI, doma, ventas, exportación).
- **Ángulo regulatorio:** SENASA está digitalizando la libreta sanitaria y el pasaporte equino y prevé "aplicaciones autorizadas" (Res. 831/2026). Ser la ficha digital oficial del caballo puede ser el foso del negocio. **Queda para más adelante**. Ver [regulación SENASA](../01-mercado/regulacion-senasa.md).

## El problema

El polista profesional maneja un **negocio** sin tratarlo como tal. Tiene decenas de caballos repartidos entre la caballeriza, el campo y otros países. Tiene petiseros, piloto, puestero, alquileres acá y afuera, fletes, temporadas y acuerdos con varios patrones. Paga casi todo en efectivo o transferencia, en varias monedas y sin registro.

El cliente objetivo lo describe así: un rubro que **mueve mucha plata y no tiene nada de tecnología**.

Dolores **[HIPÓTESIS, salvo que se indique]**:

1. **No sabe cuánto gasta ni en qué.** Es el dolor principal según Santi, y por eso **Gastos es el módulo central**. Tiene que ser súper claro: no puede haber lugar a dudas de cómo se forma cada número.
2. **Gasta en varios lugares y en varias monedas.** La gran mayoría de los gastos son en dólares, pero hay gastos en pesos (nafta, comida de los petiseros) y en euros. Quiere ver todo en **dólares** sin tener que averiguar el tipo de cambio. La moneda **no** depende del país: puede pagar en dólares un gasto del campo mientras está en Sotogrande.
3. **No tiene claro qué le deben.** Hay acuerdos con patrones por temporada (montos grandes, pagos parciales), ventas de caballos cobradas en cuotas y gastos que el patrón cubre y hay que reintegrar.
4. **Muchos caballos en muchos lugares.** Hay que saber cuáles juegan, cuáles están en el campo, en el exterior o en recuperación, qué le pasa a cada uno y qué hay pendiente (herraje, veterinaria, vacunas).
5. **La caballeriza se queda sin insumos.** Avena, fardos, viruta y balanceado se terminan sin aviso.
6. **El equipo reporta por WhatsApp y la información se pierde.** El manager, el piloto, los petiseros, el puestero, el veterinario y el herrero mandan audios todo el día al grupo de la organización; nadie los ordena.
7. **No usa la computadora.** Vive en el celular y en WhatsApp.

## La solución

```
Grupo de WhatsApp de la organización          Chat privado con el bot
(manager, polista, vete, herrero, petiseros)   (polista o manager: plata)
   │  audio, foto (factura, remito, comprobante, papeles), mensaje
   ▼
IA estructura → gasto · pago de patrón · venta · novedad de caballo ·
                vareo/herraje · stock · recordatorio · visita · consulta
   │  (si tiene una duda, PREGUNTA: nunca adivina destino ni categoría)
   ▼
Confirmación por WhatsApp   (montos en $ o € → US$ con la cotización del día)
   ▼
Web app mobile (PWA) para el polista y el manager:
Inicio · Caballos · Caballeriza · Gastos · Ingresos
   ▼
Avisos salientes por WhatsApp: tareas del piloto (7:00), pagos fijos el día
que vencen, recordatorios, cierre del día (20:00)
```

### Principios de producto (vigentes)

1. **WhatsApp es la interfaz de carga.** La app también permite cargar (botones Agregar, Nuevo, Agendar, Recordatorio), pero siempre muestra el atajo de WhatsApp primero.
2. **La app es para mirar y decidir.** Mobile-first, pensada para el celular. No hay versión de escritorio.
3. **Ante la duda, pregunta.** Si la IA no sabe el destino (lugar), la categoría o los caballos, **pregunta**. Nunca adivina. (Decisión explícita de Santi: "tal cual, ante la duda que pregunte".)
4. **Cada número se explica.** Todo total es la suma de los ítems que se ven debajo. Cada gasto muestra lo que lo generó: la foto del comprobante si hay, y si no, el audio (con transcripción) o el mensaje; y quién lo cargó.
5. **Todo en dólares, sin fricción.** Un gasto en pesos se convierte solo al dólar blue del día (promedio entre compra y venta); el bot no le pregunta el tipo de cambio al polista. En el detalle, en letra chica: «$ 800.000 al dólar blue del 22/10 ($ 1.550) = US$ 516». Euros: cotización online o, si no hay, el bot pregunta.
6. **Sin ruido y sin tablas.** Módulos con tableros, tarjetas y listas; nada de planillas ni tablitas. Nada de KPIs decorativos, minutos de vareo, "% vs mes anterior" ni botones de acción en las alertas. UX limpia y simple (preferencia explícita de Santi).
7. **Hablamos como habla el polo.** Petisero, piloto, puestero, vareo, herraje, chukker, patrón, invernada.
8. **Privacidad de la plata.** En la app, los montos los ven solo el polista y su manager. En general la plata se manda por **chat privado** con el bot; si se habla de precios en el grupo, se registra igual. Los usuarios de solo WhatsApp no entran a la app.

## Propuesta de valor por actor

| Actor | Qué gana |
|---|---|
| **Polista profesional** (comprador y usuario) | Sabe cuánto gastó (en dólares), en qué y dónde; cuánto le deben y quién; qué pasa con cada caballo; para cuántos días le alcanza el stock; sin abrir una computadora |
| **Manager** (mano derecha en organizaciones grandes; usuario) | Ve **lo mismo** que el polista. Registra todo el día a día (caballeriza, stock, lo que habla con el vete y el herrero, cada yegua) mandándolo por WhatsApp. Muchas veces es el que más usa el producto |
| **Miembros de la organización de solo WhatsApp** (ej. un familiar o asistente que lo ayuda con gastos y compras) | Sin acceso a la app. Le mandan gastos o novedades al bot y quedan registrados con su nombre |
| **Piloto** (el mayor de los petiseros) | Sin acceso a la app. Recibe tareas y avisos por WhatsApp y las tacha respondiendo |
| **Petiseros / puestero** | Sin acceso a la app. Reportan por audio en el grupo, como hoy (ej. "la yegua no comió" → alerta en la plataforma, "la cargó Ramón") |
| **Veterinario / herrero** (trabajan para varios polistas) | Sin acceso a la app. Mandan novedades al grupo de cada cliente; si escriben por privado, el bot pregunta para qué cliente es |
| **Contador** | No es usuario: recibe el export (Excel/PDF con fotos) por mail |
| **Haras / criador** (fase posterior) | Stock por categoría, reproducción, doma, ventas, sanidad y documentación |

## Visión a largo plazo

1. **Polo profesional**: gastos, cobros, caballos (con datos de la app Polo Argentino), caballeriza (lo que muestra el mockup).
2. **Ficha digital del caballo** con documentación sanitaria (libreta sanitaria digital, pasaporte equino, microchip). Eventualmente **habilitación de SENASA** como "aplicación autorizada".
3. **Haras y cría**, después **carrera, criollos y salto**.
4. **La capa de datos del ecosistema**: veterinarios, herreros, transportistas, forrajerías, compraventa y exportación de caballos.
