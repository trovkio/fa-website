# Próximos pasos

Roadmap vivo. Actualizar al final de cada sesión.

---

## 🔥 Bloqueante inmediato (próxima sesión)

### 1. Resolver el conflicto Houzez/Elementor para el footer

**Acción 1:** Identificar dónde está hecho el **header** del sitio (Elementor Theme Builder o Houzez Theme Options).

```
Cómo verificar:
1. Ir a WP admin → Templates → Theme Builder → Header
   ¿Hay un header activo con condición "Entire Site"?
2. Si sí → header es de Elementor → footer también debería ir por ahí
3. Si no → header es de Houzez Theme Options → footer también debería ir por ahí
```

**Acción 2:** Según el resultado, decidir el camino del footer:
- **Si todo va por Elementor Theme Builder:** terminar el copy/paste de la página staging 6704 al template 6706. Asignar condición "Entire Site".
- **Si todo va por Houzez Theme Options:** abandonar el template 6706 y armar el footer en Theme Options → Footer. Más limitado pero coherente con el resto.

**Criterio de decisión:** consistencia con el header existente. No mezclar sistemas.

---

## 🟠 Siguiente (post-footer)

### 2. Limpiar páginas borrador / duplicadas

- Revisar estado del post 6700 (footer original). Si no aporta nada → borrar.
- Revisar otras páginas borrador en WP admin → Pages → todas. Documentar o borrar.

### 3. Crear página `/nosotros`

Brief en `08-briefs-paginas.md`. Es la siguiente página crítica (footer linkea a ella).

### 4. Crear página `/contacto`

Brief en `08-briefs-paginas.md`. Form + datos físicos + map opcional.

---

## 🟡 Mediano plazo

### 5. Resto del menú Propiedades

- `/residencial`
- `/emprendimientos`
- `/comercial`

Estructura parecida a `/tasaciones`, ajustando tono y contenido. Reusar containers.

### 6. Plataforma editorial

- `/radar` (Radar Inmobiliario) — landing del producto
- `/intelligence` (FAP Intelligence) — landing del producto
- `/blog` — listado de posts (¿usar tema o custom?)

### 7. Sistema de "Preguntas"

Decidir formato definitivo:
- Opción A: cada pregunta es una página con respuesta editorial larga (mejor SEO)
- Opción B: FAQ centralizada en una sola página
- Opción C: posts del blog tageados como "preguntas"

Recomendación tentativa: **A** para las 4 preguntas core, mientras se mantiene B como índice navegable.

---

## ⚪ Largo plazo / a investigar

### 8. Sistema de propiedades / listings

Houzez es un tema de real estate con CPT de propiedades. Hay que decidir:
- ¿Usar el CPT nativo de Houzez con su UI?
- ¿Customizar las cards de propiedad con Elementor?
- ¿Integración con portal MLS / scraping de portales (Argenprop, Zonaprop)?

### 9. Carreras / Trabajá con nosotros

Formato: landing + form, o link a sistema externo (Workable / Ashby / Notion).

### 10. Newsletter / lead capture

Decidir si va en footer o como página dedicada. Si va → integración con Mailchimp / Sendgrid / similar.

### 11. Multilenguaje

¿FA opera con clientes internacionales? Si sí, EN como segunda lengua. Plugin sugerido: WPML o Polylang.

### 12. Performance audit

Cuando esté el sitio armado, correr:
- Lighthouse
- PageSpeed Insights
- WebPageTest

Optimizar imágenes (WebP), lazy-load, critical CSS.

---

## Histórico de sesiones (changelog)

### 2026-05-21
- Reconstruido contexto en chat nuevo (sesión anterior se quedó sin tokens)
- Identificado el sistema de diseño de `/tasaciones` como fuente de verdad
- Construido footer en página staging 6704
- Creado template footer en Theme Builder (post 6706), vacío
- Identificado el wrapper Houzez como problema crítico
- **Decisión:** armar repo de contexto para no perder más sesiones reconstruyendo

### Antes del 2026-05-21
- Páginas existentes: `/tasaciones` (post 6081) completa
- Mega menú armado (estado a verificar)
- Sistema de diseño base implementado en `/tasaciones`
