# Módulo Caballeriza — stock y equipo

> Refleja el mockup final. Visitas (herrero, veterinaria) se movieron a Inicio ("Lo que viene").

## Sede

Selector **Pilar · 16 caballos** / **Campo · 15 caballos**. Cada caballeriza tiene su propio stock y su propio consumo.

## Stock · para cuántos días alcanza

Cada insumo muestra días que alcanza, barra (marrón si alcanza menos de 8 días), "N unidades · se usan X por día" y, a veces, el último ingreso.

### Cómo se calcula (explícito, pedido de Santi)

Santi preguntó de dónde salía "se usan 3 por día". Se hizo configurable:

**unidades por día = consumo por caballo por día × caballos en ese lugar ÷ tamaño del envase**
**días que alcanza = stock ÷ unidades por día**

### Pilar (16 caballos)

| Insumo | Stock | Envase | Consumo por caballo/día | Por día | Alcanza |
|---|---|---|---|---|---|
| Avena | 18 bolsas | Bolsa de 40 kg | 7,5 kg | 3 bolsas | **6 días** |
| Fardos de alfalfa | 140 fardos | Fardo | 1 fardo | 16 | 8 días (último ingreso 18/10) |
| Viruta para cama | 35 bolsas | Bolsa, por box | 0,2 bolsas | 3,2 | 10 días |
| Alimento balanceado | 22 bolsas | Bolsa de 25 kg | 2 kg | 1,3 | 17 días |
| Electrolitos y suplementos | 4 potes | Pote de 3 kg | 30 g | 0,2 | 25 días |

### Campo (15 caballos)

| Insumo | Stock | Envase | Consumo por caballo/día | Caballos | Por día | Alcanza |
|---|---|---|---|---|---|---|
| Rollos | 22 rollos | Rollo de 400 kg | 12 kg | 15 | 0,5 | 1 mes |
| Sal mineral | 6 bolsas | Bolsa de 25 kg | 40 g | 15 | ~0 | Más de 2 meses |
| Alimento balanceado (doma) | 8 bolsas | Bolsa de 25 kg | 3 kg | **solo las 5 de doma** | 0,6 | 13 días |

Etiquetas de días: "N días", "1 mes" (≥ 30), "Más de 2 meses" (≥ 60), "Sin consumo cargado".

## Hoja del insumo (tocar un ítem)

Ej. **Avena · Pilar**: "6 días de stock al ritmo actual". Hay 18 bolsas · Se usan por día 3 bolsas · Consumo cargado 7,5 kg por caballo · Caballos 16 · Último ingreso: 30 bolsas el 20/10 · Pedro.

Sugerencia: "Según los conteos de Pedro, se están usando 3,4 bolsas por día, no 3." → **Usar 3,4 por día**. Botón **Cambiar consumo**.

## Hoja Consumo

"Consumo diario · Pilar". Atajo: «Cada caballo come 7 kilos y medio de avena por día.» Texto: "Cargá cuánto come cada caballo por día. PROGRAMON lo multiplica por los caballos que hay en Pilar y te dice para cuántos días alcanza. Cada caballeriza tiene el suyo." Por insumo: caballos, campo editable (kg / fardos / bolsas / g por caballo por día), envase y cálculo en vivo ("= 3 bolsas por día · alcanza 6 días") → **Listo**.

## Equipo

| Persona | Rol | Resumen en la lista |
|---|---|---|
| Pedro | Piloto · Caballeriza Pilar | 4 mensajes hoy |
| Ramón | Petisero · Caballeriza Pilar | 3 msj · 6 vareos |
| Lucho | Petisero · Caballeriza Pilar | 2 msj · 6 vareos |
| Juanca | Petisero · Windsor, Inglaterra | Ayer, 1 msj |
| Don Aníbal | Puestero · Campo, Cnel. Suárez | **Sin mensajes hace 2 días** (destacado) |

### Vista de una persona

Contadores (ej. Pedro: 4 mensajes hoy · 31 esta semana · 5/6 tareas hechas) y **Sus mensajes**: tipo (Mensaje / Audio / Foto), hora, texto y **qué generó** cada uno:

- Pedro 7:30 «Ración de la mañana dada, los 16.» → Parte del día.
- Pedro 11:02 (audio) «Vino Cacho, herró a la Bruja, la Gitana, la Dinamita y la Lucera. Son 180 lucas, lo pagué yo.» → Gasto en Herrería + herraje en 4 fichas.
- Pedro 12:18 (foto) «Se está terminando la avena.» → Stock de avena: 6 días.
- Pedro 12:20 «Quedan 18 bolsas.» → Alerta en tu Inicio.
- Ramón 9:38 (audio) vareos de Morena, Tordillo, Cautiva y Gitana + renguera de Rockstar → 4 vareos + novedad de Rockstar; 9:40 foto → guardada en la ficha; 12:05 Malcriada y Chiquita → 2 vareos más.
- Lucho 8:15 «La Negra no terminó la ración de la mañana.» → Novedad en la ficha de Negra; 10:30 seis vareos.
- Juanca (ayer 17:10) «Recorrí las cuatro en el paddock, todo bien. Mucho barro, les puse las mantas.» → Actividad en 4 fichas.
- Don Aníbal: "No mandó mensajes hoy. El último fue el lunes 20 a las 18:40." (15 caballos a cargo).

## Lo que se sacó

- Visitas (pasaron a Inicio).
- Banners de "ajuste" y "reponer".
- "Pedir al proveedor".
