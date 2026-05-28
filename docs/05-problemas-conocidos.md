# Problemas conocidos

Bugs, limitaciones y workarounds. Primera lectura obligatoria antes de tocar el sitio.

---

## 🔴 CRÍTICO — update_page sobre página publicada puede borrar todo el contenido

**Síntoma:** Se intenta subir un JSON grande via `update_page`. El MCP falla y el contenido queda vacío o corrupto. Ocurrió en la home al intentar construir un accordion.

**Reglas de seguridad (NO negociables):**
1. Nunca usar `update_page_from_file` — el MCP no comparte filesystem con bash_tool
2. Nunca hacer `update_page` en páginas publicadas sin backup previo en GitHub
3. Antes de cualquier `update_page`, hacer `get_page` y commitear el JSON al repo
4. Trabajar siempre en staging (draft) primero
5. Si el JSON falla al subir, NO reintentar con variaciones hasta entender qué salió mal
6. La home tiene contenido valioso — backup obligatorio antes de tocarla

---

## 🔴 CRÍTICO — Los selectores globales de Houzez no existen en esta instalación

**Confirmado 2026-05-28:** Los siguientes selectores NO existen en el DOM:
- `#page` → no existe
- `.site-main` → no existe
- `#content` → no existe
- `.elementor-section-wrap` → no existe

**Los wrappers reales son:**
- `.main-wrap` → wrapper principal de Houzez
- `.main-wrap > .elementor` → wrapper de Elementor por página (ej: `.elementor-5706` para la home)

**Consecuencia:** Todas las reglas CSS globales de ancho/padding deben apuntar a `.main-wrap > .elementor`, no a `#page` o `.elementor-section-wrap`.

---

## 🔴 CRÍTICO — Sistema full-bleed resuelto con clase helper

**Problema anterior:** Usar `width: 100vw` + `margin-left` negativo en Custom CSS del container causaba corrimiento de toda la página.

**Solución confirmada (2026-05-28):**
1. El CSS global en Houzez define `.fap-full-bleed` con el margin negativo correcto
2. El wrapper `.main-wrap > .elementor` tiene `overflow-x: hidden` que contiene el desborde
3. En el container de Elementor: **Advanced → Attributes → CSS Classes** → escribir `fap-full-bleed`
4. El Custom CSS del container queda vacío

**IMPORTANTE:** La clase va en **CSS Classes** (Attributes), NO en Custom CSS.

**Para el padding interno del container full-bleed:** poner todos los paddings en 0 desde Layout → Padding en el panel de Elementor.

---

## 🔴 CRÍTICO — Houzez wrapper rompe el layout de Elementor

**Síntoma:** Páginas con breadcrumb, título y sidebar inyectados por Houzez.

**Workaround:** Page Layout: Elementor Canvas en las páginas de staging.

---

## 🟠 MEDIO — MCP no edita templates del Theme Builder

**Síntoma:** `update_page(pageId=6706)` devuelve error.

**Causa:** Los templates son post type `elementor_library`, no `page`.

**Workaround:** Construir en staging (6704), copiar manualmente al template (6706).

---

## 🟠 MEDIO — download_page_to_file y update_page_from_file fallan

**Causa:** El MCP corre en contenedor distinto al filesystem de Claude.

**Workaround:** Siempre usar `update_page` con JSON inline. Nunca los tools de file.

---

## ⚪ INFO — Header del sitio: Houzez con CSS override, NO Elementor Theme Builder

El header es el header nativo de Houzez (`#header-hz-elementor`), domado con CSS:
- Container interno ID: `elementor-element-2757625` → max-width 1400px centrado
- Sticky: fondo blanco translúcido con blur al hacer scroll
- Menú: Max Mega Menu plugin sobre menú WP "Header FA"

---

## ⚪ INFO — Múltiples "Footer" en la instalación

- Post 6700 — footer original, desactivado (quitada condición "Entire Site")
- Post 6704 — Footer Staging FAP, página de trabajo con JSON validado
- Post 6706 — Elementor Footer, template Theme Builder, condición "Entire Site" activa

---

## ⚪ INFO — Reglas de trabajo con CSS (no negociables)

1. **Siempre pasar el código completo** del bloque CSS que se modifica, con contexto
2. **Nunca dar fragmentos** para parchear — el usuario no es developer
3. **Verificar en el DOM** antes de aplicar selectores nuevos — muchos selectores de Houzez no existen
4. **Usar el browser inspector** cuando algo no funciona — no seguir probando a ciegas
