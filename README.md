# FA Website

Repositorio de contexto, decisiones y assets técnicos del sitio de **Fabián Achával Propiedades** (FA).

## Para qué sirve este repo

Este repo existe para que cualquier persona (humana o IA, especialmente Claude) que retome el proyecto pueda entender en minutos:

- Cómo está construido el sitio (stack, integraciones, MCP).
- Qué decisiones de diseño y arquitectura se tomaron y por qué.
- Qué páginas existen, sus IDs, URLs, y estado.
- Qué problemas conocidos hay y sus workarounds.
- Qué falta hacer y con qué prioridad.

## Cómo usarlo con Claude

Al iniciar un chat nuevo de Claude vinculado a este repo (vía MCP de GitHub o copiando el contenido al Project Knowledge), arrancá con:

> Leé este repo (trovkio/fa-website) antes de hacer nada. En particular: `CONTEXTO.md`, `docs/01-sistema-diseno.md` y `docs/05-problemas-conocidos.md`. Decime qué entendiste antes de avanzar.

Ver `prompts/kickoff-chat.md` para prompts pre-armados.

## Estructura

```
fa-website/
├── README.md                       Este archivo
├── CONTEXTO.md                     Resumen ejecutivo (entrada principal)
├── docs/
│   ├── 01-sistema-diseno.md       Grilla, tipografía, colores, tokens
│   ├── 02-arquitectura-tech.md    WP + Houzez + Elementor + MCP
│   ├── 03-estructura-sitio.md     Mapa de páginas, IDs, URLs
│   ├── 04-decisiones.md           Qué se decidió y por qué
│   ├── 05-problemas-conocidos.md  Bugs, limitaciones, workarounds
│   ├── 06-proximos-pasos.md       Roadmap actualizable
│   ├── 07-branding-voz.md         Voz editorial, propuesta FA
│   └── 08-briefs-paginas.md       Briefs de páginas pendientes
├── elementor-exports/             JSON de páginas Elementor (snapshots)
└── prompts/
    └── kickoff-chat.md            Prompts para iniciar chats nuevos
```

## Mantenimiento

Cada vez que se cierra una sesión de trabajo importante, pedirle a Claude:

> Actualizá los docs del repo con lo que avanzamos hoy. En particular `06-proximos-pasos.md` y `03-estructura-sitio.md` si cambiaron páginas.

Hacer commit con mensaje descriptivo.
