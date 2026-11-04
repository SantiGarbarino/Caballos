# Preguntas abiertas

Lo que todavía no sabemos o no decidimos. Cuando se resuelve, pasa a [decisiones.md](decisiones.md).

## Resueltas
- ~~¿Cómo manejamos el tipo de cambio?~~ → **Todo en US$**: pesos al dólar blue del día, automático; euros con cotización online o, si no hay, el bot pregunta (2026-11-03).
- ~~Mockup de Santi~~ → en [`02-producto/mockups/`](../02-producto/mockups/README.md) (en construcción; Santi adjunta la versión final).
- ~~¿Quién usa la plataforma?~~ → **App**: los owners (en el caso típico polista y manager) y quien un owner habilite *(actualizado en la sesión 10)*. **Solo WhatsApp** por defecto: el resto de la organización (piloto, petiseros, puestero, familiares o asistentes) y los proveedores; cargan por el bot y figura quién lo cargó (2026-11-03).
- ~~¿Qué cotización del blue?~~ → **Promedio entre compra y venta**, de cualquier fuente (Rava, DólarHoy u otra) (2026-11-03).
- ~~¿Qué hace el bot con un gasto mandado en el grupo?~~ → **Lo registra igual.** La plata va en general por privado, pero no es obligatorio (2026-11-03).
- ~~¿Qué tan importante es lo del patrón?~~ → El patrón **no existe para la plataforma**: solo es la contraparte de los acuerdos y reintegros en Ingresos (2026-11-03).
- ~~¿Empresa nueva o línea de producto de Queiros?~~ → **Producto nuevo**; de Queiros solo el know-how y el equipo (2026-11-03). La parte societaria sigue abierta (ver abajo).
- ~~¿Repo de código nuevo o fork de Queiros App?~~ → **Nuevo**: no se mezcla nada de Queiros (2026-11-03).
- ~~¿Mismo BSP que Queiros?~~ → Número y cuenta de WhatsApp **propios**; el proveedor se elige de cero (2026-11-03).

- ~~Ingresos en otras monedas~~ → lo cobrado al euro del día de cada pago; lo que falta, al de hoy con «≈» (2026-11-03).

- ~~Quién maneja la operación~~ → los **owners** (quien crea la organización y a quien le dé todos los accesos: polista y/o manager). Reciben las preguntas del bot y configuran qué ve cada usuario (2026-11-03).

- ~~¿Permisos por módulo o por caballo/lugar?~~ → **Los dos**: secciones + qué caballos (todos, de un lugar o algunos). Gastos e Ingresos solo owners (2026-11-03).

## Negocio
- [ ] **Nombre** definitivo (PROGRAMON es provisorio) y **logo**.
- [ ] **ICP final**: ¿organizaciones grandes con manager, alto handicap sin manager, mediano handicap? Validar en entrevistas. (Tomás es solo el ejemplo del mockup.)
- [ ] Sociedad, marca y cap table del proyecto nuevo.
- [ ] **Pricing**: ¿por organización o por cantidad de caballos? ¿Mensual o anual? Ver [pricing](../05-gtm/pricing.md).
- [ ] ¿Bilingüe desde el día 1? (el polista pasa meses en Inglaterra/España; sus petiseros afuera suelen ser argentinos).
- [ ] ¿Haras/cría como segundo vertical o en paralelo? Salir de las 3–5 entrevistas a haras.

## Producto
- [ ] **App de caballos registrados** **«Polo Argentino»** (app **de terceros** del App Store con la info de los caballos registrados; no es nuestro producto, que todavía no tiene nombre): confirmar quién es el dueño, si tiene API o acuerdo de datos, qué campos trae (sangre, padre, madre, partidos jugados) y si se puede actualizar. Alternativa o complemento: registro genealógico de la AACCP. En una búsqueda web (2026-11-03) no apareció una app con ese nombre exacto; sí catálogos de cría (La Dolfina Cría, Cría Emezeta) y una app "Criadores de Polo".
- [ ] **Conversión de monedas**: ¿Qué cotización si el gasto es de una fecha pasada ("el viernes pagué…"): la de ese día? ¿Se puede corregir la cotización a mano?
- [ ] ¿Qué miembros "solo WhatsApp" pueden **cargar** gastos e ingresos por el bot (ej. un familiar que ayuda con gastos) y cuáles solo novedades de caballos y caballeriza (ej. petiseros)? Ya se sabe que **lo configuran los owners desde Equipo** y que ver Gastos e Ingresos en la app es solo de owners; falta definir los permisos de **carga** por WhatsApp.
- [ ] ¿El bot responde **consultas de plata** en el grupo? Propuesta [HIPÓTESIS]: nunca; las consultas de plata solo por privado al polista o al manager.
- [ ] **Onboarding** (postergado por decisión). Idea discutida: primera carga por WhatsApp (caballos desde la app Polo Argentino, equipo, pagos fijos y acuerdos) más una revisión web; *white-glove* para los primeros clientes.
- [ ] **Ficha digital oficial del caballo** (libreta sanitaria digital, pasaporte equino, microchip) y camino a "aplicación autorizada" de SENASA. Ver [regulación](../01-mercado/regulacion-senasa.md).
- [ ] ¿Costo por caballo? Se sacó la pestaña Costos del mockup por ruido. ¿Vuelve en algún formato o se descarta?
- [ ] ¿Prorrateo de gastos entre caballos (ej. herraje de 4 caballos)?
- [ ] ¿Cómo se registra el consumo real de stock? Definir de dónde salen los conteos (fotos o mensajes del piloto o del manager) y cómo se ajusta.
- [ ] ¿Pedidos a proveedores desde la app? Se sacó del mockup.
- [ ] Gastos que paga el piloto de su bolsillo ("lo pagué yo en efectivo"): ¿se lleva una cuenta de lo que se le debe al piloto?
- [ ] Recordatorios automáticos derivados (ej. "Sacar sangre para AIE" por un viaje): ¿qué reglas?

- [ ] **Trabajo de proveedores → gasto**: ¿a quién le pregunta el bot (polista, manager o los dos)? ¿En el momento o en un resumen? ¿Con qué monto si el proveedor no lo dice?
- [ ] **Ruido en los grupos**: cómo distingue el bot una carga de la charla sin equivocarse, y qué hace con los mensajes dudosos.
- [ ] Si los grupos chicos (manager + un proveedor + bot) se vuelven el patrón: ¿cuántos grupos por organización y cuántos grupos en total puede tener el número del bot? (verificar límites de Meta).

- [ ] **Permisos finos, lo que falta**: ¿qué ve exactamente en «Novedades del día» alguien con caballos limitados (solo las de sus caballos)? ¿Los permisos se pueden dar también por tiempo (ej. un veterinario de reemplazo por una semana)? ¿Un usuario con acceso parcial puede cargar desde la app o solo mirar?

## Técnico
- [ ] **Grupos de WhatsApp con la API oficial**: según fuentes secundarias (2026-11-03), la Groups API de Meta tendría un **límite de 8 participantes por grupo** (contando el número del bot), requiere número verificado (OBA) y no permite agregar participantes por API (solo link de invitación). **Verificar en la documentación oficial de Meta.** Si se confirma, un grupo con polista, manager, vete, herrero y varios petiseros puede no entrar, y el bot no podría sumarse a grupos que ya existen.
- [ ] Costo y diseño de los **mensajes salientes** (plantillas de Meta, ventana de 24 h): tareas del piloto 7:00, pagos fijos, recordatorios, cierre del día 20:00.
- [ ] Proveedor de WhatsApp (BSP o Cloud API directo) y número propio del producto.
- [ ] Fuente de cotizaciones y qué pasa si no responde.
- [ ] Estimación real de Mauro (ver [plan](../04-plan/plan-ejecucion.md)).
