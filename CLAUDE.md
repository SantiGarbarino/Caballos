# Instrucciones para agentes (Claude y otros)

Este repo es el **brain / knowledge base** del proyecto Caballos. El producto se llama provisoriamente **PROGRAMON** (nombre no definido). Es un **producto nuevo**, no es Queiros: gestión de la organización del polista (y luego haras y el resto del mundo del caballo) con WhatsApp como interfaz y una web app mobile (PWA).

## Al trabajar en este repo

1. **Leé primero** `README.md`, `00-vision/vision.md`, `00-vision/decisiones.md` y `00-vision/preguntas-abiertas.md` para tener el contexto vigente.
2. **Idioma y tono**: español rioplatense. Usá la jerga del polo y de los caballos tal como figura en `01-mercado/glosario.md` (petisero, petiso, chukker, patrón, organización, herraje, haras, etc.). Si aparece un término nuevo, agregalo al glosario.
3. **Actualizá, no dupliques**: si la info nueva pertenece a un doc existente, editá ese doc. Creá archivos nuevos solo si no hay dónde ponerlo, y enlazalo desde el `README.md` de la raíz.
4. **Decisiones**: toda decisión (de producto, técnica, comercial) va a `00-vision/decisiones.md` con fecha (AAAA-MM-DD), contexto, decisión y porqué.
5. **Preguntas abiertas**: lo que falta definir va a `00-vision/preguntas-abiertas.md`. Cuando se resuelve, se tacha/mueve.
6. **Hipótesis vs. validado**: marcá **[HIPÓTESIS]** lo que suponemos y **[VALIDADO]** lo que confirmamos con entrevistas o datos (citando la fuente: "entrevista a polista 4 goles, 2026-11-10").
7. **CHANGELOG**: anotá cada sesión de trabajo relevante en `CHANGELOG.md` (fecha + qué cambió).
8. **Principio rector del producto**: el usuario es un polista que *no usa computadora*. Todo se diseña **WhatsApp-first y mobile-first**. Si una feature requiere desktop o un formulario largo, está mal planteada.
9. **Queiros: solo know-how.** Es un producto totalmente nuevo. **No mezclar nada de Queiros**: ni código, ni marca, ni sus restricciones (si algo se sacó de Queiros, acá puede existir). Lo único que se comparte es el equipo y lo aprendido. Ver `03-tecnico/aprendizajes-queiros.md`.
10. **Reglas de producto que no se discuten sin Santi** (ver `00-vision/decisiones.md`): ante la duda el bot **pregunta** (pero **nunca** el tipo de cambio de los pesos); **todo se muestra en US$**: pesos al dólar blue del día automático (promedio compra/venta), con el detalle de la conversión en letra chica; euros con cotización online o, si no hay, se pregunta; sin "% vs mes anterior"; los gastos se clasifican por **destino (lugar)**; **todo total es la suma de los ítems visibles**; cada gasto muestra su foto o, si no hay, el audio o mensaje que lo generó; UX limpia **sin tablas** (módulos con tableros), sin KPIs decorativos ni botones de acción en alertas; **owners**: quien crea la organización (polista o manager) y a quien le dé todos los accesos; los owners invitan y **configuran qué ve cada usuario** (por defecto, todos los que no son owners son **solo WhatsApp**; se puede habilitar una parte de la app eligiendo **secciones y qué caballos** —todos, de un lugar o algunos—; Gastos e Ingresos solo owners, nunca proveedores); el bot **nunca** carga una charla o una pregunta; los proveedores **no registran gastos** (cargan el trabajo y el bot les pregunta a los owners); el resto de la organización (ej. piloto, petiseros, puestero, un familiar o asistente) y los proveedores son **usuarios de solo WhatsApp**: cargan por el bot, figura quién lo cargó, nunca entran a la app; el **patrón no existe** para la plataforma; bot en el **grupo de WhatsApp** y en privado; la plata va en general por privado, pero si se habla en el grupo **se registra igual**.
11. **Antes de proponer algo nuevo**, revisá `02-producto/historial-iteraciones.md`: muchas cosas ya se probaron y se sacaron (módulo Día, pestaña Costos, minutos de vareo, plantel en Inicio, etc.).
12. **Mockup**: la referencia es `02-producto/mockups/`. Está en construcción: los datos (Tomás, sus caballos, patrones) son **ficticios** y no definen el ICP. La **referencia para el desarrollo es el borrador más reciente**, `programon-borrador.html` (v11); `programon.html` es el snapshot del link compartible (v7). Se edita el borrador en Claude y el link compartible se actualiza solo cuando Santi lo pide. Si el borrador cambia, actualizá `programon-borrador.html` y el historial; si cambia el link, `programon.html` y las capturas.
13. **Cuando Santi pide análisis de una idea**: riesgos y preguntas difíciles primero, sin suavizar.
14. **No personalizar los usuarios.** En los documentos de producto, visión, datos y GTM se habla de **roles** (polista, manager, piloto, petisero, puestero, familiar o asistente, veterinario, herrero), nunca de personas con nombre. Los nombres (Tomás, Pedro, la Dra. Ibarra…) son solo datos ficticios del mockup y viven en `02-producto/mockups/`. Cada polista tiene su **organización**: una mini organización con la gente que trabaja para él y quiere registrar todo.

## Equipo

- **Santi** (Santiago Garbarino) — Lic. en Administración y Sistemas (ITBA)
- **Mati** (Matías) — Lic. en Administración y Sistemas (ITBA)
- **Mauro** — Ingeniero Informático (ITBA)

Roles en este proyecto: ver `04-plan/plan-ejecucion.md`.
