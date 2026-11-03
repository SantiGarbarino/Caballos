# Log de decisiones

Formato: fecha · decisión · contexto/porqué · quién. Las más nuevas arriba.

---

### 2026-11-03 · Arrancamos por el polo, no por haras ni caballerizas en general
- **Porqué:** es el nicho con dolor económico más claro (mucho gasto, mucha informalidad), comunidad chica e interconectada (boca en boca), y el equipo tiene acceso a la red.
- **Quién:** Santi, Mati, Mauro.

### 2026-11-03 · WhatsApp como interfaz de carga + web app mobile-first para visualizar
- **Porqué:** el polista no usa computadora; vive en WhatsApp. Misma tesis validada en Queiros con operarios de planta.
- **Implicancia:** no se diseña ninguna pantalla para desktop en el MVP.

### 2026-11-03 · El MVP se centra en gastos (e ingresos)
- **Porqué:** el control de gastos es el principal problema detectado. El módulo tiene que ser súper simple e intuitivo. Caballos (stock, sanidad, movimientos) entra en segunda instancia, pero el modelo de datos lo contempla desde el día 1 (un gasto se puede asignar a caballos).

### 2026-11-03 · Reutilizamos la base de Queiros
- **Porqué:** pipeline WhatsApp → IA → datos estructurados ya resuelto. Acelera el time-to-market. Ver [reuso-queiros](../03-tecnico/reuso-queiros.md).

### 2026-11-03 · El repo `Caballos` es el knowledge base del proyecto
- Toda la info se mantiene en `.md` en este repo. Ver [CLAUDE.md](../CLAUDE.md) para las reglas.
