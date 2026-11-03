# Preguntas abiertas

Lo que todavía no sabemos o no decidimos. Cuando se resuelve, pasa a [decisiones.md](decisiones.md).

## Resueltas (2026-11-03)
- ~~Nombre del producto~~ → **PROGRAMON** (logo pendiente).
- ~~¿Cómo manejamos el tipo de cambio?~~ → **No se convierte.** Cada moneda por separado, sin totales combinados.
- ~~Mockup de Santi~~ → en [`02-producto/mockups/`](../02-producto/mockups/README.md).
- ~~¿Puede cargar alguien más que el polista?~~ → Sí: piloto, petiseros, puestero y quien lleva las cuentas cargan por WhatsApp. El contador solo ve gastos para exportar.
- ~~¿Qué tan importante es lo del patrón?~~ → Es central en **Ingresos** (acuerdos, pagos parciales, gastos que cubre y reintegros). El patrón **no** ve la cuenta.

## Negocio
- [ ] **ICP final**: ¿alto handicap sin manager (persona del mockup), mediano handicap o ambos? Validar en entrevistas.
- [ ] **Logo** y pantalla de carga con la marca.
- [ ] ¿Empresa nueva o línea de producto de Queiros? (marca, sociedad, cap table).
- [ ] **Pricing**: ¿por organización, por cantidad de caballos, por usuario? ¿US$ mensual o anual (referencia Pensai US$ 200/año/usuario)? Ver [pricing](../05-gtm/pricing.md).
- [ ] ¿Quién paga si el patrón quiere el producto para sus profesionales?
- [ ] ¿Bilingüe desde el día 1? (el polista pasa meses en Inglaterra/España; sus petiseros afuera suelen ser argentinos).
- [ ] ¿Haras/cría como segundo vertical o en paralelo? Salir de las 3–5 entrevistas a haras.

## Producto
- [ ] **Onboarding** (postergado por decisión). Idea discutida: primera carga por WhatsApp (lista de caballos, equipo, pagos fijos y acuerdos dictados por audio) más una revisión web; *white-glove* (lo configuramos nosotros) para los primeros clientes.
- [ ] **Ficha digital oficial del caballo** (libreta sanitaria digital, pasaporte equino, microchip) y camino a "aplicación autorizada" de SENASA. Ver [regulación](../01-mercado/regulacion-senasa.md).
- [ ] ¿Costo por caballo? Se sacó la pestaña Costos del mockup por ruido. ¿Vuelve en algún formato o se descarta?
- [ ] ¿Prorrateo de gastos entre caballos (ej. herraje de 4 caballos)? Hoy el gasto se registra una vez y el herraje se anota en cada ficha.
- [ ] ¿Cómo se registra el consumo real de stock? El mockup sugiere "según los conteos de Pedro se usan 3,4 por día": definir de dónde salen los conteos (fotos o mensajes del piloto) y cómo se ajusta.
- [ ] ¿Pedidos a proveedores desde la app? Se sacó del mockup ("pedir al proveedor"). El cierre del día todavía menciona "ya le pediste 40 bolsas al corralón".
- [ ] Gastos que paga el piloto de su bolsillo ("lo pagué yo en efectivo"): ¿se lleva una cuenta de lo que se le debe al piloto?
- [ ] ¿Qué ve exactamente quien lleva las cuentas (Sofía) y qué puede editar?
- [ ] Recordatorios automáticos derivados (ej. "Sacar sangre para AIE" automático por un viaje): ¿qué reglas?

## Técnico
- [ ] Costo y diseño de los **mensajes salientes** (plantillas de Meta, ventana de 24 h): tareas del piloto 7:00, pagos fijos, recordatorios, cierre del día 20:00.
- [ ] ¿Mismo BSP que Queiros (SendPulse) o uno nuevo? Número de WhatsApp propio de PROGRAMON.
- [ ] ¿Repo de código nuevo o fork/módulo de Queiros App?
- [ ] Estimación real de Mauro sobre la brecha técnica (ver [plan](../04-plan/plan-ejecucion.md)).
