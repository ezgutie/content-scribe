# Content Scribe 📝

Agente de IA especializado en generar contenido SEO para blogs.

## ¿Qué es?

Content Scribe es un agente autónomo que:
1. Investiga un tema usando búsqueda web
2. Genera un artículo optimizado para SEO
3. Lo formatea en HTML listo para publicar
4. Lo deploya a un sitio estático (Netlify)

## Arquitectura

```
content-scribe/
├── README.md              ← Este archivo
├── SOUL.md                ← Personalidad y directrices del agente
├── config/
│   ├── site.json          ← Configuración del sitio target (URL, estilo, deploy)
│   └── seo-rules.json     ← Reglas SEO (longitud, keywords, estructura)
├── templates/
│   └── article.html       ← Template HTML del artículo
├── scripts/
│   ├── research.py        ← Investigación de tema (keywords, competencia)
│   ├── generate.py        ← Generación del artículo
│   ├── seo-check.py       ← Validación SEO pre-publicación
│   └── publish.py         ← Deploy a Netlify
├── output/                ← Artículos generados (borradores + finales)
└── docs/
    ├── ROADMAP.md         ← Estado del proyecto
    └── DESIGN.md          ← Diseño técnico detallado
```

## Stack
- Python 3 (scripts de investigación, generación, validación)
- API de búsqueda web (Brave Search)
- LLM para generación (Claude/GPT)
- Netlify API para deploy
- HTML estático (sin framework)

## Estado
🟡 En desarrollo — Fase 1 (diseño y estructura base)

## Target
- **Sitio:** https://noud.es/blog/
- **Tema:** Transformación digital, automatización, IA, consultoría tech
- **Idioma:** Español
- **Audiencia:** PYMEs españolas buscando digitalización
