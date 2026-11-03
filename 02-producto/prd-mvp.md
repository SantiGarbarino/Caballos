# PRD — MVP

**Estado:** borrador v0.1 · 2026-11-03 · Pendiente: sumar el mockup de Santi.

## Objetivo del MVP

Que un **polista profesional** pueda registrar **todos los gastos e ingresos de su organización desde WhatsApp** y ver en el celular **cuánto gasta, en qué, por caballo y por patrón**, sin cargar ni un formulario.

**Métrica norte:** % de usuarios que cargan movimientos **4 de 4 semanas** del mes (hábito).

## Usuarios del MVP

- **Principal:** polista profesional dueño de la organización (carga y mira).
- **Secundario (nice-to-have en MVP):** un "cargador" extra por organización (capataz / manager / pareja) que solo carga por WhatsApp.
- **Fuera del MVP:** patrón con login propio, petiseros, haras.

## Alcance

### ✅ Dentro (MVP)

**WhatsApp**
1. Registrar **gasto** o **ingreso** por texto, audio o foto de ticket/comprobante/transferencia.
2. La IA extrae: tipo (gasto/ingreso), monto, **moneda**, categoría, subcategoría, fecha, proveedor/persona, caballo(s) (opcional), patrón/centro de costo (opcional), medio de pago (efectivo/transferencia/cuenta corriente).
3. **Confirmación** en un mensaje con resumen + opción de corregir respondiendo ("no, eran dólares").
4. Pedir **solo el dato faltante crítico** (ej. el monto). Nunca un cuestionario.
5. Entender la **jerga** (lucas, palo, verdes, vete, herraje, petisero…).
6. **Consultas simples**: "¿cuánto gasté este mes?", "¿cuánto en vete en octubre?", "¿cuánto me debe Martín?".
7. **Resumen semanal/mensual automático** por WhatsApp.
8. Alta de **caballos** básica por WhatsApp ("tengo la Pampa, yegua zaina de 8 años") — para poder asignar gastos.

**Web app mobile-first**
1. Login por link mágico enviado por WhatsApp (sin contraseñas).
2. **Home**: gasto e ingreso del mes, saldo, comparación con mes anterior, por moneda.
3. **Movimientos**: lista con filtros (categoría, caballo, patrón, moneda, fecha), editar/borrar.
4. **Por categoría**: torta/barras del mes.
5. **Caballos**: lista + ficha con costo acumulado y movimientos asignados.
6. **Patrones**: gastos imputados a cada patrón, ingresos cobrados y pendientes → **resumen para rendir** (compartible por WhatsApp como link o PDF).
7. Exportar a Excel/CSV (para el contador).

### ❌ Fuera del MVP (backlog)
- Módulo completo de caballos (sanidad, herraje con recordatorios, movimientos/traslados, reproducción) → [modulo-caballos.md](modulo-caballos.md).
- Multiusuario con roles (patrón, petiseros).
- Presupuestos y alertas de desvío.
- Conversión automática de monedas con tipo de cambio del día.
- Integraciones (bancos, Mercado Pago, AFIP/ARCA).
- App nativa (el MVP es web app/PWA).
- Inglés (evaluar si los primeros usuarios lo necesitan en temporada afuera).

## Requerimientos funcionales clave

| ID | Requerimiento | Prioridad |
|---|---|---|
| F1 | Registrar gasto por texto con ≥90% de campos correctos sin repreguntar | Must |
| F2 | Registrar gasto por audio (transcripción + extracción) | Must |
| F3 | Registrar gasto por foto de ticket / comprobante de transferencia | Must |
| F4 | Registrar ingreso (cobro de patrón, venta de caballo, alquiler, clínica) | Must |
| F5 | Multimoneda (ARS, USD; GBP/EUR) — se guarda la original, se reporta por moneda | Must |
| F6 | Confirmar y corregir por WhatsApp | Must |
| F7 | Asignar gasto a 1, varios o todos los caballos; prorrateo simple | Should |
| F8 | Asignar gasto/ingreso a un patrón o "propio" | Must |
| F9 | Consultas en lenguaje natural por WhatsApp | Should |
| F10 | Resumen automático semanal/mensual | Should |
| F11 | Web app: home, movimientos, categorías, caballos, patrones | Must |
| F12 | Rendición al patrón compartible (link/PDF) | Should — **candidata a killer feature** |
| F13 | Exportar CSV/Excel | Should |
| F14 | Cobros pendientes ("me deben") | Could |

## Requerimientos no funcionales
- **Mobile-first**: diseñado para 375px de ancho; nunca pensado para desktop.
- **Velocidad**: confirmación por WhatsApp en < 10 s.
- **Privacidad**: los números de plata son sensibles (informalidad). Datos cifrados, nada compartido sin acción explícita del usuario. Política clara.
- **Tolerancia a errores**: todo editable/borrable desde WhatsApp ("borrá el último") y desde la app.

## Criterios de éxito del MVP (beta)
- 10–20 polistas activos en la temporada de otoño 2027.
- ≥ 60% carga al menos una vez por semana durante 8 semanas.
- ≥ 85% de movimientos registrados sin corrección manual.
- ≥ 5 usuarios dispuestos a pagar al terminar la beta.
- ≥ 3 referidos orgánicos (un polista que trae a otro).
