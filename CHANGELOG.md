# Changelog del brain

## 2026-11-03 (sesión 11) · Permisos finos en el mockup
- Borrador v11: Equipo con owners y resto del equipo; «Qué ve en la app» por persona (Nada / Todo / Una parte: secciones + qué caballos: todos, de un lugar o algunos). Actualizados `decisiones.md`, `preguntas-abiertas.md`, `app-mobile.md`, `modelo-de-datos.md` e `historial-iteraciones.md`.

## 2026-11-03 (sesión 10) · Owners y permisos por usuario
- Quien crea la organización es owner; los owners invitan y configuran qué ve cada usuario (solo WhatsApp o módulos de la app). El bot nunca carga una charla. Proveedores sin gastos, confirmado. Actualizados `decisiones.md`, `preguntas-abiertas.md`, `prd-mvp.md`, `modelo-de-datos.md`, `flujos-whatsapp.md`, `app-mobile.md` y `CLAUDE.md`.

## 2026-11-03 (sesión 9) · Operatoria de WhatsApp
- Reglas de ruteo (grupos, privados, proveedores con varias organizaciones), proveedores sin gastos, duplicados, reacción ✅ en grupos, varios grupos por organización y quién gestiona el equipo. En `flujos-whatsapp.md`, `modelo-de-datos.md`, `decisiones.md` y `preguntas-abiertas.md`.

## 2026-11-03 (sesión 8) · Chats, invitación y categorías
- Borrador v10: chats como lista (grupo + privados), invitación al grupo y/o por privado, Veterinario y Herrero redefinidos con ejemplos claros. Ver `decisiones.md`, `flujos-whatsapp.md`, `modulo-gastos-ingresos.md` e `historial-iteraciones.md` (vuelta 11).

## 2026-11-03 (sesión 7) · Aclaración: app Polo Argentino
- «Polo Argentino» es una **app de terceros** que ya existe (App Store) con la info de los caballos registrados; es la posible integración. **No es el nombre de nuestro producto**, que sigue sin definirse. Se reemplazó "Cría Polo" por "app Polo Argentino" en toda la KB y se sumó al glosario.

## 2026-11-03 (sesión 6) · Ajustes del mockup para la V1
- Borrador v9 con los 32 cambios aprobados (ver `02-producto/historial-iteraciones.md`, vuelta 10). Decisiones nuevas: acuerdos en € a US$, pestaña Datos sin nombrar la fuente («Polo Argentino», app de terceros, como posible integración), Equipo como pantalla propia desde Inicio, grupo de 7 + bot.

## 2026-11-03 (sesión 5) · Sin usuarios personalizados
- Se sacan los ejemplos con nombre (ej. "Sofía, hermana de Tomás") de las definiciones de usuarios: se habla de **roles**. Los nombres quedan solo en los datos ficticios del mockup. Nueva regla 14 en `CLAUDE.md`.

## 2026-11-03 (sesión 4) · Aclaraciones de Santi
- **Dos tipos de usuario**: los de la **app** (polista y manager) y los de **solo WhatsApp** (resto de la organización: manager de los petiseros, petiseros, piloto, puestero, familiares o asistentes, y proveedores): cargan por el bot, figura quién lo cargó, nunca entran a la app.
- **Plata en el grupo**: en general va por privado, pero si se habla en el grupo **se registra igual**.
- **Cotización**: dólar blue **promedio entre compra y venta**, de cualquier fuente (Rava, DólarHoy…).

## 2026-11-03 (sesión 3) · Correcciones de Santi
- **Nombre no definido**: PROGRAMON pasa a ser provisorio.
- **Producto totalmente nuevo**: de Queiros solo el know-how y el equipo. Se saca "Queiros es el motor", el timebox de dic 2026 y el MRR. `reuso-queiros.md` → `aprendizajes-queiros.md`.
- **Monedas**: todo en **US$**; pesos al dólar blue del día automático (sin preguntar), con el detalle en letra chica; euros con cotización online o el bot pregunta. Reemplaza "monedas siempre separadas".
- **Usuarios**: polista y **manager** (mismo acceso). Se saca el contador como usuario. El **patrón no existe** para la plataforma.
- **WhatsApp**: bot en el **grupo de la organización** + **chat privado** para la plata; piloto y petiseros de una sola organización; vete y herrero con varios clientes (por privado, el bot pregunta el cliente).
- **Comprobante**: si no hay foto, se ve el audio o el mensaje original.
- **Recordatorios personales** («mañana haceme acordar»).
- **App Polo Argentino** (de terceros): integración para elegir los caballos de un catálogo.
- **UI sin tablas**: módulos con tableros.
- Tomás y su organización son ficticios (ejemplo del mockup). Se saca Pensai.
- Nuevos riesgos y preguntas: límites de la Groups API de Meta (8 participantes, a verificar), datos y API de la app Polo Argentino, fuente y criterio de cotización.

## 2026-11-03 (sesión 2) · Todo lo charlado en las sesiones de producto 22–27/10
- **La verdad pasa a ser lo definido en las sesiones** (pedido de Santi). Se reescribieron los docs que lo contradecían.
- Nombre: **PROGRAMON** (marca vertical; Queiros es el motor). Visión: mundo del caballo, entrada por polo.
- Nuevos: `00-vision/analisis-viabilidad.md`, `01-mercado/regulacion-senasa.md`, `02-producto/modulo-caballeriza.md`, `02-producto/historial-iteraciones.md`, `02-producto/mockups/dataset-ficticio.md`, `02-producto/mockups/programon.html` (snapshot del mockup) y `02-producto/mockups/capturas/` (47 capturas).
- Reescritos: visión, decisiones (todas las del 22–27/10), preguntas abiertas, PRD v0.2, app mobile (diseño "Cancha de noche", Inicio, Quién ve tu cuenta), Caballos, Gastos e Ingresos (taxonomía, lugar, monedas, pagos fijos, export, acuerdos, reintegros, temporadas), flujos de WhatsApp (9 chats de demo), modelo de datos v0.2, competencia (relevamiento), segmentos y personas (Tomás y su equipo), arquitectura (salientes y plantillas de Meta), reuso de Queiros (estado real del repo), roadmap (kill criteria y timebox), plan de ejecución (estimación), discovery (hipótesis H1–H8, guía de haras).
- Correcciones: AACCPA → **AACCP**; "vasear" → **varear**; se sacaron "costo por caballo" y "rendición al patrón" como mensajes centrales; "solo se repregunta el monto" → **ante la duda, pregunta**; conversión de monedas → **nunca se convierte**.
- Glosario: piloto, puestero, invernada, pastoreo, acuerdo, reintegro, HPA, microchip, libreta sanitaria digital, pasaporte equino, SIGSA, DT-e, CVI, estados del caballo, etc.

## 2026-11-03
- Estructura inicial del knowledge base: visión, mercado (industria, glosario, segmentos, competencia), producto (PRD MVP, módulos, flujos WhatsApp, app mobile, modelo de datos), técnico (arquitectura, reuso Queiros), plan (roadmap, ejecución, discovery) y GTM (estrategia, clientes, pricing, contenido, media kit).
- Decisiones iniciales registradas: polo primero, WhatsApp + mobile-first, MVP de gastos, reuso de Queiros.
