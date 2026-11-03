# Aprendizajes de Queiros (solo know-how)

> **Decisión del 2026-11-03:** este es un **producto totalmente nuevo**. No se mezcla **nada** de Queiros: ni código, ni repo, ni marca, ni número de WhatsApp, ni sus restricciones. Si algo se sacó de Queiros (por ejemplo, los recordatorios), **acá puede y debe existir** si el producto lo necesita. Lo que traemos es lo que **aprendimos** construyendo Queiros, y el equipo (Santi, Mati y Mauro).

## La idea es parecida, el producto no

| | Queiros | Este producto |
|---|---|---|
| Interfaz de carga | WhatsApp | WhatsApp (grupo de la organización + privado) |
| IA | Mensaje → datos | Mensaje → gastos, cobros, caballos, stock, tareas, recordatorios |
| Web | Planillas y tablas, pensada para desktop | **Mobile-first, sin tablas**: módulos con tableros y tarjetas (como el mockup) |
| Usuario | *White collar*, pymes | Polista y su manager, que no usan computadora |

## Know-how que traemos (lo que ya sabemos hacer)

- Agente conversacional de WhatsApp: entender texto, audio y foto, y confirmar.
- Catálogos con alias (para caballos: "la Rockstar"; personas: "Cacho"; lugares: "el campo").
- Extracción con schema estricto y manejo de correcciones.
- Login sin contraseña con link de un solo uso por WhatsApp.
- Alta de personas por WhatsApp ("Unirme").
- Plantillas salientes de Meta y la ventana de 24 h.
- Trazabilidad al mensaje original.

## Lo que hay que construir (todo de cero)

1. **PWA mobile-first** con el diseño del mockup. Lo más grande: el ICP no tolera algo feo.
2. **Conversión a US$**: cotización del dólar blue del día (promedio compra/venta, de Rava, DólarHoy u otra), euros, y guardar original + cotización.
3. **Bot en grupos de WhatsApp** + chats privados, y ruteo de proveedores con varios clientes (verificar límites de la Groups API de Meta).
4. **Programador de salientes**: recordatorios personales, tareas del piloto (7:00), pagos fijos, avisos, cierre del día (20:00).
5. **Integración con la app Polo Argentino** (catálogo de caballos).
6. Estado del caballo y eventos por caballo.
7. Cobertura de stock: consumo por caballo × caballos ÷ envase → días.
8. Ingresos: acuerdos, pagos parciales, reintegros y resultado por temporada.
9. "Ante la duda, pregunta" con la [taxonomía](../02-producto/modulo-gastos-ingresos.md) y la jerga del [glosario](../01-mercado/glosario.md).

## Lecciones de Queiros a escribir (completar con el equipo)
- [ ] ¿Qué funcionó para que los usuarios adopten el canal WhatsApp?
- [ ] ¿Qué errores de extracción eran los más comunes?
- [ ] ¿Qué fricciones hubo en el onboarding?
- [ ] ¿Qué aprendimos de la disposición a pagar?
