# Análisis de viabilidad — mirada crítica

> Evaluación hecha en la sesión del 27/10/2026, a pedido de Santi ("sinceridad, criterio y profesionalidad"). Formato: riesgos primero, después oportunidad y recomendaciones. Todo lo de mercado es **[HIPÓTESIS]** hasta que haya entrevistas.
>
> **Actualizado el 2026-11-03:** producto nuevo (no Queiros), sin timebox ni referencia a Pensai, usuarios polista + manager, todo en US$.

## 1. Riesgos (en orden de gravedad)

1. **Validación solo familiar.** Hoy la única validación es el cuñado de Santi (polista) y las ideas de gastos que aportó su novia. La familia no dice "no". Hace falta validar con polistas que no nos deban nada.
2. **Mercado chico.** El polo profesional con organización propia son, a lo sumo, unos cientos de personas en Argentina. Con tickets de decenas de dólares por mes, el polo solo no alcanza para un negocio grande. Por eso la tesis tiene que ser **el mundo del caballo**, con el polo como puerta de entrada.
3. **El comprador es una persona, no una empresa.** Compra por impulso o recomendación, abandona fácil, es muy sensible a algo feo o engorroso. Por eso se valida primero con el mockup y después con la versión web nueva.
4. **Plata informal.** Puede haber resistencia a registrar montos. La privacidad tiene que ser explícita (pantalla «Quién ve tu cuenta»: solo polista y manager; la plata en general por privado).
5. **Estacionalidad y viajes.** El polista alto handicap pasa meses afuera (Inglaterra, Sotogrande, Wellington). El producto tiene que funcionar igual desde cualquier país y aceptar cualquier moneda (se muestra en US$).
6. **Costo de WhatsApp saliente.** Los avisos fuera de la ventana de 24 h necesitan plantillas aprobadas por Meta y se pagan por mensaje. Tareas del piloto, pagos fijos, recordatorios y cierre del día son todos salientes. Ver [arquitectura](../03-tecnico/arquitectura.md).
7. **Grupos de WhatsApp.** La carga por grupo es central, pero la API oficial de grupos de Meta tendría límites fuertes (8 participantes, sin sumar al bot a grupos existentes). A verificar. Ver [arquitectura](../03-tecnico/arquitectura.md).
8. **Todo se construye de cero.** Es un producto nuevo: solo traemos el know-how. Ver la estimación en [plan de ejecución](../04-plan/plan-ejecucion.md).
9. **Dependencia de Cría Polo.** Si la integración no es posible (sin API o sin acuerdo), el alta de caballos vuelve a ser manual.

## 2. La oportunidad

- Es un rubro que mueve mucho dinero y casi no usa tecnología.
- El dolor de gastos es concreto y diario, y el canal (WhatsApp) ya es el que usan.
- Comunidad chica y muy conectada: si funciona, el boca en boca es rapidísimo (y si falla, también).
- Hay un ángulo regulatorio real (SENASA digitaliza libreta y pasaporte equino, ver [regulación](../01-mercado/regulacion-senasa.md)) que puede convertir el producto en infraestructura.
- La cría de caballos de polo es enorme en volumen: la AACCP tiene ~400 socios (37 del exterior), registró ~95.500 productos en su historia, y ~90% de los nacimientos actuales son por transferencia embrionaria, clonación o ICSI (La Nación, julio 2024). Haras y cría pueden ser el mercado grande.

## 3. La tesis "mundo del caballo" (opinión dada a Santi)

- **Sí como visión, no como foco inicial.** Ser el software del mundo del caballo es una buena tesis. Pero el producto tiene que entrar por **un** subsector y ganar ahí antes de abrirse.
- **Producto nuevo, no Queiros.** No mezclar nada de Queiros (decisión del 2026-11-03).
- **Polo como entrada** porque: acceso a la red (familia y contactos), dolor claro y comunidad conectada. **Haras/cría como posible mercado grande**: conviene entrevistar 3–5 haras ya, en paralelo, para no enterarse tarde.

## 4. Recomendaciones de validación (plan propuesto)

1. **15 entrevistas con polistas que no sean familia** (profesionales, ojalá alto handicap y mediano). Mostrar el mockup al final, no al principio. Guía en [discovery](../04-plan/validacion-discovery.md).
2. **Compromisos concretos, no "me encanta"**: preventa, seña o fecha de arranque.
3. **Concierge test por WhatsApp**: 3–5 polistas mandan sus gastos a un número durante 2–3 semanas; nosotros los ordenamos (a mano) y les devolvemos un **resumen semanal**. Valida el hábito antes de construir.
4. **3–5 entrevistas a haras** para dimensionar el mercado de cría.
5. **Criterios para matar o seguir (kill criteria)** definidos antes de empezar. Ver [roadmap](../04-plan/roadmap.md).

## 5. Qué le cambiaríamos o agregaríamos al producto (ronda del 27/10)

Propuestas que Santi aprobó y ya están en el mockup:

- **«Quién ve tu cuenta»**: accesos y nota de privacidad (desde el 2026-11-03: solo polista y manager).
- **Pagos fijos**: se cargan una vez y cada mes se confirman por WhatsApp con un «sí».
- **Gastos que cubre el patrón**: marca en el gasto, se suma a lo que debe el patrón y se sigue el reintegro.
- **Compra de caballos separada** como inversión (no ensucia el gasto operativo de las temporadas).
- **Ventas de caballos** en Ingresos, con cobros parciales.
- **Resultado por temporada**: ingresos contra gastos por lugar y fechas (en US$ desde el 2026-11-03).
- **Exportar** a Excel o PDF, con fotos, directo al mail del contador.
- **Trazabilidad**: cada gasto muestra el comprobante y quién lo cargó, con link a la conversación de WhatsApp.

Lo que se dejó para más adelante:

- **Piloto con vista web**: no hace falta. **Al piloto le alcanza con WhatsApp** (decisión de Santi). La vista existe en el código del mockup pero no se llega desde la app.
- **Ficha del caballo con documentación oficial (SENASA)**: más adelante.
- **Onboarding**: "no nos metamos con el onboarding todavía, que vean directo la versión final". La idea discutida queda registrada en [preguntas abiertas](preguntas-abiertas.md).
