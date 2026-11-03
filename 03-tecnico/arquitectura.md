# Arquitectura (v0)

> El stack concreto se define a partir del de Queiros App (ver [reuso-queiros.md](reuso-queiros.md)). Esto es la arquitectura lógica.

```
 WhatsApp (polista, capataz)
        │
        ▼
 WhatsApp Business API (BSP) ── webhook ──► Ingesta
                                              │
                         ┌────────────────────┼─────────────────────┐
                         ▼                    ▼                     ▼
                    Texto              Audio → transcripción   Imagen → OCR/visión
                         └────────────────────┬─────────────────────┘
                                              ▼
                              Extractor LLM (schema Movimiento /
                              EventoCaballo / Consulta / Corrección)
                                              │
                         ┌────────────────────┼──────────────────┐
                         ▼                    ▼                  ▼
                    Base de datos       Motor de consultas   Notificador
                    (multi-tenant      (NL → query → resp.)  (confirmaciones,
                     por organización)                        resúmenes, alertas)
                         │
                         ▼
                 Web app mobile-first (PWA) — login por link mágico
```

## Componentes
1. **Ingesta WhatsApp**: recibe mensajes, identifica usuario/organización por teléfono, guarda `MensajeOrigen`.
2. **Router de intención**: ¿es un movimiento, un evento de caballo, una consulta, una corrección o charla?
3. **Extractor**: LLM con schema estricto + diccionario de jerga + contexto de la organización (caballos, patrones, proveedores conocidos) para resolver nombres ("la Pampa", "el Chino").
4. **Confirmador**: arma la respuesta de confirmación; maneja correcciones sobre el último movimiento.
5. **Consultas**: NL → consulta sobre los datos de la organización → respuesta + link.
6. **Jobs programados**: resúmenes semanales/mensuales, alertas (fase 2).
7. **Web app**: lectura, edición, rendición pública por link con token, export CSV.

## Calidad de la IA
- **Set de evaluación** desde el día 1: 200+ mensajes reales/simulados de polistas con el resultado esperado. Medir precisión por campo (monto, moneda, categoría, caballo, patrón).
- Toda corrección del usuario se loguea y alimenta el set.

## Seguridad y privacidad
- Datos financieros sensibles e informales → cifrado en reposo, acceso mínimo, links de rendición con token y expiración, nada se comparte sin acción del usuario.
