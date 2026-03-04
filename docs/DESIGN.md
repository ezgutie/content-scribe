# Content Scribe — Diseño Técnico

## Visión general

Content Scribe es un agente que genera contenido de blog a partir del trabajo real que hacemos en proyectos. No inventa temas — los extrae de conversaciones y trabajo técnico real, los enriquece con contexto de la industria, y los publica optimizados para SEO.

## Pipeline de 5 funciones

```
Conversación → Identificar → Desglosar → Investigar → Desarrollar → Publicar
```

### Función 1: Identificar (`identify`)
**Input:** Conversación de trabajo (resumen de sesión, commits, decisiones)
**Proceso:**
- Lee el contexto de lo trabajado en la sesión
- Identifica: qué se hizo, qué decisiones se tomaron, qué problemas se resolvieron
- Extrae los temas con potencial de contenido
**Output:** Lista de temas identificados con contexto

**Ejemplo:**
> "Hoy resolvimos un bug de CSS specificity en producción, implementamos soft validation en frascos médicos con override, y diseñamos la estructura de un agente de contenido"

### Función 2: Desglosar (`decompose`)
**Input:** Temas identificados
**Proceso:**
- Cada tema se analiza desde múltiples ángulos:
  - **Macro:** La industria, tendencia o problema general
  - **Micro:** La decisión específica del proyecto, llevada a tierra
  - **Metodología:** Cómo se abordó (fases previas, estructura, criterio)
  - **Resultado:** Qué quedó, qué se aprendió
- Genera N posibles posts por tema, cada uno con un ángulo distinto
- Prioriza por relevancia SEO y valor para la audiencia
**Output:** Lista de posts posibles con título tentativo, ángulo y outline

**Ejemplos de ángulos para un mismo proyecto:**
1. "Fases previas a un proyecto de software médico" (metodología)
2. "Cómo diferenciamos lo necesario de lo indispensable en un MVP" (criterio)
3. "Soft validation: cuando las reglas de negocio no son blanco y negro" (técnico aplicado)
4. "Digitalización de consultorios médicos: qué necesitan realmente" (industria macro → proyecto micro)
5. "Cómo quedó nuestra app de gestión de tratamientos alérgicos" (caso de éxito)

### Función 3: Investigar (`research`)
**Input:** Post seleccionado (título + ángulo + contexto del proyecto)
**Proceso:**
- Busca en internet información complementaria:
  - Datos de la industria, estadísticas, tendencias
  - Artículos similares (para diferenciarnos, no para copiar)
  - Fuentes citables que refuercen nuestro punto
- Identifica gaps: qué dicen otros vs. qué aportamos nosotros
**Output:** Research brief con fuentes y datos complementarios

**Regla clave:** La información externa COMPLEMENTA, no reemplaza. El proyecto nuestro es el protagonista.

### Función 4: Desarrollar (`generate`)
**Input:** Post outline + research brief + contexto del proyecto
**Proceso:**
- Escribe el artículo integrando:
  - **Experiencia propia** (70-80%) — Lo que hicimos, decidimos, aprendimos
  - **Contexto externo** (20-30%) — Datos, tendencias, referencias que enriquecen
- Aplica reglas SEO (título, meta, estructura, keywords, enlaces internos)
- Mantiene el tono: profesional, práctico, sin perder el foco del proyecto real
- No se difumina en lo genérico — siempre vuelve al caso concreto
**Output:** Artículo HTML completo, validado SEO

**Regla clave:** El lector debe terminar pensando "estos saben de lo que hablan porque lo hicieron de verdad".

### Función 5: Publicar (`publish`)
**Input:** Artículo aprobado por el humano
**Proceso:**
- Inyecta en template HTML de noud.es
- Actualiza índice de /blog/
- Actualiza sitemap.xml
- Deploy a Netlify
- Verifica que la URL responde OK
**Output:** URL publicada

## Configuración

### `config/site.json`
```json
{
  "name": "NOUD",
  "url": "https://noud.es",
  "blog_path": "/blog/",
  "language": "es",
  "author": "NOUD",
  "netlify_site_id": "a83970a0-bb93-44d5-bac9-4219f0011861",
  "internal_links": [
    {"url": "/", "anchor": "consultoría tecnológica"},
    {"url": "/#servicios", "anchor": "nuestros servicios"},
    {"url": "/#proceso", "anchor": "nuestro proceso"},
    {"url": "/nosotros/", "anchor": "sobre nosotros"}
  ]
}
```

### `config/seo-rules.json`
```json
{
  "title_min_chars": 50,
  "title_max_chars": 60,
  "meta_min_chars": 150,
  "meta_max_chars": 160,
  "min_words": 1200,
  "max_words": 2000,
  "max_keyword_density": 0.02,
  "min_internal_links": 2,
  "max_paragraph_lines": 4,
  "require_lists": true
}
```

## Ratio contenido propio vs externo

| Tipo de post | Propio | Externo |
|---|---|---|
| Caso de éxito | 90% | 10% |
| Metodología | 70% | 30% |
| Industria + proyecto | 50% | 50% |
| Técnico aplicado | 80% | 20% |

## Fases de desarrollo

### Fase 1 — Estructura ✅
- [x] Repo, SOUL.md, DESIGN.md, config

### Fase 2 — Template + primer artículo manual
- [ ] Template HTML del artículo
- [ ] Generar primer artículo manualmente (yo, Enki, ejecutando el pipeline a mano)
- [ ] Publicar en noud.es/blog/ y validar que se ve bien

### Fase 3 — Scripts
- [ ] identify.py — extrae temas de una sesión de trabajo
- [ ] decompose.py — desglosa en posts posibles
- [ ] research.py — busca info complementaria
- [ ] generate.py — escribe el artículo
- [ ] publish.py — deploya a Netlify

### Fase 4 — Integración como agente
- [ ] Conectar como agente en la plataforma (Tobias/OpenClaw)
- [ ] Flujo automatizado end-to-end
- [ ] Scheduling periódico
