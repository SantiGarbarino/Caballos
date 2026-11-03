# Modelo de datos (v0.2)

> Derivado del mockup final. Reemplaza la v0 (que tenía `patron_id` como centro de costo y conversión de monedas como vista). Nombres orientativos para Mauro.

```
Cuenta (organización del polista)
 ├──< Acceso (persona, rol, permisos)
 ├──< Persona del equipo (piloto, petisero, puestero) ── teléfono WhatsApp
 ├──< Lugar (caballeriza, campo, exterior, temporada)
 │      └──< Insumo (stock, envase) ──< Consumo (por caballo por día)
 ├──< Caballo ──< Evento (vareo, herraje, vete, práctica, partido, novedad, traslado)
 │      └──< Recordatorio
 ├──< Visita (herrero, veterinaria, proveedor) >── Caballo(s)
 ├──< Gasto ── Lugar ── Comprobante ── MensajeOrigen
 │      └── cubre → Acuerdo (reintegro: pendiente | cobrado)
 ├──< PagoFijo
 ├──< Acuerdo (patrón) ──< Pago
 ├──< Venta (caballo) ──< Pago
 ├──< Tarea (para el piloto) ── origen MensajeOrigen
 └──< MensajeOrigen (texto, audio + transcripción, foto + lectura)
```

## Entidades

**Cuenta**: id, nombre del dueño, idioma, plan.

**Acceso**: cuenta_id, persona, rol (`dueño` | `cuentas` | `contador` | `piloto`), permisos (`todo` | `gastos_ingresos_ve_y_carga` | `solo_gastos_export` | `solo_whatsapp_sin_plata`). Los patrones **nunca** tienen acceso.

**Persona del equipo**: id, nombre, rol (`piloto` | `petisero` | `puestero`), lugar, teléfono. Métricas derivadas: mensajes hoy y en la semana, vareos, tareas hechas, último mensaje.

**Lugar**: id, nombre corto y largo (Pilar / Caballeriza Pilar), país, tipo (`caballeriza` | `campo` | `exterior` | `temporada`), descripción ("4 caballos en invernada").

**Insumo**: lugar_id, nombre, stock, unidad (bolsas, fardos, rollos, potes), tamaño del envase + unidad de consumo (40 kg, 3000 g), caballos que lo consumen (puede ser un subconjunto: "solo las 5 de doma"), último ingreso.

**Consumo**: insumo_id, cantidad por caballo por día. Derivados: por día = consumo × caballos ÷ envase; días = stock ÷ por día. Sugerencia de ajuste según los conteos reales.

**Caballo**: id, nombre, sexo, edad, pelaje, estado (`jugando` | `campo` | `exterior` | `recuperacion`), lugar, línea de estado, novedad (texto, quién, cuándo, foto), microchip (opcional, leído de los papeles).

**Evento de caballo**: caballo_id, tipo (vareada, montada, práctica + chukkers, partido, herrada, veterinaria, al box, entró en reposo…), fecha, quién lo reportó, medio (audio, foto, mensaje), mensaje_origen_id, gasto_id opcional.

**Recordatorio**: caballo_id, qué, cuándo, quién (yo / piloto / veterinaria / herrero), origen (`whatsapp` | `app` | `visita` | `automático`), hecho.

**Visita**: quién viene (herrero, veterinaria, proveedor, otro), nombre (Cacho, Dra. Ibarra), día y hora, para qué, caballos.

**Gasto**
| Campo | Notas |
|---|---|
| id, cuenta_id | |
| fecha | día/mes/año |
| título | "Herraje de 4 caballos" |
| monto + moneda | `usd` \| `ars` \| `eur` (\| `gbp`). **Nunca se convierte** |
| grupo, categoría | Ver [taxonomía](modulo-gastos-ingresos.md) |
| lugar_id | **destino** del gasto |
| comprobante | `foto` (factura/remito/ticket) \| `audio` (+ transcripción) \| `texto` |
| cargado_por | persona + "por WhatsApp" |
| pagado_por | (ej. el piloto lo pagó de su bolsillo) |
| cubre_acuerdo_id | opcional, patrón que lo cubre |
| reintegro | `pendiente` \| `cobrado` |
| mensaje_origen_id | trazabilidad |

**PagoFijo**: título, monto, moneda, día del mes, lugar, grupo/categoría. Genera la pregunta mensual por WhatsApp y, con un «sí», un Gasto.

**Acuerdo**: equipo, patrón, dónde y temporada, moneda, monto acordado. **Pago**: acuerdo/venta, fecha, monto, origen ("Transferencia · foto del comprobante").

**Venta**: caballo, comprador, dónde y cuándo, precio, moneda, pagos.

**Tarea (piloto)**: qué, cuándo, caballos, origen (audio/WhatsApp de Tomás y hora), estado. Se envía a las 7:00 y se tacha por WhatsApp.

**MensajeOrigen**: persona, tipo, contenido o URL, duración (audio), transcripción, lectura de imagen, recibido_en, qué generó.

## Derivados (no se guardan)

- **Total de gastos** por período, lugar, grupo y categoría = suma de gastos, **por moneda**.
- **Por cobrar** por acuerdo = acordado − Σ pagos + Σ gastos que cubre con reintegro pendiente.
- **Resultado por temporada** (por moneda) = acuerdos y ventas de esa temporada + reintegros − gastos de ese lugar y fechas, **sin compras de caballos**.
- **Pagos que vienen** = pagos fijos con vencimiento próximo.

## Reglas
- El **mensaje original siempre se guarda**.
- **Moneda original inmutable**; sin conversiones.
- Las **correcciones** se loguean (antes/después) para evaluar la IA.
