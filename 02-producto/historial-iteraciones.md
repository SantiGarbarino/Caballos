# Historial de iteraciones del mockup (22–27/10/2026)

> Qué pidió Santi en cada vuelta, qué se cambió y por qué. Sirve para no volver a proponer lo que ya se descartó.

## Vuelta 1 · Primer mockup

- Pedido: mockup para mostrarle al cuñado (polista). Empezar por **gastos, caballerizas y día**. Preguntas de definición:
  - **Persona**: profesional de alto handicap sin manager; el polista hace todo.
  - **~35 caballos**, con botón para agregar y alta por WhatsApp.
  - Datos **ficticios pero creíbles**, Argentina y exterior.
  - Mostrar **conversaciones de WhatsApp**: sí.
  - **SENASA** como sección en la ficha.
  - Marca "Un Programón".
  - **Vista simple para el encargado**.
- Se armó primero en un canvas de diseño (archivos Main, Encargado, WhatsApp). En el celular se veía en blanco ("Loading…"), así que **se rehízo como un HTML autónomo**. El canvas quedó obsoleto.

## Vuelta 2 · Feedback de Inicio, caballos y equipo

- Le gustaron Inicio, novedades y el plantel.
- Pidió y se hizo:
  - **Recordatorios por caballo** (por WhatsApp o desde la web).
  - **Visitas agendadas**.
  - **Tocar a alguien del equipo** y ver sus mensajes.
  - **Gastos por tipo**.
  - Prácticas en Día.
  - **Windsor (Inglaterra)** en vez de Florida, y **Sotogrande**.
  - "Encargado" pasa a **"piloto"**.
  - **Tareas de Tomás al piloto**.
- El piloto necesita **notificaciones** (web y WhatsApp: "el WhatsApp lo tiene en el bolsillo").

## Vuelta 3 · Marca y monedas

- "Un Programón" → **PROGRAMON**.
- Gastos: **no un solo total**, sino por moneda (US$, $, €).
- En Inicio, "Plata" → **"Gastos"**, con selector de rango de fechas. Los montos en distintas monedas, del mismo tamaño.
- **Sacar el "% vs mes pasado".**
- **La moneda es independiente del país.** Clasificar por **destino**: US$ 2.000 para el campo pagados desde Sotogrande son del Campo.
- "Tal cual, **ante la duda que pregunte**."

## Vuelta 4 · Compartir y consumo

- Se pasa el mockup por WhatsApp; se publicó como **link** (el archivo se veía en blanco en el celular).
- "Avena: se usan 3 por día": ¿de dónde sale? → **consumo configurable por caballeriza** (por caballo por día).
- **Pochola → Rockstar.**
- Más categorías: caballeriza (incluye comida de petiseros), tacos, cascos, monturas, indumentaria, y gastos del día a día (nafta, fletes de trailers). **Filtro por temporada.** Más creatividad en Día.
- Forma de trabajo: **se edita el borrador acá y se pasa al link cuando Santi dice "Dale, listo todo esto. Reemplazalo"**.

## Vuelta 5 · Rediseño de Gastos (1)

- "No me gusta nada cómo quedó el módulo de gastos… reformulalo todo" (UX, limpio).
- Santi no entendía cómo se formaban los totales: "US$ 14.200 de tacos" contra ítems de 540 + 600. Quiere **ver la foto o el audio de cada gasto**.
- Lista completa de gastos del polista (ver [industria](../01-mercado/industria-polo.md)). "Trailer y camión" = **fletes**.
- "Es el **módulo principal**… súper claro… no tiene que haber lugar a dudas."
- Resultado: **una sola lista** como fuente de verdad, taxonomía grupo › categoría, lugar, detalle con comprobante.

## Vuelta 6 · Día y análisis por módulo

- Gastos OK por ahora.
- En Día: **sacar el plan de chukkers**; mostrar **solo lo que ya pasó**; sacar "mañana tormenta…".
- Pidió un análisis exhaustivo por módulo: ¿hace falta "Hoy en la caballeriza"? ¿Hay una visualización de Inicio mejor que el plantel?
- Decisiones:
  - Los **botones de acción en las alertas no son viables** → se sacaron.
  - **Sacar el banner de WhatsApp.**
  - "Esta semana" está bien.
  - **Sacar los minutos de vareo.**
  - **Sacar las cantidades** de chukkers, vareos y prácticas, y la **pestaña Costos**.
- Se aplicó y se publicó en el link.

## Vuelta 7 · Día → Ingresos

- **Se elimina el módulo Día** y entra **Ingresos**: patrones, monto arreglado, pagos parciales, configurable por WhatsApp o desde la app.
- Se publicó en el link.

## Vuelta 8 · Diseño "Cancha de noche" (borrador aparte)

- ¿Una UI más innovadora, con colores y degradados? Se hizo en un **borrador aparte** (sin tocar el link).
- Feedback:
  - Le gustó.
  - Sacar la fecha abajo de PROGRAMON y el botón "(vista piloto)".
  - Probar la fuente Lexend en negrita para PROGRAMON → después Caveat en negrita → no gustó: **sacar "PROGRAMON" directamente** ("pondremos un logo cuando lo tengamos").
  - En "Por cobrar", los US$ y los € tenían colores distintos → **saludo en dorado y todos los números del mismo color** (blanco).
- "Perfecto, ahora sí actualizá el link."

## Vuelta 9 · Mejoras de producto (después del análisis de la idea)

- Santi aprobó implementar casi todo lo propuesto. Bajó la prioridad de algunos puntos:
  - **Piloto solo con notificaciones por WhatsApp** (sin vista web).
  - **Ficha con documentación oficial / SENASA**: más adelante.
- Se implementó:
  - «Quién ve tu cuenta».
  - Pagos fijos.
  - Gastos que cubre el patrón y reintegros.
  - Compra de caballos aparte.
  - Venta de caballos en Ingresos.
  - Resultado por temporada.
  - Exportar al contador.
  - Gastos cargados por Sofía.
  - Link del gasto a su chat.
  - Chats nuevos: alta de un caballo, pagos fijos, gasto que cubre el patrón, carga de un gasto.
- Se quitaron de la ficha la pestaña Papeles/SENASA y los KPIs. De Caballeriza salieron las visitas (pasaron a Inicio), los banners de ajuste/reponer y "pedir al proveedor". Al piloto web se le sacó Avisos y se lo dejó fuera del recorrido.

## Correcciones de Santi a la KB (2026-11-03, sesión 3)

No es una vuelta del mockup, pero cambia cosas que el mockup muestra:
- **Monedas**: de "siempre separadas, nunca se convierte" a **todo en US$** con conversión automática (pesos al blue del día; euros con cotización online o el bot pregunta).
- **Usuarios**: en la app, polista y **manager** (ven lo mismo). El resto de la organización (petiseros, piloto, puestero, familiares o asistentes) y los proveedores: **solo WhatsApp**, figura quién cargó. El contador no es usuario.
- **Cotización**: blue promedio entre compra y venta. La plata en el grupo se registra igual.
- **Patrón**: no existe para la plataforma.
- **WhatsApp**: bot en el grupo de la organización + chat privado para la plata; vete/herrero con varios clientes.
- **Recordatorios personales** («mañana haceme acordar»).
- **Caballos** desde Cría Polo (catálogo).
- **Sin tablas**: módulos con tableros.
- Nombre provisorio; producto nuevo, no Queiros.

## Vuelta 10 · Ajustes para la V1 (2026-11-03, borrador v9)

Santi aprobó la lista de 32 cambios (con ajustes). Se hizo en el **borrador** (el link compartible todavía no):
- **Todo en US$**: Inicio, Gastos (total, grupos, categorías, días), Ingresos y temporadas. Cada gasto en $ o € muestra la conversión en letra chica («$ 180.000 al dólar blue del 22/10 ($ 1.550, promedio compra y venta) = US$ 116»). Acuerdos en €: cobrado al euro del día de cada pago, lo que falta al de hoy con «≈».
- **Resultado por temporada** en una sola línea en US$ (ingresos, gastos y resultado).
- **«En qué se fue»** con una barrita fina por grupo y su % del total.
- **Equipo**: botón en Inicio → pantalla propia (entran a la app: polista y manager; cargan por WhatsApp: piloto, petiseros, puestero, familiar, veterinaria, herrero), mensajes de cada uno marcados «en el grupo» o «por privado», e **Invitar** por WhatsApp. Se sacó Equipo de Caballeriza y la hoja «Quién ve tu cuenta».
- **Manager** (ficticio: Nacho) visible: carga gastos, aparece en el grupo y tiene su chat.
- **Recordatorio personal** en «Lo que viene» (Vie 23, «llamar a Cacho…») y en el chat de recordatorios.
- Ficha del caballo con pestaña **Datos** (padre, madre, criador, nacimiento, registro, microchip, marca, partidos jugados), sin nombrar la fuente.
- **Chats**: grupo de la organización (7 personas + bot, con un gasto que se registra igual), manager, piloto (solo tareas), Sofía (gasto en pesos convertido), veterinaria por privado con varios clientes, recordatorio personal; montos en US$.
- **Se eliminó**: la vista web del piloto, el contador y la persona que lleva las cuentas como usuarios de la app.
- **Se corrigieron** las inconsistencias: «Día» en el chat, consulta de veterinario (ahora US$ 2.206), Windsor (US$ 7.300), cierre del día sin corralón ni chukkers, herrero con 3 caballos, Sotogrande = agosto en todos lados (el pasaje Londres–Málaga pasó al 1/8). Se sumó el gasto de US$ 600 de veterinario de hoy para que coincida con el chat.

## Errores de consistencia que se corrigieron

- **Días de la semana**: el 22/10/2026 es jueves. Se corrigieron las fechas (el herrero quedó el jueves 29).
- **Totales que no coincidían con los ítems** → una sola lista.
- **Números iguales por casualidad** (Ingresos Inglaterra = Por cobrar) → el pago de La Ensenada pasó a US$ 30.000.

## Inconsistencias que todavía tiene el mockup (corregir en la próxima vuelta)

- [ ] El chat de Ramón dice "6 vareos en «Día»" (Día ya no existe).
- [ ] Consulta "veterinario este mes = $ 1.950.000" no coincide con la lista de octubre (ARS 320.000 + US$ 2.000).
- [ ] Cierre del día: "ya le pediste 40 bolsas al corralón" (se sacó pedir al proveedor) y "Morena llega a 6 chukkers en la semana" (se sacaron las cantidades de chukkers).
- [ ] Inicio dice "Cacho: Chiquita, Rubia, Malcriada y 3 más", pero el chat de agenda agenda 3 caballos.
- [ ] Sotogrande: en Gastos la temporada es "agosto 2026"; en Ingresos dice "julio y agosto".
- [ ] La vista web del piloto (fuera del recorrido) muestra "Vista de Tomás" y la palabra PROGRAMON.
