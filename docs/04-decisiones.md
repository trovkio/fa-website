# Decisiones

Registro de decisiones de diseño, arquitectura y producto. **No re-debatir sin motivo nuevo.** Si se revierte una decisión, agregar entrada nueva con fecha y razón, no editar la anterior.

---

## 2026-05 — Referencia visual: Criterion Global

**Decisión:** El sistema de diseño se inspira en [criterionglobal.com](https://criterionglobal.com): sobrio, tipográfico, grilla rigurosa, mucho aire.

**Por qué:** FA quiere posicionarse como autoridad editorial del sector inmobiliario argentino, no como una inmobiliaria más. El lenguaje visual de Criterion (consultora global de medios) transmite seriedad, datos, criterio. Es el tono correcto.

**Implicancias:**
- Cero stock photos genéricas de propiedades en hero
- Mucho peso visual en tipografía y números
- Layout editorial, no comercial
- Animaciones discretas, no efectistas

---

## 2026-05 — Sistema de diseño: replicar Tasaciones

**Decisión:** La página `/tasaciones` (post 6081) es la fuente de verdad. Cualquier página nueva debe replicar su sistema (grilla 6 cols, max-width 1400, Helvetica Now, bordes, grilla guía decorativa).

**Por qué:** Ya está construida, validada, y el cliente la aprobó. Inventar variaciones genera fricción y rompe coherencia.

**Implicancias:**
- Antes de construir una página nueva, hacer `get_page(6081)` y mirar los containers como template mental
- No usar sections viejos de Elementor, solo containers grid

---

## 2026-05 — Tipografía: Helvetica Now Display + Helvetica Now Text

**Decisión:** Familia única Helvetica Now en dos cortes (Display para títulos, Text para body). Peso dominante 500.

**Por qué:** Es la elección de Criterion. Es tipografía de sistema editorial moderno. FA ya pagó la licencia.

**No usar:** Roboto, Inter, Arial como fallback público. Si la font no carga, **es un bug a arreglar**, no un fallback aceptable.

---

## 2026-05 — Footer: estructura de 5 columnas + logo

**Decisión:** Footer con 6 columnas (logo + 5 de contenido):

```
Logo | Propiedades | Plataforma | Preguntas | Compañía | Social
```

**Por qué:**
- "Compañía" es FA (no las submarcas como hace Criterion, que es holding).
- "Preguntas" funciona como contenido editorial propio, refuerza posicionamiento.
- "Plataforma" agrupa los productos editoriales/tech (Radar, FAI, Blog).
- Social separado en su propia columna por jerarquía visual.

---

## 2026-05 — Footer: sección "Preguntas"

**Decisión:** Incluir una columna de "Preguntas" en el footer con 4 preguntas editoriales:
- ¿Cuánto vale mi propiedad?
- ¿Es buen momento para comprar?
- ¿Cómo leer el mercado?
- ¿Qué es el valor relativo?

**Por qué:** FA tiene propuesta editorial fuerte. Estas preguntas posicionan a FA como referencia. Funcionan como gancho para contenido del blog o landings dedicadas.

**Pendiente:** decidir si cada pregunta es una página, un post del blog, o una sección en una página FAQ. Mientras tanto, links provisorios a `/preguntas/{slug}`.

---

## 2026-05 — Legal del footer: matrículas

**Decisión:** El legal del footer debe incluir matrículas profesionales obligatorias:

```
© 2026 Fabián Achával Propiedades · Matrícula CUCICBA 6576 · CMCPSI 6385 · Política de Privacidad
```

**Por qué:** Cumplimiento normativo argentino para inmobiliarias. CUCICBA (Colegio Único de Corredores Inmobiliarios CABA) y CMCPSI (Colegio Martilleros y Corredores Públicos PBA).

**Fuente:** sitio actual de FA (fabianachaval.com.ar/gastos), donde aparecen ambas matrículas.

---

## 2026-05 — MCP de Elementor: alcance limitado a páginas

**Decisión:** Aceptar que el MCP no puede editar templates del Theme Builder. Para footer/header se trabaja en página staging (post type `page`) y se copia manualmente al template.

**Por qué:** Tools disponibles del MCP solo soportan post type `page`. No vale la pena buildear un MCP custom solo para esto en esta etapa.

**Workaround:**
1. Construir el elemento (footer, header) en una página staging
2. Copiar el container desde el editor de Elementor (click derecho > Copy)
3. Pegar en el template del Theme Builder

---

## 2026-05 — Page Layout: Canvas para staging

**Decisión:** Las páginas staging (como 6704 Footer Staging FAP) deben usar **Page Layout: Elementor Canvas** para evitar el wrapper Houzez.

**Por qué:** Houzez inyecta breadcrumb, título de página y sidebar incluso con template "elementor_header_footer". Canvas es la única forma de aislar.

**Cómo:** En el editor de Elementor de la página → engranaje ⚙️ abajo a la izquierda → Page Layout → Elementor Canvas → Update.

---

## Decisiones pendientes (a tomar)

- [ ] ¿Header se mantiene como está o se rediseña? Y dónde se edita (Theme Builder vs Houzez Theme Options).
- [ ] ¿Footer va por Elementor Theme Builder o por Houzez footer builder?
- [ ] Estructura de URLs para "Preguntas": páginas, posts, o FAQ.
- [ ] Logo del footer: ¿isotipo solo o logotipo completo?
- [ ] Idioma: ¿multilenguaje (ES/EN) o solo ES?
- [ ] Newsletter / lead capture en footer: ¿sí o no?
- [ ] Dirección física en footer: ¿sí o no?
- [ ] Datos de contacto en footer (teléfono, email): ¿sí o no?
