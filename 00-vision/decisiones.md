# Log de decisiones

Formato: fecha · decisión · contexto y porqué · quién. Las más nuevas arriba.

> Las decisiones de las sesiones de producto del **22 al 27/10/2026** (Santi con Claude, construyendo el mockup PROGRAMON) se registraron el 2026-11-03. Cuando se sabe el día exacto, se indica. Para el detalle de qué se cambió en cada vuelta del mockup ver [historial de iteraciones](../02-producto/historial-iteraciones.md).

---

## 2026-11-04 · Modelo de dominio: decisiones para el desarrollo

> Santi decidió estas 31 preguntas al armar el modelo de dominio ([anexo A](../02-producto/dominio/anexo-a-decisiones.md) tiene el detalle y el porqué de cada una). **Nada es intocable:** es lo que hoy creemos mejor y se ajusta con el MVP. Son decisiones de producto, no están validadas con usuarios.

### El bot responde lo menos posible
- **Contexto:** no estaba definido a quién le pregunta el bot ni cuándo contesta por escrito.
- **Decisión:** si tiene una duda, le pregunta a **quien mandó el mensaje**, sea quien sea. A quien registra un **gasto o un ingreso** le contesta **siempre**, por **privado**, qué entendió y qué cargó; en el grupo solo reacciona con ✅. Para el resto (novedades, vareos, stock), solo ✅ si no hay dudas. El trabajo de un proveedor que puede ser gasto, la pregunta del pago fijo y un ingreso que manda alguien sin permiso van a los owners, por privado.
- **Quién:** Santi.

### El lugar de un gasto no se pregunta: sale del calendario
- **Contexto:** preguntar el lugar en cada gasto se vuelve engorroso.
- **Decisión:** en la app hay un **calendario** donde el polista carga las fechas en que va a estar en cada lugar (sus temporadas, cada una con un **lugar principal**). El lugar de un gasto sale, en orden: del **lugar nombrado** en el mensaje (siempre gana) → de los **caballos nombrados** si están todos en un lugar → del **calendario**, si lo carga un owner → del **lugar fijo** de quien lo carga (Don Aníbal → Campo) → si nada lo da, **General**. Un owner lo corrige o lo asocia a otra temporada desde la app. Hay **gastos generales**, sin lugar ni temporada.
- **Quién:** Santi (idea del calendario: Santi).

### Temporada = la estadía del polista en un lugar
- **Decisión:** una temporada es el tiempo en que el polista estuvo (o va a estar) en uno o más lugares, con fechas y un lugar principal. Puede incluir varios torneos, patrones e ingresos; en un año hay varias. Los gastos de ese lugar fuera de esas fechas (la invernada de Windsor entre temporadas) son del **destino**, no de la temporada.
- **Quién:** Santi.

### Resultado por temporada
- **Decisión:** ingresos de la temporada (**acordados y ya cobrados**, los dos) − gastos de sus lugares en sus fechas − gastos que un owner asoció a mano a esa temporada. Las **ventas y compras de caballos van aparte** y no entran en el resultado.
- **Quién:** Santi.

### No hay gasto por caballo
- **Decisión:** un gasto se vincula a los caballos a los que se refiere («Herraje de 4 caballos»), pero no se reparte el monto. En la ficha de cada caballo queda **qué se le hizo** (herrado, vacunado, medicamento), **sin el monto**.
- **Quién:** Santi.

### Eliminar registros y acuerdos caídos
- **Decisión:** un acuerdo o una venta se pueden marcar como **caídos** (lo cobrado queda, se deja de esperar el resto). **Quien cargó algo puede eliminarlo, y un owner puede eliminar cualquier registro**: desaparece de la app y de los totales; el mensaje de origen queda oculto (no se borra) para auditoría y para medir la IA.
- **Quién:** Santi.

### Reintegros: se anota lo que se dice
- **Decisión:** un reintegro se anota tal como se dice (monto y moneda), valuado con la cotización de su día; puede haber diferencia con el gasto original. Si devuelve menos de lo pendiente, el resto queda pendiente sin preguntar. Un pago va a cuenta del acuerdo salvo que el mensaje diga que es un reintegro.
- **Quién:** Santi.

### Plata: quién carga y quién ve
- **Decisión:** **gastos** los puede cargar cualquier miembro; **ingresos**, solo owners; los proveedores **nunca** gastos. Las consultas de plata **nunca** se contestan en el grupo; al owner, por privado. Quien tiene acceso parcial solo mira, y solo sus caballos. Manager es un **rol** y owner es un **permiso**: van por separado; siempre hay al menos un owner.
- **Quién:** Santi.

### Números, fechas y horarios
- **Decisión:** cotización **del día del gasto** (fin de semana o feriado: último día hábil); el monto en US$ se **redondea a entero** al registrar y los totales suman esos enteros; un owner puede corregir la cotización. Si falla la fuente del blue, se usa la última de hasta 3 días y, si no hay, la conversión queda pendiente («≈»): nunca se pregunta. La fecha es la que dice el mensaje («el viernes» = el último viernes); si no dice, el día local de quien lo manda. Cada persona tiene su **huso horario**: los avisos salen a su hora local. US$ es la moneda de todas las organizaciones en la V1.
- **Quién:** Santi.

### "Lo pagué yo" y "queda a pagar"
- **Decisión:** el gasto suma igual; se marca quién pagó o «a pagar» y la app muestra «Le debés a Pedro US$ 116». Sin cuenta corriente con comercios en la V1.
- **Quién:** Santi.

### Otras decisiones del modelo
- Venta de caballo: sale del plantel el día que se entrega. Patrón y comprador: contraparte con nombre y apodos dentro de la organización, sin acceso. Situación del caballo (en trabajo, descanso, doma, recuperación, retirada) separada del lugar; los filtros de la app no cambian. Sin pendientes automáticos (AIE por viaje, etc.) en la V1. Sin propiedad de caballos de terceros en la V1. Una pregunta sin respuesta se repite una vez y después queda «sin terminar» en la app (no suma). Varios mensajes del mismo emisor en el mismo chat, en 5 minutos y antes de confirmar, son una carga. Los conteos de stock solo sugieren un ajuste del consumo. Días de stock truncados. «Pagos que vienen» = próximos 15 días.
- **Quién:** Santi.

---

## 2026-11-03 (sesión 11) · Permisos finos: qué ve cada usuario

### Los permisos no son solo por módulo: se elige qué ve cada persona
- **Contexto:** con habilitar un módulo entero no alcanza (ej. el veterinario no tiene por qué ver los 35 caballos).
- **Decisión:** al invitar o desde la ficha de la persona en Equipo, un owner elige **Qué ve en la app**:
  - **Nada** → solo WhatsApp (por defecto para todos los que no son owners).
  - **Todo** → owner (no se ofrece para proveedores).
  - **Una parte** → elige **secciones** (Novedades del día, Caballos, Lo que viene, Caballeriza) y **qué caballos**: todos, **los de un lugar** (Pilar, Campo, Windsor) o **algunos caballos** elegidos uno por uno.
  - **Gastos e Ingresos: solo owners**, nunca para proveedores.
- **Ejemplo del mockup:** la veterinaria ve Novedades del día, Caballos y Lo que viene, solo de 4 caballos (Rockstar, Patria, Nube y Negra).
- **Quién:** Santi.

## 2026-11-03 (sesión 10) · Owners, permisos por usuario y un bot que no se equivoca

### Owners de la organización y permisos por usuario
- **Quien crea la organización** (el polista o el manager) es **owner**. Puede invitar usuarios y, al invitarlos, les da el acceso que corresponde. Si el polista crea la organización e invita a su manager con el rol de manager, le da **todos los accesos** y el manager pasa a ser también owner.
- Los owners (polista y/o manager) **configuran qué ve cada usuario** desde **Equipo**: solo WhatsApp, o una parte de la plataforma.
- **Por defecto**: veterinario, herrero, piloto, petiseros, puestero y familiares → **solo WhatsApp**.
- **Excepción configurable**: si un polista quiere que su veterinario vea, por ejemplo, el módulo de **Caballos** y las **novedades diarias de la caballeriza** (pero nunca Gastos ni Ingresos), un owner se lo habilita desde Equipo. "Cada organización es un mundo": en una el veterinario ve algo, en otra nada.
- **Reemplaza** a "usuarios de la app: solo polista y manager". Eso sigue siendo el caso típico, pero ahora es configurable por usuario.
- Los owners son también **quienes reciben las preguntas del bot** (confirmar un gasto, duplicados, trabajo de proveedores). Así se resuelve "quién maneja la operación": depende de quién creó la organización y a quién hizo owner.
- **Quién:** Santi.

### El bot nunca carga una charla
- Un mensaje como «che, ¿cuánto te salió el flete a vos?» es una pregunta y **nunca** se carga. El modelo tiene que ser **muy inteligente** para distinguir una carga de la charla.
- **Quién:** Santi.

### Proveedores sin gastos: confirmado
- El proveedor carga el trabajo y el bot les pregunta a los owners si lo registran como gasto y por cuánto.
- **Quién:** Santi.

## 2026-11-03 (sesión 9) · Operatoria de WhatsApp con varias organizaciones

### Ruteo de mensajes de proveedores con varios clientes
- Grupo → organización del grupo. Privado de alguien con una sola organización → esa. Privado de un proveedor con varias → el bot deduce por caballo o cliente; si no puede, pregunta con botones de clientes recientes, recuerda la elección un rato, cada confirmación dice la organización y se puede corregir. Nunca se muestran datos de otra organización.
- **Quién:** Santi ("es correcto y espero que así sea en el producto").

### Los proveedores no registran gastos
- Veterinario, herrero, etc. cargan **el trabajo**; si implica un gasto, el bot le pregunta al polista o al manager si lo registra. Detalle a definir.
- **Quién:** Santi.

### Detección de duplicados, con este nivel de detalle
- Antes de cargar un gasto, buscar uno parecido (monto, categoría, fecha cercana, de cualquier grupo o persona) y preguntar si es el mismo.
- **Quién:** Santi ("muy importante").

### En los grupos, el bot confirma con una reacción
- ✅ cuando carga; contesta por escrito solo si tiene una duda, diciendo qué cargó. No toca la charla. Se les pedirá a los usuarios no usar los grupos para cualquier cosa.
- **Quién:** Santi.
- *(Ajustada el 2026-11-04: un gasto o un ingreso se confirma además por escrito, **por privado**, a quien lo cargó.)*

### Una organización puede tener varios grupos de WhatsApp
- Ej.: manager + veterinario + bot, manager + herrero + bot. Cada grupo pertenece a una sola organización.
- **Quién:** Santi (idea propia).

### Altas y bajas del equipo: polista o manager
- Cada polista es una mini organización: en algunas el polista habla con todos; en otras solo juega y el manager hace todo. Cualquiera de los dos gestiona el equipo y recibe las preguntas del bot, según cómo se configure.
- **Quién:** Santi.

## 2026-11-03 (sesión 8) · Chats, invitaciones y categorías

### Al invitar, se elige si va al grupo, al privado o a los dos
- **Contexto:** Santi preguntó cómo saber si una invitación era para el grupo o para hablar con el bot por privado.
- **Decisión:** la invitación tiene «Cómo lo sumás»: *al grupo de la organización* (link del grupo) y/o *por privado con el bot* (el bot le escribe para que lo agende), con valores sugeridos por rol. Ver [flujos de WhatsApp](../02-producto/flujos-whatsapp.md).
- **Quién:** Santi.

### Los chats de ejemplo se muestran como en WhatsApp
- **Contexto:** con una fila de 12 conversaciones no se entendía qué era cada una.
- **Decisión:** lista de chats: el grupo y un privado por persona. Los ejemplos del polista van todos en **su** chat privado, separados por fecha.
- **Quién:** Santi.

### Veterinario y Herrero: qué incluyen
- **Veterinario**: visitas, medicamentos, vacunas, desparasitaciones, análisis y estudios. **Herrero**: herrajes, despalmes, herraduras y clavos. Un pago mixto se separa en dos gastos. Las demás categorías se afinan con las entrevistas. Ver [Gastos](../02-producto/modulo-gastos-ingresos.md).
- **Quién:** Santi.

## 2026-11-03 (sesión 6) · Ajustes del mockup para la V1

### Acuerdos en euros: cómo se pasan a dólares
- Lo **ya cobrado**: a la cotización del euro **del día de cada pago** (queda fija).
- Lo que **falta cobrar**: a la cotización **de hoy**, con un **«≈»** adelante porque puede cambiar. En letra chica: «€ 45.000 al euro de hoy (US$ 1,09)».
- Resuelve la pregunta abierta sobre ingresos en otras monedas.
- **Quién:** Santi.

### Datos de los caballos: en el mockup, sin nombrar la fuente
- La ficha muestra **toda la información del caballo** (padre, madre, criador, nacimiento, registro, microchip, marca, partidos jugados) en una pestaña **Datos**.
- Cómo se carga se define después: integración con la app de los caballos de polo registrados **«Polo Argentino»**: una app **de terceros** que ya existe en el App Store con la info de los caballos registrados (no confundir con "Cría Polo", nombre que se usó antes por error, ni con nuestro producto, que todavía no tiene nombre) o carga manual por WhatsApp o web. En el mockup **no se nombra** ninguna app.
- Esa información sola no le agrega valor al polista ni al veterinario (ya la ven en esa app); el valor es tenerla junto con lo operativo.
- **Quién:** Santi.

### Equipo sale de Caballeriza y pasa a su propia pantalla, desde Inicio
- Botón **Equipo** en Inicio → pantalla para gestionar a la gente: quiénes entran a la app (polista y manager), quiénes cargan solo por WhatsApp, qué mandó cada uno, y **Invitar** (le llega un WhatsApp; con responder «Sí» queda adentro).
- Reemplaza la hoja «Quién ve tu cuenta».
- **Quién:** Santi.

### El mockup muestra un grupo de WhatsApp de la organización
- Con 7 personas + el bot, para no prometer más de lo que la API de grupos podría permitir (límite de 8 a verificar).
- **Quién:** Santi.

## 2026-11-03 (sesión 3) · Correcciones de Santi a la KB

> Estas decisiones **reemplazan** a las anteriores que las contradigan (están marcadas como *reemplazada* más abajo).

### El nombre del producto no está definido
- **PROGRAMON** es un **nombre provisorio** de trabajo (es el que usa el mockup). Puede cambiar.
- **Quién:** Santi.

### Producto totalmente nuevo; de Queiros solo usamos el know-how
- No es "Queiros como motor" ni una marca vertical de Queiros. Es un **producto nuevo**, sin mezclar **nada** de Queiros (ni código, ni marca, ni producto, ni sus restricciones).
- Se parecen en la idea: **WhatsApp como interfaz + IA + web app mobile-first con módulos**. Nos apalancamos en lo que aprendimos construyendo Queiros.
- Si algo se sacó de Queiros (ej. recordatorios), **eso no aplica acá**. Ver [aprendizajes de Queiros](../03-tecnico/aprendizajes-queiros.md).
- Lo único que se mantiene: **el equipo (Santi, Mati y Mauro)**.
- **Quién:** Santi.

### Es un proyecto paralelo, sin timebox atado a Queiros
- Se saca el timebox de diciembre 2026 y el criterio de MRR (era algo personal de Santi sobre Queiros). Si el mercado responde, se encara de lleno.
- **Quién:** Santi.

### Dos tipos de usuario: los de la app (polista y manager) y los de solo WhatsApp
- El **manager** es la mano derecha de las organizaciones grandes y va a ser un usuario muy importante: registra todo (caballeriza, stock, lo que habla con el veterinario y el herrero, el día a día de cada yegua).
- **El manager ve exactamente lo mismo que el polista.** No hay información que vea uno y no el otro.
- Muchas veces el usuario no va a ser el jugador sino el manager: el producto y el vocabulario tienen que contemplarlo.
- **Usuarios de la app** (ven e interactúan con los datos en la web): **polista y manager**.
- **Usuarios de solo WhatsApp** (*aclarado por Santi*): son **parte de la organización** y cargan por el bot, pero **nunca entran a la app**. Lo que mandan se registra y figura en la plataforma con **quién lo cargó**. Ejemplos:
  - **Un familiar o asistente** que ayuda al polista con gastos y compras: le manda un gasto al bot y queda registrado con su nombre como quien lo cargó.
  - Un **petisero** avisa que una yegua no comió: queda como alerta en la plataforma, cargada por ese petisero.
- Cada polista tiene su **organización**: una mini organización con la gente que trabaja para él (manager, petiseros, piloto, puestero, algún familiar) y quiere registrar todo.
  - También piloto, puestero, y los proveedores (vete, herrero) desde el grupo.
- El contador no es usuario: recibe el export por mail.
- **Quién:** Santi.

### El patrón no existe para la plataforma
- No es usuario, no es comprador, no es canal. Solo aparece como **la contraparte que le paga al polista** (acuerdos, pagos y reintegros en Ingresos).
- **Quién:** Santi.

### Grupos de WhatsApp y chat privado
- El bot está en el **grupo de WhatsApp de la organización** (manager, polista, veterinario, herrero, algún petisero). Lo que se manda ahí sobre una yegua o la caballeriza entra a la app.
- Gastos e ingresos que el polista no quiere que vean el veterinario o los petiseros se mandan por **chat privado con el bot**.
- *Aclarado por Santi:* la plata **en general** va por privado, **pero no obligatoriamente**. Si en el grupo se habla de un precio o un gasto, **se registra igual**.
- **Quién:** Santi.

### Piloto y petiseros trabajan para una sola organización; los proveedores, para varias
- Piloto, petiseros y puestero son siempre de **una** organización.
- Un **veterinario o herrero** puede trabajar para varios polistas: carga a través del **grupo de cada cliente**. Si le escribe al bot **por privado**, el bot le pregunta **para cuál de sus clientes** es.
- **Quién:** Santi.

### Moneda de la plataforma: dólares, con conversión automática
- **Reemplaza a** "Monedas siempre separadas; nunca se convierte".
- La gran mayoría de los gastos del polista son en dólares. La app muestra todo **en US$**.
- Un gasto en **pesos** se convierte **automáticamente al dólar blue del día** en que llega. El bot **no le pregunta el tipo de cambio** al polista: eso es fricción.
- **Cotización = promedio entre el blue compra y el blue venta**, de cualquier sitio que lo publique (Rava Bursátil, DólarHoy u otro: el que sea más fácil de integrar). Ej.: compra 1.530 y venta 1.570 → 1.550.
- En el detalle del gasto, en letra chica y prolija: «$ 800.000 al dólar blue del 22/10 ($ 1.550) = US$ 516».
- **Euros** (y otras monedas): misma lógica si hay una fuente para la cotización. Si no la hay, el bot pregunta: «Me estás cargando un gasto en euros y en la app los tengo en dólares. ¿Sabés el tipo de cambio?».
- Se guarda siempre el **monto y la moneda originales**, la cotización usada y su fuente.
- **Quién:** Santi.

### Comprobante: si no hay foto, se ve el audio o el mensaje
- Cada gasto muestra **lo que lo generó**: la foto (factura, remito, ticket) si hay, y si no, **el audio o el mensaje de texto** que se mandó al bot.
- **Quién:** Santi.

### Recordatorios sí
- «Mañana haceme acordar tal cosa» → al día siguiente el bot se lo recuerda. Vale para el polista y el manager.
- **Quién:** Santi.

### Datos de los caballos desde la app Polo Argentino (integración a explorar)
- La app Polo Argentino tiene la información de los caballos de polo registrados (nombre, sangre, padre, madre, partidos jugados), en Argentina y afuera.
- Idea: integrarla para que el polista **elija sus caballos de un catálogo** en vez de cargarlos uno por uno. Ver [Caballos](../02-producto/modulo-caballos.md) y [preguntas abiertas](preguntas-abiertas.md).
- **Quién:** Santi.

### UI sin tablas: módulos con tableros
- Nada de planillas ni tablitas (como Queiros hoy). Todo en **módulos con tableros, tarjetas y listas**, como el mockup.
- **Quién:** Santi.

### Tomás y su organización son ficticios
- Son el ejemplo del mockup, que Santi sigue ajustando. **No definen el ICP.** Cuando el mockup esté terminado, Santi lo adjunta como referencia.
- Pensai (Joaco) **no es referencia ni competencia**: se saca de la KB.
- **Quién:** Santi.

---

## 2026-11-03

### La KB en GitHub refleja lo charlado en las sesiones de producto
- Si algo de la KB contradecía lo decidido en las sesiones 22–27/10, **manda lo decidido en las sesiones**. Se reescribieron visión, PRD, módulos, flujos, modelo de datos, plan y GTM.
- **Quién:** Santi.

## Sesiones 22–27/10/2026 · Estrategia

### Vertical = mundo del caballo; entrada = polo; después haras/cría
- **Porqué:** Queiros multi-industria complica venta y producto. El rubro mueve mucho dinero y no tiene tecnología. La red de Santi está en el polo. Haras/cría puede ser el mercado más grande.
- **Quién:** Santi, Mati y Mauro (ya lo hablaron entre los tres).

### ~~Queiros es el motor, PROGRAMON es la marca vertical~~ (reemplazada el 2026-11-03: producto nuevo, nombre provisorio)
- Nombre de trabajo: **PROGRAMON** (antes "Un Programón"). Logo pendiente.

### Validar primero con el mockup
- **Porqué:** el ICP es muy sensible a algo feo o engorroso. Primero mockup, después una versión web para celular simple e intuitiva. SENASA y otras funciones se suman de a poco.

### El onboarding queda fuera por ahora
- "No nos metamos con el onboarding todavía, que vean directo la versión final." La idea discutida está en [preguntas abiertas](preguntas-abiertas.md).

### Ficha digital oficial del caballo / habilitación SENASA: más adelante
- Le interesa a Santi como diferencial (digitalizar las fichas que hoy son de papel). Se posterga para no frenar la validación del núcleo (gastos).

## Sesiones 22–27/10/2026 · Producto

### Formato: web app mobile instalable (PWA), no app nativa
- **Porqué:** se comparte por link de WhatsApp, no pasa por tiendas y se itera rápido.

### Persona del mockup: profesional de alto handicap sin manager (ejemplo ficticio)
- Es solo el ejemplo del mockup; no define el ICP (2026-11-03). El polista hace todo él mismo. Tiene ~35 caballos, todo ficticio pero creíble, con operación en Argentina y en el exterior. Ver [segmentos y personas](../01-mercado/segmentos-y-personas.md).

### Cinco módulos: Inicio · Caballos · Caballeriza · Gastos · Ingresos
- El módulo **Día** existió y se **eliminó**; su lugar lo ocupó **Ingresos**.
- **Gastos es el módulo principal**: el dolor número uno. Tiene que ser súper claro y no dejar lugar a dudas.

### Ante la duda, el bot pregunta
- Nunca adivina el destino ni la categoría. Ejemplo: "Le pagué 600 dólares al veterinario" → "¿Para qué caballos es: Pilar, el campo o Windsor?".
- *(Ajustada el 2026-11-04: el **lugar** ya no se pregunta; sale del mensaje, de los caballos, del calendario o del lugar fijo de quien carga. Para categoría, caballos y cliente, sigue preguntando.)*

### ~~Monedas siempre separadas; nunca se convierte~~ (reemplazada el 2026-11-03: todo en US$ con conversión automática)
- Totales por moneda (US$, $, €; £ en Ingresos). No hay total combinado. No hay "+X% vs mes anterior" (se pidió sacarlo).
- La **moneda es independiente del lugar**: se puede pagar en US$ algo del campo estando en Sotogrande.

### Los gastos se clasifican por destino (lugar), no por dónde estaba el polista
- Ejemplo de Santi: US$ 2.000 para el campo pagados desde Sotogrande cuentan como **Campo**.
- Veterinaria "afuera" y comida "afuera" no son categorías aparte: son la misma categoría con otro **lugar**.
- *(Sigue vigente: el destino nombrado siempre gana. Desde el 2026-11-04, si el mensaje no lo dice, lo completa el calendario o el lugar fijo; si no, es un gasto General.)*

### Una sola lista de gastos como fuente de verdad
- **Porqué:** en una versión anterior los totales no coincidían con los ítems (US$ 14.200 de tacos contra 540 + 600 visibles) y Santi no entendía cómo se formaban. Ahora todo total es la suma de los gastos visibles para el período y el lugar elegidos.

### Taxonomía de gastos por grupo › categoría
- Definida a partir de la lista que dio Santi. Ver [módulo de gastos e ingresos](../02-producto/modulo-gastos-ingresos.md). "Trailer y camión" contratados son **Fletes de caballos**.

### Compra de caballos va aparte (inversión)
- Se ve como grupo propio en Gastos y **no** entra en el resultado por temporada.

### Ingresos = acuerdos con patrones + ventas de caballos + reintegros
- Por cobrar = acordado − cobrado + gastos que cubre el patrón pendientes de reintegro.
- Configurable por WhatsApp o desde la app.

### El piloto solo usa WhatsApp (sigue vigente: petiseros, piloto y puestero no tienen acceso a la app)
- Le llegan tareas y avisos por WhatsApp y las tacha respondiendo. **No necesita vista web** (decisión de Santi del 27/10). En el mockup se usa "piloto" en lugar de "encargado".

### Inicio informativo, sin botones de acción en las alertas
- **Porqué:** Santi dijo que los botones de acción en las alertas no son viables. Las alertas abren la ficha, el insumo o la lista.

### Se sacaron: KPIs, minutos de vareo, cantidades de chukkers/vareos/prácticas, pestaña Costos, pestaña Papeles/SENASA, plantel en Inicio, "Hoy en la caballeriza", banner de WhatsApp, plan de chukkers
- **Porqué:** ruido. El polista no necesita esos números; ensucian la pantalla.

### Consumo de stock configurable por caballeriza
- Los días que alcanza un insumo salen de **consumo por caballo por día × caballos en ese lugar ÷ tamaño del envase**. Santi preguntó de dónde salía "se usan 3 por día" y se hizo explícito y editable.

### Pochola pasa a llamarse Rockstar
- Pedido de Santi (el id interno del mockup sigue siendo `pochola`).

### Lugares del exterior: Windsor (Inglaterra) y Sotogrande (España)
- Reemplazan a Florida/Wellington como temporadas del mockup. Wellington queda como acuerdo futuro (Palm Ridge 2027).

### Diseño "Cancha de noche"
- Degradado verde oscuro con dorado y fondo crema. El saludo va en dorado y **todos los números en blanco y del mismo tamaño** (antes los US$ y € tenían colores distintos y eso generaba ruido). Sin la palabra PROGRAMON, sin fecha y sin botón "Vista piloto" en el header. Se descartaron las fuentes Lexend para la marca y Caveat.

### Forma de trabajo del mockup
- Se edita el **borrador** en Claude. El **link compartible** se actualiza solo cuando Santi dice "Dale, listo todo esto. Reemplazalo". Ver [mockups](../02-producto/mockups/README.md).

---

## 2026-11-03 · Decisiones iniciales del brain (siguen vigentes, con ajustes)

### Arrancamos por el polo, no por haras ni caballerizas en general
- **Porqué:** es el nicho con dolor económico más claro (mucho gasto, mucha informalidad), comunidad chica e interconectada (boca en boca), y el equipo tiene acceso a la red.
- **Ajuste:** la visión es el mundo del caballo (ver arriba).

### WhatsApp como interfaz de carga + web app mobile-first para visualizar
- **Porqué:** el polista no usa computadora; vive en WhatsApp.
- **Implicancia:** no se diseña ninguna pantalla para desktop.

### El MVP se centra en gastos (e ingresos)
- **Ajuste:** el mockup ya muestra cinco módulos. Gastos sigue siendo el centro. Para el primer desarrollo, ver la priorización en el [roadmap](../04-plan/roadmap.md).

### ~~Reutilizamos la base de Queiros~~ (reemplazada el 2026-11-03)
- Solo el know-how. Ver [aprendizajes de Queiros](../03-tecnico/aprendizajes-queiros.md).

### El repo `Caballos` es el knowledge base del proyecto
- Toda la info se mantiene en `.md` en este repo. Ver [CLAUDE.md](../CLAUDE.md).
