# Modelo de datos (v0.3)

> Derivado del mockup. v0.3 (2026-11-03): monto en US$ con conversión guardada, usuarios polista + manager, grupos de WhatsApp, proveedores con varios clientes, recordatorios personales y caballos desde la app Polo Argentino. Nombres orientativos para Mauro.

```
Cuenta (organización del polista)
 ├──< Usuario (owners: polista y/o manager; otros con acceso parcial)
 ├──< Miembro solo WhatsApp (piloto, petisero, puestero, familiar o asistente) ── teléfono · una sola cuenta
 ├──< GrupoWhatsApp (varios por cuenta; cada grupo → una sola cuenta)
 ├──<>── Proveedor (vete, herrero) ── teléfono · puede estar en varias cuentas
 ├──< Lugar (caballeriza, campo, exterior, temporada)
 │      └──< Insumo (stock, envase) ──< Consumo (por caballo por día)
 ├──< Caballo (ref. app Polo Argentino, opcional) ──< Evento (vareo, herraje, vete, práctica, partido, novedad, traslado)
 │      └──< Recordatorio
 ├──< Visita (herrero, veterinaria, proveedor) >── Caballo(s)
 ├──< Gasto ── Lugar ── Comprobante ── MensajeOrigen
 │      └── cubre → Acuerdo (reintegro: pendiente | cobrado)
 ├──< PagoFijo
 ├──< Acuerdo (patrón) ──< Pago
 ├──< Venta (caballo) ──< Pago
 ├──< Tarea (para el piloto) ── origen MensajeOrigen
 ├──< RecordatorioPersonal (polista / manager)
 └──< MensajeOrigen (texto, audio + transcripción, foto + lectura)
```

## Entidades

**Cuenta**: id, nombre del dueño, idioma, plan.

**Usuario (app)**: cuenta_id, nombre, teléfono, rol (`polista` | `manager` | otro con acceso habilitado). Los **owners** (quien creó la organización y a quien le dé todos los accesos) ven todo y configuran los accesos de los demás desde Equipo. *(Actualizado 2026-11-03: los permisos son por usuario.)*

**Miembro (solo WhatsApp)**: id, **cuenta_id (una sola)**, nombre, rol (`piloto` | `petisero` | `puestero` | `familiar/asistente` | otro), lugar, teléfono. Carga por el bot; **nunca entra a la app**. Todo lo que carga queda con `cargado_por`. Abierto: qué puede cargar cada rol.

**Proveedor**: id, nombre, rol (`veterinario` | `herrero` | otro), teléfono; relación muchos-a-muchos con Cuenta. Si escribe por privado y tiene más de un cliente, el bot pregunta para cuál.

**Membresía**: teléfono, cuenta_id, rol, **owner (sí/no)**, canales (`grupo` | `privado` | ambos), **accesos a la app**: `tipo` (`nada` = solo WhatsApp | `todo` = owner | `parte`), y si es `parte`: `secciones` (novedades, caballos, agenda, caballeriza; Gastos e Ingresos solo owners) y `alcance` de caballos (`todos` | `lugar` + lista de lugares | `caballos` + lista de caballos), invitada_por, activa/inactiva. Define a qué organización va cada mensaje. Un proveedor tiene varias; el resto, una.

**Contexto de conversación** (privado de alguien con varias organizaciones): última organización elegida y hasta cuándo vale, para no repreguntar en cada mensaje.

**TrabajoProveedor**: lo que carga un veterinario o herrero (qué hizo, caballos, fecha). No es un gasto: si corresponde, genera una **pregunta** al polista o al manager para registrarlo como gasto.

**GrupoWhatsApp**: id del grupo, cuenta_id, participantes. **Una cuenta puede tener varios grupos** (ej. manager + veterinario + bot, manager + herrero + bot). Todo mensaje que llega desde un grupo pertenece a la cuenta de ese grupo. Lo que se habla de plata en el grupo se registra igual. Métricas derivadas: mensajes hoy y en la semana, vareos, tareas hechas, último mensaje.

**Lugar**: id, nombre corto y largo (Pilar / Caballeriza Pilar), país, tipo (`caballeriza` | `campo` | `exterior` | `temporada`), descripción ("4 caballos en invernada").

**Insumo**: lugar_id, nombre, stock, unidad (bolsas, fardos, rollos, potes), tamaño del envase + unidad de consumo (40 kg, 3000 g), caballos que lo consumen (puede ser un subconjunto: "solo las 5 de doma"), último ingreso.

**Consumo**: insumo_id, cantidad por caballo por día. Derivados: por día = consumo × caballos ÷ envase; días = stock ÷ por día. Sugerencia de ajuste según los conteos reales.

**Caballo**: id, polo_argentino_id (opcional, ref. a la app Polo Argentino: sangre, padre, madre, partidos vienen de ahí), nombre, sexo, edad, pelaje, estado (`jugando` | `campo` | `exterior` | `recuperacion`), lugar, línea de estado, novedad (texto, quién, cuándo, foto), microchip (opcional, leído de los papeles).

**Evento de caballo**: caballo_id, tipo (vareada, montada, práctica + chukkers, partido, herrada, veterinaria, al box, entró en reposo…), fecha, quién lo reportó, medio (audio, foto, mensaje), mensaje_origen_id, gasto_id opcional.

**Recordatorio**: caballo_id, qué, cuándo, quién (yo / piloto / veterinaria / herrero), origen (`whatsapp` | `app` | `visita` | `automático`), hecho.

**Visita**: quién viene (herrero, veterinaria, proveedor, otro), nombre (Cacho, Dra. Ibarra), día y hora, para qué, caballos.

**Gasto**
| Campo | Notas |
|---|---|
| id, cuenta_id | |
| fecha | día/mes/año |
| título | "Herraje de 4 caballos" |
| monto_usd | Lo que se muestra y se suma |
| monto_original + moneda_original | `usd` \| `ars` \| `eur` \| `gbp`. Se guarda siempre |
| cotizacion | Valor, fecha, tipo (dólar blue **promedio compra/venta**; compra y venta guardadas), fuente (ej. Rava, DólarHoy, o "la dio el usuario") |
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

**RecordatorioPersonal**: usuario, qué, cuándo (fecha y hora), origen (mensaje), hecho. «Mañana haceme acordar…» → saliente a esa hora.

**Tarea (piloto)**: qué, cuándo, caballos, origen (audio/WhatsApp de Tomás y hora), estado. Se envía a las 7:00 y se tacha por WhatsApp.

**MensajeOrigen**: persona, canal (`grupo` + grupo_id | `privado`), tipo, contenido o URL, duración (audio), transcripción, lectura de imagen, recibido_en, qué generó.

## Derivados (no se guardan)

- **Total de gastos** por período, lugar, grupo y categoría = suma de `monto_usd`.
- **Por cobrar** por acuerdo = acordado − Σ pagos + Σ gastos que cubre con reintegro pendiente.
- **Resultado por temporada** (en US$) = acuerdos y ventas de esa temporada + reintegros − gastos de ese lugar y fechas, **sin compras de caballos**.
- **Pagos que vienen** = pagos fijos con vencimiento próximo.

## Reglas
- El **mensaje original siempre se guarda**.
- **Monto y moneda originales inmutables**; la conversión a US$ se guarda con su cotización y fuente (no se recalcula sola).
- Las **correcciones** se loguean (antes/después) para evaluar la IA.
