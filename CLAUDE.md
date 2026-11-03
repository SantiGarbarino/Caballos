# Instrucciones para agentes (Claude y otros)

Este repo es el **brain / knowledge base** del proyecto Caballos (nombre del producto a definir): gestión de polo, caballerizas y haras con WhatsApp como interfaz y web app mobile-first.

## Al trabajar en este repo

1. **Leé primero** `README.md`, `00-vision/vision.md`, `00-vision/decisiones.md` y `00-vision/preguntas-abiertas.md` para tener el contexto vigente.
2. **Idioma y tono**: español rioplatense. Usá la jerga del polo y de los caballos tal como figura en `01-mercado/glosario.md` (petisero, petiso, chukker, patrón, organización, herraje, haras, etc.). Si aparece un término nuevo, agregalo al glosario.
3. **Actualizá, no dupliques**: si la info nueva pertenece a un doc existente, editá ese doc. Creá archivos nuevos solo si no hay dónde ponerlo, y enlazalo desde el `README.md` de la raíz.
4. **Decisiones**: toda decisión (de producto, técnica, comercial) va a `00-vision/decisiones.md` con fecha (AAAA-MM-DD), contexto, decisión y porqué.
5. **Preguntas abiertas**: lo que falta definir va a `00-vision/preguntas-abiertas.md`. Cuando se resuelve, se tacha/mueve.
6. **Hipótesis vs. validado**: marcá **[HIPÓTESIS]** lo que suponemos y **[VALIDADO]** lo que confirmamos con entrevistas o datos (citando la fuente: "entrevista a polista 4 goles, 2026-11-10").
7. **CHANGELOG**: anotá cada sesión de trabajo relevante en `CHANGELOG.md` (fecha + qué cambió).
8. **Principio rector del producto**: el usuario es un polista que *no usa computadora*. Todo se diseña **WhatsApp-first y mobile-first**. Si una feature requiere desktop o un formulario largo, está mal planteada.
9. **Herencia Queiros**: el producto reutiliza la lógica de Queiros (WhatsApp → IA → datos estructurados → tablero/alertas → consultas en lenguaje natural). Ver `03-tecnico/reuso-queiros.md`.

## Equipo

- **Santi** (Santiago Garbarino) — Lic. en Administración y Sistemas (ITBA)
- **Mati** (Matías) — Lic. en Administración y Sistemas (ITBA), CEO de Queiros
- **Mauro** — Ingeniero Informático (ITBA)

Roles en este proyecto: ver `04-plan/plan-ejecucion.md`.
