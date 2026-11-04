# Segmentos y personas

> **Usuarios de la plataforma (2026-11-03):** los **owners** (quien crea la organización, polista o manager, y a quien le dé todos los accesos; en el caso típico, el polista y su manager) ven todo y configuran qué ve cada usuario. El resto de la organización (piloto, petiseros, puestero, un familiar o asistente) y los proveedores son por defecto **usuarios de solo WhatsApp**: cargan por el bot y figura quién lo cargó. Un owner les puede habilitar una parte de la app (secciones y qué caballos), nunca Gastos ni Ingresos. El patrón no existe para la plataforma. Tomás y su equipo son el **ejemplo ficticio del mockup**: no definen el ICP.

## Segmentos (a validar)

| # | Segmento | Tamaño de organización | Dolor de gastos | Disposición a pagar | Prioridad |
|---|---|---|---|---|---|
| 1 | **Profesional de alto handicap sin manager** (el polista hace todo) | 30–40 caballos entre caballeriza, campo y exterior; piloto, 3–4 petiseros, puestero | Altísimo: varias monedas, varios lugares, varios patrones, montos grandes | Alta | Ejemplo del mockup; a validar |
| 2 | **Profesional de mediano handicap (≈2–6 goles) con organización propia** | 15–40 caballos, 2–6 petiseros | Muy alto | Media-alta | A validar como beachhead alternativo |
| 3 | **Organización grande con manager** (la mano derecha registra todo) | 40–100+ caballos | Altísimo; el manager es quien más usaría el producto | Alta | **Clave**: el manager es usuario principal y owner (todos los accesos, si el polista se los da o si él crea la organización) |
| 5 | Amateur con caballos propios | 4–12 caballos | Medio | Baja-media | Volumen, más adelante |
| 6 | **Haras / criador** | 50–500 caballos | Alto y más complejo | Alta | Posible mercado grande: entrevistar 3–5 ya |
| 7 | Club / pensión de caballos | Muchos caballos de terceros | Facturar pensión y extras | Media | Más adelante |

**[HIPÓTESIS]** El ICP es muy sensible: rechaza lo feo o engorroso. Por eso se valida primero con el mockup.

> El **patrón** no es un segmento: no usa ni compra la plataforma. Es quien le paga al polista.

## El manager (usuario clave)

- Es la **mano derecha** del polista en las organizaciones grandes.
- **Registra todo**: lo que pasa en las caballerizas, el stock, lo que habla con el veterinario y el herrero, el día a día de cada yegua.
- **Ve exactamente lo mismo que el polista** en la app. No hay información que uno vea y el otro no.
- Muchas veces el que usa el producto **no es el jugador sino el manager**: el producto, los textos y la venta tienen que hablarle a los dos.

## Persona del mockup (ejemplo ficticio)

### "Tomás", polista profesional de alto handicap
- Hace todo él mismo: no tiene manager. Lo que no hace él lo hace su **piloto**.
- **35 caballos**: 14 jugando en la caballeriza de Pilar, 15 en el campo de Cnel. Suárez (descanso, doma, madres, una preñada), 4 en invernada en Windsor (Inglaterra) y 2 en recuperación en Pilar. Ver el [dataset del mockup](../02-producto/mockups/dataset-ficticio.md).
- Juega la temporada argentina (Pilar), Inglaterra (Windsor, abril a julio) y Sotogrande (agosto). Tiene cerrado Wellington 2027.
- Juega para varios **patrones** con acuerdos por temporada: Northfield (Inglaterra, US$ 250.000), Palm Ridge (Wellington 2027, US$ 180.000), La Ensenada (Argentina, US$ 60.000), Les Pins (Chantilly, € 45.000), Valle Alto (Sotogrande, € 80.000). También vende caballos (Halcona US$ 85.000, Trueno US$ 40.000).
- Gasta en US$, $ y €, acá y afuera. Paga alquiler de caballeriza y casa en Pilar, invernada en Windsor, sueldos, fletes aéreos, pasajes, inscripciones y handicap (AAP y HPA).
- **Quiere**: saber cuánto gastó y en qué, cuánto le deben, qué le pasa a cada caballo, que no se le termine la avena, y que el piloto se entere de las cosas.
- **No quiere**: aprender una app, cargar formularios, sentarse en una compu, que sus patrones vean sus números.

### Su equipo (personas secundarias)

| Persona | Rol | Cómo usa PROGRAMON |
|---|---|---|
| **Pedro** | **Piloto** (encargado) de la caballeriza de Pilar | Solo WhatsApp: recibe tareas a las 7:00, avisos y recordatorios; las tacha respondiendo. Reporta herrajes, stock y gastos que paga. **No ve plata** |
| **Ramón** | Petisero en Pilar | Audios con vareos y novedades (ej. "la Rockstar renguea"), fotos |
| **Lucho** | Petisero en Pilar | Audios con vareos y novedades (ej. "la Negra no terminó la ración") |
| **Juanca** | Petisero en Windsor | Reporta las 4 de la invernada; carga gastos de Inglaterra |
| **Don Aníbal** | **Puestero** del campo (Cnel. Suárez) | Reporta los 15 del campo; manda la foto de los rollos. Si no manda mensajes hace 2 días, se destaca |
| Dra. Ibarra / Cacho | Veterinaria / herrero | Trabajan para varios polistas. Cargan en el grupo de WhatsApp de cada cliente; si escriben por privado, el bot pregunta para qué cliente. No usan la app |
| Estudio Ruiz | Contador | No es usuario: recibe el export por mail |

> En el mockup hay una persona que lleva las cuentas con acceso a la app: pasa a ser de solo WhatsApp. Los usuarios de la app son el polista y el manager.

### El patrón (contexto, no es usuario)
- Le paga al polista por jugar y a veces le reintegra gastos (fletes, pasajes de petiseros). Para la plataforma **no existe**: solo aparece en Ingresos como contraparte.

### "Laura", dueña de haras (fase posterior)
- 150 caballos entre yeguas madre, receptoras, potrillos y caballos en doma.
- Quiere control de reproducción, sanidad, stock por categoría, ventas y documentación.

## Jobs to be done

1. *Cuando pago algo, quiero mandarlo por WhatsApp en 5 segundos (audio o foto) para no olvidarme.*
2. *Cuando quiero saber cuánto gasté, quiero verlo por período (mes, temporada, rango) y por lugar, en dólares, y entender de dónde sale cada número (y cómo se convirtieron los pesos).*
3. *Cuando cierro con un patrón o vendo un caballo, quiero registrar lo acordado y cada pago para saber cuánto me deben.*
4. *Cuando pago algo que cubre el patrón, quiero que se sume a lo que me debe.*
5. *Cuando termina una temporada, quiero ver si me quedó plata en ese lugar.*
6. *Cuando un petisero avisa algo de un caballo, quiero que quede en su ficha y que me llegue si es importante.*
7. *Cuando le pido algo al piloto, quiero que le llegue y saber si lo hizo.*
8. *Cuando se está terminando un insumo, quiero saberlo antes de que falte.*
9. *Cuando llega fin de mes, quiero que los pagos fijos se carguen solos con un «sí».*
10. *Cuando el contador me pide los gastos, quiero mandárselos con las fotos en un toque.*
11. *Cuando algo no me lo quiero olvidar, quiero decirle al bot «mañana haceme acordar» y que me lo recuerde.*
12. *Cuando sumo un caballo, quiero elegirlo de la app Polo Argentino y no cargar su sangre a mano.*
13. *(Manager) Cuando pasa algo en la caballeriza o hablo con el vete, quiero mandarlo al grupo y que quede registrado.*
