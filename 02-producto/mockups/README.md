# Mockup PROGRAMON

Mockup navegable para celular, armado por Santi con Claude entre el 22 y el 27/10/2026. **Está en construcción**: Santi lo sigue ajustando y adjunta la versión final cuando la tenga. Todos los datos (Tomás, su equipo, caballos, patrones, montos) son **ficticios** y son un ejemplo, no definen el ICP. Es la referencia de producto: si algo de la KB lo contradice, revisar el [historial](../historial-iteraciones.md) y las [decisiones](../../00-vision/decisiones.md).

## Dónde está

| Qué | Link / archivo | Estado |
|---|---|---|
| **Link para compartir** (WhatsApp, cuñado, polistas) | https://claude.ai/artifact/3cZKSNp1tywiqWrFzFBzJR · título "PROGRAMON" | Público con link · versión 7 · igual al borrador |
| **Borrador** (donde se edita) | https://claude.ai/artifact/HMnQoyKLWcYgtCTQ8oGmsS · título "PROGRAMON Borrador" | Privado · es la versión maestra |
| Variante de diseño "Cancha de noche" | https://claude.ai/artifact/KoAUBpqUkvF8TF8pNNyxKk | Ya integrada en borrador y link |
| Canvas de diseño original (Main, Encargado, WhatsApp) | https://claude.ai/artifact/7rX9atNBuh28Mijf6CSY6Q | **Obsoleto**, no se mantiene (en el celular se veía en blanco) |
| Copia en este repo | [`programon.html`](programon.html) | Snapshot del 27/10/2026 (= link v7). Se abre con cualquier navegador |
| Capturas | [`capturas/`](capturas/) | Generadas del snapshot a 390 px de ancho |
| Datos ficticios | [`dataset-ficticio.md`](dataset-ficticio.md) | Caballos, gastos, acuerdos |

> Los links de claude.ai son artifacts de la cuenta de Santi. El link público lo puede abrir cualquiera que lo tenga.

## Cambios pendientes en el mockup por las decisiones del 2026-11-03

- [ ] Totales en **US$** (Inicio, Gastos, Ingresos, temporadas) y detalle de la conversión en letra chica en cada gasto en $ o €.
- [ ] «Quién ve tu cuenta»: polista + manager en la app; Sofía, piloto, petiseros, puestero y proveedores como "cargan por WhatsApp"; sacar a Estudio Ruiz.
- [ ] Mostrar al **manager** como usuario (ej. gastos y novedades cargados por el manager).
- [ ] Chats: grupo de la organización vs. privado; vete con varios clientes; recordatorio personal; gasto en pesos convertido.
- [ ] Agregar caballo desde el catálogo de Cría Polo.
- [ ] Nombre provisorio (PROGRAMON).

## Forma de trabajo

1. Se edita el **borrador** en Claude.
2. El **link compartible** se actualiza solo cuando Santi dice: *"Dale, listo todo esto. Reemplazalo."*
3. Después de cada reemplazo, actualizar `programon.html`, las capturas y el [historial](../historial-iteraciones.md) en este repo.

## Detalles técnicos del mockup

- Un solo HTML autónomo (~132 KB): JavaScript sin frameworks, render por `innerHTML`, eventos delegados con `data-act` / `data-v` y un objeto de estado `S`.
- Hojas inferiores (*sheets*) con fondo oscurecido.
- Google Fonts: Instrument Serif, Manrope, Lexend. Colores como tokens en `:root`.
- Fuente única de datos de gastos: `LEDGER` (todo total sale de ahí). Stock: `STOCK` + consumo `S.cons`. Ingresos: `S.acuerdos`. Equipo: `PERS`. Chats de demo: `CHATS`.
- Hay una vista **WhatsApp** con 9 chats de demo (ver [flujos](../flujos-whatsapp.md)) y una vista **piloto** que quedó fuera del recorrido.

## Índice de capturas

| Pantalla | Captura |
|---|---|
| Inicio | [01](capturas/01-inicio.png) · Quién ve tu cuenta [02](capturas/02-acceso.png) · Agendar [03](capturas/03-agendar.png) |
| Caballos | Lista [04](capturas/04-caballos.png) · Agregar [05](capturas/05-caballo-agregar.png) · Ficha Rockstar [06](capturas/06-ficha-rockstar.png) · Salud [07](capturas/07-ficha-rockstar-salud.png) · Recordatorio [08](capturas/08-recordatorio.png) · Ficha Patria [09](capturas/09-ficha-patria.png) |
| Caballeriza | Pilar [10](capturas/10-caballeriza-pilar.png) · Avena [11](capturas/11-insumo-avena.png) · Consumo [12](capturas/12-consumo.png) · Campo [13](capturas/13-caballeriza-campo.png) · Pedro [14](capturas/14-persona-pedro.png) · Don Aníbal [15](capturas/15-persona-anibal.png) |
| Gastos | Inicio [16](capturas/16-gastos.png) · Período [17](capturas/17-gastos-rango.png) · Lugar [18](capturas/18-gastos-lugar.png) · Grupo Caballos [19](capturas/19-gastos-grupo-caballos.png) · Veterinario [20](capturas/20-gastos-cat-veterinario.png) · Todos [21](capturas/21-gastos-todos.png) · Pagos fijos [22](capturas/22-gastos-fijos.png) · Exportar [23](capturas/23-gastos-export.png) · Temporada Inglaterra [24](capturas/24-gastos-temporada-inglaterra.png) · Traslados [24b](capturas/24b-gastos-grupo-traslados.png) · Flete que cubre el patrón [25](capturas/25-gasto-flete-cubre.png) · Tacos con foto [25b](capturas/25b-gasto-tacos.png) · Herraje con audio [25c](capturas/25c-gasto-herraje-audio.png) |
| Ingresos | Por cobrar [26](capturas/26-ingresos.png) · Northfield [27](capturas/27-acuerdo-northfield.png) · Registrar pago [28](capturas/28-registrar-pago.png) · Por temporada [29](capturas/29-ingresos-temporadas.png) · Les Pins [29b](capturas/29b-acuerdo-lespins.png) · Venta Halcona [29c](capturas/29c-venta-halcona.png) · Valle Alto [29d](capturas/29d-acuerdo-valle-alto.png) · Nuevo patrón [30](capturas/30-ingresos-nuevo.png) · Nueva venta [31](capturas/31-ingresos-nuevo-venta.png) |
| WhatsApp | [Ramón](capturas/wa-ramon.png) · [Pedro](capturas/wa-pedro.png) · [Tomás](capturas/wa-tomas.png) · [Recordatorios](capturas/wa-agenda.png) · [Acuerdos](capturas/wa-ingresos.png) · [Cubre el patrón](capturas/wa-reintegro.png) · [Pagos fijos](capturas/wa-fijos.png) · [Carga de gasto](capturas/wa-gasto.png) · [Alta de caballo](capturas/wa-alta.png) |
| Piloto (fuera del recorrido) | [40](capturas/40-piloto-web.png) |
