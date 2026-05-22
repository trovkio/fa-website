# CONTEXTO — FA Website

**Última actualización:** 22 de mayo de 2026
**Cliente:** Fabián Achával Propiedades (FA / FAP)
**Stack:** WordPress + Houzez Theme + Elementor Pro + MCP (Elementor)
**URL staging:** https://papayawhip-fly-823460.hostingersite.com/

---

## TL;DR

Estamos construyendo el nuevo sitio web de **Fabián Achával Propiedades**, una inmobiliaria argentina de alta gama que se posiciona como autoridad editorial del sector (información, inteligencia, ejecución). La referencia visual y conceptual es **Criterion Global** (criterionglobal.com): sobrio, tipográfico, mucho aire, grilla de 6 columnas, sistema de diseño riguroso.

Trabajamos sobre un sitio existente en **Hostinger + WordPress + tema Houzez**, modificando páginas con **Elementor Pro** vía **MCP de Elementor** (servidor `elementor-mcp` que permite leer/escribir páginas de WordPress desde Claude).

## Reglas de trabajo (leer SIEMPRE primero)

Ver `docs/00-reglas-de-trabajo.md`. Resumen:

- **R1:** todo código se entrega **completo**, nunca en fragmentos parcheados.
- **R2:** todo código validado se guarda en `/snippets/` y se indexa en `/snippets/INDEX.md`.

## Estado actual (snapshot)

- ✅ **Página Tasaciones** (post 6081, slug `/tasaciones`): completa, sirve como referencia del sistema de diseño.
- 🟡 **Mega menú / Header**: armado en sesiones anteriores, funcional.
- 🟡 **Footer**: en construcción. Hay una página staging (post 6704 "Footer Staging FAP") y un template footer del Theme Builder (post 6706 "Elementor Footer").
- ❌ **Resto de páginas**: Residencial, Emprendimientos, Comercial, Radar Inmobiliario, FAP Intelligence, Blog, Preguntas, Nosotros, Contacto, Carreras → pendientes.

## Problema crítico activo

**Houzez impone un wrapper de tema sobre las páginas Elementor**, generando un container angosto (~1000px) con breadcrumb, título y sidebar inyectados. Esto rompe el diseño full-bleed que requiere el sistema.

**Workaround actual:** cambiar Page Layout a "Elementor Canvas" en Page Settings de cada página. Pero **no resuelve** para el footer del Theme Builder, que igual hereda el wrapper en ciertas vistas.

**Próximo intento:** evaluar si el header del sitio se hizo con Elementor Theme Builder o con Houzez Theme Options, para decidir el camino del footer.

Ver detalle completo en `docs/05-problemas-conocidos.md`.

## Sistema de diseño en una línea

Container grid de 6 columnas (fr), `max-width: 1400px` centrado, tipografía **Helvetica Now Display** para títulos / **Helvetica Now Text** para body, peso 500 dominante, color negro sobre blanco, grilla guía visible con `repeating-linear-gradient`.

Detalle completo en `docs/01-sistema-diseno.md`.

## Cómo seguir

1. **Antes de tocar nada**, leer en este orden:
   - `docs/00-reglas-de-trabajo.md` (cómo se trabaja)
   - `docs/01-sistema-diseno.md` (qué tipografía, qué grilla, qué tokens)
   - `docs/02-arquitectura-tech.md` (cómo está el stack, qué hace el MCP)
   - `docs/05-problemas-conocidos.md` (qué NO funciona y por qué)
   - `docs/06-proximos-pasos.md` (qué hay que hacer ahora)
   - `snippets/INDEX.md` (qué código validado existe disponible)

2. **Para retomar el trabajo del footer específicamente**, mirar también `docs/03-estructura-sitio.md` sección "Footer".

3. **Para construir páginas nuevas**, usar como referencia `elementor-exports/6081-tasaciones.json` (es el JSON completo del Elementor de la página Tasaciones).

## Decisiones grandes ya tomadas (no re-debatir sin motivo)

- Sistema de diseño: copiar la arquitectura de la página Tasaciones (no inventar nuevo).
- Footer columnas: Propiedades / Plataforma / Preguntas / Compañía / Social + logo + fila legal con matrículas CUCICBA 6576 y CMCPSI 6385.
- Voz editorial: FA tiene propuesta editorial fuerte (información, inteligencia, ejecución), no es una inmobiliaria genérica.
- MCP de Elementor solo escribe en post type `page`, **no** en `elementor_library` (templates del Theme Builder). Footers/headers de Theme Builder hay que tocarlos manualmente o vía workaround.

Ver detalle en `docs/04-decisiones.md`.

## Contacto técnico

- Acceso WP admin: vía login del cliente (no en repo por seguridad)
- MCP server activo: `elementor-mcp` + `github` (ambos locales, configurados en `claude_desktop_config.json` del usuario)
- Repositorio: este mismo
- Flujo de commits con Claude: **directo al repo vía MCP de GitHub local** (PAT con scope `fa-website`). Branches + PR para cambios no triviales.
