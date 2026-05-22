# Problemas conocidos

Bugs, limitaciones y workarounds. Esta es la primera lectura obligatoria antes de tocar el sitio para evitar volver a chocarse con problemas ya identificados.

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

**Avance del 22 de mayo de 2026 (estado actualizado):**
- Verificado que el header del sitio está hecho con Elementor Theme Builder (template `Header Principal`, condición `Entire Site`).
- El footer va a ir por el mismo camino: nuevo template del Theme Builder.
- Para construirlo, se trabaja primero en la página staging 6704 (post type `page`, accesible por el MCP) y después se copia al template.
- Sigue pendiente entender si páginas finales con Page Layout normal (no Canvas) pueden coexistir bien con el header del Theme Builder + el footer nuevo, sin que Houzez inyecte breadcrumbs/sidebar.

---

## 🟠 MEDIO — MCP no edita templates del Theme Builder

**Síntoma:** `update_page(pageId=6706)` sobre un template footer del Theme Builder devuelve error.

**Causa:** Los templates del Theme Builder son post type `elementor_library`, no `page`. El MCP solo opera sobre `page`.

**Workaround:**
1. Construir el footer en una página staging (post type `page`) → 6704
2. Abrir el editor de Elementor del template footer (post 6706, o uno nuevo)
3. Abrir el editor de Elementor de la página staging en otra pestaña
4. En la staging: click derecho sobre el container raíz del footer → **Copy**
5. En el template: click derecho en el área vacía → **Paste**
6. Save

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
- Si persiste, ir a Elementor → Tools → Regenerate CSS

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

Hay al menos 3 entidades relacionadas a footer:
- Post 6700 — "footer" original, estado dudoso, posible candidato a borrar.
- Post 6704 — "Footer Staging FAP", página de trabajo.
- Post 6706 — "Elementor Footer", supuesto template del Theme Builder. Estado a verificar: el listado del Theme Builder al 22/05/2026 NO muestra un footer activo, lo que sugiere que 6706 o no existe ya o está vacío / no asignado.

Antes de hacer cualquier cosa con el footer, verificar el estado de los 3 y consolidar si es necesario.

---

## ⚪ INFO — `Elementor #5791` (draft viejo en Theme Builder)

En el listado del Theme Builder hay un template `Elementor #5791` en estado Draft, sin tipo asignado, modificado por última vez el 1 de abril de 2026. No tiene Display Rules. Probable candidato a borrar después de verificar que no contiene nada útil.

---

## Convenciones para reportar nuevos problemas

Al detectar un problema nuevo, agregarlo acá con:
- **Severidad:** 🔴 CRÍTICO / 🟠 MEDIO / 🟡 BAJO / ⚪ INFO
- **Síntoma:** qué se ve
- **Causa:** qué lo provoca (hipótesis si no se confirmó)
- **Workaround:** cómo se resuelve hoy
- **Pendiente:** qué falta investigar
