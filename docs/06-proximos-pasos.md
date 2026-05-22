# Próximos pasos

Roadmap vivo. Actualizar al final de cada sesión.

---

## 🔥 Bloqueante inmediato (próxima sesión)

### 1. Corregir tamaño de property cards en la home

**Problema:** Las cards del widget `houzez_elementor_property-card-v5` (section `5811ff4`) se ven más grandes que en `demo05.houzez.co`. El grid es correcto (3 columnas) pero el ancho total es demasiado grande.

**Acción:** Antes de tocar cualquier CSS, abrir `demo05.houzez.co` con DevTools y medir:
- Ancho del `.property-cards-module`
- Ancho de cada `.item-listing-wrap`
- Altura de `.listing-featured-thumb`

Después replicar esas medidas con CSS en el Kit global (post-9) usando el selector correcto (no `.elementor-element-5811ff4 .property-cards-module` que no aplicó).

**Approach alternativo:** Cambiar el `content_width` del section 5811ff4 directamente en el JSON de la home via `update_page`. Más limpio que CSS.

### 2. Terminar de revisar todos los bloques de la home

Uno por uno, comparar con demo05.houzez.co y ajustar lo que quedó diferente:
- [ ] Property cards (tamaño) — pendiente
- [ ] Search builder (ancho) — aplicado, verificar
- [ ] "Descubre nuestra selección" (slideshow section)
- [ ] Agentes
- [ ] Blog posts
- [ ] Barrios / grid builder

### 3. Activar backup automático en WPvivid

**Ruta:** WP Admin → WPvivid Backup → Schedule → daily, Local Storage.
Hacer también un backup manual ahora como baseline antes de seguir trabajando.

---

## 🟠 Siguiente (post-home)

### 4. Clonar home a /residencial

Ya se intentó pero el JSON de 72KB tuvo problemas con el CSS global. Con el backup activo y el approach correcto (cambiar `content_width` en lugar de CSS global), hacerlo de nuevo.

Post target: 6688 (page, publish, vacía).

### 5. Construir /nosotros, /contacto

Brief en `08-briefs-paginas.md`.

---

## 🟡 Mediano plazo

### 6. Resolver footer (renderizado en frontend)

El footer Principal (post 6716, `fts_builder`) está publicado con condición "Entire Site" pero no aparece en el frontend. Hipótesis: Houzez Theme Options pisa el template `fts_builder`. Investigar con DevTools inspeccionando el footer en el DOM.

### 7. Resto del menú Propiedades

- `/emprendimientos`
- `/comercial`

### 8. Plataforma editorial

- `/radar`
- `/intelligence`
- `/blog`

---

## Histórico de sesiones (changelog)

### 2026-05-22
- **Incidente:** `update_page` sobre `/residencial` (72KB JSON) regeneró el CSS global y rompió los estilos de property cards en toda la instalación
- **Resolución:** Forzar regeneración del Kit global (post-9) via Custom CSS → Save. CSS restaurado.
- **Pendiente:** Afinar tamaño de property cards (comparar con demo05.houzez.co)
- **Aprendizaje crítico:** Todo `update_page` puede romper CSS global. Siempre tener backup activo antes de operar.
- **Estado al cierre:** Home funcionando, cards en 3 columnas correctas pero tamaño a ajustar. /residencial vacía.

### 2026-05-21
- Reconstruido contexto en chat nuevo (sesión anterior se quedó sin tokens)
- Identificado el sistema de diseño de `/tasaciones` como fuente de verdad
- Construido footer en página staging 6704
- Creado template footer en Theme Builder (post 6716), vacío
- Identificado el wrapper Houzez como problema crítico
- **Decisión:** armar repo de contexto para no perder más sesiones reconstruyendo

### Antes del 2026-05-21
- Páginas existentes: `/tasaciones` (post 6081) completa
- Mega menú armado
- Sistema de diseño base implementado en `/tasaciones`
