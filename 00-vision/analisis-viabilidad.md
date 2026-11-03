# Análisis de viabilidad — mirada crítica

> Evaluación hecha en la sesión del 27/10/2026, a pedido de Santi ("sinceridad, criterio y profesionalidad"). Formato: riesgos primero, después oportunidad y recomendaciones. Todo lo de mercado es **[HIPÓTESIS]** hasta que haya entrevistas.

## 1. Riesgos (en orden de gravedad)

1. **Validación solo familiar.** Hoy la única validación es el cuñado de Santi (polista) y las ideas de gastos que aportó su novia. La familia no dice "no". Hace falta validar con polistas que no nos deban nada.
2. **Mercado chico.** El polo profesional con organización propia son, a lo sumo, unos cientos de personas en Argentina. Con tickets de decenas de dólares por mes, el polo solo no alcanza para un negocio grande. Por eso la tesis tiene que ser **el mundo del caballo**, con el polo como puerta de entrada.
3. **El comprador es una persona, no una empresa.** Compra por impulso o recomendación, abandona fácil, es muy sensible a algo feo o engorroso. El ICP es sensible: por eso **no se prueba con el producto actual de Queiros**, sino primero con el mockup y después con la versión web nueva.
4. **Plata informal.** Puede haber resistencia a registrar montos. La privacidad tiene que ser explícita (pantalla «Quién ve tu cuenta»).
5. **Estacionalidad y viajes.** El polista alto handicap pasa meses afuera (Inglaterra, Sotogrande, Wellington). El producto tiene que funcionar igual desde cualquier país y en cualquier moneda.
6. **Costo de WhatsApp saliente.** Los avisos fuera de la ventana de 24 h necesitan plantillas aprobadas por Meta y se pagan por mensaje. Tareas del piloto, pagos fijos, recordatorios y cierre del día son todos salientes. Ver [arquitectura](../03-tecnico/arquitectura.md).
7. **Timebox.** El equipo tiene como plazo **diciembre 2026** para ver tracción en Queiros. Criterio planteado: **MRR > US$ 1.500 y 7–8 clientes**. Validar un vertical nuevo y llegar a eso en ~2 meses es muy ajustado.
8. **Brecha técnica.** El producto actual de Queiros está lejos de la experiencia del mockup. Ver la estimación en [plan de ejecución](../04-plan/plan-ejecucion.md).

## 2. La oportunidad

- Es un rubro que mueve mucho dinero y casi no usa tecnología.
- El dolor de gastos es concreto y diario, y el canal (WhatsApp) ya es el que usan.
- Comunidad chica y muy conectada: si funciona, el boca en boca es rapidísimo (y si falla, también).
- Hay un ángulo regulatorio real (SENASA digitaliza libreta y pasaporte equino, ver [regulación](../01-mercado/regulacion-senasa.md)) que puede convertir el producto en infraestructura.
- La cría de caballos de polo es enorme en volumen: la AACCP tiene ~400 socios (37 del exterior), registró ~95.500 productos en su historia, y ~90% de los nacimientos actuales son por transferencia embrionaria, clonación o ICSI (La Nación, julio 2024). Haras y cría pueden ser el mercado grande.

## 3. La tesis "mundo del caballo" (opinión dada a Santi)

- **Sí como visión, no como foco inicial.** Ser "el Pensai de los caballos" es una buena tesis. Pero el producto tiene que entrar por **un** subsector y ganar ahí antes de abrirse.
- **Queiros = motor, PROGRAMON = marca vertical.** No mezclar la marca Queiros (B2B, pymes industriales) con el polista.
- **Polo como entrada** porque: acceso a la red (familia y contactos), dolor claro y comunidad conectada. **Haras/cría como posible mercado grande**: conviene entrevistar 3–5 haras ya, en paralelo, para no enterarse tarde.

### Referencia: Pensai (Joaco)

- Software de ganadería (vacas) con bot de WhatsApp.
- Precio: **US$ 200 por año por usuario** (dato dado por el desarrollador).
- ~**1.000 campos** usándolo (dato del desarrollador, sin verificar).
- **Acción:** hablar con Joaco: cómo vende, cómo hace el onboarding, qué precio funciona, cómo resolvió los mensajes salientes de WhatsApp.

## 4. Recomendaciones de validación (plan propuesto)

1. **15 entrevistas con polistas que no sean familia** (profesionales, ojalá alto handicap y mediano). Mostrar el mockup al final, no al principio. Guía en [discovery](../04-plan/validacion-discovery.md).
2. **Compromisos concretos, no "me encanta"**: preventa, seña o fecha de arranque.
3. **Concierge test por WhatsApp**: 3–5 polistas mandan sus gastos a un número durante 2–3 semanas; nosotros los ordenamos (a mano o con el motor) y les devolvemos un **resumen semanal**. Valida el hábito antes de construir.
4. **3–5 entrevistas a haras** para dimensionar el mercado de cría.
5. **Criterios para matar o seguir (kill criteria)** definidos antes de empezar. Ver [roadmap](../04-plan/roadmap.md).
6. **Hablar con Joaco (Pensai).**

## 5. Qué le cambiaríamos o agregaríamos al producto (ronda del 27/10)

Propuestas que Santi aprobó y ya están en el mockup:

- **«Quién ve tu cuenta»**: accesos por persona (dueño, quien lleva las cuentas, contador, piloto) y nota de privacidad.
- **Pagos fijos**: se cargan una vez y cada mes se confirman por WhatsApp con un «sí».
- **Gastos que cubre el patrón**: marca en el gasto, se suma a lo que debe el patrón y se sigue el reintegro.
- **Compra de caballos separada** como inversión (no ensucia el gasto operativo de las temporadas).
- **Ventas de caballos** en Ingresos, con cobros parciales.
- **Resultado por temporada**: ingresos contra gastos por lugar y fechas, por moneda.
- **Exportar** a Excel o PDF, con fotos, directo al mail del contador.
- **Trazabilidad**: cada gasto muestra el comprobante y quién lo cargó, con link a la conversación de WhatsApp.

Lo que se dejó para más adelante:

- **Piloto con vista web**: no hace falta. **Al piloto le alcanza con WhatsApp** (decisión de Santi). La vista existe en el código del mockup pero no se llega desde la app.
- **Ficha del caballo con documentación oficial (SENASA)**: más adelante.
- **Onboarding**: "no nos metamos con el onboarding todavía, que vean directo la versión final". La idea discutida queda registrada en [preguntas abiertas](preguntas-abiertas.md).
