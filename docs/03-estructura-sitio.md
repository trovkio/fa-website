# Estructura del sitio

Mapa actualizable de todas las páginas, sus IDs en WP, slugs, estado y rol.

## Tabla maestra de páginas

| ID | Slug | Título | Estado | Rol |
|---|---|---|---|---|
| 6081 | `/tasaciones` | Tasaciones | ✅ Completa | Fuente de verdad del sistema de diseño |
| 6700 | `/footer-original` | (footer trabajo previo) | 🟡 Estado dudoso | A revisar, posible candidato a borrar |
| 6704 | `/footer-staging-fap` | Footer Staging FAP | 🟡 En construcción | Página staging para diseñar el footer antes de copiarlo al template real |
| 6706 | — | Elementor Footer | 🟡 Vacío | Template del Theme Builder donde irá el footer final, asignado como condición "Entire Site" |

## Páginas pendientes de crear

Estructura propuesta de URLs (alineada con el menú principal):

### Propiedades

- `/tasaciones` ✅
- `/residencial` ❌
- `/emprendimientos` ❌
- `/comercial` ❌

### Investigación / Plataforma

- `/radar` (Radar Inmobiliario) ❌
- `/intelligence` (FAP Intelligence) ❌
- `/blog` ❌
- `/perspectivas` ❌ (si se confirma como sección editorial)

### Preguntas (sección editorial — formato y ubicación a definir)

- `/preguntas/cuanto-vale` ❌
- `/preguntas/buen-momento` ❌
- `/preguntas/leer-mercado` ❌
- `/preguntas/valor-relativo` ❌

Estas páginas funcionan como contenido editorial que posiciona a FA como autoridad en lectura de mercado. Funcionalmente parecidas a las "Resources" de Criterion Global. **Pendiente decidir** si son páginas completas, posts del blog, o cards en una sola página tipo FAQ.

### Compañía

- `/nosotros` ❌
- `/contacto` ❌
- `/carreras` ❌

### Legal

- `/politica-de-privacidad` ❌
- `/terminos` ❌ (opcional)

## Header

Menú principal visible en todas las páginas:

```
Propiedades ▾    Investigación    Radar    FAi    Compañía    Blog    Contacto
  ├ Tasaciones
  ├ Residencial
  ├ Emprendimientos
  └ Comercial
```

**Estado:** existe y funciona, pero **no está documentado** dónde se edita (Elementor Theme Builder vs Houzez Theme Options). **Pendiente verificar y documentar acá** apenas se confirme.

## Footer

### Estructura visual definida (referencia Criterion Global, sobrio)

```
┌──────────────────────────────────────────────────────────────────────┐
│  Logo │ Propiedades │ Plataforma │ Preguntas        │ Compañía │ Social
│   *   │ Tasaciones  │ Radar Inm. │ ¿Cuánto vale?    │ Nosotros │ Instagram
│       │ Residencial │ FAP Intel. │ ¿Buen momento?   │ Contacto │ LinkedIn
│       │ Emprendim.  │ Blog       │ ¿Leer mercado?   │ Carreras │
│       │ Comercial   │            │ ¿Valor relativo? │          │
├──────────────────────────────────────────────────────────────────────┤
│  © 2026 Fabián Achával Propiedades · CUCICBA 6576 · CMCPSI 6385 · Pol. Priv.
└──────────────────────────────────────────────────────────────────────┘
```

### Tokens del footer

- Container grid 6 fr, max-width 1400, fondo blanco
- Borde top fuerte `rgba(0,0,0,0.85)`, borde bottom suave `rgba(0,0,0,0.12)`
- Header de columna: 15px Helvetica Now Display weight 500, margin-bottom 36px
- Links: 14px Helvetica Now Text weight 400, line-height 1.6 (1.4 para Preguntas)
- Hover en links: `opacity: 0.5`
- Padding: 80px top, 60px bottom, 30px horizontal
- Logo: 40px de ancho, SVG (ID 6100 en media library: RADAR-ISO.svg — confirmar si es ese o hay otro)
- Fila legal: 12px Helvetica Now Text, color negro, border-bottom 1px solid 0.12

### Decisiones tomadas sobre el footer

- ✅ "Compañía" es para FA (Nosotros / Contacto / Carreras), **no** para las submarcas (como Criterion).
- ✅ Sección "Preguntas" es contenido editorial propio, refuerza voz FA.
- ✅ Matrículas obligatorias en el legal: CUCICBA 6576 + CMCPSI 6385.
- ✅ Logo es el isotipo `RADAR-ISO.svg` (a confirmar si hay un logotipo completo FAP para el footer).

### Issues activos del footer

Ver `05-problemas-conocidos.md`. El wrapper Houzez sigue rompiendo el layout.

## Convenciones de slugs

- Todo en minúsculas, sin tildes ni ñ
- Separador: guion medio `-`
- Sin sufijo `/page` ni `.html`
- Plurales naturales del español (tasaciones, emprendimientos)
- Preguntas: `/preguntas/{slug-corto}`

## Convenciones de naming en Elementor

- IDs de elementos: alfanuméricos cortos, semánticos cuando se puede (`ftcol02`, `ftlogo01`)
- Evitar IDs con guiones bajos al inicio
- Para containers de página completa, prefijar con código de sección: `tas_hero_01`, `tas_3cols_01`, etc.
