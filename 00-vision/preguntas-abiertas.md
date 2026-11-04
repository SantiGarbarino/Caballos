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

- ~~Conversión: fechas pasadas, corrección a mano~~ → cotización del día del gasto (fin de semana: último hábil); un owner la puede corregir; si falla la fuente, la última de hasta 3 días (2026-11-04).
- ~~Qué miembros de solo WhatsApp pueden cargar plata~~ → gastos cualquier miembro; ingresos solo owners; proveedores nunca gastos (2026-11-04).
- ~~¿El bot responde consultas de plata en el grupo?~~ → nunca; al owner, por privado (2026-11-04).
- ~~¿Prorrateo de gastos entre caballos?~~ → no: el gasto se vincula a los caballos sin repartir el monto; la ficha muestra qué se le hizo, sin plata (2026-11-04).
- ~~¿Cómo se registra el consumo real de stock?~~ → los conteos sugieren un ajuste; un owner lo acepta (2026-11-04).
- ~~Gastos que paga el piloto de su bolsillo~~ → suman igual, marcados «pagado por»; la app muestra «Le debés a Pedro» (2026-11-04).
- ~~Recordatorios automáticos derivados~~ → fuera de la V1 (2026-11-04).
- ~~Trabajo de proveedores → gasto: a quién y cuándo~~ → a los owners, por privado, en el momento; si no dijo el monto, se pregunta (2026-11-04).
- ~~Permisos finos, lo que falta~~ → acceso parcial = solo mirar, solo sus caballos, sin vencimiento en la V1 (2026-11-04).
- ~~¿Costo por caballo?~~ → no en la V1 (2026-11-04).

## Negocio
- [ ] **Nombre** definitivo (PROGRAMON es provisorio) y **logo**.
- [ ] **ICP final**: ¿organizaciones grandes con manager, alto handicap sin manager, mediano handicap? Validar en entrevistas. (Tomás es solo el ejemplo del mockup.)
- [ ] Sociedad, marca y cap table del proyecto nuevo.
- [ ] **Pricing**: ¿por organización o por cantidad de caballos? ¿Mensual o anual? Ver [pricing](../05-gtm/pricing.md).
- [ ] ¿Bilingüe desde el día 1? (el polista pasa meses en Inglaterra/España; sus petiseros afuera suelen ser argentinos).
- [ ] ¿Haras/cría como segundo vertical o en paralelo? Salir de las 3–5 entrevistas a haras.

## Producto
- [ ] **App de caballos registrados** **«Polo Argentino»** (app **de terceros** del App Store con la info de los caballos registrados; no es nuestro producto, que todavía no tiene nombre): confirmar quién es el dueño, si tiene API o acuerdo de datos, qué campos trae (sangre, padre, madre, partidos jugados) y si se puede actualizar. Alternativa o complemento: registro genealógico de la AACCP. En una búsqueda web (2026-11-03) no apareció una app con ese nombre exacto; sí catálogos de cría (La Dolfina Cría, Cría Emezeta) y una app "Criadores de Polo".
- [ ] **Onboarding** (postergado por decisión). Idea discutida: primera carga por WhatsApp (caballos desde la app Polo Argentino, equipo, pagos fijos y acuerdos) más una revisión web; *white-glove* para los primeros clientes.
- [ ] **Ficha digital oficial del caballo** (libreta sanitaria digital, pasaporte equino, microchip) y camino a "aplicación autorizada" de SENASA. Ver [regulación](../01-mercado/regulacion-senasa.md).
- [ ] ¿Pedidos a proveedores desde la app? Se sacó del mockup.

- [ ] **Ruido en los grupos**: cómo distingue el bot una carga de la charla sin equivocarse, y qué hace con los mensajes dudosos.
- [ ] Si los grupos chicos (manager + un proveedor + bot) se vuelven el patrón: ¿cuántos grupos por organización y cuántos grupos en total puede tener el número del bot? (verificar límites de Meta).

- [ ] **Supuestos del modelo de dominio a confirmar** (ver [análisis de dominio](../02-producto/dominio/analisis-dominio.md), sección 5): las preguntas a owners van siempre por privado (S-15); el bot escribe por privado también a quien está solo en el grupo (S-16); las temporadas no se superponen (S-22); un owner actualiza el lugar fijo de quien viaja (S-23); ante la duda entre carga y charla, es charla (S-24); un audio con más de 4 registros se confirma con un resumen (S-25).
- [ ] **Datos del mockup** (ver [anexo C](../02-producto/dominio/anexo-c-dataset.md), sección 10): el acuerdo Les Pins es de Chantilly, sin lugar ni fechas y superpuesto con Windsor y Sotogrande; los pasajes de vuelta del 30/8 no restan en ninguna temporada.
- [ ] **Set de evaluación del bot (anexo H)**: conseguir exportaciones reales de grupos de WhatsApp de 2 o 3 organizaciones (con permiso) para medir el modelo y validar el glosario.

## Técnico
- [ ] **Grupos de WhatsApp con la API oficial**: según fuentes secundarias (2026-11-03), la Groups API de Meta tendría un **límite de 8 participantes por grupo** (contando el número del bot), requiere número verificado (OBA) y no permite agregar participantes por API (solo link de invitación). **Verificar en la documentación oficial de Meta.** Si se confirma, un grupo con polista, manager, vete, herrero y varios petiseros puede no entrar, y el bot no podría sumarse a grupos que ya existen.
- [ ] Costo y diseño de los **mensajes salientes** (plantillas de Meta, ventana de 24 h): tareas del piloto 7:00, pagos fijos, recordatorios, cierre del día 20:00.
- [ ] Proveedor de WhatsApp (BSP o Cloud API directo) y número propio del producto.
- [ ] Fuente de cotizaciones. *(La regla de negocio si no responde ya está decidida: última cotización de hasta 3 días y, si no hay, conversión pendiente; ver decisiones del 2026-11-04.)*
- [ ] Estimación real de Mauro (ver [plan](../04-plan/plan-ejecucion.md)).
