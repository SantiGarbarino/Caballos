# App mobile (PWA) — principios, diseño, navegación, Inicio y accesos

> Refleja el mockup final ([mockups](mockups/README.md)). Capturas en [`mockups/capturas/`](mockups/capturas/).

## Principios

- **Web app mobile instalable (PWA)**, se abre desde un link de WhatsApp. No es app nativa. No hay versión de escritorio: en una computadora se ve la versión de celular.
- **Usuarios**: el **polista** y su **manager**, con el mismo acceso. Piloto, petiseros y proveedores no entran a la app.
- **Login sin contraseña**: link de un solo uso por WhatsApp.
- **Para mirar y decidir.** Se puede cargar desde la app (Agregar, Nuevo, Agendar, Recordatorio, Registrar pago), pero cada formulario muestra primero el atajo de WhatsApp ("Por WhatsApp: «…»").
- **Limpia y sin tablas.** Módulos con tableros, tarjetas y listas. Sin KPIs decorativos, sin "% vs mes anterior", sin botones de acción en alertas.
- **Números grandes, en US$.** El detalle de una conversión va en letra chica dentro del gasto.

## Diseño — "Cancha de noche"

| Token | Valor | Uso |
|---|---|---|
| `--grad` | `linear-gradient(145deg, #082419, #0F3D2B, #1C6B4B)` | Fondo de la tarjeta *hero* de Inicio, tarjetas de totales y botones principales (`.btn-g`) |
| Dorado | `#D9B565` | Saludo "Buen día, Tomás", barra de la pestaña activa |
| Verde | `#155C3F` | Acentos, estados "Jugando", barras de stock OK |
| Crema | `#F3F0E8` | Fondo de la app |
| Otros | azul, violeta, "saddle" (marrón cuero) | Estados Campo, Exterior, Recuperación; alertas de stock bajo |

- Clases: `.hero` (tarjeta con degradado), `.glass` (cajas translúcidas sobre el degradado), `.btn-g` (botón con degradado).
- **Tipografías**: Manrope (texto y números), Instrument Serif (títulos), Lexend (disponible). Para la marca se probaron Lexend negrita y Caveat negrita: **se descartaron** y no se muestra la palabra PROGRAMON.
- **Números**: en el *hero* de Inicio, todos en **blanco y a 17 px**, sin colores distintos por moneda (pedido explícito: los colores distintos para US$ y € metían ruido).
- Pestaña activa: barra dorada.
- Hojas inferiores (*sheets*) con fondo oscurecido (*scrim*) para formularios y detalles.

## Navegación

Barra inferior: **Inicio · Caballos · Caballeriza · Gastos · Ingresos**.

> Historia: hubo un módulo **Día** (vareos, prácticas, plan de chukkers). Primero se le sacó lo futuro (plan de chukkers, "mañana tormenta…") y quedó solo lo pasado. Después **se eliminó** y su lugar lo ocupó **Ingresos**. Ver [historial](historial-iteraciones.md).

## Inicio

Arriba, el **hero** con degradado:

- **"Buen día, Tomás"** en dorado. A la derecha, el botón redondo **"T"** abre **Quién ve tu cuenta**.
- Dos cajas *glass*:
  - **Gastado · [período]** (ej. "Este mes"): un total en US$ (el mockup todavía muestra US$ 38.690 · $ 5.625.000 · € 4.000; hay que pasarlo a US$).
  - **Por cobrar**: en US$ (el mockup muestra US$ 366.200 · € 45.000).
- Sin palabra PROGRAMON, sin fecha y sin botón "Vista piloto".

Debajo, en este orden:

1. **Necesita tu atención** (solo informativo, sin botones de acción). Cada ítem lleva a su pantalla:
   - "Rockstar renguea de la mano izquierda" · Ramón · hoy 9:40 · con foto → **ficha de Rockstar**.
   - "Avena para 6 días" · 18 bolsas en Pilar · se usan 3 por día → **hoja del insumo**.
   - "Herraje vencido en 3 caballos" · Chiquita, Rubia y Malcriada · Cacho viene el jueves 29 → **lista de Caballos**.
2. **Gastos**: botón de período ("Este mes · Octubre, al día 22 · todos los lugares"), total en US$ y **Últimos** 3 gastos (fecha · categoría · lugar · monto). Lleva a Gastos.
3. **Lo que viene** (agenda) con botón **Agendar**:
   - SÁB 24 · Partido · Cancha 2, Pilar · 16:00.
   - LUN 26 · Dra. Ibarra, veterinaria · Control de Rockstar · vacunas de las de doma.
   - JUE 29 · Cacho, herrero · Chiquita, Rubia, Malcriada y 3 más.
   - Hoja **Agendar visita**: Quién viene (Herrero / Veterinaria / Proveedor / Otro), Qué día (Vie 23 / Lun 26 / Mié 28 / Elegir fecha), Para qué. Atajo: «El miércoles viene la veterinaria a ver a la Patria.»
4. **Pagos que vienen** · US$ 8.000: DOM 1/11 Alquiler caballeriza Pilar US$ 1.900 · DOM 1/11 Alquiler de la casa en Pilar US$ 2.500 · JUE 5/11 Sueldos de los petiseros US$ 3.000 · JUE 5/11 Sueldo del puestero US$ 600. Nota: "Los pagos que se repiten todos los meses, según tus gastos cargados."

**Se sacó de Inicio:** el plantel (tiles por estado), "Hoy en la caballeriza", el banner de WhatsApp y los KPIs. Las visitas pasaron de Caballeriza a Inicio ("Lo que viene").

## Quién ve tu cuenta

Hoja que se abre con el botón "T":

| Persona | Rol | Acceso |
|---|---|---|
| Tomás | Vos · dueño de la cuenta | Todo |
| (Manager) | Tu mano derecha | Todo, igual que vos |

Abajo, **Cargan por WhatsApp** (no entran a la app): Sofía, Pedro (piloto), los petiseros, el puestero, la veterinaria y el herrero. Botón **Sumar a alguien** (para que el bot lo reconozca).

Nota: "Tus montos los ven solo vos y tu manager. Nadie más." Botón **Invitar a tu manager**.

> El mockup muestra a Sofía con acceso a la app: pasa a **solo WhatsApp** (carga gastos, no entra). Estudio Ruiz (contador) se saca (decisión del 2026-11-03).

## Vista del piloto (fuera del recorrido)

Existe en el código del mockup pero **no se llega desde Inicio** (decisión: al piloto le alcanza WhatsApp). Contenido, por si se retoma: "Hola, Pedro · Piloto · Caballeriza Pilar"; "Todo lo de acá también te llega por WhatsApp. Gastos y sueldos los ve solo Tomás."; **Lo que te pidió Tomás** (tareas con origen: audio o WhatsApp y hora); **Rutina de hoy** (ración, vareo, herraje, Rockstar al box); **Lo que se hizo hoy**; **Stock**; **Agenda**. Se le sacó la sección Avisos.

## Pendiente de diseño
- [ ] Logo y pantalla de carga con la palabra PROGRAMON.
- [ ] Instalación como PWA (ícono, *splash*).
