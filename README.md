# PROGRAMON — Brain del proyecto Caballos

> **PROGRAMON** es la marca vertical para el mundo del caballo, construida sobre el motor de **Queiros**. Logo pendiente.

Toda la organización del polista en el celular, cargada por WhatsApp. El polista, el piloto, los petiseros y el puestero mandan audios, fotos y mensajes, y la app (web mobile instalable) los ordena en **Inicio · Caballos · Caballeriza · Gastos · Ingresos**. Arrancamos por el **polo profesional** y la visión es el **mundo del caballo** (haras/cría, carrera, criollos, salto).

Equipo: **Santi, Mati y Mauro** (mismo equipo de Queiros).

**Mockup para compartir:** https://claude.ai/artifact/3cZKSNp1tywiqWrFzFBzJR · ver [mockups](02-producto/mockups/README.md).

---

## Cómo está organizado este repo

| Carpeta | Qué hay |
|---|---|
| [`00-vision/`](00-vision/) | Visión, análisis de viabilidad, decisiones y preguntas abiertas |
| [`01-mercado/`](01-mercado/) | Industria del polo y del caballo, regulación SENASA, glosario, segmentos y personas, competencia |
| [`02-producto/`](02-producto/) | PRD, app mobile, módulos (Caballos, Caballeriza, Gastos e Ingresos), flujos de WhatsApp, modelo de datos, historial de iteraciones y mockup |
| [`03-tecnico/`](03-tecnico/) | Arquitectura y qué reutilizamos de Queiros |
| [`04-plan/`](04-plan/) | Roadmap, plan de ejecución, validación y entrevistas |
| [`05-gtm/`](05-gtm/) | Go-to-market, clientes objetivo, pricing, contenido y media kit |

### Documentos clave

1. [Visión y propuesta de valor](00-vision/vision.md)
2. [Análisis de viabilidad (riesgos primero)](00-vision/analisis-viabilidad.md)
3. [Decisiones](00-vision/decisiones.md)
4. [PRD](02-producto/prd-mvp.md)
5. [Gastos e Ingresos](02-producto/modulo-gastos-ingresos.md): el corazón del producto
6. [Mockup, capturas y datos ficticios](02-producto/mockups/README.md)
7. [Flujos de WhatsApp](02-producto/flujos-whatsapp.md)
8. [Historial de iteraciones del mockup](02-producto/historial-iteraciones.md): qué se sacó y por qué
9. [Regulación SENASA](01-mercado/regulacion-senasa.md)
10. [Roadmap y kill criteria](04-plan/roadmap.md)
11. [Glosario](01-mercado/glosario.md): **usar siempre esta terminología**

### Índice completo

- **Visión**: [vision](00-vision/vision.md) · [analisis-viabilidad](00-vision/analisis-viabilidad.md) · [decisiones](00-vision/decisiones.md) · [preguntas-abiertas](00-vision/preguntas-abiertas.md)
- **Mercado**: [industria-polo](01-mercado/industria-polo.md) · [regulacion-senasa](01-mercado/regulacion-senasa.md) · [segmentos-y-personas](01-mercado/segmentos-y-personas.md) · [competencia](01-mercado/competencia.md) · [glosario](01-mercado/glosario.md)
- **Producto**: [prd-mvp](02-producto/prd-mvp.md) · [app-mobile](02-producto/app-mobile.md) · [modulo-caballos](02-producto/modulo-caballos.md) · [modulo-caballeriza](02-producto/modulo-caballeriza.md) · [modulo-gastos-ingresos](02-producto/modulo-gastos-ingresos.md) · [flujos-whatsapp](02-producto/flujos-whatsapp.md) · [modelo-de-datos](02-producto/modelo-de-datos.md) · [historial-iteraciones](02-producto/historial-iteraciones.md) · [mockups](02-producto/mockups/README.md) · [dataset-ficticio](02-producto/mockups/dataset-ficticio.md)
- **Técnico**: [arquitectura](03-tecnico/arquitectura.md) · [reuso-queiros](03-tecnico/reuso-queiros.md)
- **Plan**: [roadmap](04-plan/roadmap.md) · [plan-ejecucion](04-plan/plan-ejecucion.md) · [validacion-discovery](04-plan/validacion-discovery.md) · [entrevistas](04-plan/entrevistas/README.md)
- **GTM**: [estrategia-gtm](05-gtm/estrategia-gtm.md) · [clientes-objetivo](05-gtm/clientes-objetivo.md) · [pricing](05-gtm/pricing.md) · [contenido](05-gtm/contenido.md) · [media-kit](05-gtm/media-kit.md)

---

## Reglas del brain

- **Todo en `.md`**, en español rioplatense y con la **jerga del polo** (ver [glosario](01-mercado/glosario.md)).
- Cada decisión importante va a [decisiones.md](00-vision/decisiones.md) con fecha y porqué.
- Lo que no sabemos va a [preguntas-abiertas.md](00-vision/preguntas-abiertas.md).
- Lo no validado va marcado **[HIPÓTESIS]** y lo validado **[VALIDADO]** con la fuente.
- Cambios relevantes se anotan en [CHANGELOG.md](CHANGELOG.md).
- Instrucciones para agentes de IA en [CLAUDE.md](CLAUDE.md).
