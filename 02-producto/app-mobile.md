# Web app mobile-first

> **Pendiente:** sumar el mockup/prototipo de Santi en `02-producto/mockups/` y ajustar este doc a partir de él.

## Principios
- **Diseñada para el celular** (375–430 px). No se diseña para desktop en el MVP; en desktop se ve la versión mobile centrada.
- **PWA**: se puede "instalar" en la pantalla de inicio desde el link de WhatsApp.
- **Login sin contraseña**: link mágico por WhatsApp.
- **Para mirar, no para cargar.** La carga es por WhatsApp. En la app solo se edita/corrige.
- Botón flotante **"Cargar por WhatsApp"** que abre el chat.
- Números grandes, poco texto, jerga del polo.

## Navegación (tab bar inferior)

| Tab | Contenido |
|---|---|
| 🏠 **Inicio** | Gasto e ingreso del mes por moneda, saldo, vs. mes anterior, top categorías, últimos movimientos, "te deben" |
| 📋 **Movimientos** | Lista cronológica, filtros (categoría, caballo, patrón, moneda, fecha), búsqueda. Tap → detalle con comprobante y mensaje original |
| 🐴 **Caballos** | Lista con foto, estado y costo del mes/acumulado. Tap → ficha |
| 🤝 **Patrones** | Por patrón: gastos imputados, ingresos, saldo → botón "Compartir rendición" |
| ⚙️ **Más** | Categorías, monedas, usuarios que cargan, exportar a Excel, perfil |

## Pantallas clave — detalle

### Inicio
```
Noviembre ▾
┌─────────────────────────┐
│ Gastos      $2.340.000  │
│             USD 3.500   │
│ Ingresos    USD 12.000  │
└─────────────────────────┘
[ barras por categoría ]
Te deben: Martín $850.000 + USD 2.000 →
Últimos movimientos …
```

### Ficha de caballo
- Foto, nombre, pelaje, edad, estado.
- Costo del mes / del año / desde que lo tenés.
- Movimientos asignados (vete, herraje…).
- (Fase 2) último herraje, sanidad, historial de traslados.

### Rendición al patrón (vista pública por link)
- Período, totales por categoría y moneda, detalle de movimientos con comprobantes.
- Sin login para el patrón (link con token). **Potencial gancho viral**: cada patrón que recibe una rendición ve el producto.

## Stack sugerido
Ver [arquitectura](../03-tecnico/arquitectura.md). Reutilizar el front de Queiros si es mobile-friendly.
