# footer-staging-6704.json

**Componente:** Footer principal del sitio (estructura completa).
**Origen:** Pagina staging WP post 6704 "Footer Staging FAP" (post type `page`).
**Validado:** 2026-05-22
**Dependencias:**
- Custom Fonts en Elementor: `Helvetica Now Display` y `Helvetica Now Text`.
- Imagen media library ID 6100: `RADAR-ISO.svg` (isotipo).
- Slugs de paginas referenciadas (algunos todavia no existen): `/tasaciones`, `/residencial`, `/emprendimientos`, `/comercial`, `/radar`, `/intelligence`, `/blog`, `/preguntas/cuanto-vale`, `/preguntas/buen-momento`, `/preguntas/leer-mercado`, `/preguntas/valor-relativo`, `/nosotros`, `/contacto`, `/carreras`, `/politica-de-privacidad`.

## Estructura

Tres containers raiz:

1. **`ftmain02`** - container grid 6fr, max-width 1400px interno, padding 80/30/60/30. Borde top fuerte, borde bottom suave. Grilla guia decorativa via `repeating-linear-gradient` aplicada al `.e-con-inner`. Hijos: 6 columnas.
   - `ftcol01` (logo isotipo, 40px) - col 1
   - `ftcol02` (Propiedades + 4 links) - col 2
   - `ftcol03` (Plataforma + 3 links) - col 3
   - `ftcol04` (Preguntas + 4 links, line-height mas chico por longitud) - col 4
   - `ftcol05` (Compania + 3 links) - col 5
   - `ftcol06` (Social + Instagram) - col 6

2. **`ftcontact01`** - container grid 6fr. Bloque Contacto + Matriculas en su propia fila, separado por border-top suave.
   - `ftcontactA` (Contacto: tel/email/direccion) - cols 2-4 (col 1 vacia, debajo del logo)
   - `ftcontactB` (Matriculas: CUCICBA + CMCPSI) - cols 5-6

3. **`ftlegal02`** - container flex, fila legal de copyright + Politica de Privacidad. 12px.

## Tokens de tipografia

| Elemento | Family | Size | Weight | LH |
|---|---|---|---|---|
| Header de columna | Helvetica Now Display | 15px | 500 | 1.4em |
| Link normal | Helvetica Now Text | 14px | 400 | 1.6em |
| Link en Preguntas | Helvetica Now Text | 14px | 400 | 1.4em |
| Label gris (Contacto/Matriculas) | Helvetica Now Display | 13px | 500 | 1.4em |
| Texto de Contacto/Matriculas | Helvetica Now Text | 14px | 400 | 1.6em |
| Legal | Helvetica Now Text | 12px | 400 | 1.6em |

## Notas operativas

- Mientras se mira en una **pagina** (post type `page` con template default), Houzez agrega un wrapper con breadcrumb + titulo H1 grande. Eso desaparece cuando este container se copia al **template Footer Principal** del Theme Builder.
- La grilla guia decorativa puede verse mas tenue de lo previsto por el padding del `.e-con-inner`. Si no se ve nada, mover el `background-image` al container externo en vez de al inner.
- El correo `info@fabianachaval.com` (sin `.ar`) fue elegido explicitamente.

## Como restaurar este footer en WP

Pegar el JSON entero al meta `_elementor_data` del post 6704 (o cualquier otro post de tipo `page`) y guardar.

Usando el MCP de Elementor:

```
elementor-mcp:update_page(pageId=6704, elementor_data=<contenido del json>)
```
