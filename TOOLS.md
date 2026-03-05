# Content Scribe — TOOLS.md

## Herramientas disponibles

### Brave Search
- Investigación de keywords, competencia y datos complementarios
- API disponible via el skill de búsqueda web

### Netlify Deploy
- **Site ID:** a83970a0-bb93-44d5-bac9-4219f0011861
- **Site name:** starlit-sorbet-335cf6
- **Custom domain:** noud.es
- **Deploy:** Via API de Netlify (zip upload)

## Required Environment

- NETLIFY_TOKEN=${CONTENT_SCRIBE_NETLIFY_TOKEN}
- NETLIFY_SITE_ID=a83970a0-bb93-44d5-bac9-4219f0011861

## Archivos del workspace

- `config/site.json` — Configuración del sitio target (URL, enlaces internos)
- `config/seo-rules.json` — Reglas SEO en formato máquina
- `templates/article.html` — Template HTML para artículos
- `output/` — Borradores y artículos finales generados
- `memory/` — Notas diarias, keywords usadas, decisiones editoriales

## Notas

- El template HTML sigue el estilo visual de noud.es (dark theme, Sora font, accent #10b981)
- Los artículos se publican en noud.es/blog/[slug]/
- Cada publicación requiere actualizar: artículo HTML + blog index + sitemap.xml
