# Preguntas abiertas

Lo que todavía no sabemos o no decidimos. Cuando se resuelve, pasa a [decisiones.md](decisiones.md).

## Resueltas
- ~~¿Cómo manejamos el tipo de cambio?~~ → **Todo en US$**: pesos al dólar blue del día, automático; euros con cotización online o, si no hay, el bot pregunta (2026-11-03).
- ~~Mockup de Santi~~ → en [`02-producto/mockups/`](../02-producto/mockups/README.md) (en construcción; Santi adjunta la versión final).
- ~~¿Quién usa la plataforma?~~ → **App**: polista y manager (ven lo mismo). **Solo WhatsApp**: el resto de la organización (ej. Sofía, piloto, petiseros, puestero) y los proveedores; cargan por el bot y figura quién lo cargó (2026-11-03).
- ~~¿Qué cotización del blue?~~ → **Promedio entre compra y venta**, de cualquier fuente (Rava, DólarHoy u otra) (2026-11-03).
- ~~¿Qué hace el bot con un gasto mandado en el grupo?~~ → **Lo registra igual.** La plata va en general por privado, pero no es obligatorio (2026-11-03).
- ~~¿Qué tan importante es lo del patrón?~~ → El patrón **no existe para la plataforma**: solo es la contraparte de los acuerdos y reintegros en Ingresos (2026-11-03).
- ~~¿Empresa nueva o línea de producto de Queiros?~~ → **Producto nuevo**; de Queiros solo el know-how y el equipo (2026-11-03). La parte societaria sigue abierta (ver abajo).
- ~~¿Repo de código nuevo o fork de Queiros App?~~ → **Nuevo**: no se mezcla nada de Queiros (2026-11-03).
- ~~¿Mismo BSP que Queiros?~~ → Número y cuenta de WhatsApp **propios**; el proveedor se elige de cero (2026-11-03).

## Negocio
- [ ] **Nombre** definitivo (PROGRAMON es provisorio) y **logo**.
- [ ] **ICP final**: ¿organizaciones grandes con manager, alto handicap sin manager, mediano handicap? Validar en entrevistas. (Tomás es solo el ejemplo del mockup.)
- [ ] Sociedad, marca y cap table del proyecto nuevo.
- [ ] **Pricing**: ¿por organización o por cantidad de caballos? ¿Mensual o anual? Ver [pricing](../05-gtm/pricing.md).
- [ ] ¿Bilingüe desde el día 1? (el polista pasa meses en Inglaterra/España; sus petiseros afuera suelen ser argentinos).
- [ ] ¿Haras/cría como segundo vertical o en paralelo? Salir de las 3–5 entrevistas a haras.

## Producto
- [ ] **Cría Polo**: confirmar nombre exacto de la app, quién es el dueño, si tiene API o acuerdo de datos, qué campos trae (sangre, padre, madre, partidos jugados) y si se puede actualizar. Alternativa o complemento: registro genealógico de la AACCP. En una búsqueda web (2026-11-03) no apareció una app con ese nombre exacto; sí catálogos de cría (La Dolfina Cría, Cría Emezeta) y una app "Criadores de Polo".
- [ ] **Conversión de monedas**: ¿Qué cotización si el gasto es de una fecha pasada ("el viernes pagué…"): la de ese día? ¿Se puede corregir la cotización a mano?
- [ ] **Ingresos en otras monedas** (acuerdos en € o £): ¿se convierten a US$ con la cotización de cada pago? ¿Cómo se muestra lo acordado en € y lo que falta cobrar?
- [ ] ¿Qué miembros "solo WhatsApp" pueden cargar **gastos e ingresos** (ej. Sofía sí) y cuáles solo novedades de caballos y caballeriza (ej. petiseros)? ¿Lo configura el polista o el manager desde la app?
- [ ] ¿El bot responde **consultas de plata** en el grupo? Propuesta [HIPÓTESIS]: nunca; las consultas de plata solo por privado al polista o al manager.
- [ ] **Onboarding** (postergado por decisión). Idea discutida: primera carga por WhatsApp (caballos desde Cría Polo, equipo, pagos fijos y acuerdos) más una revisión web; *white-glove* para los primeros clientes.
- [ ] **Ficha digital oficial del caballo** (libreta sanitaria digital, pasaporte equino, microchip) y camino a "aplicación autorizada" de SENASA. Ver [regulación](../01-mercado/regulacion-senasa.md).
- [ ] ¿Costo por caballo? Se sacó la pestaña Costos del mockup por ruido. ¿Vuelve en algún formato o se descarta?
- [ ] ¿Prorrateo de gastos entre caballos (ej. herraje de 4 caballos)?
- [ ] ¿Cómo se registra el consumo real de stock? Definir de dónde salen los conteos (fotos o mensajes del piloto o del manager) y cómo se ajusta.
- [ ] ¿Pedidos a proveedores desde la app? Se sacó del mockup.
- [ ] Gastos que paga el piloto de su bolsillo ("lo pagué yo en efectivo"): ¿se lleva una cuenta de lo que se le debe al piloto?
- [ ] Recordatorios automáticos derivados (ej. "Sacar sangre para AIE" por un viaje): ¿qué reglas?

## Técnico
- [ ] **Grupos de WhatsApp con la API oficial**: según fuentes secundarias (2026-11-03), la Groups API de Meta tendría un **límite de 8 participantes por grupo** (contando el número del bot), requiere número verificado (OBA) y no permite agregar participantes por API (solo link de invitación). **Verificar en la documentación oficial de Meta.** Si se confirma, un grupo con polista, manager, vete, herrero y varios petiseros puede no entrar, y el bot no podría sumarse a grupos que ya existen.
- [ ] Costo y diseño de los **mensajes salientes** (plantillas de Meta, ventana de 24 h): tareas del piloto 7:00, pagos fijos, recordatorios, cierre del día 20:00.
- [ ] Proveedor de WhatsApp (BSP o Cloud API directo) y número propio del producto.
- [ ] Fuente de cotizaciones y qué pasa si no responde.
- [ ] Estimación real de Mauro (ver [plan](../04-plan/plan-ejecucion.md)).
