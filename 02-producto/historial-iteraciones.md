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
