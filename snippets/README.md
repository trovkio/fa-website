# Snippets vault

Este directorio guarda **todo el código validado** del proyecto FA Website: CSS de Elementor, JSON exports, snippets HTML, configuraciones varias. Se versiona junto con los docs.

Ver `docs/00-reglas-de-trabajo.md` regla R2 para el flujo de entrada al vault.

## Estructura

```
snippets/
├── README.md           Este archivo
├── INDEX.md            Índice cronológico y por componente de todo lo validado
├── css/                Bloques de CSS custom de Elementor
├── elementor-json/     JSON exports completos de páginas o secciones de Elementor
└── html/               Snippets HTML embebibles (poco frecuente, ej: HTML widgets)
```

## Convenciones

### Naming

- Archivos en minúsculas, separados con guion medio: `footer-staging-6704.json`, `grilla-guia-decorativa.css`.
- Prefijar con sección/componente cuando aplique: `footer-`, `tasaciones-`, `header-`.
- Para JSON de páginas: incluir el ID del post WP: `footer-staging-6704.json`, no solo `footer.json`.

### Encabezado obligatorio en cada archivo

**CSS:**
```css
/*
 * Componente: [nombre del componente]
 * Origen: [página/template donde se usa, ID WP]
 * Validado: YYYY-MM-DD
 * Dependencias: [tipografías, otros CSS, etc.]
 * Notas: [contexto breve]
 */
```

**JSON:**
No se puede comentar en JSON puro. Se documenta en el INDEX y, si hace falta más, en un `.md` hermano con el mismo nombre base (`footer-staging-6704.md`).

### Cuándo entra al vault

Solo cuando el usuario valida explícitamente el código (mensaje tipo "ok, está bueno, guardalo" o "validado, dale"). No antes.

### Cuándo se actualiza un archivo del vault

Cuando hay un cambio funcional al código ya validado:
1. Se reemplaza el archivo entero (R1).
2. Se agrega entrada al INDEX con la fecha y el motivo del cambio.
3. El commit message explicita: `snippets(footer): refactor de grilla a 5 columnas`.

## Cómo usar el vault desde Claude

Al inicio de un chat nuevo:

> Leé `snippets/INDEX.md` para ver qué código validado hay disponible.
> Si vas a tocar el footer, partí de `snippets/elementor-json/footer-staging-6704.json`.

Al cerrar un chat con código validado:

> Agregá los snippets validados de esta sesión al vault.
> Actualizá `snippets/INDEX.md`.
