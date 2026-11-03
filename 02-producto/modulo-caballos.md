# Módulo de caballos (fase 2)

> En el MVP solo existe el **alta básica** del caballo para poder asignarle gastos. Todo lo demás es fase 2. Igual, el modelo de datos lo contempla desde el inicio.

## Ficha del caballo

| Campo | Notas |
|---|---|
| Nombre | Como lo llaman ("la Pampa") |
| Sexo | Yegua / caballo / padrillo |
| Pelaje | Zaino, alazán, tordillo, moro, overo… |
| Edad / año de nacimiento | |
| Raza / registro | Polo Argentino, n° AACCPA (opcional) |
| Padre / madre | Opcional (clave para haras) |
| Marca | Opcional |
| Nivel | Verde / a medio hacer / hecho / crack |
| Estado | En trabajo · jugando · lesionado · parado · a campo · en doma · vendido · muerto |
| Ubicación | Caballeriza / campo / club / temporada afuera |
| Propiedad | Propio · de patrón X · en sociedad (%) · alquilado |
| Fotos | Desde WhatsApp |
| Costo acumulado | Calculado de los gastos asignados |
| Valor estimado | Opcional (para decidir venta) |

## Eventos que se reportan por WhatsApp

| Evento | Ejemplo de mensaje |
|---|---|
| **Alta / compra** | "Compré una yegua zaina de 6 años, la Negra, en 15 mil verdes" |
| **Baja / venta / muerte** | "Vendí la Morocha" |
| **Traslado** | "Mandé 10 caballos a Tortugas" · "La Pampa se fue a campo" |
| **Herraje** | "Herró el Gordo a la Pampa, la Tormenta y el Rayo" → registra fecha + gasto |
| **Sanidad** | "Vacuné a todos contra influenza" · "Sacamos sangre para AIE" |
| **Lesión / estado** | "La Tormenta está rengueando, la paramos 15 días" |
| **Juego** | "Jugué la Pampa 2 chukkers en el partido de hoy" (fase 3: rendimiento por caballo) |
| **Cría** (haras) | "Transferimos embrión de la Pampa a la receptora 34" |

## Alertas y recordatorios (fase 2)
- Herraje vencido (> X semanas desde el último).
- Vencimiento de AIE / vacunas / documentación para viajar.
- Caballo parado hace más de X días.
- Costo por caballo por encima del promedio.

## Stock (vista de la app)
- Total de caballos por estado, por ubicación, por propietario.
- Cuántos están "para jugar" hoy.
- Movimientos recientes.
