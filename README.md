# Content Scribe 📝

Agente de contenido para el blog de [noud.es](https://noud.es/blog/). Estratega editorial + redactor SEO.

## Qué hace

Transforma conversaciones de trabajo reales en artículos de blog optimizados para SEO. No inventa temas — trabaja con lo que el equipo ya hizo.

## Pipeline

1. **Identificar** — Extraer temas de sesiones de trabajo
2. **Desglosar** — Generar posts posibles con ángulo, keyword y etapa de funnel
3. **Investigar** — Buscar datos complementarios en internet
4. **Desarrollar** — Escribir el artículo integrando experiencia real + contexto externo
5. **Publicar** — Deploy a Netlify (solo con aprobación humana)

## Estructura

```
content-scribe/
├── SOUL.md          — Identidad, criterio editorial, estilo, reglas SEO
├── AGENTS.md        — Contrato operativo, prioridades, niveles de autonomía
├── IDENTITY.md      — Nombre, criatura, vibe, emoji
├── TOOLS.md         — Config del entorno (Netlify, APIs, rutas)
├── CAPABILITIES.md  — Qué puede hacer, pipeline, límites
├── MEMORY.md        — Keywords usadas, posts publicados, decisiones
├── HEARTBEAT.md     — Tareas autónomas programadas
├── config/
│   ├── site.json    — Configuración de noud.es
│   └── seo-rules.json — Reglas SEO en formato máquina
├── templates/
│   └── article.html — Template HTML (matching estilo noud.es)
├── scripts/         — Scripts del pipeline (por desarrollar)
├── output/          — Artículos generados
└── docs/
    ├── DESIGN.md    — Diseño técnico
    └── ROADMAP.md   — Estado del proyecto
```

## Target

- **Sitio:** https://noud.es/blog/
- **Audiencia:** PYMEs españolas buscando digitalización
- **Plataforma:** Tobias (MTP)

## Estado

🟡 En desarrollo — Definición del agente completa, scripts pendientes
