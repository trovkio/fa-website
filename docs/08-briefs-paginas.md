# Briefs de páginas pendientes

Briefs editoriales y estructurales de las páginas que faltan crear. Cada uno con: propósito, audiencia, estructura propuesta, copy de referencia, prioridad.

---

## Convención

Cada brief tiene la siguiente estructura:

- **Propósito:** qué hace esta página
- **Audiencia:** a quién le habla
- **Prioridad:** 🔴 alta / 🟠 media / 🟡 baja
- **Estructura propuesta:** secciones en orden vertical
- **Copy seed:** primeras frases o headlines tentativos
- **Referencias:** páginas similares en Criterion o en sitio actual

---

## 🔴 /nosotros

**Propósito:** Presentar quién es Fabián, qué es la compañía, qué la hace distinta. NO es un "about us" genérico — es la declaración editorial de FA.

**Audiencia:** clientes potenciales premium, brokers que se acercan a la compañía, prensa, talento.

**Prioridad:** 🔴 alta (link directo desde footer y header)

**Estructura propuesta:**

1. **Hero:** declarativo. *"Decidir bien."* o variación.
2. **Sección biografía Fabián** — años en el sector, hitos clave, no formato CV.
3. **La compañía hoy** — equipo, departamentos, capacidad operativa. Replicar tono de `/tasaciones`.
4. **Los 5 pilares** (Información / Inteligencia / Ejecución / Marketing / Productora) ya están en `/tasaciones`. Acá se profundizan.
5. **Equipo** — opcional. Si va, fotos con producción propia, no LinkedIn.
6. **Cierre:** "Decidir bien." con CTA a contacto.

**Copy seed:**
> Fabián Achával es la experiencia del sector inmobiliario.
> El conocimiento de los ciclos del mercado local, de los pormenores del negocio, de operaciones que se grabaron en la historia del real estate argentino.

(Ya está en `/tasaciones`, reutilizable y expansible.)

**Referencias:** Criterion `/about`, ó la sección que viene en mitad de `/tasaciones` ("Innovación de la Tradición").

---

## 🔴 /contacto

**Propósito:** Form de contacto + información de oficina. Conversión clara.

**Audiencia:** lead que ya decidió contactar.

**Prioridad:** 🔴 alta

**Estructura propuesta:**

1. **Header:** "Hablemos." o "Conversemos." (sobrio, no comercial)
2. **Form:** Nombre / Apellido / Email / Teléfono / Mensaje / Tipo de consulta (dropdown: tasación, compra, venta, otro)
3. **Datos de oficina:** dirección, teléfono, email, horarios
4. **Map opcional:** discreto, si se decide incluir

**Notas:**
- Usar el widget `houzez_elementor_contact_form` ya implementado en `/tasaciones`
- Button color naranja (#C4634A) hover (#DA7756) coherente con `/tasaciones`

**Pendiente confirmar:**
- Dirección física exacta
- Horarios de atención
- Email de destino

---

## 🟠 /residencial

**Propósito:** Landing del vertical "Residencial" — propiedades para vivir.

**Audiencia:** comprador / inquilino de propiedad residencial premium.

**Prioridad:** 🟠 media

**Estructura propuesta:**

1. **Hero:** "01. Residencial" + título declarativo
2. **Propuesta del vertical:** qué hace FA específicamente en residencial. 2-3 párrafos.
3. **Listings destacados:** grid de 3-6 propiedades curadas (CPT Houzez o custom)
4. **Servicios al cliente residencial:** tasación, búsqueda asistida, asesoramiento legal/fiscal
5. **CTA:** Contactanos

**Replicar estructura de `/tasaciones`** ajustando contenido.

---

## 🟠 /emprendimientos

**Propósito:** Vertical de proyectos en pozo y desarrollos.

**Audiencia:** inversores, compradores en pozo, desarrolladores.

**Prioridad:** 🟠 media

**Estructura propuesta:**

1. **Hero:** "02. Emprendimientos"
2. **Propuesta editorial del vertical** — por qué FA en emprendimientos
3. **Proyectos activos** — grid con cards de cada emprendimiento
4. **Información para desarrolladores** — si FA ofrece servicios a developers (gestión de comercialización completa)
5. **CTA**

---

## 🟠 /comercial

**Propósito:** Vertical de oficinas, locales, activos comerciales.

**Audiencia:** empresas, fondos, family offices, inversores institucionales.

**Prioridad:** 🟠 media

**Estructura propuesta:**

1. **Hero:** "03. Comercial"
2. **Propuesta del vertical** — análisis de portfolio, gestión integral, market reports
3. **Tipologías de activos** — oficinas, locales, naves, hotelería, mixed-use
4. **Casos / Track record** — operaciones cerradas si es público
5. **Servicios institucionales** — brokerage, gestión, valuación de portfolio
6. **CTA institucional**

---

## 🟠 /radar (Radar Inmobiliario)

**Propósito:** Landing del producto editorial principal de FA. Es el "newsletter / reporte de mercado" que diferencia a FA.

**Audiencia:** público general interesado en mercado inmobiliario, prensa, otros brokers, inversores.

**Prioridad:** 🟠 media-alta (es bandera del posicionamiento)

**Estructura propuesta:**

1. **Hero:** "Radar Inmobiliario"
2. **Qué es:** un reporte / publicación periódica con indicadores propios
3. **Metodología:** explicación corta de cómo se construyen los indicadores
4. **Últimas ediciones:** lista de publicaciones recientes con preview
5. **Suscripción:** email opt-in
6. **Indicadores destacados:** gráficos clave (precio m2, tiempo de venta, oferta/demanda)

**Notas:**
- Es el producto editorial estrella. Diseño cuidadoso.
- Puede tener integración con datos (Google Sheets / API) — investigar.

---

## 🟠 /intelligence (FAP Intelligence)

**Propósito:** Landing de la plataforma tech propia. Vende capacidades técnicas.

**Audiencia:** clientes B2B (otras inmobiliarias, fondos), prensa tech, talento.

**Prioridad:** 🟠 media

**Estructura propuesta:**

1. **Hero:** "FAP Intelligence" + claim sobre tech propia
2. **Filosofía:** "No adoptamos tecnología genérica, la construimos."
3. **Herramientas:** lista de productos internos (pricing engine, scenario analyzer, etc.)
4. **IA aplicada al real estate:** sección específica de capacidades de IA
5. **Para brokers:** si hay producto licenciable, CTA institucional
6. **Cierre:** roadmap o visión

---

## 🟡 /blog

**Propósito:** Hub editorial. Posts de análisis, market reports, perspectivas.

**Audiencia:** SEO + posicionamiento editorial.

**Prioridad:** 🟡 baja (importante pero después de las landings core)

**Estructura propuesta:**

1. Listado de posts paginado, grid o lista
2. Filtros por categoría (Análisis de mercado, Casos, Tutoriales, Perspectivas, Radar)
3. Cards con: imagen + título + bajada + fecha + categoría
4. Tipografía fiel al sistema

**Decisión técnica pendiente:** usar el sistema de blog nativo de WP con tema Houzez, o customizar con Elementor templates.

---

## 🟡 /preguntas/{slug}

**Propósito:** Páginas editoriales que responden las 4 preguntas core. Refuerzan voz FA y SEO long-tail.

**Audiencia:** búsqueda orgánica + usuarios del footer que clickean.

**Prioridad:** 🟡 baja-media

**4 páginas:**
- `/preguntas/cuanto-vale` — ¿Cuánto vale mi propiedad?
- `/preguntas/buen-momento` — ¿Es buen momento para comprar?
- `/preguntas/leer-mercado` — ¿Cómo leer el mercado?
- `/preguntas/valor-relativo` — ¿Qué es el valor relativo?

**Estructura propuesta de cada una:**

1. **Header:** la pregunta como título
2. **Respuesta corta:** 1 párrafo, ejecutiva
3. **Desarrollo:** 3-5 secciones que profundizan el tema. Tono editorial.
4. **Datos / indicadores:** si hay del Radar, citar
5. **CTA:** "Querés conversar con un broker FA?" → contacto

**Decisión técnica pendiente:** ver `04-decisiones.md` punto "decisiones pendientes".

---

## 🟡 /carreras

**Propósito:** Atracción de talento. Vacantes activas + cultura.

**Audiencia:** brokers, analistas, devs, creativos.

**Prioridad:** 🟡 baja

**Estructura propuesta:**

1. **Hero:** "Sumate al equipo." (sin signos de exclamación)
2. **Cultura:** qué se siente trabajar en FA (3-4 párrafos)
3. **Vacantes activas:** lista, link a form/email
4. **Postulación abierta:** form genérico para quien no encuentra vacante específica

---

## 🟡 /politica-de-privacidad

**Propósito:** Cumplimiento legal.

**Prioridad:** 🟡 baja pero obligatoria antes de ir a producción

**Notas:** texto legal estándar argentino. Se puede generar con templates legales y revisar con abogado.

---

## Notas generales de implementación

- **Empezar siempre por mirar `/tasaciones`** (post 6081) como referencia estructural.
- **Reusar containers** cuando hay un patrón conocido (hero, 3-cols con números, 2-cols heading+body).
- **No inventar componentes nuevos** salvo necesidad clara.
- **Antes de pedir copy nuevo**, revisar si ya existe algo en `/tasaciones` o en el sitio actual fabianachaval.com.ar que se pueda reciclar.
