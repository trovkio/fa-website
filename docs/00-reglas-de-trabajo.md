# Reglas de trabajo

Reglas operativas para cualquier persona (humana o IA) que trabaje en este proyecto. **No negociables sin acuerdo explícito**. Si una regla nueva se acepta, agregarla acá con fecha.

---

## R1 — Código completo, nunca fragmentos

Cuando se entrega código (CSS, JSON, HTML, JS, SQL, lo que sea), siempre se entrega **el archivo completo** o **el bloque entero auto-contenido**, listo para copiar/pegar y usar.

**Esto significa:**
- Nunca entregar diffs sueltos del tipo "agregale esto al final del CSS de la página".
- Nunca decir "y entonces modificá la línea 47 por...".
- Si la modificación es chica, igual se devuelve el bloque entero del componente / sección / archivo, marcando qué cambió en un comentario aparte.
- Si la modificación es grande, se entrega el archivo entero.

**Por qué:** sesiones largas con código fragmentado terminan en archivos rotos por copy/paste inconsistente. El costo de re-entregar el archivo completo es 0 para Claude; el costo de debuggear un mal merge manual es muy alto para humanos.

**Cómo se aplica en práctica:**
- Para CSS de Elementor (custom CSS de un widget o container), se devuelve el bloque CSS completo de ese elemento.
- Para JSON de Elementor (un container y sus hijos), se devuelve la rama entera, no fragmentos parchados.
- Para docs `.md` del repo, se devuelve el archivo entero.

---

## R2 — Snippets vault: todo código validado se versiona

Hay un directorio `/snippets/` en el repo donde se guarda **todo el código validado** (CSS, JSON, snippets HTML, etc.), organizado por componente.

**Flujo:**
1. Claude genera el código en el chat (R1: completo).
2. El usuario lo prueba en WP / Elementor.
3. Si funciona y el usuario lo valida explícitamente, Claude lo guarda en `/snippets/{componente}/{nombre}.{ext}`.
4. Se agrega entrada al índice `/snippets/INDEX.md` con: nombre, fecha de validación, qué hace, dónde se usa, link al chat / sesión donde se gestó (opcional).
5. Si el código se modifica después, se actualiza el archivo en `/snippets/` y se agrega nota en el INDEX.

**Por qué:**
- Recuperar código validado sin tener que abrir chats viejos.
- Tener historial git de cambios al código real, no solo a los docs.
- Reutilizar componentes entre páginas sin re-pedirlos.

**Qué NO va al vault:**
- Código que todavía no se validó.
- Experimentos.
- Snippets fugaces (un fix de 2 líneas en consola).

**Estructura propuesta del vault:**
```
snippets/
├── INDEX.md
├── README.md                       Cómo está organizado el vault
├── css/
│   ├── grilla-guia-decorativa.css
│   └── ...
├── elementor-json/
│   ├── footer-staging-6704.json
│   └── ...
└── html/
    └── ...
```

---

## Histórico de reglas

- **2026-05-22** — Creación del doc con R1 y R2.
