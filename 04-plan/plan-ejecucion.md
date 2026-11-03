# Plan de ejecución

## Roles (propuesta, a confirmar)

| Persona | Rol en el proyecto | Responsable de |
|---|---|---|
| **Mauro** (CTO) | Tech lead | Arquitectura (de cero), WhatsApp (grupos y privados), IA, cotizaciones, integración Cría Polo, PWA |
| **Santi** | Producto + validación | Mockup, PRD, entrevistas (red del polo: cuñado y contactos), este brain |
| **Mati** | Ops / Growth / BD | Red de contactos, ventas, alianzas, decisiones societarias |

## Estimación técnica (preliminar, a confirmar por Mauro)

- **V1 usable para un polista** (Gastos + carga por WhatsApp + Ingresos básico), construido de cero con el know-how de Queiros: **a estimar por Mauro**.
- **Todo lo que muestra el mockup**: **2 a 3 meses**.
- Lo que más pesa: la UI mobile nueva (PWA), el bot en grupos de WhatsApp, la conversión a US$, el programador de salientes (recordatorios, tareas, pagos fijos), la integración con Cría Polo, estado de los caballos y cobertura de stock. Ver [aprendizajes de Queiros](../03-tecnico/aprendizajes-queiros.md).

## Próximas semanas (nov – mediados dic 2026)

| Tarea | Dueño |
|---|---|
| Mostrar el mockup al cuñado y anotar la reacción | Santi |
| Lista de 25–30 polistas que **no sean familia** para llegar a 15 entrevistas | Santi, Mati |
| 15 entrevistas (guía en [discovery](validacion-discovery.md)); mockup al final | Santi, Mati |
| 3–5 entrevistas a haras | Santi |
| Averiguar Cría Polo: dueño, API o acuerdo de datos | Santi, Mati |
| Verificar límites de la Groups API de Meta (participantes, bot en grupos existentes) | Mauro |
| Concierge test: número de WhatsApp, 3–5 polistas mandan gastos 2–3 semanas, resumen semanal | Santi + Mauro |
| Pedir preventa, seña o fecha de arranque | Santi, Mati |
| Estimación real de la V1, del costo de los mensajes salientes y elección de la fuente de cotizaciones | Mauro |
| Terminar el mockup (US$, manager, grupos, Cría Polo) y corregir inconsistencias ([mockups](../02-producto/mockups/README.md)) | Santi |
| Decisión con kill criteria ([roadmap](roadmap.md)) | Todos |

## Rituales
- **Lunes**: planning de 30 min.
- **Viernes**: update en `CHANGELOG.md` y decisiones en `decisiones.md`.
- **Después de cada entrevista**: nota en `04-plan/entrevistas/AAAA-MM-DD-alias.md`.
