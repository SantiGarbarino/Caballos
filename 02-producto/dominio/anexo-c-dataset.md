# Anexo C — Dataset de referencia con resultados esperados

> **Qué es:** la organización ficticia del mockup (Tomás) convertida en un **juego de datos de prueba** con todos los resultados **ya calculados** según las reglas decididas en el [anexo A](anexo-a-decisiones.md). Si el producto, cargado con estos datos, no muestra exactamente estos números, hay un bug.
> **Cómo se usa:** Mauro lo carga como datos de prueba; los escenarios del [anexo B](anexo-b-escenarios.md) lo usan como punto de partida ("dado el dataset C…"). Cualquier cambio de regla obliga a recalcular este anexo.
> **Nada es intocable:** las reglas que usa este anexo son las decididas hoy; si cambian con el MVP, se recalcula.
> **Fuente:** `02-producto/mockups/dataset-ficticio.md` de la KB (generado del mockup v7), con los ajustes de la sección 1.
> **"Hoy" = jueves 22/10/2026.** Todos los datos son ficticios.

## 1. Ajustes respecto al dataset del mockup

| Id | Ajuste | Por qué |
|---|---|---|
| A1 | «Veterinario y herrero de las de doma» (8/10, US$ 2.000) se separa en **Vacunas y desparasitación** (US$ 1.200, Veterinario) y **Despalme y herraje** (US$ 800, Herrero). | Regla: un pago mixto son dos gastos. El reparto 1.200 / 800 es **ficticio**; el mockup no lo dice. |
| A2 | El pasaje Londres – Málaga pasa del 30/7 al **1/8**. | Así quedó en el borrador v9 (historial de iteraciones), para que caiga en la temporada Sotogrande. |
| A3 | Se suma el gasto del chat de Tomás: **Visita del veterinario a las de doma**, US$ 600, Campo, 22/10. | Está en el chat de demo y el borrador v9 lo sumó a la lista. |
| A4 | El herraje del 22/10 queda **pagado por Pedro** (en efectivo) y vinculado a Bruja, Gitana, Dinamita y Lucera; la ecografía del 21/10, vinculada a Patria. | Chat del piloto; decisiones P-8 y P-9. |
| A5 | Sofía es **familiar o asistente de solo WhatsApp** (carga gastos, no entra a la app). Estudio Ruiz no tiene acceso: solo recibe el export. | Decisiones del 2026-11-03 y P-2. El bloque "Accesos" del dataset del mockup quedó viejo. |
| A6 | Se fijan **cotizaciones ficticias** (sección 2), porque el mockup solo da una: blue $ 1.550 el 22/10. | Sin cotización por fecha no se pueden calcular los US$. |

## 2. Cotizaciones ficticias

Se usa el mismo valor para todos los días hábiles de cada mes. No hay feriados en el dataset. Fin de semana → último día hábil anterior (P-14), aunque caiga en el mes anterior.

| Mes 2026 | Dólar blue (promedio compra/venta), $ por US$ | Euro, US$ por € |
|---|---|---|
| Enero | 1.250 | — |
| Febrero | 1.280 | — |
| Marzo | 1.310 | — |
| Abril | 1.340 | — |
| Mayo | 1.370 | — |
| Junio | 1.400 | — |
| Julio | 1.430 | 1,07 |
| Agosto | 1.460 | 1,08 |
| Septiembre | 1.500 | 1,08 |
| Octubre | 1.550 | 1,09 |

**Reglas de cálculo:** pesos → US$ = monto ÷ blue; euros → US$ = monto × euro; **se redondea a entero en cada gasto** y los totales suman esos enteros (P-14). Ejemplo: $ 180.000 ÷ 1.550 = 116,13 → **US$ 116**.

## 3. Lugares, temporadas y caballos

| Lugar | Tipo | Caballos hoy |
|---|---|---|
| Caballeriza Pilar | caballeriza | 16 (14 en trabajo + 2 en recuperación) |
| Campo, Cnel. Suárez | campo | 15 |
| Windsor, Inglaterra | exterior (invernada) | 4 |
| Sotogrande, España | exterior (caballeriza de temporada) | 0 |
| Wellington, EE.UU. | exterior | 0 (se crea para el acuerdo Palm Ridge 2027) |

Las temporadas son también el **calendario** del polista (P-30): dicen dónde está Tomás cada día.

| Temporada | Lugares | Lugar principal | Desde | Hasta |
|---|---|---|---|---|
| Inglaterra 2026 | Windsor | Windsor | 1/4/2026 | 31/7/2026 |
| Sotogrande 2026 | Sotogrande | Sotogrande | 1/8/2026 | 31/8/2026 |
| Argentina 2026 | Pilar, Campo | Pilar | 1/9/2026 | 31/12/2026 (al 22/10) |
| Wellington 2027 | Wellington | Wellington | a definir | a definir |

Entre el 1/1 y el 31/3 no hay temporada en el calendario: un gasto que cargue Tomás en esas fechas sin nombrar un lugar va a **General**.

**Lugar fijo de los miembros** (P-30): Pedro, Ramón y Lucho → Pilar · Don Aníbal → Campo · Juanca → Windsor (en agosto viajó a Sotogrande: ver S-23) · Sofía → sin lugar fijo (usa el calendario).

**Nota:** en el dataset todos los gastos ya tienen lugar porque en los chats del mockup el lugar se dijo. La regla de P-30 se prueba en los escenarios B-113 a B-120.

Caballos: los 35 del dataset del mockup, con **situación** y **lugar** separados (P-12). Ejemplos que hay que verificar: Patria y Nube = En recuperación · Pilar (aparecen en el filtro Recuperación y no en Jugando); Guerrera = En descanso · Windsor (filtro Exterior). Filtros esperados: **Todos 35 · Jugando 14 · Campo 15 · Exterior 4 · Recuperación 2**.

## 4. Lista única de gastos (140)

⚑ = la fecha cae en fin de semana y se usó la cotización del último día hábil anterior.

| # | Fecha | Gasto | Monto original | Cotización usada | US$ | Grupo › categoría | Lugar | Cargó | Nota |
|---|---|---|---|---|---|---|---|---|---|
| G001 | 1/1 | Alquiler caballeriza Pilar | US$ 1.900 | — | 1.900 | Caballerizas y casa › Caballerizas | Pilar | Tomás | «Pagué el alquiler de la caballeriza, 1.900 dólares.» |
| G002 | 1/1 | Alquiler de la casa en Pilar | US$ 2.500 | — | 2.500 | Caballerizas y casa › Casa | Pilar | Tomás | «Pagué el alquiler de la casa, 2.500 dólares.» |
| G003 | 5/1 | Sueldos de los petiseros | US$ 3.000 | — | 3.000 | Personal › Petiseros | Pilar | Tomás | «Pagué los sueldos de Ramón, Lucho y Juanca.» |
| G004 | 5/1 | Sueldo del puestero | US$ 600 | — | 600 | Personal › Petiseros | Campo | Tomás | «Le pagué a Don Aníbal.» |
| G005 | 6/1 | 22 rollos | $ 640.000 | blue 1.250 (6/1) | 512 | Caballos › Comida | Campo | Don Aníbal |  |
| G006 | 14/1 | Veterinaria del mes | $ 900.000 | blue 1.250 (14/1) | 720 | Caballos › Veterinario | Pilar | Dra. Ibarra |  |
| G007 | 15/1 | Pago del handicap 2026 · AAP | $ 850.000 | blue 1.250 (15/1) | 680 | Torneos y handicap › Handicap | Pilar | Tomás | «Pagué el handicap de este año, 850 mil.» |
| G008 | 16/1 | Herrajes del mes | $ 1.200.000 | blue 1.250 (16/1) | 960 | Caballos › Herrero | Pilar | Pedro | «Le pagué a Cacho los herrajes del mes, un millón doscientos.» |
| G009 | 17/1 | Comida para los petiseros | $ 650.000 | blue 1.250 (16/1) ⚑ | 520 | Personal › Comida de los petiseros | Pilar | Pedro |  |
| G010 | 18/1 | 200 fardos de alfalfa | $ 2.400.000 | blue 1.250 (16/1) ⚑ | 1.920 | Caballos › Comida | Pilar | Pedro |  |
| G011 | 20/1 | 30 bolsas de avena | $ 840.000 | blue 1.250 (20/1) | 672 | Caballos › Comida | Pilar | Pedro |  |
| G012 | 25/1 | Nafta del mes | $ 300.000 | blue 1.250 (23/1) ⚑ | 240 | Traslados y viajes › Nafta y vehículos | Pilar | Tomás |  |
| G013 | 1/2 | Alquiler caballeriza Pilar | US$ 1.900 | — | 1.900 | Caballerizas y casa › Caballerizas | Pilar | Tomás | «Pagué el alquiler de la caballeriza, 1.900 dólares.» |
| G014 | 1/2 | Alquiler de la casa en Pilar | US$ 2.500 | — | 2.500 | Caballerizas y casa › Casa | Pilar | Tomás | «Pagué el alquiler de la casa, 2.500 dólares.» |
| G015 | 5/2 | Sueldos de los petiseros | US$ 3.000 | — | 3.000 | Personal › Petiseros | Pilar | Tomás | «Pagué los sueldos de Ramón, Lucho y Juanca.» |
| G016 | 5/2 | Sueldo del puestero | US$ 600 | — | 600 | Personal › Petiseros | Campo | Tomás | «Le pagué a Don Aníbal.» |
| G017 | 6/2 | 22 rollos | $ 640.000 | blue 1.280 (6/2) | 500 | Caballos › Comida | Campo | Don Aníbal |  |
| G018 | 12/2 | Compra de Chispa (potranca) | US$ 9.000 | — | 9.000 | Compra de caballos › Compras | Pilar | Tomás |  |
| G019 | 14/2 | Veterinaria del mes | $ 900.000 | blue 1.280 (13/2) ⚑ | 703 | Caballos › Veterinario | Pilar | Dra. Ibarra |  |
| G020 | 16/2 | Herrajes del mes | $ 1.200.000 | blue 1.280 (16/2) | 938 | Caballos › Herrero | Pilar | Pedro | «Le pagué a Cacho los herrajes del mes, un millón doscientos.» |
| G021 | 17/2 | Comida para los petiseros | $ 650.000 | blue 1.280 (17/2) | 508 | Personal › Comida de los petiseros | Pilar | Pedro |  |
| G022 | 18/2 | 200 fardos de alfalfa | $ 2.400.000 | blue 1.280 (18/2) | 1.875 | Caballos › Comida | Pilar | Pedro |  |
| G023 | 20/2 | 30 bolsas de avena | $ 840.000 | blue 1.280 (20/2) | 656 | Caballos › Comida | Pilar | Pedro |  |
| G024 | 20/2 | 4 tacos | US$ 900 | — | 900 | Equipo de polo › Tacos | Pilar | Tomás |  |
| G025 | 25/2 | Nafta del mes | $ 300.000 | blue 1.280 (25/2) | 234 | Traslados y viajes › Nafta y vehículos | Pilar | Tomás |  |
| G026 | 1/3 | Alquiler caballeriza Pilar | US$ 1.900 | — | 1.900 | Caballerizas y casa › Caballerizas | Pilar | Tomás | «Pagué el alquiler de la caballeriza, 1.900 dólares.» |
| G027 | 1/3 | Alquiler de la casa en Pilar | US$ 2.500 | — | 2.500 | Caballerizas y casa › Casa | Pilar | Tomás | «Pagué el alquiler de la casa, 2.500 dólares.» |
| G028 | 5/3 | Sueldos de los petiseros | US$ 3.000 | — | 3.000 | Personal › Petiseros | Pilar | Tomás | «Pagué los sueldos de Ramón, Lucho y Juanca.» |
| G029 | 5/3 | Sueldo del puestero | US$ 600 | — | 600 | Personal › Petiseros | Campo | Tomás | «Le pagué a Don Aníbal.» |
| G030 | 6/3 | 22 rollos | $ 640.000 | blue 1.310 (6/3) | 489 | Caballos › Comida | Campo | Don Aníbal |  |
| G031 | 8/3 | Casco nuevo | US$ 650 | — | 650 | Equipo de polo › Cascos e indumentaria | Pilar | Sofía |  |
| G032 | 14/3 | Veterinaria del mes | $ 900.000 | blue 1.310 (13/3) ⚑ | 687 | Caballos › Veterinario | Pilar | Dra. Ibarra |  |
| G033 | 16/3 | Herrajes del mes | $ 1.200.000 | blue 1.310 (16/3) | 916 | Caballos › Herrero | Pilar | Pedro | «Le pagué a Cacho los herrajes del mes, un millón doscientos.» |
| G034 | 17/3 | Comida para los petiseros | $ 650.000 | blue 1.310 (17/3) | 496 | Personal › Comida de los petiseros | Pilar | Pedro |  |
| G035 | 18/3 | 200 fardos de alfalfa | $ 2.400.000 | blue 1.310 (18/3) | 1.832 | Caballos › Comida | Pilar | Pedro |  |
| G036 | 20/3 | 30 bolsas de avena | $ 840.000 | blue 1.310 (20/3) | 641 | Caballos › Comida | Pilar | Pedro |  |
| G037 | 25/3 | Nafta del mes | $ 300.000 | blue 1.310 (25/3) | 229 | Traslados y viajes › Nafta y vehículos | Pilar | Tomás |  |
| G038 | 1/4 | Alquiler caballeriza Pilar | US$ 1.900 | — | 1.900 | Caballerizas y casa › Caballerizas | Pilar | Tomás | «Pagué el alquiler de la caballeriza, 1.900 dólares.» |
| G039 | 1/4 | Alquiler de la casa en Pilar | US$ 2.500 | — | 2.500 | Caballerizas y casa › Casa | Pilar | Tomás | «Pagué el alquiler de la casa, 2.500 dólares.» |
| G040 | 5/4 | Sueldos de los petiseros | US$ 3.000 | — | 3.000 | Personal › Petiseros | Pilar | Tomás | «Pagué los sueldos de Ramón, Lucho y Juanca.» |
| G041 | 5/4 | Sueldo del puestero | US$ 600 | — | 600 | Personal › Petiseros | Campo | Tomás | «Le pagué a Don Aníbal.» |
| G042 | 6/4 | 22 rollos | $ 640.000 | blue 1.340 (6/4) | 478 | Caballos › Comida | Campo | Don Aníbal |  |
| G043 | 14/4 | Veterinaria del mes | $ 900.000 | blue 1.340 (14/4) | 672 | Caballos › Veterinario | Pilar | Dra. Ibarra |  |
| G044 | 16/4 | Herrajes del mes | $ 1.200.000 | blue 1.340 (16/4) | 896 | Caballos › Herrero | Pilar | Pedro | «Le pagué a Cacho los herrajes del mes, un millón doscientos.» |
| G045 | 17/4 | Comida para los petiseros | $ 650.000 | blue 1.340 (17/4) | 485 | Personal › Comida de los petiseros | Pilar | Pedro |  |
| G046 | 18/4 | 200 fardos de alfalfa | $ 2.400.000 | blue 1.340 (17/4) ⚑ | 1.791 | Caballos › Comida | Pilar | Pedro |  |
| G047 | 20/4 | 30 bolsas de avena | $ 840.000 | blue 1.340 (20/4) | 627 | Caballos › Comida | Pilar | Pedro |  |
| G048 | 20/4 | Flete aéreo de 10 caballos a Inglaterra | US$ 38.000 | — | 38.000 | Traslados y viajes › Fletes de caballos | Windsor | Tomás | Lo cubre Northfield (a reintegrar) |
| G049 | 25/4 | Nafta del mes | $ 300.000 | blue 1.340 (24/4) ⚑ | 224 | Traslados y viajes › Nafta y vehículos | Pilar | Tomás |  |
| G050 | 28/4 | Pasaje Buenos Aires – Londres | US$ 2.400 | — | 2.400 | Traslados y viajes › Pasajes propios | Windsor | Tomás |  |
| G051 | 28/4 | Pasajes de 2 petiseros a Londres | US$ 3.200 | — | 3.200 | Traslados y viajes › Pasajes de los petiseros | Windsor | Tomás | Lo cubre Northfield (a reintegrar) |
| G052 | 1/5 | Caballeriza en Windsor | US$ 6.000 | — | 6.000 | Caballerizas y casa › Caballerizas | Windsor | Tomás |  |
| G053 | 1/5 | Casa en Windsor | US$ 5.500 | — | 5.500 | Caballerizas y casa › Casa | Windsor | Tomás |  |
| G054 | 3/5 | Handicap en Inglaterra · HPA | US$ 900 | — | 900 | Torneos y handicap › Handicap | Windsor | Tomás | «Pagué el handicap de Inglaterra, 900 dólares.» |
| G055 | 5/5 | Sueldos de los petiseros | US$ 4.200 | — | 4.200 | Personal › Petiseros | Windsor | Tomás | «Pagué los sueldos de los petiseros en Inglaterra.» |
| G056 | 5/5 | Sueldo del puestero | US$ 600 | — | 600 | Personal › Petiseros | Campo | Tomás | «Le pagué a Don Aníbal.» |
| G057 | 6/5 | 22 rollos | $ 640.000 | blue 1.370 (6/5) | 467 | Caballos › Comida | Campo | Don Aníbal |  |
| G058 | 10/5 | Pastoreo | US$ 1.500 | — | 1.500 | Caballos › Pastoreo | Windsor | Tomás |  |
| G059 | 10/5 | Inscripción torneo de mayo | US$ 2.500 | — | 2.500 | Torneos y handicap › Inscripciones | Windsor | Tomás | «Pagué la inscripción del torneo, 2.500 dólares.» |
| G060 | 12/5 | Avena y fardos | US$ 2.800 | — | 2.800 | Caballos › Comida | Windsor | Juanca |  |
| G061 | 14/5 | Veterinario | US$ 1.200 | — | 1.200 | Caballos › Veterinario | Windsor | Tomás |  |
| G062 | 16/5 | Herrero | US$ 1.600 | — | 1.600 | Caballos › Herrero | Windsor | Juanca | «Vino el herrero, herró a las diez, mil seiscientos dólares.» |
| G063 | 17/5 | Comida para los petiseros | US$ 900 | — | 900 | Personal › Comida de los petiseros | Windsor | Juanca |  |
| G064 | 1/6 | Caballeriza en Windsor | US$ 6.000 | — | 6.000 | Caballerizas y casa › Caballerizas | Windsor | Tomás |  |
| G065 | 1/6 | Casa en Windsor | US$ 5.500 | — | 5.500 | Caballerizas y casa › Casa | Windsor | Tomás |  |
| G066 | 3/6 | 6 tacos | US$ 1.300 | — | 1.300 | Equipo de polo › Tacos | Windsor | Tomás |  |
| G067 | 5/6 | Sueldos de los petiseros | US$ 4.200 | — | 4.200 | Personal › Petiseros | Windsor | Tomás | «Pagué los sueldos de los petiseros en Inglaterra.» |
| G068 | 5/6 | Sueldo del puestero | US$ 600 | — | 600 | Personal › Petiseros | Campo | Tomás | «Le pagué a Don Aníbal.» |
| G069 | 6/6 | 22 rollos | $ 640.000 | blue 1.400 (5/6) ⚑ | 457 | Caballos › Comida | Campo | Don Aníbal |  |
| G070 | 8/6 | Inscripción torneo de junio | US$ 2.500 | — | 2.500 | Torneos y handicap › Inscripciones | Windsor | Tomás | «Inscripción del torneo de junio, 2.500.» |
| G071 | 10/6 | Pastoreo | US$ 1.500 | — | 1.500 | Caballos › Pastoreo | Windsor | Tomás |  |
| G072 | 12/6 | Avena y fardos | US$ 2.800 | — | 2.800 | Caballos › Comida | Windsor | Juanca |  |
| G073 | 14/6 | Veterinario | US$ 1.200 | — | 1.200 | Caballos › Veterinario | Windsor | Tomás |  |
| G074 | 16/6 | Herrero | US$ 1.600 | — | 1.600 | Caballos › Herrero | Windsor | Juanca | «Vino el herrero, herró a las diez, mil seiscientos dólares.» |
| G075 | 17/6 | Comida para los petiseros | US$ 900 | — | 900 | Personal › Comida de los petiseros | Windsor | Juanca |  |
| G076 | 1/7 | Caballeriza en Windsor | US$ 6.000 | — | 6.000 | Caballerizas y casa › Caballerizas | Windsor | Tomás |  |
| G077 | 1/7 | Casa en Windsor | US$ 5.500 | — | 5.500 | Caballerizas y casa › Casa | Windsor | Tomás |  |
| G078 | 5/7 | Sueldos de los petiseros | US$ 4.200 | — | 4.200 | Personal › Petiseros | Windsor | Tomás | «Pagué los sueldos de los petiseros en Inglaterra.» |
| G079 | 5/7 | Sueldo del puestero | US$ 600 | — | 600 | Personal › Petiseros | Campo | Tomás | «Le pagué a Don Aníbal.» |
| G080 | 6/7 | 22 rollos | $ 640.000 | blue 1.430 (6/7) | 448 | Caballos › Comida | Campo | Don Aníbal |  |
| G081 | 10/7 | Pastoreo | US$ 1.500 | — | 1.500 | Caballos › Pastoreo | Windsor | Tomás |  |
| G082 | 12/7 | Avena y fardos | US$ 2.800 | — | 2.800 | Caballos › Comida | Windsor | Juanca |  |
| G083 | 14/7 | Veterinario | US$ 1.200 | — | 1.200 | Caballos › Veterinario | Windsor | Tomás |  |
| G084 | 15/7 | Cena con el equipo | US$ 400 | — | 400 | Varios › Regalos y extras | Windsor | Tomás | «Invité la cena al equipo, 400 dólares.» |
| G085 | 16/7 | Herrero | US$ 1.600 | — | 1.600 | Caballos › Herrero | Windsor | Juanca | «Vino el herrero, herró a las diez, mil seiscientos dólares.» |
| G086 | 17/7 | Comida para los petiseros | US$ 900 | — | 900 | Personal › Comida de los petiseros | Windsor | Juanca |  |
| G087 | 1/8 | Pasajes Londres – Málaga | € 600 | € a US$ 1,07 (31/7) ⚑ | 642 | Traslados y viajes › Pasajes propios | Sotogrande | Tomás | (A2) fecha corregida al 1/8 (borrador v9) |
| G088 | 1/8 | Caballeriza en Sotogrande | € 5.000 | € a US$ 1,07 (31/7) ⚑ | 5.350 | Caballerizas y casa › Caballerizas | Sotogrande | Tomás |  |
| G089 | 1/8 | Casa en Sotogrande | € 4.500 | € a US$ 1,07 (31/7) ⚑ | 4.815 | Caballerizas y casa › Casa | Sotogrande | Tomás |  |
| G090 | 2/8 | Flete de caballos Windsor – Sotogrande | € 9.000 | € a US$ 1,07 (31/7) ⚑ | 9.630 | Traslados y viajes › Fletes de caballos | Sotogrande | Tomás | Lo cubre Valle Alto (reintegrado) |
| G091 | 5/8 | Sueldos de los petiseros | € 3.800 | € a US$ 1,08 (5/8) | 4.104 | Personal › Petiseros | Sotogrande | Tomás | «Pagué los sueldos de los petiseros en España.» |
| G092 | 5/8 | Sueldo del puestero | US$ 600 | — | 600 | Personal › Petiseros | Campo | Tomás | «Le pagué a Don Aníbal.» |
| G093 | 6/8 | 22 rollos | $ 640.000 | blue 1.460 (6/8) | 438 | Caballos › Comida | Campo | Don Aníbal |  |
| G094 | 8/8 | Inscripción torneo en Sotogrande | € 3.000 | € a US$ 1,08 (7/8) ⚑ | 3.240 | Torneos y handicap › Inscripciones | Sotogrande | Tomás | «Pagué la inscripción en Sotogrande, 3 mil euros.» |
| G095 | 10/8 | Pastoreo | € 1.800 | € a US$ 1,08 (10/8) | 1.944 | Caballos › Pastoreo | Sotogrande | Tomás |  |
| G096 | 14/8 | Veterinario | € 900 | € a US$ 1,08 (14/8) | 972 | Caballos › Veterinario | Sotogrande | Tomás |  |
| G097 | 16/8 | Herrero | € 1.100 | € a US$ 1,08 (14/8) ⚑ | 1.188 | Caballos › Herrero | Sotogrande | Tomás |  |
| G098 | 17/8 | Comida para los petiseros | € 800 | € a US$ 1,08 (17/8) | 864 | Personal › Comida de los petiseros | Sotogrande | Juanca |  |
| G099 | 30/8 | Pasaje de vuelta a Buenos Aires | US$ 1.400 | — | 1.400 | Traslados y viajes › Pasajes propios | Pilar | Tomás |  |
| G100 | 30/8 | Pasajes de vuelta de los petiseros | US$ 2.800 | — | 2.800 | Traslados y viajes › Pasajes de los petiseros | Pilar | Tomás |  |
| G101 | 1/9 | Alquiler caballeriza Pilar | US$ 1.900 | — | 1.900 | Caballerizas y casa › Caballerizas | Pilar | Tomás | «Pagué el alquiler de la caballeriza, 1.900 dólares.» |
| G102 | 1/9 | Alquiler de la casa en Pilar | US$ 2.500 | — | 2.500 | Caballerizas y casa › Casa | Pilar | Tomás | «Pagué el alquiler de la casa, 2.500 dólares.» |
| G103 | 1/9 | Invernada en Windsor · 4 caballos | US$ 4.250 | — | 4.250 | Caballerizas y casa › Caballerizas | Windsor | Tomás |  |
| G104 | 5/9 | Sueldos de los petiseros | US$ 3.000 | — | 3.000 | Personal › Petiseros | Pilar | Tomás | «Pagué los sueldos de Ramón, Lucho y Juanca.» |
| G105 | 5/9 | Sueldo del puestero | US$ 600 | — | 600 | Personal › Petiseros | Campo | Tomás | «Le pagué a Don Aníbal.» |
| G106 | 6/9 | 22 rollos | $ 640.000 | blue 1.500 (4/9) ⚑ | 427 | Caballos › Comida | Campo | Don Aníbal |  |
| G107 | 10/9 | Bozales y riendas | US$ 380 | — | 380 | Equipo de polo › Bozales y riendas | Pilar | Tomás |  |
| G108 | 14/9 | Veterinaria del mes | $ 900.000 | blue 1.500 (14/9) | 600 | Caballos › Veterinario | Pilar | Dra. Ibarra |  |
| G109 | 16/9 | Herrajes del mes | $ 1.200.000 | blue 1.500 (16/9) | 800 | Caballos › Herrero | Pilar | Pedro | «Le pagué a Cacho los herrajes del mes, un millón doscientos.» |
| G110 | 17/9 | Comida para los petiseros | $ 650.000 | blue 1.500 (17/9) | 433 | Personal › Comida de los petiseros | Pilar | Pedro |  |
| G111 | 18/9 | 200 fardos de alfalfa | $ 2.400.000 | blue 1.500 (18/9) | 1.600 | Caballos › Comida | Pilar | Pedro |  |
| G112 | 20/9 | 30 bolsas de avena | $ 840.000 | blue 1.500 (18/9) ⚑ | 560 | Caballos › Comida | Pilar | Pedro |  |
| G113 | 25/9 | Nafta del mes | $ 300.000 | blue 1.500 (25/9) | 200 | Traslados y viajes › Nafta y vehículos | Pilar | Tomás |  |
| G114 | 25/9 | Inscripción torneo de septiembre | US$ 3.000 | — | 3.000 | Torneos y handicap › Inscripciones | Pilar | Tomás | «Pagué la inscripción del torneo, 3 mil dólares.» |
| G115 | 1/10 | Alquiler caballeriza Pilar | US$ 1.900 | — | 1.900 | Caballerizas y casa › Caballerizas | Pilar | Tomás | «Pagué el alquiler de la caballeriza, 1.900 dólares.» |
| G116 | 1/10 | Alquiler de la casa en Pilar | US$ 2.500 | — | 2.500 | Caballerizas y casa › Casa | Pilar | Tomás | «Pagué el alquiler de la casa, 2.500 dólares.» |
| G117 | 5/10 | Sueldos de los petiseros | US$ 3.000 | — | 3.000 | Personal › Petiseros | Pilar | Tomás | «Pagué los sueldos de Ramón, Lucho y Juanca.» |
| G118 | 5/10 | Sueldo del puestero | US$ 600 | — | 600 | Personal › Petiseros | Campo | Tomás | «Le pagué a Don Aníbal.» |
| G119 | 5/10 | 22 rollos | $ 640.000 | blue 1.550 (5/10) | 413 | Caballos › Comida | Campo | Don Aníbal |  |
| G120 | 8/10 | Vacunas y desparasitación de las de doma | US$ 1.200 | — | 1.200 | Caballos › Veterinario | Campo | Tomás | (A1) separado del gasto mixto |
| G121 | 8/10 | Despalme y herraje de las de doma | US$ 800 | — | 800 | Caballos › Herrero | Campo | Tomás | (A1) separado del gasto mixto |
| G122 | 9/10 | Gomas nuevas del trailer | $ 600.000 | blue 1.550 (9/10) | 387 | Traslados y viajes › Nafta y vehículos | Pilar | Tomás | «Cambiamos las cuatro gomas del trailer, 600 mil.» |
| G123 | 10/10 | Adelanto de sueldo a Lucho | US$ 200 | — | 200 | Personal › Petiseros | Pilar | Tomás | «Le adelanté 200 dólares a Lucho.» |
| G124 | 11/10 | Tacos para la temporada inglesa | US$ 600 | — | 600 | Equipo de polo › Tacos | Windsor | Tomás | «Encargué 4 tacos para Inglaterra, 600 dólares.» |
| G125 | 12/10 | Saldo del flete de la temporada | US$ 2.450 | — | 2.450 | Traslados y viajes › Fletes de caballos | Windsor | Tomás | «Pagué el saldo del flete de Inglaterra, 2.450 dólares.» |
| G126 | 13/10 | Regalo de cumpleaños para Ramón | $ 120.000 | blue 1.550 (13/10) | 77 | Varios › Regalos y extras | Pilar | Tomás | «Le compré un regalo a Ramón por el cumple, 120 mil.» |
| G127 | 14/10 | Botas y rodilleras | US$ 450 | — | 450 | Equipo de polo › Cascos e indumentaria | Pilar | Sofía |  |
| G128 | 15/10 | Invernada en Windsor · 4 caballos | US$ 4.250 | — | 4.250 | Caballerizas y casa › Caballerizas | Windsor | Tomás |  |
| G129 | 16/10 | Seña caballeriza Sotogrande 2027 | € 4.000 | € a US$ 1,09 (16/10) | 4.360 | Caballerizas y casa › Caballerizas | Sotogrande | Tomás | «Dejé 4 mil euros de seña para la caballeriza de Sotogrande del año que viene.» |
| G130 | 17/10 | Comida para los petiseros | $ 160.000 | blue 1.550 (16/10) ⚑ | 103 | Personal › Comida de los petiseros | Pilar | Pedro |  |
| G131 | 18/10 | 200 fardos de alfalfa | $ 2.400.000 | blue 1.550 (16/10) ⚑ | 1.548 | Caballos › Comida | Pilar | Pedro |  |
| G132 | 19/10 | Montura nueva | US$ 2.200 | — | 2.200 | Equipo de polo › Monturas | Pilar | Tomás | «Compré una montura nueva, 2.200 dólares.» |
| G133 | 19/10 | Flete Pilar → campo · 4 caballos | $ 280.000 | blue 1.550 (19/10) | 181 | Traslados y viajes › Fletes de caballos | Pilar | Pedro | «Llevamos 4 caballos al campo en el trailer de Gómez, son 280 mil.» |
| G134 | 20/10 | 30 bolsas de avena | $ 840.000 | blue 1.550 (20/10) | 542 | Caballos › Comida | Pilar | Pedro |  |
| G135 | 21/10 | Revisión y ecografía de Patria | $ 320.000 | blue 1.550 (21/10) | 206 | Caballos › Veterinario | Pilar | Dra. Ibarra |  |
| G136 | 21/10 | 3 tacos nuevos | US$ 540 | — | 540 | Equipo de polo › Tacos | Pilar | Tomás |  |
| G137 | 21/10 | Compra de Fortuna | US$ 18.000 | — | 18.000 | Compra de caballos › Compras | Pilar | Tomás |  |
| G138 | 22/10 | Herraje de 4 caballos | $ 180.000 | blue 1.550 (22/10) | 116 | Caballos › Herrero | Pilar | Pedro | «Vino Cacho, herró a la Bruja, la Gitana, la Dinamita y la Lucera. Son 180 lucas.» |
| G139 | 22/10 | Nafta de la camioneta | $ 85.000 | blue 1.550 (22/10) | 55 | Traslados y viajes › Nafta y vehículos | Pilar | Sofía |  |
| G140 | 22/10 | Visita del veterinario a las de doma | US$ 600 | — | 600 | Caballos › Veterinario | Campo | Tomás | (A3) «Le pagué 600 dólares al veterinario.» → «Las de doma del campo» |

## 5. Totales esperados de Gastos

| Vista | Gastos | Total US$ |
|---|---|---|
| Todo 2026 (1/1 al 22/10) | 140 | **295.638** |
| Todo 2026 sin compra de caballos | 138 | 268.638 |
| Este mes (octubre, al 22) | 26 | **47.278** |
| Últimos 30 días (23/9 al 22/10) | 28 | 50.478 |

**Por lugar**

| Lugar | Octubre: gastos | Octubre: US$ | Todo 2026: gastos | Todo 2026: US$ |
|---|---|---|---|---|
| Caballeriza Pilar | 17 | 32.005 | 70 | 111.450 |
| Campo, Cnel. Suárez | 5 | 3.613 | 23 | 13.229 |
| Windsor, Inglaterra | 3 | 7.300 | 36 | 133.850 |
| Sotogrande, España | 1 | 4.360 | 11 | 37.109 |
| General (sin lugar) | 0 | 0 | 0 | 0 |
| **Total** | **26** | **47.278** | **140** | **295.638** |

En el dataset todos los gastos tienen lugar, porque en los chats del mockup el lugar se dijo o se respondió. Con P-29, un gasto sin lugar explícito va a **General**: el renglón existe aunque esté en cero, y los escenarios B-104 a B-108 lo prueban.

**En qué se fue · octubre**

| Grupo | Gastos | US$ |
|---|---|---|
| Caballos | 8 | 5.425 |
| Personal | 4 | 3.903 |
| Caballerizas y casa | 4 | 13.010 |
| Equipo de polo | 4 | 3.790 |
| Traslados y viajes | 4 | 3.073 |
| Varios | 1 | 77 |
| Compra de caballos | 1 | 18.000 |
| **Total** | **26** | **47.278** |

Torneos y handicap no tiene gastos en octubre: **no se muestra** el renglón (o se muestra en cero; decidir en el diseño, no cambia el total).

**Caballos › por categoría · octubre:** Comida 3 gastos · US$ 2.503 · Veterinario 3 · US$ 2.006 · Herrero 2 · US$ 916.

**Controles que tiene que pasar el producto:** la suma de los grupos da el total del mes; la suma de los lugares da el total; cada total coincide con la suma de los US$ de la tabla 4 filtrada. Si alguno no da, hay un error de redondeo o un gasto contado dos veces.

## 6. Ingresos esperados

| Acuerdo o venta | Contraparte | Temporada | Acordado | Pagos (fecha · monto · US$) | Reintegros | Estado | Por cobrar |
|---|---|---|---|---|---|---|---|
| Northfield | Erik Halvorsen | Inglaterra 2026 | US$ 250.000 | 15/5 · 100.000 · 20/6 · 40.000 | Flete aéreo US$ 38.000 y pasajes de 2 petiseros US$ 3.200, **a reintegrar** | Cobrando | **US$ 151.200** |
| Palm Ridge | Daniel Whitmore | Wellington 2027 | US$ 180.000 | 10/10 · seña 30.000 | — | Cobrando | **US$ 150.000** |
| La Ensenada | Pablo Ferrer | Argentina 2026 | US$ 60.000 | 1/10 · 30.000 | — | Cobrando | **US$ 30.000** |
| Les Pins | Antoine Moreau | Chantilly 2026 (ver O-1) | € 45.000 | — | — | Sin pagos | **≈ US$ 49.050** (€ 45.000 × 1,09 de hoy) |
| Valle Alto | Javier Ordóñez | Sotogrande 2026 | € 80.000 | 10/8 · € 50.000 · US$ 54.000; 31/8 · € 30.000 · US$ 32.400 | Flete Windsor – Sotogrande € 9.000 · **reintegrado** el 31/8 (supuesto): «me devolvió los 9 mil euros del flete» · € 9.000 × 1,08 = US$ 9.720 (P-28) | Cobrado | US$ 0 |
| Venta de Halcona | Erik Halvorsen | Inglaterra 2026 | US$ 85.000 | 25/7 · 50.000 | — | Cobrando | **US$ 35.000** |
| Venta de Trueno | Un polista de Wellington | Argentina 2026 | US$ 40.000 | 15/9 (supuesto) · 40.000 | — | Cobrado | US$ 0 |

| Total | Valor esperado |
|---|---|
| **Por cobrar** | **US$ 366.200 + ≈ US$ 49.050 = ≈ US$ 415.250**. Coincide con el mockup (US$ 366.200 · € 45.000) una vez pasados los euros a dólares. |
| **Ya cobrado** | US$ 290.000 + US$ 86.400 (€ 80.000 a la cotización de cada pago) + US$ 9.720 (reintegro, a la cotización del día en que se cobró, P-28) = **US$ 386.120** |
| **Le debés a Pedro** | US$ 116 (herraje del 22/10, P-8) |

**Imputación que se tiene que verificar:** «Me pagó 40 mil Halvorsen» tiene **dos** destinos posibles (Northfield y la venta de Halcona) → el bot **pregunta** (P-6). Con «me pagó 40 mil Halvorsen por Northfield», va directo.

## 7. Resultado por temporada esperado (P-5, P-25)

Ingresos = acuerdos de la temporada + reintegros (valuados a su día, P-28). Gastos = gastos de los lugares de la temporada **dentro de sus fechas**, más los que un owner **asoció a mano** a la temporada (ninguno en el dataset), sin compra de caballos. Los gastos generales no asociados no entran (P-29). Las ventas van aparte.

| Temporada | Ingresos acordados | Ya cobrado | Gastos del destino | Resultado (acordado) | Resultado (con lo cobrado) |
|---|---|---|---|---|---|
| Inglaterra 2026 (Windsor, 1/4–31/7) | 291.200 | 140.000 | −122.300 (32 gastos) | **+168.900** | +17.700 |
| Sotogrande 2026 (1/8–31/8) | 96.120 | 96.120 | −32.749 (10 gastos) | **+63.371** | +63.371 |
| Argentina 2026 (Pilar y Campo, 1/9 al 22/10) | 60.000 | 30.000 | −33.618 (34 gastos) | **+26.382** | -3.618 |

**Caballos (aparte):** vendiste US$ 125.000 (Halcona 85.000 en Inglaterra 2026, Trueno 40.000 en Argentina 2026) · compraste US$ 27.000 (Chispa 9.000, Fortuna 18.000).

**Gastos de destino fuera de temporada (P-25):** 62 gastos · US$ 79.971. Se ven en Gastos con su lugar y **no** entran en ningún resultado:
- Pilar: 41 gastos · US$ 55.472 (enero a abril, y los pasajes de vuelta del 30/8).
- Campo: 16 gastos · US$ 8.589 (puestero y rollos mientras el polista estaba afuera).
- Windsor: 4 gastos · US$ 11.550 (invernada de septiembre y octubre, tacos y saldo del flete de octubre).
- Sotogrande: 1 gasto · US$ 4.360 (seña de la caballeriza 2027).

**Control:** Inglaterra 2026 da gastos de US$ 122.300, igual que el mockup. Los ingresos cambian respecto del mockup (376.200) porque, por P-5, la venta de Halcona sale del resultado.

## 8. Caballeriza esperada

Días que alcanza = stock ÷ (consumo por caballo por día × caballos ÷ envase), **truncado a días enteros**. Etiquetas: ≥ 30 días → "1 mes"; ≥ 60 → "Más de 2 meses"; < 8 → alerta de stock bajo.

| Sede | Insumo | Stock | Por día | Alcanza | Alerta |
|---|---|---|---|---|---|
| Pilar (16) | Avena | 18 bolsas de 40 kg | 7,5 × 16 ÷ 40 = 3 | **6 días** | Sí |
| Pilar | Fardos de alfalfa | 140 | 1 × 16 = 16 | 8 días | No |
| Pilar | Viruta | 35 bolsas | 0,2 × 16 = 3,2 | 10 días | No |
| Pilar | Balanceado | 22 bolsas de 25 kg | 2 × 16 ÷ 25 = 1,28 | 17 días | No |
| Pilar | Electrolitos | 4 potes de 3 kg | 0,03 × 16 ÷ 3 = 0,16 | 25 días | No |
| Campo (15) | Rollos | 22 de 400 kg | 12 × 15 ÷ 400 = 0,45 | 48 días → "1 mes" | No |
| Campo | Sal mineral | 6 bolsas de 25 kg | 0,04 × 15 ÷ 25 = 0,024 | 250 días → "Más de 2 meses" | No |
| Campo | Balanceado doma | 8 bolsas de 25 kg | 3 × **5** ÷ 25 = 0,6 | 13 días | No |

**Verificar:** si Tormenta pasa de Pilar al campo (*CaballoTrasladado*), Pilar queda con 15 caballos y la avena pasa a 18 ÷ (7,5 × 15 ÷ 40 = 2,81) = **6 días** (6,4 truncado); los rollos del campo, a 22 ÷ 0,48 = 45 días. El balanceado de doma no cambia (solo lo comen las 5 de doma).

## 9. Inicio esperado

- **Gastado · Este mes:** US$ 47.278 (26 gastos).
- **Por cobrar:** ≈ US$ 415.250.
- **Necesita tu atención:** Rockstar renguea (Ramón, 9:40, con foto) · Avena para 6 días en Pilar · Herraje vencido en 3 caballos (Malcriada, Chiquita, Rubia).
- **Pagos que vienen** (próximos 15 días, supuesto): 1/11 Alquiler caballeriza Pilar US$ 1.900 · 1/11 Alquiler de la casa US$ 2.500 · 5/11 Sueldos de los petiseros US$ 3.000 · 5/11 Sueldo del puestero US$ 600 = **US$ 8.000** (igual que el mockup). La invernada del 15/11 queda afuera de la ventana.

## 10. Observaciones sobre los datos (para Santi)

| Id | Observación | Propuesta |
|---|---|---|
| O-1 | El acuerdo **Les Pins** es de "Francia · Chantilly 2026", pero la organización no tiene un lugar en Chantilly ni una temporada con fechas, y en julio–agosto el polista estaba en Windsor y Sotogrande. Con el calendario (S-22), una temporada en Chantilly no se puede superponer con esas. | Crear el lugar Chantilly con fechas propias (por ejemplo, cortando un tramo de Inglaterra 2026), o cambiar el ejemplo a otra temporada. |
| O-2 | Los **pasajes de vuelta** (30/8) tienen lugar Pilar y caen fuera de toda temporada, así que no restan ni en Sotogrande ni en Argentina. | Con P-29, un owner los puede **asociar a mano** a Sotogrande 2026 desde la app (escenario B-108). En el dataset quedan sin asociar. |
| O-3 | En la consulta del chat, el mockup dice «veterinario este mes = US$ 2.206»; con la separación A1, el total da US$ 2.006 en Veterinario y US$ 916 en Herrero. | Actualizar el chat del mockup. |
| O-5 | El flete Windsor – Sotogrande (€ 9.000) se pagó el 2/8 (cotización del 31/7: US$ 9.630) y se reintegró el 31/8 (cotización 1,08: US$ 9.720). **Decidido (P-28):** puede haber diferencias; se anota lo que se dice, valuado a su día. Sotogrande 2026 gana US$ 90 por diferencia de cambio, y eso es correcto. | — |
| O-4 | El total de Gastos **incluye** la Compra de caballos (como grupo aparte) y el resultado por temporada **no**. Es lo que dice la KB, pero conviene que el diseño lo deje claro. | Mostrar «de los cuales US$ 18.000 son compra de caballos». |
