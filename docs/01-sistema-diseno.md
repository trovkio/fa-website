# Sistema de diseño FA

Decodificado de la página Tasaciones (post 6081), que funciona como **fuente de verdad del sistema**. Cualquier página nueva debe replicar estos patrones, no inventar nuevos.

## Grilla

- **Container type:** `grid` (containers nativos de Elementor, no sections viejos)
- **Columnas:** 6 fracciones (`grid_columns_grid: {unit: "fr", size: 6}`)
- **Content width:** `full`
- **Max-width interno:** `1400px` vía custom CSS (`max-width: 1400px; margin: 0 auto`)
- **Padding del container:** 0 horizontal (el max-width controla el ancho)
- **Row gap:** 0
- **Posicionamiento de widgets:** cada widget tiene `grid-column: X / Y` en su `custom_css` individual

### Grilla guía visible (decorativa)

Patrón recurrente en cada container: líneas verticales muy sutiles cada 1/6 del ancho.

```css
background-image: repeating-linear-gradient(
  90deg,
  transparent 0,
  transparent calc((100% / 6) - 1px),
  rgba(0,0,0,0.035) calc((100% / 6) - 1px),
  rgba(0,0,0,0.035) calc(100% / 6)
);
```

### Bordes entre secciones

Cada container suele tener:
- `border-top: 1px solid rgba(0,0,0,0.85)` (fuerte arriba)
- `border-bottom: 1px solid rgba(0,0,0,0.12)` (sutil abajo)
- Sin bordes laterales

## Tipografía

### Familias

- **Helvetica Now Display** → títulos, headings, números grandes
- **Helvetica Now Text** → body, párrafos, links de footer

Ambas son fonts custom cargadas en Elementor (Custom Fonts). Confirmar carga en el editor antes de asumir.

### Pesos

- **500** es el peso dominante (medium). Casi todo el sitio.
- **600** se usa para números grandes (01., 02., 03.)
- **400** para body de footer/links menores

### Escala (px desktop)

| Uso | Size | Family | Weight | Line height | Letter spacing |
|---|---|---|---|---|---|
| Hero / Section title XL | 75 | Display | 500 | 1.03em | -2px |
| Section title L | 50 | Display | 500 | 1.03em | — |
| Sub-section title | 35 | Display | 500 | 1em | — |
| Numbers (01. 02.) | 50 | Display | 600 | 1em | — |
| Section label / breadcrumb | 30 | Display | 500 | 1em | — |
| Body paragraph | 20 | Text | 500 | 1.4-1.5em | — |
| Footer column header | 15 | Display | 500 | 1.4em | — |
| Footer link | 14 | Text | 400 | 1.6em | — |
| Legal text | 12 | Text | 400 | 1.6em | — |
| Display CTA (decidir bien) | 5vw | Display | 500 | 1em | -2.5px |

### Responsive

Reducir 25-40% en tablet, 50-60% en mobile. Helvetica Now Display 75px → 55px tablet → 45px mobile.

## Colores

Paleta minimalista:

- `#000000` — negro (texto principal, bordes fuertes)
- `#FFFFFF` — blanco (fondo)
- `rgba(0,0,0,0.85)` — borders top fuertes
- `rgba(0,0,0,0.12)` — borders bottom suaves
- `rgba(0,0,0,0.035)` — líneas de grilla guía
- `#C4634A` — naranja oxidado (CTAs, buttons) — visto en form de Tasaciones
- `#DA7756` — naranja hover

No usar grises medios ni colores corporativos saturados. La identidad es la tipografía y el blanco.

## Padding / Spacing patterns

- Containers de sección: `padding-top: 60-100px`, `padding-bottom: 60-100px`
- Headings xl: `padding: 60px 0 40px 0` cuando son standalone
- Gap entre columnas del grid: 24px típico
- Footer principal: padding-top 80px, padding-bottom 60px

## Componentes recurrentes

### Section header pattern

```
[Borde top fuerte] [Borde decorativo grilla 6 cols]
  [Padding 60px top]
  [Numeración pequeña: 01. Tasaciones] — 30px Display 500
  [Padding 60px bottom]
  [Borde negro sutil entre número y título]
  [Título XL: Innovación de la Tradición] — 75px Display 500
```

### Three-column comparison (01. 02. 03.)

Grid de 12 columnas (no 6), con:
- Números en `grid-column: 1/3`, `5/7`, `9/11`
- Títulos sub en `grid-column: 1/4`, `5/8`, `9/12`
- Body en mismas columnas que títulos
- Todos en `grid-row` distintos (1, 2, 3) para alinearse en filas

### Two-column heading + body

Grid de 6 columnas:
- Heading en `grid-column: 1/3` (izquierda, ~33%)
- Body en `grid-column: 3/6` (derecha, ~50%)

## Reglas no negociables

1. **Nunca usar sections viejos de Elementor**, solo containers grid.
2. **Nunca poner widths en porcentaje fijo de columnas.** Usar `grid-column: X/Y` con fr units.
3. **Nunca cambiar la tipografía.** Si Helvetica Now Display/Text no carga, primero verificar Custom Fonts en Elementor; no fallback a Roboto/Inter.
4. **Mantener `max-width: 1400px`** centrado, salvo casos hero full-bleed donde se documenta excepción.
5. **Bordes finos siempre `1px solid`**, nunca thicker. La sobriedad es el lenguaje.

## Referencia visual

- **Criterion Global** (criterionglobal.com) — referencia principal de layout y composición.
- **Página Tasaciones del sitio** — implementación real del sistema.
