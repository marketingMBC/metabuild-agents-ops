# Meta Build City — Paquete Operacional

## Qué es esto

Este repositorio es el **sistema operativo** de Meta Build City (MBC), una agencia de tecnología 4.0 especializada en la industria de la construcción en Chile y LATAM.

Está diseñado para funcionar con **Claude Code** como orquestador, con 5 sub-agentes especializados que automatizan las operaciones del equipo.

## Quick Start

1. Abrir terminal en este directorio
2. Ejecutar `claude` para iniciar Claude Code
3. El archivo `CLAUDE.md` se carga automáticamente como contexto
4. Usar los comandos de sub-agentes:

```
/sales proposal [cliente] [servicio]    → Genera propuesta comercial
/sales outreach [segmento]              → Genera secuencia de outreach
/content post linkedin [tema]           → Genera post para LinkedIn
/content blog [tema]                    → Genera artículo de blog
/ops weekly                             → Genera reporte semanal
/ops onboard [cliente]                  → Inicia onboarding de cliente
/tech spec [proyecto] [servicio]        → Genera spec técnico
/tech feasibility [requerimiento]       → Estudio de factibilidad
/strategy market [sector]               → Análisis de mercado
/strategy competitive [competidor]      → Análisis competitivo
```

## Sub-Agentes Disponibles

| Agente | Comando | Función |
|--------|---------|---------|
| **Sales** | `/sales` | Leads, propuestas, outreach, CRM |
| **Content** | `/content` | Blog, redes sociales, case studies, newsletters |
| **Ops** | `/ops` | Proyectos, onboarding, reportes semanales |
| **Tech** | `/tech` | Specs técnicos, factibilidad, estimaciones |
| **Strategy** | `/strategy` | Mercado, competencia, pricing, planning |

## Estructura del Repositorio

```
metabuild/
├── CLAUDE.md                    # Orquestador principal (5 sub-agentes)
├── context.md                   # Contexto completo de MBC
├── 00_brief/                    # Misión, estrategia, decisiones
├── 01_customers/                # CRM, segmentos, pipeline, outreach
├── 02_services/                 # Catálogo de servicios (XR, IA, Blockchain, Marketing, BIM)
├── 03_engineering/              # Stack técnico, pipelines, estándares
├── 04_pricing/                  # Modelos de precio, paquetes, unit economics
├── 05_growth/                   # Contenido, redes sociales, partnerships
└── 06_ops/                      # Gestión de proyectos, onboarding, QA
```

Ver `PROJECT_STRUCTURE.md` para detalles completos.

## Flujo de Trabajo Diario

1. **Inicio del día**: Revisar `00_brief/open_questions.md` y `01_customers/pipeline.md`
2. **Trabajo comercial**: Usar `/sales` para outreach, propuestas, pipeline
3. **Contenido**: Usar `/content` para posts y artículos programados
4. **Proyectos**: Usar `/ops` para status y gestión
5. **Fin de semana**: Usar `/ops weekly` para generar reporte semanal

## Convenciones

- **Idioma**: Español principal, inglés para términos técnicos
- **Formato**: Markdown para todo
- **Moneda**: USD (con equivalente CLP cuando sea relevante)
- **Archivos**: Kebab-case para nombres de archivo, snake_case para campos de datos
- **Updates**: Mantener CRM y pipeline actualizados después de cada interacción comercial

## Equipo

Meta Build City — Tecnología 4.0 para Construcción
- Servicios: XR | IA | Blockchain | Marketing | BIM
- Mercado: Chile → LATAM
- Web: metabuildcity.com
