# Elementor Exports

Snapshots de páginas en JSON. Usar como backup y referencia.

## Archivos

| Archivo | ID | Página | Fecha | Estado |
|---|---|---|---|---|
| `6081-tasaciones.json` | 6081 | /tasaciones | — | Fuente de verdad del sistema de diseño |
| `6704-footer-staging.json` | 6704 | Footer Staging FAP | — | Footer construido, pendiente pasarlo al Theme Builder |
| `5706-home-snapshot-2026-05-27.json` | 5706 | Homepage | 2026-05-27 | Snapshot de seguridad pre-trabajo |

## Cómo usar

Antes de hacer `update_page` sobre cualquier página, hacer `get_page` y guardar el JSON acá como snapshot. Formato de nombre: `{ID}-{slug}-snapshot-{fecha}.json`.

## Nota sobre el home (5706)

La home tiene 20 containers (58KB de elementor_data). Contiene:
- Container `8474a88`: accordion hero (widget HTML custom con CSS inline)
- Section `c1d7965`: search builder con imagen de fondo
- Section `5811ff4`: property cards v5
- Container `9d86310`: "Decidir Bien" typography section
- Y más secciones de Houzez demo que están pendientes de reemplazar

**No tocar sin backup previo.**
