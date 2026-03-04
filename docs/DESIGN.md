# Content Scribe — Diseño Técnico

## Visión general

Content Scribe es un agente que automatiza el pipeline de creación de contenido:

```
Tema/Keyword → Investigación → Borrador → Validación SEO → Aprobación → Publicación
```

## Componentes

### 1. Research Module (`scripts/research.py`)
- **Input:** Keyword o tema
- **Proceso:**
  - Busca en Google/Brave los top 10 resultados
  - Extrae: títulos, headers, longitud, keywords usados
  - Identifica preguntas frecuentes (People Also Ask)
  - Detecta gaps de contenido (qué NO se ha cubierto)
- **Output:** `research-report.json` con datos para el generador

### 2. Generator Module (`scripts/generate.py`)
- **Input:** Research report + config de estilo
- **Proceso:**
  - Genera outline (H2/H3 structure)
  - Escribe sección por sección
  - Aplica el tono definido en SOUL.md
  - Inserta enlaces internos a noud.es
- **Output:** Artículo en HTML

### 3. SEO Validator (`scripts/seo-check.py`)
- **Input:** Artículo HTML
- **Validaciones:**
  - ✅ Título: longitud, keyword presente
  - ✅ Meta description: longitud, keyword presente
  - ✅ H1 único
  - ✅ Estructura H2/H3 jerárquica
  - ✅ Longitud del artículo (palabras)
  - ✅ Keyword density
  - ✅ Alt text en imágenes
  - ✅ Enlaces internos presentes
  - ✅ Párrafos no exceden 4 líneas
- **Output:** Score SEO + lista de issues

### 4. Publisher (`scripts/publish.py`)
- **Input:** Artículo HTML validado + aprobación
- **Proceso:**
  - Inyecta en template HTML
  - Actualiza sitemap.xml
  - Actualiza página /blog/ (índice)
  - Deploy a Netlify via API
- **Output:** URL del artículo publicado

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
  "require_lists": true,
  "require_alt_text": true
}
```

## Fases de desarrollo

### Fase 1 — Estructura (actual)
- [x] Repo creado
- [x] README, SOUL.md, DESIGN.md
- [ ] Template HTML del artículo
- [ ] Config files (site.json, seo-rules.json)

### Fase 2 — Research
- [ ] Script de investigación con Brave Search API
- [ ] Extracción de headers y estructura de competidores
- [ ] Generación de research report

### Fase 3 — Generación
- [ ] Script de generación de artículos
- [ ] Integración con LLM (Claude API o similar)
- [ ] Aplicación de reglas de estilo

### Fase 4 — Validación + Publicación
- [ ] SEO checker automático
- [ ] Publisher con Netlify API
- [ ] Actualización automática de sitemap e índice de blog

### Fase 5 — Autonomía
- [ ] Scheduling (publicación periódica)
- [ ] Sugerencia de temas basada en tendencias
- [ ] Analytics feedback loop (qué artículos rankean mejor)
