# Modelo de datos (v0)

> Pensado para que el MVP (gastos) y la fase 2 (caballos) convivan sin migraciones grandes, y para escalar a multiusuario y haras.

```
Organizacion ──< Usuario (rol: dueño | cargador | patrón | petisero)
     │
     ├──< Caballo ──< EventoCaballo (herraje, sanidad, traslado, estado, cría…)
     │       │
     │       └──< AsignacionMovimiento >── Movimiento
     │
     ├──< Patron (centro de costo)
     ├──< Proveedor / Persona (herrero, vete, forrajería, petisero)
     ├──< Categoria (sistema + personalizadas)
     │
     └──< Movimiento ──> MensajeOrigen (texto/audio/foto, transcripción, OCR)
```

## Entidades

**Organizacion**: id, nombre, moneda_principal, país, plan, creada_en.

**Usuario**: id, organizacion_id, nombre, teléfono_whatsapp, rol, idioma.

**Movimiento**
| Campo | Tipo |
|---|---|
| id | uuid |
| organizacion_id | fk |
| tipo | gasto \| ingreso |
| monto | decimal |
| moneda | ARS \| USD \| GBP \| EUR … |
| categoria_id / subcategoria | fk / texto |
| fecha | date |
| proveedor_id | fk nullable |
| patron_id | fk nullable (null = propio) |
| medio_pago | efectivo \| transferencia \| cuenta_corriente \| otro |
| estado | confirmado \| pendiente_confirmacion \| pendiente_cobro |
| nota | texto |
| cargado_por | usuario_id |
| mensaje_origen_id | fk (trazabilidad) |
| confianza_ia | float (para el loop de corrección) |

**AsignacionMovimiento**: movimiento_id, caballo_id, monto_prorrateado.

**Caballo**: id, organizacion_id, nombre, sexo, pelaje, año_nacimiento, raza, registro, padre, madre, nivel, estado, ubicación, propiedad (propio / patrón / sociedad %), fotos.

**EventoCaballo**: id, caballo_id, tipo, fecha, detalle (json), movimiento_id nullable, mensaje_origen_id.

**Patron**: id, organizacion_id, nombre, teléfono (opcional), reglas de imputación.

**MensajeOrigen**: id, usuario_id, tipo (texto/audio/imagen), contenido/url, transcripción, ocr, payload_ia, recibido_en.

## Decisiones de modelo
- El **mensaje original siempre se guarda** (trazabilidad + dataset para mejorar la IA).
- **Moneda original inmutable**; conversiones como vista/reporte.
- Las **correcciones** del usuario se loguean (antes/después) → entrenamiento/evaluación del extractor.
