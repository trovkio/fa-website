# Próximos pasos

Roadmap vivo. Actualizar al final de cada sesión.

---

## 🔥 Activo ahora (home)

### 1. Accordion full-bleed — padding interno

El accordion tiene `fap-full-bleed` en CSS Classes pero todavía tiene padding lateral en Layout → Padding. Ponerlos todos en 0.

### 2. Hero con imagen — centrar el texto

El container de la imagen hero tiene `fap-full-bleed` funcionando. El texto "Fabián Achával" todavía no está centrado verticalmente. Resolver con Min Height en el container y Justify Content: Center.

### 3. Copy de la home

Estamos trabajando en el copy introductorio. La estructura es:
- Línea 1: **Fabián Achával** (nombre propio, sin "Propiedades")
- Línea 2: claim que expresa más que una inmobiliaria de forma serena y convocante

Dirección explorada: zona del "territorio" — donde la información y la experiencia operan como una sola cosa.

---

## 🟠 Siguiente (post-home)

### 4. Footer — approach por página

Decisión tomada: no usar Theme Builder para el footer. Agregar el footer como containers al final de cada página via MCP. Más control, sin conflictos con Houzez.

El JSON del footer está construido en el 6704 (staging). Hay que adaptarlo para que funcione con el nuevo sistema de margen lateral (`.main-wrap > .elementor`) — el truco `100vw` ya no es necesario, el footer puede usar `max-width: 1400px; margin: auto` como el resto de los containers.

### 5. Páginas pendientes

- `/nosotros` — prioridad alta (brief en 08-briefs-paginas.md)
- `/contacto` — prioridad alta
- `/residencial`, `/emprendimientos`, `/comercial` — media
- `/radar`, `/intelligence`, `/blog` — media

---

## Histórico de sesiones

### 2026-05-28
- Resuelto el problema de full-bleed con clase helper `fap-full-bleed`
- Descubierto que los wrappers reales de Houzez son `.main-wrap > .elementor` (no `#page` etc.)
- CSS de Houzez auditado y corregido
- Home: imagen hero full-bleed funcionando
- Home: accordion full-bleed parcialmente funcionando (padding pendiente)
- Explorado copy introductorio de la home (zona del territorio)
- Documentadas reglas de trabajo con CSS

### 2026-05-27
- Construido footer en staging (6704)
- Creado template footer Theme Builder (6706), asignado condición "Entire Site"
- Identificado problema: MCP no puede editar elementor_library
- CSS del footer corregido múltiples veces
- Snapshot backup home (5706) guardado en elementor-exports

### 2026-05-21
- Reconstruido contexto
- Construido footer staging
- Identificado wrapper Houzez como problema crítico
- Creado repo de contexto
