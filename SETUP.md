# Setup del repo en GitHub

Pasos para inicializar el repo `fa-website` en GitHub y conectarlo con Claude.

## 1. Crear el repo en GitHub

```bash
# Opción A: vía web
# Ir a https://github.com/new
# Repo name: fa-website
# Privado (recomendado)
# Sin README, sin .gitignore, sin license (porque ya tenemos los archivos)
```

## 2. Inicializar git localmente y subir

```bash
# Después de descargar/descomprimir el repo en tu computadora:
cd fa-website
git init
git add .
git commit -m "Initial commit: contexto, docs, briefs, prompts"
git branch -M main
git remote add origin git@github.com:trovkio/fa-website.git
git push -u origin main
```

Si no tenés SSH configurado, usá la URL HTTPS:
```bash
git remote add origin https://github.com/trovkio/fa-website.git
```

## 3. Conectar con Claude (3 opciones)

### Opción A — MCP de GitHub (más serio)

1. En Claude (web o desktop), ir a **Settings → Connectors**
2. Buscar "GitHub" en la lista de connectors disponibles
3. Conectar tu cuenta de GitHub
4. Una vez conectado, en cualquier chat podés pedir:
   > "Leé el repo `trovkio/fa-website` y resumime el estado del proyecto"

### Opción B — Project Knowledge (más simple)

1. En claude.ai, abrir el Project actual (donde estás trabajando este proyecto)
2. En el panel izquierdo, buscar **"Project knowledge"**
3. Subir todos los archivos `.md` del repo a Project knowledge:
   - `CONTEXTO.md`
   - `README.md`
   - Todos los `docs/*.md`
   - `prompts/kickoff-chat.md`
4. Claude leerá estos archivos en CADA chat nuevo del Project, automáticamente.

### Opción C — Copy/paste manual (sin setup)

Al iniciar un chat nuevo, copiá el contenido de `CONTEXTO.md` y pegalo como primer mensaje. Funciona pero es lo menos eficiente.

## 4. Mantenimiento

Cada vez que termines una sesión de trabajo:

```
[En Claude]
> Actualizá los docs del repo con lo que avanzamos hoy.
> En particular docs/06-proximos-pasos.md y docs/03-estructura-sitio.md.
> Devolveme los archivos modificados.

[En tu terminal]
cd fa-website
# Actualizar los archivos modificados
git add .
git commit -m "Sesión 2026-MM-DD: [resumen corto]"
git push
```

## 5. Si querés que Claude haga commits por vos

El MCP de GitHub permite a Claude leer y escribir directamente en el repo. Si lo activás, podés decir:

> "Actualizá los docs del repo, hacé commit con mensaje 'Sesión 2026-05-22' y push."

Y Claude lo hace solo. Cuidado con dar acceso write si el repo tiene cosas sensibles.

## Notas de seguridad

- **No incluir credenciales en el repo**: el repo no tiene passwords ni API keys. El acceso al WP admin sigue siendo manual del cliente.
- **Repo privado**: aunque no hay secretos, hay URLs internas de staging y decisiones de cliente. Mejor privado.
- **No commitear** el archivo de Project Knowledge con info confidencial específica del cliente si lo expandís.
