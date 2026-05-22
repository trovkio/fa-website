# Exports Elementor

Los snapshots JSON de páginas Elementor van acá. Sirven como referencia del sistema y backup.

## Cómo regenerar un export

En un chat de Claude con MCP de Elementor conectado:

```
1. tool_search(query="get page")
2. get_page(pageId=XXXX) → trae JSON completo
3. Guardar el campo `meta._elementor_data` (es un string JSON) parseado en `XXXX-{slug}.json`
```

## Archivos esperados

| Archivo | Página | Estado |
|---|---|---|
| `6081-tasaciones.json` | /tasaciones | Fuente de verdad del sistema de diseño |
| `6704-footer-staging.json` | /footer-staging-fap | Trabajo en progreso del footer |
| `6706-elementor-footer.json` | Template Theme Builder | Vacío al 2026-05-21 |

## ¿Por qué no están todos commiteados?

Los JSON de Elementor son grandes (40-100KB cada uno) y cambian frecuentemente durante desarrollo. Para no inflar el repo:

- Solo se commitea el JSON cuando hay un cambio estructural significativo.
- Los snapshots intermedios viven en memoria del chat de Claude.
- Para una sesión de trabajo, traer el JSON en vivo con `get_page(ID)`.

## Convención de naming

`{POST_ID}-{slug-corto}.json` — siempre el post ID primero, después el slug del WP.
