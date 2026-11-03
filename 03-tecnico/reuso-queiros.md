# Qué reciclamos de Queiros

Queiros convierte mensajes de WhatsApp (audios, fotos, texto) de operarios de planta en datos estructurados, KPIs, alertas y consultas en lenguaje natural ("second brain operativo"). **Es exactamente la misma mecánica**, cambiando el dominio.

## Reutilizable casi tal cual
| Pieza de Queiros | Uso en Caballos |
|---|---|
| Integración WhatsApp Business (recepción/envío, webhooks, plantillas) | Igual, con número y marca nuevos |
| Transcripción de audios | Igual |
| OCR / lectura de imágenes | Tickets, facturas, comprobantes de transferencia |
| Extracción con LLM a un schema | Cambia el schema: Movimiento / EventoCaballo |
| Trazabilidad al mensaje original | Igual |
| Dashboard web | Re-skin a mobile-first |
| Reportes y alertas automáticas por WhatsApp | Resumen semanal, rendición al patrón, herraje vencido |
| Consultas en lenguaje natural (second brain) | "¿Cuánto gasté en vete?" |

## A adaptar
- **Prompts / schema** con la taxonomía de [gastos](../02-producto/modulo-gastos-ingresos.md) y la jerga del [glosario](../01-mercado/glosario.md).
- **Normalización de montos y monedas** (lucas, palo, verdes, libras).
- **Modelo multi-tenant**: en Queiros la unidad es la empresa/planta; acá es la **organización** del polista.
- **Front mobile-first** (en Queiros el comprador es white collar y mira en desktop; acá todo es celular).

## Aprendizajes de Queiros a llevar (completar con el equipo)
- [ ] ¿Qué funcionó para que los usuarios adopten el canal WhatsApp?
- [ ] ¿Qué errores de extracción eran los más comunes y cómo se resolvieron?
- [ ] ¿Qué pasó con el onboarding? ¿Qué fricciones hubo?
- [ ] Pricing: Queiros cobra USD 20/usuario/mes. ¿Qué aprendimos de la disposición a pagar?
- [ ] ¿Qué aprendimos del ciclo de venta y de las demos?

## A revisar en el repo de Queiros App
- [ ] Stack (backend, base de datos, front, hosting, proveedor de WhatsApp/BSP, modelos de IA) → documentarlo en [arquitectura.md](arquitectura.md).
- [ ] Qué módulos se pueden extraer como librería compartida vs. fork.
