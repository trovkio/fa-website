# Problemas conocidos

Bugs, limitaciones y workarounds. Esta es la primera lectura obligatoria antes de tocar el sitio para evitar volver a chocarse con problemas ya identificados.

---

## 🔴 BLOQUEANTE NO RESUELTO — Footer Principal no renderiza en frontend

**Estado:** Pendiente de resolver. Sesión 2026-05-22 trabajamos varias horas sin éxito. Decisión: pasamos a construir las páginas y volvemos al footer después con otro approach.

**Setup que tenemos:**
- Post 6704 (`Footer Staging FAP`, post type `page`) tiene el JSON validado del footer (ver `snippets/elementor-json/footer-staging-6704.json`). Renderiza correctamente en el editor de Elementor.
- Post 6716 (`Footer Principal`, post type `fts_builder`) es el template del Theme Builder de Houzez/Elementor. Status: Published. Visibility: Public. Display Location: Entire Website. Type: Footer.
- El contenido del post 6716 fue copiado desde el post 6704 vía copy/paste manual entre tabs de Elementor.

**Síntoma:**
- En el editor de Elementor del post 6716, el footer se ve renderizado con su contenido (las 5 columnas + Contacto/Matrículas + legal).
- En frontend (ej. `/tasaciones` en incógnito), el footer NO aparece. Tampoco aparece el footer anterior de Houzez. Es como si no hubiera footer.
- Después del paste, los containers perdieron los CSS IDs custom (`ftmain02`, `ftcol01`, etc.) y la configuración de grid 6fr. Los hijos quedaron apilados verticalmente.

**Lo que se intentó (sin éxito):**
1. Copy/paste containers raíz uno por uno entre tabs → contenido pega pero grid se rompe.
2. Export como Template Kit (`fa-footer-template.json`) e Import vía Saved Templates → no resuelve.
3. CSS global apuntando a IDs originales (`#ftmain02`, etc.) → IDs no existen, no aplica.
4. Clear Elementor Cache (Files & Data) + Delete Cache de Houzez + hard refresh incógnito → footer sigue sin aparecer en frontend.
5. Verificar Display Conditions en Theme Builder → confirmado "Entire Site", Published.
6. Re-verificar Houzez Theme Options → Footer → tiene layouts predefinidos propios pero no opción para asignar template custom desde ahí.

**Hipótesis no probadas:**
- **Houzez Theme Options → Footer está activo y pisa el template `fts_builder` de Footer Principal.** Habría que desactivar el footer de Houzez desde Theme Options para que solo renderice el de Elementor.
- **CSS del template Footer Principal no se generó.** Posible regenerar manualmente vía Elementor → Tools → Replace URL o forzar un re-save del template.
- **El post 6716 tiene contenido en el editor pero `_elementor_data` está corrupto** (paste incompleto). Verificar el meta directamente vía phpMyAdmin o WP REST API.
- **Conflicto entre `fts_builder` (Houzez Theme Builder) y `elementor_library` (Elementor Theme Builder).** El theme tiene 2 sistemas de templates conviviendo. El template fue creado en `fts_builder` (post 6716, ver `02-arquitectura-tech.md`), pero quizás solo `elementor_library` se respeta en frontend.

**Próximo approach sugerido (cuando retomemos):**
- Usar Chrome DevTools → Inspect en frontend de `/tasaciones` para ver si el footer está en el DOM pero oculto vía CSS, o si directamente no está en el HTML.
- Si está oculto: ajustar CSS.
- Si no está en el HTML: el template `fts_builder` no se está llamando. Habría que ir a phpMyAdmin a verificar el `_elementor_data` del post 6716 y/o crear el footer en `elementor_library` (Theme Builder estándar de Elementor) en su lugar.

**El JSON validado del footer (post 6704) está guardado y reusable:**
- `snippets/elementor-json/footer-staging-6704.json`
- Doc en `snippets/elementor-json/footer-staging-6704.md`

---

## 🔴 CRÍTICO — Houzez wrapper rompe el layout de Elementor

**Síntoma:** Cuando abrís una página construida con Elementor en preview público, ves:
- Header del sitio normal ✅
- Breadcrumb "Home > [Título de página]" ⚠️ inyectado por Houzez
- Título grande de la página ⚠️ inyectado por Houzez
- El contenido Elementor aparece encajado en una caja ~1000px de ancho centrada ⚠️
- Sidebar con calendario, archivos, "March 2016" ⚠️ inyectado por Houzez en ciertos templates

**Causa:** Houzez tiene un sistema de templates que se monta encima de WordPress. El template "elementor_header_footer" aplicado a una página NO elimina los wrappers nativos del tema, solo el header/footer.

**Workaround conocido:**
- Cambiar **Page Layout** a **"Elementor Canvas"** desde Page Settings de Elementor (engranaje abajo izq.)
- Esto SÍ elimina header, footer, breadcrumb, título y sidebar de Houzez.
- Resultado: página totalmente vacía donde sólo se ve lo que dibuja Elementor.

**Limitación del workaround:**
- Canvas elimina TAMBIÉN el header del sitio. Sirve para páginas de staging/preview pero **no para páginas finales** que necesitan menú arriba.
- Para páginas finales hay que resolver el conflicto Houzez/Elementor de otra forma (a investigar).

**Hipótesis a probar (próxima sesión):**
- Que el header del sitio esté hecho con Elementor Theme Builder. Si es así, basta con Canvas + agregar el header como container al inicio de cada página.
- O resolver con CSS global que sobreescriba los wrappers de Houzez.

---

## 🟠 MEDIO — Copy/paste de containers entre tabs de Elementor pierde grid

**Síntoma:** Al copiar un container con `container_type: grid` y `grid_columns_grid` configurado desde una tab de Elementor y pegarlo en otra tab, los hijos pegan correctamente pero el container raíz pierde la configuración de grid 6fr. Los hijos quedan apilados verticalmente sin asignación de `grid-column`. Los CSS IDs custom también se pierden.

**Causa:** Bug de Elementor. El portapapeles pasa los widgets pero no algunos meta-settings del container.

**Workaround intentado:** Asignar IDs manualmente desde el panel Advanced de cada container. PERO: en Elementor 4.x el campo "CSS ID" no es visible por default en Grid containers, requiere activar opciones avanzadas.

**Workaround real:** Editar `_elementor_data` del post destino directamente (vía MCP si es `page`, o vía phpMyAdmin si es `fts_builder`/`elementor_library`).

---

## 🟠 MEDIO — MCP no edita templates del Theme Builder

**Síntoma:** `update_page(pageId=6706)` sobre un template footer del Theme Builder devuelve error.

**Causa:** Los templates del Theme Builder son post type `elementor_library` o `fts_builder`, no `page`. El MCP solo opera sobre `page`.

**Workaround:**
1. Construir el footer en una página staging (post type `page`) → 6704
2. Abrir el editor de Elementor del template footer (post 6716)
3. Abrir el editor de Elementor de la página staging en otra pestaña
4. En la staging: click derecho sobre el container raíz del footer → **Copy**
5. En el template: click derecho en el área vacía → **Paste**
6. Save

**Limitación del workaround:** Ver "Copy/paste pierde grid" arriba. En la práctica, el copy/paste no es confiable. Para escritura directa hay que ir a phpMyAdmin.

---

## 🟠 MEDIO — `download_page_to_file` y `update_page_from_file` fallan con paths locales

**Síntoma:** Estos tools devuelven `ENOENT: no such file or directory` aunque el archivo exista en `/home/claude/`.

**Causa:** El MCP corre en un contenedor distinto al filesystem de Claude. Los paths no son compartidos.

**Workaround:**
- Siempre usar `update_page` con el JSON inline en el parámetro `elementor_data`
- Para "bajar" una página, usar `get_page` y procesar el JSON en memoria
- Evitar los tools de file

---

## 🟡 BAJO — Font Helvetica Now no siempre carga en preview

**Síntoma:** A veces el editor renderiza con fallback (Roboto/system font).

**Causa probable:** Cache del navegador, o Custom Fonts no propagadas, o el CSS de Elementor todavía no se regeneró.

**Workaround:**
- Hard refresh (Cmd+Shift+R)
- Verificar que el plugin "Delete Cache" del admin bar haya corrido
- Si persiste, ir a Elementor → Tools → **Clear Files & Data** (no se llama "Regenerate CSS" en Elementor 4.x)

---

## 🟡 BAJO — IDs de Elementor con guiones bajos al inicio

**Síntoma:** Algunos parsers se confunden con IDs como `_logo01`.

**Convención:** IDs alfanuméricos, sin guion bajo al inicio. Preferir `ftlogo01` a `_logo_01`.

---

## 🟡 BAJO — Caracteres especiales en custom_css

**Síntoma:** Cuando un `custom_css` tiene comillas dobles, JSON.stringify puede romper el escape.

**Workaround:** Usar comillas simples dentro de los selectores cuando sea posible. Para HTML embebido en widgets `text-editor`, escapar manualmente.

---

## ⚪ INFO — Slider Revolution presente pero no usado

El sitio tiene Slider Revolution 6.7.41 instalado (viene con Houzez). **No usar** salvo necesidad muy específica. Preferir construir cualquier slider con containers Elementor o widgets nativos.

---

## ⚪ INFO — Múltiples "Footer" en la instalación

Hay al menos 4 entidades relacionadas a footer:
- Post 6700 — "footer" original, estado dudoso, posible candidato a borrar
- Post 6704 — "Footer Staging FAP", página de trabajo (post type `page`). Contiene el JSON validado.
- Post 6706 — "Elementor Footer", template del Theme Builder antiguo (`elementor_library`)
- Post 6716 — "Footer Principal", template actual del Theme Builder de Houzez (`fts_builder`). NO RENDERIZA EN FRONTEND. Ver bloqueante arriba.

---

## Convenciones para reportar nuevos problemas

Al detectar un problema nuevo, agregarlo acá con:
- **Severidad:** 🔴 CRÍTICO / 🟠 MEDIO / 🟡 BAJO / ⚪ INFO
- **Síntoma:** qué se ve
- **Causa:** qué lo provoca (hipótesis si no se confirmó)
- **Workaround:** cómo se resuelve hoy
- **Pendiente:** qué falta investigar
