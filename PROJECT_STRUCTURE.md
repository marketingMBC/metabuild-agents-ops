# Estructura del Proyecto — Meta Build City

## Overview

Este repositorio sigue una estructura modular donde cada directorio corresponde a un área funcional de la empresa. Los sub-agentes de Claude Code utilizan estos archivos como base de conocimiento para generar outputs de alta calidad.

---

## Directorios

### `00_brief/` — Misión y Estrategia
El "cerebro" de MBC. Contiene la dirección estratégica y el tracking de decisiones.

| Archivo | Propósito | Actualización |
|---------|-----------|---------------|
| `mbc_brief.md` | Overview de la empresa, misión, visión | Trimestral |
| `decision_log.md` | Registro de decisiones clave | Cada decisión |
| `open_questions.md` | Preguntas sin resolver que necesitan atención | Continua |
| `quarterly_execution_plan.md` | Plan de ejecución del trimestre actual | Trimestral |

### `01_customers/` — Desarrollo Comercial y CRM
Todo lo relacionado con clientes: desde la prospección hasta la gestión de relaciones.

| Subdirectorio/Archivo | Propósito |
|----------------------|-----------|
| `segments/` | Perfiles detallados de cada segmento (constructoras, inmobiliarias, arquitectura, gobierno) |
| `competitive/` | Análisis competitivo del mercado LATAM |
| `outreach-drafts/` | Templates de email frío y secuencias LinkedIn por servicio |
| `discovery-prep/` | Templates de research pre-llamada |
| `crm_lite.md` | CRM liviano en markdown |
| `discovery_call_script.md` | Script para llamadas de descubrimiento |
| `pipeline.md` | Pipeline de ventas con stages y métricas |
| `proposal_template.md` | Template base para propuestas comerciales |

### `02_services/` — Catálogo de Servicios
Descripción completa de cada línea de servicio. Es la referencia principal para armar propuestas y contenido.

| Archivo | Servicio |
|---------|----------|
| `xr_services.md` | Realidad Virtual, Aumentada y Mixta |
| `ai_services.md` | Inteligencia Artificial y Machine Learning |
| `blockchain_services.md` | Blockchain y Smart Contracts |
| `marketing_services.md` | Marketing Digital especializado en AEC |
| `bim_services.md` | Building Information Modeling |
| `packages.md` | Paquetes combinados de servicios |
| `case_studies/template.md` | Template para crear casos de estudio |

### `03_engineering/` — Arquitectura Técnica
Stack tecnológico y pipelines de producción. Referencia para specs técnicos y estimaciones.

| Archivo | Propósito |
|---------|-----------|
| `tech_stack.md` | Stack completo de MBC por área |
| `xr_pipeline.md` | Pipeline de producción XR paso a paso |
| `ai_stack.md` | Stack IA/ML y metodología |
| `blockchain_stack.md` | Stack blockchain y templates de contratos |
| `delivery_standards.md` | Estándares de entrega por tipo de proyecto |

### `04_pricing/` — Modelo de Negocio
Pricing, paquetes y análisis financiero. Referencia para propuestas y decisiones de pricing.

| Archivo | Propósito |
|---------|-----------|
| `pricing_models.md` | Precios por línea de servicio |
| `packages_pricing.md` | Pricing de paquetes combinados |
| `unit_economics.md` | Costos, márgenes y métricas financieras |

### `05_growth/` — Crecimiento y Marketing
Estrategia de contenido, redes sociales y alianzas para crecimiento orgánico e inbound.

| Archivo | Propósito |
|---------|-----------|
| `content_strategy.md` | Estrategia de contenido y pilares |
| `social_media_playbook.md` | Playbook de redes sociales por canal |
| `partnerships.md` | Alianzas estratégicas y eventos |
| `newsletter_templates.md` | Templates de newsletter |
| `thought_leadership.md` | Estrategia de posicionamiento como líderes |

### `06_ops/` — Operaciones
Procesos operacionales para gestión de proyectos, onboarding y calidad.

| Archivo | Propósito |
|---------|-----------|
| `weekly_review_template.md` | Template para revisión semanal |
| `project_management.md` | Metodología de gestión de proyectos |
| `client_onboarding.md` | Proceso de onboarding paso a paso |
| `quality_standards.md` | Estándares QA por tipo de servicio |

### Archivos Raíz

| Archivo | Propósito |
|---------|-----------|
| `CLAUDE.md` | Orquestador principal — define los 5 sub-agentes |
| `context.md` | Contexto completo de MBC (~1500 líneas) |
| `README.md` | Guía de inicio rápido |
| `PROJECT_STRUCTURE.md` | Este archivo |
| `SALES_PLAYBOOK.md` | Playbook completo de ventas |
| `OUTREACH_PREPARATION_SUMMARY.md` | Resumen de preparación de outreach |
| `OUTREACH_READINESS_CHECKLIST.md` | Checklist de readiness para outreach |

---

## Cómo Usar Esta Estructura

### Para el Sales Agent
1. Lee el segmento del prospecto en `01_customers/segments/`
2. Consulta el servicio en `02_services/`
3. Arma pricing con `04_pricing/`
4. Genera propuesta usando `01_customers/proposal_template.md`

### Para el Content Agent
1. Lee la estrategia en `05_growth/content_strategy.md`
2. Consulta detalles técnicos en `02_services/` o `03_engineering/`
3. Sigue el playbook de `05_growth/social_media_playbook.md`

### Para el Ops Agent
1. Usa templates de `06_ops/`
2. Consulta estado en `01_customers/crm_lite.md` y `pipeline.md`
3. Documenta decisiones en `00_brief/decision_log.md`

### Para el Technical Agent
1. Consulta stacks en `03_engineering/`
2. Referencia servicios en `02_services/`
3. Usa estándares de `03_engineering/delivery_standards.md`

### Para el Strategy Agent
1. Lee `01_customers/competitive/landscape.md`
2. Analiza pricing en `04_pricing/`
3. Consulta brief en `00_brief/`

---

## Mantenimiento

- **CRM y Pipeline**: Actualizar después de cada interacción comercial
- **Decision Log**: Actualizar con cada decisión relevante
- **Open Questions**: Revisar semanalmente, resolver o escalar
- **Contenido de servicios**: Actualizar cuando haya cambios en offerings
- **Pricing**: Revisar trimestralmente
- **Análisis competitivo**: Actualizar mensualmente
