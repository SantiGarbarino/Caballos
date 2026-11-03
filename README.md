# Caballos — Brain del proyecto

> Nombre de producto: **a definir** (ver [preguntas abiertas](00-vision/preguntas-abiertas.md)). Mientras tanto lo llamamos *"el producto"* o *Caballos*.

Gestión de caballerizas, haras y polo con **WhatsApp como interfaz** y una **web app mobile-first** como tablero. Arrancamos por el **polo**: el polista (y su organización) manda por WhatsApp gastos, ingresos y novedades de los caballos, y lo ve ordenado en el celular.

Equipo: **Santi, Mati y Mauro** (mismo equipo de Queiros). Reciclamos todo lo que sirvió de Queiros: pipeline de WhatsApp + IA, aprendizajes de producto y de venta.

---

## Cómo está organizado este repo

Este repo es el **knowledge base y la memoria del proyecto**. Todo lo que decidimos, aprendemos o definimos queda acá en `.md`.

| Carpeta | Qué hay |
|---|---|
| [`00-vision/`](00-vision/) | Visión, problema, propuesta de valor, log de decisiones y preguntas abiertas |
| [`01-mercado/`](01-mercado/) | Cómo funciona la industria del polo, glosario/jerga, segmentos y personas, competencia |
| [`02-producto/`](02-producto/) | PRD del MVP, módulos (gastos/ingresos, caballos), flujos de WhatsApp, app mobile, modelo de datos |
| [`03-tecnico/`](03-tecnico/) | Arquitectura y qué reutilizamos de Queiros |
| [`04-plan/`](04-plan/) | Roadmap, plan de ejecución por fases, discovery y validación |
| [`05-gtm/`](05-gtm/) | Go-to-market, mapa de clientes, pricing, contenido y media kit |

### Documentos clave para arrancar

1. [Visión y propuesta de valor](00-vision/vision.md)
2. [La industria del polo (cómo se mueve la plata)](01-mercado/industria-polo.md)
3. [Glosario de jerga](01-mercado/glosario.md) — **usar siempre esta terminología**
4. [PRD del MVP](02-producto/prd-mvp.md)
5. [Módulo de gastos e ingresos](02-producto/modulo-gastos-ingresos.md) — el corazón del MVP
6. [Plan de ejecución](04-plan/plan-ejecucion.md)
7. [Estrategia go-to-market](05-gtm/estrategia-gtm.md)

---

## Reglas del brain

- **Todo en `.md`**, en español rioplatense y con la **jerga del polo** (ver [glosario](01-mercado/glosario.md)).
- Cada decisión importante se registra en [decisiones.md](00-vision/decisiones.md) con fecha y porqué.
- Lo que no sabemos va a [preguntas-abiertas.md](00-vision/preguntas-abiertas.md); cuando se responde, se mueve a decisiones o al doc correspondiente.
- Marcamos lo no validado como **[HIPÓTESIS]** y lo validado con entrevistas/datos como **[VALIDADO]**.
- Cambios relevantes se anotan en [CHANGELOG.md](CHANGELOG.md).
- Instrucciones para agentes de IA (Claude, etc.) en [CLAUDE.md](CLAUDE.md).
