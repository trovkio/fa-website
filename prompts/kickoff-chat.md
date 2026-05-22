# Prompts para iniciar chats nuevos

Plantillas listas para copiar/pegar al inicio de un chat de Claude vinculado a este repo.

---

## 🎯 Prompt de kickoff genérico (recomendado)

```
Estoy trabajando en el sitio web de Fabián Achával Propiedades (FA).
Todo el contexto está en el repo de GitHub `trovkio/fa-website`.

Antes de hacer cualquier cosa, leé en este orden:
1. CONTEXTO.md (entrada)
2. docs/01-sistema-diseno.md
3. docs/02-arquitectura-tech.md
4. docs/03-estructura-sitio.md
5. docs/05-problemas-conocidos.md
6. docs/06-proximos-pasos.md

Después decime en 3 bullets: (a) en qué estábamos, (b) qué problema crítico
hay abierto, (c) qué proponés hacer hoy.

Después esperá que te diga en qué quiero enfocarme.
```

---

## 🔧 Prompt para retomar el footer específicamente

```
Necesito terminar el footer del sitio de FA. Leé:
- CONTEXTO.md
- docs/03-estructura-sitio.md (sección Footer)
- docs/05-problemas-conocidos.md (el wrapper Houzez es crítico)
- elementor-exports/6081-tasaciones.json (referencia del sistema)

Resumime el estado actual del footer en 5 líneas y proponé el próximo paso
concreto. No empieces a tocar Elementor hasta que yo confirme.
```

---

## 🆕 Prompt para crear una página nueva

```
Voy a crear la página [/slug-de-la-página] de FA. Leé:
- CONTEXTO.md
- docs/01-sistema-diseno.md
- docs/07-branding-voz.md
- docs/08-briefs-paginas.md (buscá el brief de esta página)
- elementor-exports/6081-tasaciones.json (úsala como template estructural)

Después armá un plan de la página en 5-7 secciones (containers) replicando
el sistema de /tasaciones. No escribas JSON todavía, solo el plan.
Esperá mi aprobación antes de construir.
```

---

## 🔄 Prompt para cerrar sesión y actualizar docs

```
Cerramos la sesión de hoy. Actualizá los siguientes docs del repo con lo
que avanzamos:
- docs/06-proximos-pasos.md (changelog + tareas completadas/nuevas)
- docs/03-estructura-sitio.md (si cambió alguna página, ID o URL)
- docs/04-decisiones.md (si tomamos decisiones nuevas, agregalas con fecha)
- docs/05-problemas-conocidos.md (si encontramos bugs nuevos)
- CONTEXTO.md (sección "Estado actual" si cambió el estado general)

Devolveme los archivos modificados para hacer commit.
```

---

## 🐛 Prompt para reportar un nuevo bug

```
Encontré un problema nuevo:

Síntoma: [descripción]
Páginas/IDs afectados: [...]
Qué intenté: [...]

Leé docs/05-problemas-conocidos.md para chequear si ya está documentado,
diagnosticá la causa, proponé un workaround, y agregalo al doc.
```

---

## ⚙️ Prompt para conectar el MCP de GitHub

Una vez que tengas el MCP de GitHub configurado en Claude:

```
Conectate al repo trovkio/fa-website vía el MCP de GitHub.
Listame los archivos del repo y leé CONTEXTO.md como entrada.
```

Si todavía no tenés el MCP configurado, copiá manualmente los .md
relevantes al Project Knowledge del proyecto en Claude.
