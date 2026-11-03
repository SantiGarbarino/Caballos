# Qué reciclamos de Queiros

> Relevado en octubre 2026 leyendo el repo **Queiros App** (monorepo Firebase / Node / React, en la Mac de Santi, actualizado con `git pull`). Para confirmar con Mauro.

Queiros convierte mensajes de WhatsApp (texto, audio, foto) en datos estructurados. **Es la misma mecánica**: Queiros es el motor y PROGRAMON la marca vertical.

## Lo que Queiros ya tiene

| Pieza | Estado en Queiros | Uso en PROGRAMON |
|---|---|---|
| **Agente conversacional de WhatsApp** | Funciona | Carga de gastos, pagos, novedades, consultas |
| **Catálogos con alias** | Funciona | Caballos ("la Rockstar"), personas ("Cacho"), lugares ("el campo"), categorías |
| **Planillas con campos** y tipos de columna **monto, fecha y catálogo** | Funciona | Gasto, pago, evento, insumo |
| **Permisos por planilla** | Funciona | Base para «Quién ve tu cuenta» (dueño, cuentas, contador, piloto) |
| **Onboarding por WhatsApp «Unirme»** | Funciona | Sumar al piloto, petiseros y puestero |
| **Link web de un solo uso** (login sin contraseña) | Funciona | Entrar a la app desde WhatsApp |
| **Módulo Tablero** | Nuevo: saldos de clientes y stock para Shiva; talleres para Dimex (#1192) | Base para Inicio, Gastos e Ingresos (dejar de pensar en tablas y mostrar datos ya analizados) |
| Plantillas de WhatsApp vía **SendPulse** | Funciona | Mensajes salientes |
| Trazabilidad al mensaje original | Funciona | Comprobante en cada gasto |

## Lo que se sacó o no existe

- **Reportes**: se retiraron el 1/10/2026.
- **Recordatorios**: se quitaron (#588).
- **PWA**: no hay.
- Front pensado para desktop (el comprador de Queiros es *white collar*).

## Brecha para PROGRAMON

1. **UI mobile-first nueva (PWA)** con el diseño del mockup. Es lo más grande. El ICP no tolera algo feo.
2. **Moneda en los montos**: el tipo monto tiene que llevar moneda (US$, $, €, £) y los totales agruparse por moneda.
3. **Programador de mensajes salientes** con plantillas de Meta: tareas del piloto a las 7:00, pagos fijos el día que vencen, recordatorios, avisos, cierre del día 20:00. Hay que rehacerlo (se quitó en #588).
4. **Estado del caballo** (jugando / campo / exterior / recuperación) y eventos por caballo.
5. **Cobertura de stock**: consumo por caballo × caballos ÷ envase → días.
6. **Lógica de Ingresos**: acuerdos, pagos parciales, reintegros y resultado por temporada.
7. **"Ante la duda, pregunta"**: repreguntar lugar, categoría o caballos cuando la confianza es baja.
8. Prompts y extracción con la [taxonomía](../02-producto/modulo-gastos-ingresos.md) y la jerga del [glosario](../01-mercado/glosario.md).

## Aprendizajes de Queiros a llevar (completar con el equipo)
- [ ] ¿Qué funcionó para que los usuarios adopten el canal WhatsApp?
- [ ] ¿Qué errores de extracción eran los más comunes?
- [ ] ¿Qué fricciones hubo en el onboarding?
- [ ] Pricing: Queiros cobra USD 20/usuario/mes (Starter). ¿Qué aprendimos de la disposición a pagar?
- [ ] ¿Repo nuevo, fork o módulo de Queiros App?
