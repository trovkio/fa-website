# Arquitectura técnica

## Stack

| Capa | Tecnología | Notas |
|---|---|---|
| Hosting | Hostinger | Plan compartido, dominio staging `papayawhip-fly-823460.hostingersite.com` |
| CMS | WordPress | Última versión estable |
| Tema | Houzez | Tema de real estate. Tiene su propio header/footer builder, sidebar, breadcrumbs. **Es la fuente principal de conflictos con Elementor.** |
| Page builder | Elementor Pro | Theme Builder activo, Custom Fonts cargadas (Helvetica Now Display/Text) |
| Slider | Slider Revolution 6.7.41 | Ya instalado, uso a definir |
| Forms | Houzez Elementor Contact Form | Form propio del tema, integrado con Elementor |

## URLs clave

- **Sitio staging:** https://papayawhip-fly-823460.hostingersite.com/
- **WP admin:** https://papayawhip-fly-823460.hostingersite.com/wp-admin/
- **Editor Elementor de una página:** `/wp-admin/post.php?post={ID}&action=elementor`
- **Preview público de página:** `/?page_id={ID}&preview=true`
- **Theme Builder (lista):** `/wp-admin/edit.php?post_type=elementor_library&tabs_group=theme`

## MCP de Elementor

Servidor MCP llamado `elementor-mcp` configurado en el cliente Claude del usuario. Permite operar sobre WordPress desde Claude sin abrir el navegador.

### Tools disponibles

| Tool | Qué hace | Limitaciones |
|---|---|---|
| `get_page` | Trae JSON completo de una página (incluye `_elementor_data`) | Solo post type `page` |
| `get_page_id_by_slug` | Devuelve ID dado el slug | — |
| `create_page` | Crea una página nueva con elementor_data | Solo `page`, no templates |
| `update_page` | Actualiza una página existente | **Solo `page`. NO funciona en `elementor_library` (footers/headers del Theme Builder).** |
| `download_page_to_file` | Baja JSON a archivo local | Path puede fallar según el entorno del MCP |
| `update_page_from_file` | Sube JSON desde archivo local | Mismo problema de path |

### Lo que el MCP NO puede hacer

- ❌ Editar templates del Theme Builder (footer, header, single post, archive) — distinto post type
- ❌ Cambiar `page_template` (no expone el parámetro)
- ❌ Subir imágenes / media
- ❌ Crear posts (solo páginas)
- ❌ Tocar Houzez Theme Options
- ❌ Tocar settings globales de Elementor (Custom Fonts, Global Colors, etc.)

### Patrón de uso del MCP

```
1. tool_search(query="elementor get page") → cargar tools
2. get_page_id_by_slug(slug="tasaciones") → ID
3. get_page(pageId=ID) → trae estructura actual
4. Modificar el JSON localmente (en Claude)
5. update_page(pageId=ID, elementor_data=JSON) → escribe
```

## Estructura de datos de Elementor (mini-glosario)

```json
{
  "id": "abc123",                    // string, alfanumérico, único
  "elType": "container",             // container | widget | column | section
  "settings": {
    "container_type": "grid",        // grid | flex
    "grid_columns_grid": {...},      // si es grid
    "custom_css": "selector {...}",  // CSS local
    ...
  },
  "elements": [...]                  // hijos (recursivo)
}
```

- **Widgets más usados:** `heading`, `text-editor`, `image`, `icon-list`, `button`, `houzez_elementor_contact_form`
- **Selector mágico:** dentro de `custom_css`, la palabra `selector` se reemplaza por el ID del elemento.

## Limitaciones del entorno de Claude

- El MCP corre en un contenedor separado del file system de Claude → no se pueden usar paths absolutos compartidos entre `bash_tool` y `update_page_from_file`. **Siempre pasar el JSON inline en `update_page`.**
- El JSON debe ir como string en el parámetro `elementor_data`. Cuidado con escapes de comillas en `custom_css`.

## Tema Houzez — qué hay que saber

- Houzez tiene **su propio sistema de templates** que se monta encima de WordPress.
- El template "elementor_header_footer" en una página WP **NO elimina el header/footer del tema completamente** — sigue habiendo wrappers.
- Para full-bleed real hay que usar **Page Layout: Elementor Canvas** (settings de la página, no del template).
- Houzez tiene su propio **footer builder en Theme Options** que es independiente del Elementor Theme Builder. A veces conviven, a veces se pisan.

## Header/Footer del sitio actual

### Header — confirmado en Elementor Theme Builder

**Estado:** verificado el 22 de mayo de 2026 inspeccionando WP-Admin → Templates → Theme Builder.

| Template | Tipo | Display Rules | Estado |
|---|---|---|---|
| `Header Principal` | Header | Entire Site | Published |
| `Elementor #5791` | (sin tipo) | — | Draft (descartar / borrar después) |

- El header del sitio entero está hecho con **Elementor Theme Builder**, NO con Houzez Theme Options.
- Shortcode interno (visible en Theme Builder): `[fts_template id='60']`.
- El menú visible arriba (Propiedades / Investigación / Radar / FAi / Compañía / Blog / Contacto) sale de este template `Header Principal`.

### Footer — debe ir por Elementor Theme Builder, para consistencia con el header

**Estado:** no hay ningún template tipo Footer activo en el Theme Builder todavía.

Decisión derivada del hallazgo del header:
- El footer va a ser un template nuevo del Theme Builder.
- Construir el footer primero en la página staging post 6704 (`page` type, donde el MCP de Elementor sí puede escribir).
- Cuando esté validado, copiar el container raíz al template del Theme Builder y asignarle condición "Entire Site".
- **No usar** Houzez Footer Builder (Theme Options) para mantener consistencia con el header.
