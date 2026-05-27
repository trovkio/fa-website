# Problemas conocidos

Bugs, limitaciones y workarounds. Esta es la primera lectura obligatoria antes de tocar el sitio para evitar volver a chocarse con problemas ya identificados.

---

## 🔴 CRÍTICO — update_page sobre página publicada puede borrar todo el contenido

**Síntoma:** Se intenta subir un JSON grande via `update_page` (o `update_page_from_file`). El MCP falla en el proceso, y el contenido de la página queda vacío o corrupto. **Ocurrió en la home del sitio al intentar construir un accordion.**

**Causa confirmada:** El flujo fue:
1. Se intentó construir un accordion en la home
2. Se usó `update_page_from_file` que falla porque el MCP no comparte filesystem con `bash_tool`
3. Se intentaron múltiples workarounds pasando el JSON inline
4. El JSON estaba mal formado o incompleto en algún intento
5. `update_page` con datos incorrectos sobreescribió la página con contenido vacío/roto
6. La home quedó borrada

**Reglas de seguridad derivadas (NO negociables):**

1. **Nunca usar `update_page_from_file`** — el path del MCP y el de `bash_tool` son filesystems distintos, el archivo nunca llega. Siempre pasar el JSON inline en `elementor_data`.
2. **Nunca hacer `update_page` en páginas publicadas sin backup previo** del JSON completo guardado en GitHub (`elementor-exports/`).
3. **Antes de cualquier `update_page`, hacer `get_page` y commitear el JSON al repo** como snapshot de seguridad.
4. **Trabajar siempre en staging (draft) primero.** Recién publicar cuando el resultado está verificado visualmente.
5. **Si el JSON falla al subir, NO reintentar con variaciones** hasta entender qué salió mal. Cada intento fallido puede dejar la página en peor estado.
6. **La home tiene contenido valioso.** Antes de tocarla, backup obligatorio.

---

## 🔴 CRÍTICO — Escribir en cualquier página con MCP regenera el CSS global de Elementor

**Síntoma:** Al hacer `update_page` con un JSON grande (72KB+), Elementor regenera el CSS global del sitio. Esto puede romper estilos de widgets de Houzez (property cards, search builder, etc.) en todas las páginas.

**Causa confirmada (2026-05-22):** Cuando Elementor regenera el CSS, el archivo `post-9.css` (Kit global) se reescribe y algunos estilos de Houzez quedan fuera del nuevo archivo generado.

**Workaround confirmado:**
1. Si el CSS se rompe después de un `update_page`, ir al Kit predeterminado de Elementor (post 9) via el editor
2. Entrar a Custom CSS → agregar un salto de línea al final → Save Changes
3. Esto fuerza la regeneración completa del CSS global y restaura los estilos
4. URL directa: `wp-admin/post.php?post=9&action=elementor`

**Lección aprendida:** Antes de hacer `update_page` sobre cualquier página, tener claro el plan de rollback. Siempre tener el JSON original guardado.

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

---

## 🟠 MEDIO — MCP no edita templates del Theme Builder

**Síntoma:** `update_page(pageId=6706)` sobre un template footer del Theme Builder devuelve error.

**Causa:** Los templates del Theme Builder son post type `elementor_library`, no `page`. El MCP solo opera sobre `page`.

**Workaround:**
1. Construir el footer en una página staging (post type `page`) → 6704
2. Abrir el editor de Elementor del template footer (post 6706)
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

## 🟠 MEDIO — El MCP no puede pasar JSONs de más de ~30KB como parámetro inline sin errores de escape

**Síntoma:** `update_page(elementor_data=<json grande>)` falla con "not valid JSON string" cuando el JSON supera cierto tamaño o contiene muchos caracteres escapados.

**Causa:** Límites de encoding del parámetro string en el MCP.

**Workaround:**
- Para JSONs grandes, usar `ensure_ascii=True` al serializar con Python (convierte todos los caracteres especiales a `\uXXXX`)
- Aun así, JSONs de 70KB+ pueden fallar. En ese caso fragmentar el contenido o usar el browser con sesión de admin activa.

---

## 🟠 MEDIO — WPvivid Backup sin backups guardados

**Estado (2026-05-22):** El plugin WPvivid Backup está instalado pero el schedule estaba deshabilitado y no había ningún backup guardado.

**Acción recomendada:** Activar el schedule automático diario. Hacer un backup manual ahora como baseline.

**Ruta:** WP Admin → WPvivid Backup → Schedule → activar daily backup a Local Storage.

---

## 🟡 BAJO — Property cards más grandes de lo esperado en la home

**Síntoma (detectado 2026-05-22):** Las imágenes del widget `houzez_elementor_property-card-v5` en la home se ven más grandes que en la demo de Houzez (`demo05.houzez.co`). Las cards son 3 columnas correctas pero el widget ocupa el ancho completo del section (1496px) y las imágenes quedan más altas de lo deseado.

**Estado:** Parcialmente resuelto — el CSS global fue regenerado y las cards volvieron a 3 columnas. Falta afinar el ancho del container para que las cards sean más pequeñas.

**Pendiente próxima sesión:** Determinar el ancho exacto que tenían antes (comparar con demo05.houzez.co) y ajustar el selector CSS correcto.

---

## 🟡 BAJO — Font Helvetica Now no siempre carga en preview

**Síntoma:** A veces el editor renderiza con fallback (Roboto/system font).

**Causa probable:** Cache del navegador, o Custom Fonts no propagadas.

**Workaround:**
- Hard refresh (Cmd+Shift+R)
- Verificar que el plugin "Delete Cache" del admin bar haya corrido
- Si persiste, ir a Elementor → Tools → Clear Files & Data

---

## ⚪ INFO — Header del sitio: Houzez con CSS override, NO Elementor Theme Builder

**Confirmado (2026-05-27):** El header es el header nativo de Houzez (`#header-hz-elementor`), NO un template de Elementor Theme Builder. Está "domado" con CSS en Houzez Custom Code:
- `#header-hz-elementor .elementor-element-2757625` → container interno, max-width 1400px centrado
- `.elementor-sticky--active .e-con-inner` → fondo blanco translúcido con blur al hacer scroll
- El menú usa Max Mega Menu plugin sobre el menú WP "Header FA"

**Implicación para el footer:** el footer NO tiene que ir por Houzez Theme Options necesariamente — puede ir por Elementor Theme Builder. Pero la lógica del header sugiere que hay mezcla de sistemas. Verificar antes de decidir.

---

## ⚪ INFO — Múltiples "Footer" en la instalación

Hay al menos 3 entidades relacionadas a footer:
- Post 6700 — "footer" original, estado dudoso, posible candidato a borrar
- Post 6704 — "Footer Staging FAP", página de trabajo con JSON validado
- Post 6706 — "Elementor Footer", template Theme Builder, **vacío actualmente**

---

## ⚪ INFO — CSS Global del Kit (post-9) — estado actual

El Custom CSS del Kit predeterminado (post 9) contiene:
1. Fixes del footer grid (para cuando se resuelva el renderizado del footer)
2. Regla parcial para property cards: `.elementor-element-5811ff4 .property-cards-module { max-width: 960px }` — **no está funcionando correctamente**, pendiente ajuste
3. Regla para el search builder: `.elementor-element-c1d7965 .elementor-inner-section .elementor-container { max-width: 800px }` — **aplicada y funcionando**
