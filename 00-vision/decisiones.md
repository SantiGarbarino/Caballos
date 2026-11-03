# Log de decisiones

Formato: fecha · decisión · contexto y porqué · quién. Las más nuevas arriba.

> Las decisiones de las sesiones de producto del **22 al 27/10/2026** (Santi con Claude, construyendo el mockup PROGRAMON) se registraron el 2026-11-03. Cuando se sabe el día exacto, se indica. Para el detalle de qué se cambió en cada vuelta del mockup ver [historial de iteraciones](../02-producto/historial-iteraciones.md).

---

## 2026-11-03

### La KB en GitHub refleja lo charlado en las sesiones de producto
- Si algo de la KB contradecía lo decidido en las sesiones 22–27/10, **manda lo decidido en las sesiones**. Se reescribieron visión, PRD, módulos, flujos, modelo de datos, plan y GTM.
- **Quién:** Santi.

## Sesiones 22–27/10/2026 · Estrategia

### Vertical = mundo del caballo; entrada = polo; después haras/cría
- **Porqué:** Queiros multi-industria complica venta y producto. El rubro mueve mucho dinero y no tiene tecnología. La red de Santi está en el polo. Haras/cría puede ser el mercado más grande.
- **Quién:** Santi, Mati y Mauro (ya lo hablaron entre los tres).

### Queiros es el motor, PROGRAMON es la marca vertical
- Nombre elegido por Santi: **PROGRAMON** (antes "Un Programón"). Logo pendiente.

### Validar primero con el mockup; no testear con el producto actual de Queiros
- **Porqué:** el ICP es muy sensible a algo feo o engorroso. Primero mockup, después una versión web para celular simple e intuitiva. SENASA y otras funciones se suman de a poco.

### El onboarding queda fuera por ahora
- "No nos metamos con el onboarding todavía, que vean directo la versión final." La idea discutida está en [preguntas abiertas](preguntas-abiertas.md).

### Ficha digital oficial del caballo / habilitación SENASA: más adelante
- Le interesa a Santi como diferencial (digitalizar las fichas que hoy son de papel). Se posterga para no frenar la validación del núcleo (gastos).

## Sesiones 22–27/10/2026 · Producto

### Formato: web app mobile instalable (PWA), no app nativa
- **Porqué:** se comparte por link de WhatsApp, no pasa por tiendas y se itera rápido. Queiros hoy no tiene PWA: hay que construirla.

### Persona del mockup: profesional de alto handicap sin manager
- El polista hace todo él mismo. Tiene ~35 caballos, todo ficticio pero creíble, con operación en Argentina y en el exterior. Ver [segmentos y personas](../01-mercado/segmentos-y-personas.md).

### Cinco módulos: Inicio · Caballos · Caballeriza · Gastos · Ingresos
- El módulo **Día** existió y se **eliminó**; su lugar lo ocupó **Ingresos**.
- **Gastos es el módulo principal**: el dolor número uno. Tiene que ser súper claro y no dejar lugar a dudas.

### Ante la duda, el bot pregunta
- Nunca adivina el destino ni la categoría. Ejemplo: "Le pagué 600 dólares al veterinario" → "¿Para qué caballos es: Pilar, el campo o Windsor?".

### Monedas siempre separadas; nunca se convierte
- Totales por moneda (US$, $, €; £ en Ingresos). No hay total combinado. No hay "+X% vs mes anterior" (se pidió sacarlo).
- La **moneda es independiente del lugar**: se puede pagar en US$ algo del campo estando en Sotogrande.

### Los gastos se clasifican por destino (lugar), no por dónde estaba el polista
- Ejemplo de Santi: US$ 2.000 para el campo pagados desde Sotogrande cuentan como **Campo**.
- Veterinaria "afuera" y comida "afuera" no son categorías aparte: son la misma categoría con otro **lugar**.

### Una sola lista de gastos como fuente de verdad
- **Porqué:** en una versión anterior los totales no coincidían con los ítems (US$ 14.200 de tacos contra 540 + 600 visibles) y Santi no entendía cómo se formaban. Ahora todo total es la suma de los gastos visibles para el período y el lugar elegidos.

### Taxonomía de gastos por grupo › categoría
- Definida a partir de la lista que dio Santi. Ver [módulo de gastos e ingresos](../02-producto/modulo-gastos-ingresos.md). "Trailer y camión" contratados son **Fletes de caballos**.

### Compra de caballos va aparte (inversión)
- Se ve como grupo propio en Gastos y **no** entra en el resultado por temporada.

### Ingresos = acuerdos con patrones + ventas de caballos + reintegros
- Por cobrar = acordado − cobrado + gastos que cubre el patrón pendientes de reintegro.
- Configurable por WhatsApp o desde la app.

### El piloto solo usa WhatsApp
- Le llegan tareas y avisos por WhatsApp y las tacha respondiendo. **No necesita vista web** (decisión de Santi del 27/10). En el mockup se usa "piloto" en lugar de "encargado".

### Inicio informativo, sin botones de acción en las alertas
- **Porqué:** Santi dijo que los botones de acción en las alertas no son viables. Las alertas abren la ficha, el insumo o la lista.

### Se sacaron: KPIs, minutos de vareo, cantidades de chukkers/vareos/prácticas, pestaña Costos, pestaña Papeles/SENASA, plantel en Inicio, "Hoy en la caballeriza", banner de WhatsApp, plan de chukkers
- **Porqué:** ruido. El polista no necesita esos números; ensucian la pantalla.

### Consumo de stock configurable por caballeriza
- Los días que alcanza un insumo salen de **consumo por caballo por día × caballos en ese lugar ÷ tamaño del envase**. Santi preguntó de dónde salía "se usan 3 por día" y se hizo explícito y editable.

### Pochola pasa a llamarse Rockstar
- Pedido de Santi (el id interno del mockup sigue siendo `pochola`).

### Lugares del exterior: Windsor (Inglaterra) y Sotogrande (España)
- Reemplazan a Florida/Wellington como temporadas del mockup. Wellington queda como acuerdo futuro (Palm Ridge 2027).

### Diseño "Cancha de noche"
- Degradado verde oscuro con dorado y fondo crema. El saludo va en dorado y **todos los números en blanco y del mismo tamaño** (antes los US$ y € tenían colores distintos y eso generaba ruido). Sin la palabra PROGRAMON, sin fecha y sin botón "Vista piloto" en el header. Se descartaron las fuentes Lexend para la marca y Caveat.

### Forma de trabajo del mockup
- Se edita el **borrador** en Claude. El **link compartible** se actualiza solo cuando Santi dice "Dale, listo todo esto. Reemplazalo". Ver [mockups](../02-producto/mockups/README.md).

---

## 2026-11-03 · Decisiones iniciales del brain (siguen vigentes, con ajustes)

### Arrancamos por el polo, no por haras ni caballerizas en general
- **Porqué:** es el nicho con dolor económico más claro (mucho gasto, mucha informalidad), comunidad chica e interconectada (boca en boca), y el equipo tiene acceso a la red.
- **Ajuste:** la visión es el mundo del caballo (ver arriba).

### WhatsApp como interfaz de carga + web app mobile-first para visualizar
- **Porqué:** el polista no usa computadora; vive en WhatsApp.
- **Implicancia:** no se diseña ninguna pantalla para desktop.

### El MVP se centra en gastos (e ingresos)
- **Ajuste:** el mockup ya muestra cinco módulos. Gastos sigue siendo el centro. Para el primer desarrollo, ver la priorización en el [roadmap](../04-plan/roadmap.md).

### Reutilizamos la base de Queiros
- Ver [reuso de Queiros](../03-tecnico/reuso-queiros.md).

### El repo `Caballos` es el knowledge base del proyecto
- Toda la info se mantiene en `.md` en este repo. Ver [CLAUDE.md](../CLAUDE.md).
