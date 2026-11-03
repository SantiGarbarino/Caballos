# Arquitectura (v0.3)

> Arquitectura lógica. Producto y código **nuevos** (no se reutiliza nada de Queiros App; solo el know-how, ver [aprendizajes](aprendizajes-queiros.md)). Stack a definir por Mauro.

```
 WhatsApp: grupo de la organización (manager, polista, vete, herrero, petiseros)
           + privados (polista, manager, piloto, proveedores)
        │
        ▼
 WhatsApp Business API (número propio; BSP a elegir) ── webhook ──► Ingesta
                                              │  grupo → cuenta · privado → persona → cuenta
                                              │  (proveedor con varios clientes → pregunta)
                                              │
              ┌───────────────────────────────┼───────────────────────────┐
              ▼                               ▼                           ▼
            Texto                    Audio → transcripción        Imagen → lectura
                                                                  (factura, remito,
                                                                   papeles: microchip)
              └───────────────────────────────┬───────────────────────────┘
                                              ▼
       Extractor LLM (gasto / pago / acuerdo / venta / evento de caballo / stock /
       recordatorio / visita / tarea / consulta / corrección)
       + catálogos con alias (caballos, personas, lugares) + "ante la duda, preguntar"
       + conversión a US$ (API de cotización: dólar blue del día; euros)
                                              │
          ┌───────────────────┬───────────────┼───────────────┬────────────────────┐
          ▼                   ▼               ▼               ▼                    ▼
     Base de datos      Motor de consultas  Programador de  Confirmaciones      Export
     (por cuenta)       (NL → datos →       salientes       y repreguntas      (Excel/PDF
                         respuesta)         (plantillas)                        con fotos → mail)
          │
          ▼
 PWA mobile (polista y manager): Inicio · Caballos · Caballeriza · Gastos · Ingresos
 (login por link de un solo uso)          ▲
                                          └── Cría Polo (catálogo de caballos, a integrar)
```

## Componentes
1. **Ingesta**: si viene de un **grupo**, la cuenta sale del grupo; si es **privado**, de la persona (piloto, petiseros y puestero tienen una sola cuenta; un proveedor con varios clientes recibe la pregunta "¿para qué cliente es?"). Guarda el mensaje original.
1b. **Cotizaciones**: consulta el dólar blue del día (y euro) y guarda valor, fecha y fuente. Si no hay cotización para la moneda, se repregunta al usuario.
2. **Router de intención** y **extractor** con schema estricto.
3. **Repregunta** cuando falta el lugar, la categoría o los caballos ("ante la duda, pregunta").
4. **Confirmador**: respuesta corta y correcciones sobre lo último.
5. **Consultas** en lenguaje natural sobre los mismos datos de la app.
6. **Programador de salientes**: recordatorios personales («mañana haceme acordar…»), tareas del piloto (7:00), pagos fijos (el día del vencimiento; si responde "mañana", reintenta al día siguiente a las 9), recordatorios, avisos al piloto, cierre del día (20:00), aviso si una persona deja de reportar.
7. **PWA** de lectura y carga para polista y manager (mismo acceso). Sin tablas: módulos con tableros.
7b. **Integración Cría Polo**: catálogo para elegir los caballos propios (a confirmar API/acuerdo).
8. **Export** a Excel/PDF con fotos y envío al mail del contador.

## WhatsApp saliente: restricciones y costo
- Fuera de la **ventana de 24 h** desde el último mensaje del usuario solo se pueden mandar **plantillas aprobadas por Meta**, que se **pagan por mensaje**.
- En PROGRAMON casi todos los avisos son salientes. Hay que diseñar plantillas (tareas del día, pago fijo, recordatorio, cierre) y estimar el costo por cuenta y por mes antes de fijar precio.
- Truco de diseño: invitar a responder (ej. "¿Lo pagaste?") para reabrir la ventana de 24 h.

## Calidad de la IA
- Set de evaluación con mensajes reales del concierge test: monto, moneda, categoría, **lugar**, caballos, patrón.
- Toda corrección se loguea.

## Grupos de WhatsApp: restricciones a verificar
- Según fuentes secundarias (2026-11-03), la Groups API de Meta tendría **máximo 8 participantes por grupo** (contando al bot), requiere número verificado (OBA) y los participantes entran por link de invitación (no se pueden agregar por API). **Verificar en la documentación oficial de Meta antes de diseñar.**
- Si se confirma: el bot no podría entrar a los grupos que ya existen y los grupos grandes no entran. Evaluar alternativas (grupo nuevo creado por el bot con los clave, o carga por privado).

## Seguridad y privacidad
- Datos financieros sensibles. Solo polista y manager entran a la app; en los grupos no se muestran montos [HIPÓTESIS]; patrón, contador y equipo no tienen acceso. Cifrado en reposo.
