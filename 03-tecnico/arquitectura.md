# Arquitectura (v0.2)

> Arquitectura lógica. El stack concreto sale de Queiros App (Firebase / Node / React). Ver [reuso de Queiros](reuso-queiros.md).

```
 WhatsApp (polista, piloto, petiseros, puestero, quien lleva las cuentas)
        │
        ▼
 WhatsApp Business API (BSP: hoy SendPulse en Queiros) ── webhook ──► Ingesta
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
                                              │
          ┌───────────────────┬───────────────┼───────────────┬────────────────────┐
          ▼                   ▼               ▼               ▼                    ▼
     Base de datos      Motor de consultas  Programador de  Confirmaciones      Export
     (por cuenta)       (NL → datos →       salientes       y repreguntas      (Excel/PDF
                         respuesta)         (plantillas)                        con fotos → mail)
          │
          ▼
 PWA mobile: Inicio · Caballos · Caballeriza · Gastos · Ingresos (login por link de un solo uso)
```

## Componentes
1. **Ingesta**: identifica persona y cuenta por teléfono, guarda el mensaje original.
2. **Router de intención** y **extractor** con schema estricto.
3. **Repregunta** cuando falta el lugar, la categoría o los caballos ("ante la duda, pregunta").
4. **Confirmador**: respuesta corta y correcciones sobre lo último.
5. **Consultas** en lenguaje natural sobre los mismos datos de la app.
6. **Programador de salientes**: tareas del piloto (7:00), pagos fijos (el día del vencimiento; si responde "mañana", reintenta al día siguiente a las 9), recordatorios, avisos al piloto, cierre del día (20:00), aviso si una persona deja de reportar.
7. **PWA** de lectura y carga, con permisos por rol.
8. **Export** a Excel/PDF con fotos y envío al mail del contador.

## WhatsApp saliente: restricciones y costo
- Fuera de la **ventana de 24 h** desde el último mensaje del usuario solo se pueden mandar **plantillas aprobadas por Meta**, que se **pagan por mensaje**.
- En PROGRAMON casi todos los avisos son salientes. Hay que diseñar plantillas (tareas del día, pago fijo, recordatorio, cierre) y estimar el costo por cuenta y por mes antes de fijar precio.
- Truco de diseño: invitar a responder (ej. "¿Lo pagaste?") para reabrir la ventana de 24 h.

## Calidad de la IA
- Set de evaluación con mensajes reales del concierge test: monto, moneda, categoría, **lugar**, caballos, patrón.
- Toda corrección se loguea.

## Seguridad y privacidad
- Datos financieros sensibles. Permisos por rol; el piloto no ve montos; los patrones no tienen acceso. Cifrado en reposo.
