# Plan de ejecución

## Roles (propuesta — a confirmar)

| Persona | Rol en el proyecto | Responsable de |
|---|---|---|
| **Mauro** | Tech lead | Arquitectura, reuso de Queiros, bot de WhatsApp, IA, web app |
| **Santi** | Producto + GTM | PRD, mockups, discovery, contenido, media kit, este brain |
| **Mati** | CEO / comercial | Red de contactos en polo, ventas, alianzas, pitch, decisiones societarias |

> Cada uno es dueño de mantener actualizados sus docs en este repo.

## Fase 0 — Discovery (3 nov → 15 dic 2026)

| Semana | Tareas | Dueño |
|---|---|---|
| 3–9 nov | Cerrar guía de entrevista · listar 40 polistas a contactar (red propia) · subir mockup al repo | Santi, Mati |
| 10–23 nov | 10+ entrevistas (en clubes, prácticas, Tortugas/Hurlingham) · mostrar mockup · test "mandame tus gastos de la semana por WhatsApp" (**concierge MVP**: un humano los procesa) | Santi, Mati |
| 10–30 nov | Relevar stack de Queiros · spike técnico: extractor de gastos con jerga + set de evaluación de 100 mensajes | Mauro |
| 24 nov–7 dic | 10+ entrevistas más (Palermo) · relevar competencia · síntesis | Santi, Mati |
| 8–15 dic | **Decisión**: segmento beachhead, alcance final del MVP, nombre, pricing inicial | Todos |

**El concierge MVP es clave**: crear un número de WhatsApp, que 5–10 polistas manden sus gastos durante 2–3 semanas, y nosotros les devolvemos el resumen a mano (o con el spike de IA). Valida el hábito antes de escribir el producto.

## Fase 1 — MVP Gastos (dic 2026 → feb 2027)

Sprints de 2 semanas:

1. **Sprint 1**: ingesta WhatsApp (fork/reuso Queiros) + extractor de texto + confirmación + guardado.
2. **Sprint 2**: audio + foto (OCR) + correcciones + multimoneda + alta de caballos y patrones.
3. **Sprint 3**: web app — login link mágico, inicio, movimientos, categorías.
4. **Sprint 4**: caballos (costo por caballo), patrones y rendición compartible, consultas por WhatsApp, resumen semanal.
5. **Sprint 5**: pulido, set de evaluación ≥ 90%, onboarding, alpha con 3–5 polistas.

## Fase 2 — Beta (mar → may 2027)
- Onboarding 1 a 1 de 10–20 organizaciones.
- Check-in semanal con cada usuario (WhatsApp/llamada).
- Medir: hábito semanal, % sin corrección, uso de rendición, NPS.
- Iterar cada semana.

## Rituales
- **Lunes**: planning de 30 min (qué hace cada uno esta semana).
- **Viernes**: update en `CHANGELOG.md` + decisiones de la semana en `decisiones.md`.
- **Post-entrevista**: notas en `04-plan/entrevistas/AAAA-MM-DD-nombre.md` (usar la plantilla de [discovery](validacion-discovery.md)).
