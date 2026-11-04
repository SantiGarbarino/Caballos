# Módulo Caballos

> Refleja el mockup (en construcción). Las novedades, los pendientes y la actividad se cargan sobre todo por WhatsApp, en el **grupo de la organización** (manager, polista, piloto, petiseros, vete, herrero).

## Datos del caballo desde la app Polo Argentino (integración a explorar)

**La app Polo Argentino** (de terceros, no es nuestro producto) tiene la información de los caballos de polo registrados, en Argentina y en el exterior: nombre, sangre, padre, madre y hasta los partidos que jugó.

Idea (Santi, 2026-11-03): **no hacer que cada polista cargue sus caballos**. Integrarnos con la app Polo Argentino, mostrarle un **catálogo** y que el polista (o el manager) **elija cuáles son suyos**. Nosotros sumamos lo operativo: estado, lugar, novedades, pendientes, actividad, salud y gastos.

- Lo que viene de la app Polo Argentino: nombre, sexo, edad, pelaje, sangre (padre, madre), criador, partidos jugados **[a confirmar qué campos expone]**.
- Lo que es nuestro: estado, ubicación, novedades, pendientes, actividad, salud, gastos.
- Caballos que no estén en la app Polo Argentino (ej. caballos en doma sin registrar): alta por WhatsApp como hoy.
- **Pendiente:** confirmar nombre exacto y dueño de la app, si tiene API o acuerdo de datos, y condiciones de uso (ver [preguntas abiertas](../00-vision/preguntas-abiertas.md)). Alternativa: registro de la AACCP.

## Lista

- Encabezado "Caballos" y botón **Agregar**.
- **Filtros** con cantidad: Todos · 35 · Jugando · 14 · Campo · 15 · Exterior · 4 · Recuperación · 2.
- **Búsqueda** por nombre (funciona en el mockup).
- Cada fila: inicial (avatar), nombre, "N pendientes" si tiene, **línea de estado** (ej. "Vareada hoy · viaja a Inglaterra en marzo", "Herraje vencido (7 semanas)", "Pasa al campo mañana a las 7:00", "Preñada · pare en diciembre") y la píldora de estado.

### Estados

| Estado | Dónde | Ejemplos |
|---|---|---|
| **Jugando** | Caballeriza Pilar | En trabajo, vareada, herrada, va a la práctica, viaja a Inglaterra |
| **En el campo** | Campo, Cnel. Suárez | Descanso, en doma (1.er o 2.º año), retirada · madre, preñada, vuelve a Pilar en noviembre |
| **Exterior** | Windsor, Inglaterra | Invernada desde el 1/9 |
| **Recuperación** | Caballeriza Pilar · box | Tendón (reposo hasta el 15/11), post cólico (alta el 25/10) |

## Agregar caballo (hoja)

- **Objetivo: elegirlo del catálogo de la app Polo Argentino** (buscar por nombre, ver sangre y foto, "Es mío"). Todavía no está en el mockup.
- **Si no está en la app Polo Argentino, mandalo por WhatsApp.** "Un audio o un mensaje con nombre, sexo, edad y pelaje alcanza. Si mandás foto de los papeles, sacamos el microchip de ahí." Ejemplo: «Nuevo caballo: Fortuna, yegua, 6 años, zaina. Llega el sábado a Pilar.» → **Ver ejemplo en WhatsApp**.
- **O cargalo acá**: Nombre, Sexo, Edad, Pelaje → Guardar caballo.
- Si es una compra, el monto queda en Gastos › Compra de caballos (aparte de los gastos del mes).

## Ficha del caballo

1. **Encabezado**: inicial, nombre, "Yegua · 8 años · alazana", píldora de estado y ubicación ("Caballeriza Pilar").
2. **Novedad** (si hay), con quién la reportó y cuándo. Ej.: "Renguea de la mano izquierda. La reportó Ramón hoy a las 9:40, con foto. Quedó en el box hasta que la vea la Dra. Ibarra."
3. **Pendientes** (recordatorios), con botón **Recordatorio**. Cada uno: qué, cuándo, quién; se pueden tachar. Origen posible: "vos por WhatsApp", "vos en la app", "visita agendada". *("Automático por el viaje" sale de la V1: 2026-11-04.)*
4. Pestañas **Actividad** y **Salud** (solo esas dos).

### Pendientes del mockup

| Caballo | Qué | Cuándo | Quién | Origen |
|---|---|---|---|---|
| Morena | Cambiar la embocadura: probar la de goma | Mañana | Pedro (piloto) | vos por WhatsApp |
| Rockstar | Hielo en la mano izquierda, mañana y tarde | Todos los días | Pedro (piloto) | vos por WhatsApp |
| Rockstar | Control veterinario de la mano | Lun 26/10 | Dra. Ibarra | visita agendada |
| Negra | Controlar si come la ración de la noche | Hoy | Pedro (piloto) | vos por WhatsApp |
| Chiquita, Rubia, Malcriada | Herrar | Jue 29/10 | Cacho, herrero | visita agendada |
| Patria | Ecografía de control del tendón | 5/11 | Dra. Ibarra | vos en la app |
| Tormenta | Cargar en el camión al campo | Mañana 7:00 | Pedro (piloto) | vos por WhatsApp |

### Hoja Recordatorio

- Atajo: «A Rockstar hay que cambiarle la embocadura mañana, que lo haga Pedro.»
- **Qué hay que hacer**, **Cuándo** (Hoy / Mañana / Esta semana / Elegir fecha), **Quién lo hace** (Yo / Pedro (piloto) / Veterinaria).
- "Si se lo asignás al piloto, le llega por WhatsApp y le aparece en sus tareas."

### Actividad

Lista por fecha, distinta para cada caballo: vareada, montada, práctica (N chukkers), partido, herrada, veterinaria, al box. Cada evento dice quién lo reportó y cómo ("Ramón · audio y foto", "Cacho · cargó Pedro", "Dra. Ibarra · foto de la orden").

Ejemplo Rockstar: Hoy · Al box por renguera (Ramón · audio y foto) · Lun 19 · Vareada (Lucho · audio) · Vie 16 · Herrada (Cacho · cargó Pedro) · Mié 14 · Revisión veterinaria (Dra. Ibarra · foto de la orden).

Ejemplo Patria: Ayer · Control veterinario: evoluciona bien (Dra. Ibarra · audio) · Lun 12 · Ecografía del tendón (foto del informe) · Dom 4 · Entró en reposo (Tomás · audio).

### Salud

| Ítem | Ejemplo | Estado |
|---|---|---|
| Herraje | Al día · próximo a fin de noviembre | Al día / Vencido (N semanas) |
| Vacunas | Influenza y encefalomielitis · 10/08 | Al día |
| Desparasitación | Última: 02/09 · próxima en diciembre | Al día |
| Veterinaria | Control de la mano izquierda: lunes 26/10 | Pendiente |

## Lo que se sacó y por qué

- **KPIs de la ficha y minutos de vareo** ("Vareo 40 minutos"): ruido.
- **Pestaña Costos** (costo por caballo): ruido; se deja para evaluar más adelante.
- **Pestaña Papeles/SENASA**: la ficha con documentación oficial queda para más adelante (ver [regulación](../01-mercado/regulacion-senasa.md)).

## Más adelante

- Documentación oficial: microchip, libreta sanitaria digital, pasaporte equino, AIE, vacunas para exportar.
- Traslados con historial (Pilar ↔ campo ↔ exterior). Hoy se reportan por WhatsApp ("La Tormenta se va al campo mañana").
- Cría: madres, preñeces, servicios, ET.
- Propiedad (propio / de un patrón / en sociedad) **[HIPÓTESIS, no está en el mockup]**.
