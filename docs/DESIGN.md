# Content Scribe — Diseño Técnico

## Visión general

Content Scribe es un agente que genera contenido de blog a partir del trabajo real de proyectos de NOUD. Corre dentro de Tobias (MTP) como un agente independiente.

## Pipeline de 5 funciones

```
Input de trabajo → Identificar → Desglosar → Investigar → Desarrollar → Publicar
```

### 1. Identificar
- **Input:** Conversaciones de trabajo, notas de proyecto, commits, decisiones
- **Proceso:** Lee todo, extrae qué se hizo, qué decisiones se tomaron, qué problemas se resolvieron
- **Output:** Lista de temas con contexto

### 2. Desglosar
- **Input:** Temas identificados
- **Proceso:** Analiza desde múltiples ángulos (macro industria, micro proyecto, metodología, técnico, caso de éxito). Prioriza por madurez del blog, relevancia SEO, valor para el lector.
- **Output:** Posts posibles con título tentativo, ángulo, keyword objetivo, etapa de funnel

### 3. Investigar
- **Input:** Post aprobado (título + ángulo + contexto)
- **Proceso:** Busca datos complementarios (estadísticas, tendencias, artículos similares). Identifica gaps: qué dicen otros vs. qué aportamos nosotros.
- **Output:** Research brief con fuentes y datos

### 4. Desarrollar
- **Input:** Post outline + research brief + contexto del proyecto
- **Proceso:** Escribe el artículo integrando experiencia real (70-80%) + contexto externo (20-30%). Aplica reglas SEO.
- **Output:** Artículo completo en markdown → HTML

### 5. Publicar
- **Input:** Artículo aprobado por humano
- **Proceso:** Genera HTML desde template, actualiza índice de /blog/, actualiza sitemap.xml, deploy a Netlify, verifica URL
- **Output:** URL publicada

## Flujo de aprobación

```
Proponer temas → [feedback] → Briefing → [feedback] → Borrador → [aprobación] → HTML → [aprobación] → Deploy
```

Nada se publica sin aprobación explícita.

## Stack

- **Plataforma:** Tobias (MTP)
- **Búsqueda:** Brave Search API
- **Deploy:** Netlify API (zip upload)
- **Output:** HTML estático (template en `templates/article.html`)
- **Sitio target:** noud.es/blog/

## Configuración

- `config/site.json` — URL, blog path, Netlify site ID, enlaces internos
- `config/seo-rules.json` — Reglas SEO medibles (longitud título, density, etc.)
