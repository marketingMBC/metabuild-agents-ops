# Gestión de Proyectos — Meta Build City

> **Versión:** 2.0 | **Última actualización:** Febrero 2026
> **Aplica a:** Todos los proyectos de servicios MBC (XR, AI, Blockchain, Marketing Digital, BIM)
> **Responsable:** Director de Operaciones / Project Lead asignado

---

## Filosofía de Gestión

MBC opera en la intersección de tecnología y construcción, donde los proyectos requieren tanto la agilidad del desarrollo de software como la rigurosidad de la entrega en obra. Nuestra metodología es un híbrido pragmático que toma lo mejor de cada mundo.

**Principio rector**: "Entregar valor temprano y frecuentemente, sin sacrificar calidad."

---

## Metodología

### Enfoque Híbrido: Agile + Construction-Adapted

No aplicamos Scrum dogmáticamente. Usamos un framework adaptado a la realidad de proyectos de tecnología para construcción:

**Agile Adapted para desarrollo iterativo**:
- Sprints de 2 semanas con check-ins semanales con el cliente
- Backlog priorizado por valor de negocio para el cliente
- Demos al final de cada sprint (mostrar progreso tangible)
- Retrospectivas para mejora continua del proceso

**Kanban para trabajo continuo y retainers**:
- Tablero visual con columnas: Backlog → To Do → In Progress → Review → Done
- WIP limits: máximo 2-3 tareas por persona simultáneamente
- Flujo continuo sin sprints rígidos (ideal para soporte, mantenimiento, marketing)
- Priorización semanal con el cliente

**Waterfall elements para producción XR y entregables críticos**:
- Milestones claros y secuenciales cuando la naturaleza del proyecto lo requiere
- Gates de aprobación entre fases (especialmente diseño → desarrollo → producción)
- Útil para: recorridos virtuales, modelos BIM, smart contracts (donde los cambios tardíos son costosos)

### Cuándo usar cada enfoque

| Tipo de Proyecto | Metodología | Razón |
|-----------------|-------------|-------|
| Desarrollo XR (recorridos, apps) | Waterfall + iteraciones en cada fase | Producción secuencial con revisiones |
| Proyectos de AI/ML | Agile (sprints de 2 semanas) | Experimentación iterativa, resultados incrementales |
| Smart Contracts / Blockchain | Waterfall con reviews | Seguridad crítica, cambios costosos |
| Marketing Digital (retainer) | Kanban | Flujo continuo, prioridades cambiantes |
| BIM (modelado, coordinación) | Agile + milestones | LOD progresivo, coordinación iterativa |
| Consultoría / Estrategia | Waterfall | Fases claras, entregables definidos |

---

## Project Lifecycle

### Fase 1: Kickoff (Día 1-5)

**Objetivo**: alinear al equipo interno y al cliente sobre el alcance, expectativas y forma de trabajo.

**Actividades**:
- [ ] Confirmar scope final (basado en propuesta firmada)
- [ ] Asignar equipo interno: Project Lead, Technical Lead, equipo de ejecución
- [ ] Identificar Client Champion (contacto principal del lado del cliente)
- [ ] Configurar herramientas: proyecto en Notion/Linear, canal de Slack, carpeta compartida
- [ ] Realizar reunión de kickoff con el cliente (ver Onboarding para agenda completa)
- [ ] Firmar project brief con el cliente

**Entregables**:
- Project brief firmado
- Equipo asignado y notificado
- Herramientas configuradas
- Canal de comunicación activo

**Duración típica**: 3-5 días hábiles.

### Fase 2: Discovery / Design (Semana 1-3)

**Objetivo**: entender a profundidad el problema, recopilar inputs, y diseñar la solución antes de construir.

**Actividades**:
- [ ] Recopilar toda la información del cliente: assets, data, accesos, modelos existentes
- [ ] Investigación técnica: evaluar constraints, plataformas, integraciones
- [ ] Workshops de discovery con stakeholders del cliente (si aplica)
- [ ] Definir arquitectura / approach técnico
- [ ] Crear prototipos o mockups (wireframes, concept art, flowcharts)
- [ ] Presentar approach al cliente para validación
- [ ] Documentar requerimientos finales

**Entregables**:
- Documento de requerimientos (sign-off del cliente)
- Arquitectura técnica / approach documentado
- Prototipo o mockup (si aplica)
- Backlog inicial priorizado
- Sprint 1 planificado

**Duración típica**: 1-3 semanas según complejidad.

### Fase 3: Development / Ejecución (Variable)

**Objetivo**: construir la solución iterativamente, mostrando progreso al cliente frecuentemente.

**Actividades por sprint (2 semanas)**:
- [ ] Sprint planning: definir qué se va a entregar en este sprint
- [ ] Daily standup async (Slack): qué hice ayer, qué haré hoy, blockers
- [ ] Desarrollo / ejecución de tareas del sprint
- [ ] Demo semanal al cliente (mostrar progreso, recoger feedback)
- [ ] Sprint review: presentar lo completado al final del sprint
- [ ] Sprint retrospective (interna): ¿qué mejorar para el próximo sprint?

**Cadencia**:
- Sprints de 2 semanas
- Demos semanales o bi-semanales al cliente
- Releases incrementales cuando sea posible

**Duración típica**: 4-12 semanas según proyecto.

### Fase 4: Testing / QA (Semana penúltima)

**Objetivo**: asegurar que el entregable cumple con los estándares de calidad y los requerimientos del cliente.

**Actividades**:
- [ ] Testing interno según checklist de calidad (ver quality_standards.md)
- [ ] Peer review de código/modelos
- [ ] Testing de performance (FPS para XR, accuracy para AI, gas para blockchain)
- [ ] Testing de usabilidad (si aplica)
- [ ] Corrección de bugs y defectos encontrados
- [ ] Documentación de testing realizado

**Entregables**:
- Reporte de QA con resultados
- Lista de defectos corregidos
- Aprobación interna para pasar a UAT

**Duración típica**: 3-5 días (paralelo a la última semana de development).

### Fase 5: Delivery (Semana final)

**Objetivo**: entregar la solución al cliente de forma controlada y profesional.

**Actividades**:
- [ ] Deploy a ambiente de staging / pre-producción
- [ ] UAT (User Acceptance Testing) con el cliente
- [ ] Correcciones finales basadas en feedback UAT
- [ ] Deploy a producción
- [ ] Verificación post-deployment
- [ ] Sign-off formal del cliente

**Entregables**:
- Solución deployed en producción
- Sign-off de aceptación del cliente
- Reporte de entrega

**Duración típica**: 3-7 días.

### Fase 6: Handoff y Cierre (Post-delivery)

**Objetivo**: asegurar que el cliente puede usar, mantener y sacar valor de lo entregado sin depender de MBC.

**Actividades**:
- [ ] Documentación completa: técnica, de usuario, de mantenimiento
- [ ] Sesión de training / capacitación al equipo del cliente
- [ ] Transición a soporte/mantenimiento (si hay contrato de soporte)
- [ ] Reunión de cierre: retrospectiva del proyecto con el cliente
- [ ] Encuesta de satisfacción al cliente
- [ ] Solicitar testimonial / case study (si la experiencia fue positiva)
- [ ] Solicitar referrals
- [ ] Post-mortem interno del proyecto

**Entregables**:
- Documentación completa entregada
- Training realizado
- Encuesta de satisfacción completada
- Post-mortem documentado

**Duración típica**: 1-2 semanas.

---

## Tools (Stack de Herramientas)

### Project Tracking

| Herramienta | Uso | Acceso |
|-------------|-----|--------|
| **Notion** | Project management, wikis, documentación, templates | Equipo MBC + clientes (con permisos) |
| **Linear** | Task tracking para desarrollo (alternativa a Notion para dev) | Equipo técnico |

**Estructura en Notion**:
```
Workspace MBC
├── Projects/
│   ├── {Nombre Cliente} - {Nombre Proyecto}/
│   │   ├── Brief
│   │   ├── Requirements
│   │   ├── Backlog / Tasks
│   │   ├── Sprint Board
│   │   ├── Meeting Notes
│   │   ├── Decisions
│   │   └── Delivery / Handoff
│   └── ...
├── Templates/
├── Ops/
└── Internal/
```

### Communication

| Herramienta | Uso | Cuándo |
|-------------|-----|--------|
| **Slack** | Comunicación interna del equipo MBC | Siempre (daily async standups, decisiones rápidas, coordinación) |
| **Email** | Comunicación formal con clientes | Propuestas, contratos, reportes formales, primera toma de contacto |
| **WhatsApp** | Comunicación informal con clientes | Coordinación rápida, recordatorios, urgencias (solo si el cliente lo prefiere) |
| **Google Meet / Zoom** | Videollamadas con clientes y equipo | Reuniones semanales, demos, kickoffs |

**Estructura de canales Slack**:
```
#general            — Anuncios y temas generales
#random             — Off-topic, cultura, team building
#sales              — Pipeline, leads, deals, propuestas
#content            — Contenido, marketing, redes sociales
#dev                — Desarrollo técnico, bugs, arquitectura
#client-{nombre}    — Canal por cada cliente activo
#ops                — Operaciones, procesos, herramientas
```

### Archivos y Repositorios

| Herramienta | Uso |
|-------------|-----|
| **Google Drive** | Archivos compartidos con clientes (docs, presentaciones, assets) |
| **GitHub** | Código fuente, versionamiento, CI/CD |
| **Google Docs/Sheets** | Documentos colaborativos, spreadsheets |

### Design y Colaboración

| Herramienta | Uso |
|-------------|-----|
| **Figma** | Diseño de UI/UX, mockups, prototipos interactivos |
| **Miro** | Workshops remotos, brainstorming, mapas conceptuales |
| **Whimsical** | Diagramas de flujo, wireframes rápidos |

---

## Roles por Proyecto

### Estructura Mínima

Cada proyecto tiene al menos estos 3 roles cubiertos:

| Rol | Responsabilidad | Quién |
|-----|----------------|-------|
| **Project Lead** (MBC) | Gestión del proyecto: scope, timeline, comunicación, riesgos. Es el punto de contacto principal para el cliente. | PM o CEO (en proyectos pequeños) |
| **Technical Lead** (MBC) | Decisiones técnicas: arquitectura, calidad, estimaciones. Lidera al equipo de desarrollo. | CTO o ingeniero senior |
| **Client Champion** (Cliente) | Punto de contacto del lado del cliente. Toma decisiones, valida entregables, facilita accesos e información. | Designado por el cliente |

### Roles Adicionales (según tamaño del proyecto)

| Rol | Cuándo se Necesita |
|-----|-------------------|
| **Developer(s)** | Proyectos con desarrollo de software, XR, AI |
| **BIM Modeler** | Proyectos de modelado BIM |
| **Designer (UX/UI)** | Proyectos con interfaz de usuario |
| **QA Tester** | Proyectos medianos-grandes (en proyectos chicos, lo hace el dev) |
| **Stakeholders** (Cliente) | Personas del lado del cliente que tienen interés/influencia pero no gestionan día a día |

### Matriz RACI (Template)

| Actividad | Project Lead | Tech Lead | Developer | Client Champion | Stakeholders |
|-----------|:-----------:|:---------:|:---------:|:--------------:|:------------:|
| Definir scope | R | C | I | A | C |
| Decisiones técnicas | C | R/A | C | I | I |
| Desarrollo | I | R | A | I | — |
| QA/Testing | A | R | R | C | — |
| Aprobación de entregables | R | C | I | A | C |
| Comunicación de status | R/A | C | I | I | I |

R = Responsible, A = Accountable, C = Consulted, I = Informed

---

## Communication Cadence

### Comunicación Interna (Equipo MBC)

| Tipo | Frecuencia | Formato | Duración | Participantes |
|------|-----------|---------|----------|--------------|
| Daily standup | Diario (async) | Slack #dev o #client-{nombre} | 5 min escribir | Todo el equipo del proyecto |
| Sprint planning | Bi-semanal | Video call | 30-60 min | Project Lead + Tech Lead + devs |
| Sprint review | Bi-semanal | Video call | 30 min | Equipo del proyecto |
| Retrospectiva | Bi-semanal | Video call | 30 min | Equipo del proyecto |

**Formato de daily standup (async en Slack)**:
```
Ayer: {qué completé}
Hoy: {qué voy a hacer}
Blockers: {qué me frena} (o "ninguno")
```
Hora límite para postear: 10:00 AM CLT.

### Comunicación con el Cliente

| Tipo | Frecuencia | Formato | Duración | Participantes |
|------|-----------|---------|----------|--------------|
| Sync semanal | Semanal | Video call (Google Meet/Zoom) | 30 min | Project Lead + Client Champion |
| Sprint demo | Bi-semanal | Video call con screen share | 30-45 min | Equipo MBC + cliente |
| Executive report | Mensual | Email + documento | — | Project Lead → stakeholders |
| Quarterly Business Review | Trimestral (retainers) | Presencial o video | 60-90 min | Equipo MBC + equipo cliente |

**Agenda del sync semanal con cliente** (30 min):
1. Resumen de progreso (5 min)
2. Demo de avances (10 min)
3. Feedback del cliente (5 min)
4. Blockers y necesidades (5 min)
5. Plan de la próxima semana (5 min)

**Executive Report Mensual** (estructura):
1. Resumen ejecutivo (2-3 oraciones)
2. Progreso vs plan (% de avance, milestones completados)
3. Métricas clave (según el tipo de proyecto)
4. Riesgos y mitigaciones
5. Plan para el próximo mes
6. Decisiones pendientes del cliente

---

## Risk Management

### Identificación de Riesgos (en Kickoff)

En el kickoff de cada proyecto, se realiza una sesión de identificación de riesgos con el equipo y, si es posible, con el cliente.

**Categorías comunes de riesgo en proyectos MBC**:

| Categoría | Ejemplos |
|-----------|---------|
| **Técnico** | Tecnología no funciona como se esperaba, performance issues, integración fallida |
| **Scope** | Scope creep, requerimientos ambiguos, cambios frecuentes del cliente |
| **Recursos** | Falta de disponibilidad del equipo, dependencia de un solo developer |
| **Cliente** | Retrasos en aprobaciones, falta de información, cambio de prioridades |
| **Externo** | Cambios en APIs/plataformas de terceros, problemas de licenciamiento |
| **Timeline** | Plazos muy ajustados, dependencias externas que se retrasan |
| **Financiero** | Presupuesto insuficiente, pagos retrasados del cliente |

### Risk Register (Template)

| # | Riesgo | Probabilidad | Impacto | Nivel | Mitigación | Owner | Status |
|---|--------|:------------:|:-------:|:-----:|-----------|-------|--------|
| 1 | {descripción} | Alta/Media/Baja | Alto/Medio/Bajo | Crítico/Alto/Medio/Bajo | {acción preventiva} | {nombre} | Open/Mitigated/Closed |

**Nivel de riesgo** = Probabilidad x Impacto:
- **Crítico** (Alta x Alto): requiere acción inmediata, escalar al CEO
- **Alto** (Alta x Medio o Media x Alto): plan de mitigación activo, monitoreo semanal
- **Medio** (Media x Medio): monitoreo bi-semanal, plan de contingencia
- **Bajo** (Baja x cualquiera o cualquiera x Bajo): registrar, monitoreo mensual

### Weekly Risk Review

Cada semana, como parte de la revisión semanal o del sync con el cliente:
1. Revisar risk register: ¿algún riesgo cambió de nivel?
2. ¿Aparecieron riesgos nuevos?
3. ¿Las mitigaciones están funcionando?
4. Actualizar el register

### Escalation Process

```
Nivel 1: Project Lead identifica el riesgo/problema
    ↓ Si no puede resolver en 24h
Nivel 2: Project Lead + Tech Lead evalúan opciones
    ↓ Si impacta timeline, presupuesto o scope significativamente
Nivel 3: Escalar al CEO para decisión y comunicación al cliente
    ↓ Si afecta la relación con el cliente o la reputación de MBC
Nivel 4: CEO + Cliente Champion resuelven juntos
```

**Regla de oro**: escalar temprano es mejor que escalar tarde. Nunca ocultar problemas al cliente.

---

## Templates

### 1. Project Brief Template

```markdown
# Project Brief: {Nombre del Proyecto}

## Información General
- **Cliente**: {nombre}
- **Contacto principal**: {nombre, cargo, email}
- **Servicio**: {XR / AI / Blockchain / BIM / Marketing}
- **Fecha inicio**: {fecha}
- **Fecha fin estimada**: {fecha}
- **Presupuesto**: ${monto}
- **Project Lead MBC**: {nombre}
- **Tech Lead MBC**: {nombre}

## Contexto
{2-3 párrafos sobre el cliente, su situación actual, y por qué buscan a MBC}

## Objetivos del Proyecto
1. {Objetivo 1 — medible}
2. {Objetivo 2 — medible}
3. {Objetivo 3 — medible}

## Scope
### In Scope
- {Entregable/funcionalidad 1}
- {Entregable/funcionalidad 2}
- {Entregable/funcionalidad 3}

### Out of Scope
- {Lo que explícitamente NO está incluido}
- {Para evitar scope creep}

## Milestones
| # | Milestone | Fecha Estimada | Entregable |
|---|-----------|---------------|-----------|
| 1 | Kickoff + Discovery | {fecha} | Requirements doc |
| 2 | {milestone} | {fecha} | {entregable} |
| 3 | {milestone} | {fecha} | {entregable} |
| 4 | Final Delivery | {fecha} | {entregable final} |

## Riesgos Identificados
| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|:-----------:|:-------:|-----------|
| {riesgo} | {P} | {I} | {acción} |

## Supuestos
- {Supuesto 1: ej. "El cliente proporcionará el modelo BIM existente"}
- {Supuesto 2: ej. "El feedback del cliente se entregará en máximo 3 días hábiles"}

## Aprobación
- Cliente: _________________ Fecha: _________
- MBC: _________________ Fecha: _________
```

### 2. Sprint Planning Template

```markdown
# Sprint Planning: Sprint #{número}
## Proyecto: {nombre} | Período: {fecha inicio} — {fecha fin}

### Objetivo del Sprint
{1 oración que describe qué queremos lograr en este sprint}

### Backlog Items para este Sprint
| # | Item | Prioridad | Estimación | Asignado a | Status |
|---|------|:---------:|:----------:|-----------|--------|
| 1 | {tarea} | Alta | {horas/puntos} | {nombre} | To Do |
| 2 | {tarea} | Alta | {horas/puntos} | {nombre} | To Do |
| 3 | {tarea} | Media | {horas/puntos} | {nombre} | To Do |

### Capacidad del Equipo
| Persona | Horas Disponibles | Horas Asignadas | Buffer |
|---------|:----------------:|:---------------:|:------:|
| {nombre} | {#} | {#} | {#} |

### Dependencias y Riesgos del Sprint
- {Dependencia/riesgo 1}
- {Dependencia/riesgo 2}

### Definition of Done (para este sprint)
- [ ] Código/modelo completo y funcional
- [ ] Revisado por peer
- [ ] Testeado (QA básico)
- [ ] Documentado (si aplica)
- [ ] Demo-ready para el cliente
```

### 3. Status Report Template (Mensual para Cliente)

```markdown
# Status Report Mensual
## Proyecto: {nombre} | Mes: {mes año}

### Resumen Ejecutivo
{2-3 oraciones: estado general, logros del mes, próximos pasos clave}

### Progreso vs Plan
- **Estado general**: On Track / At Risk / Delayed
- **% Avance total**: {%}
- **Milestones este mes**: {completados} de {planificados}

### Logros del Mes
1. {Logro 1 con detalle}
2. {Logro 2 con detalle}
3. {Logro 3 con detalle}

### Métricas Clave
| Métrica | Target | Actual | Status |
|---------|--------|--------|--------|
| {métrica relevante} | {target} | {actual} | OK / Atención |

### Riesgos y Issues
| Item | Tipo | Impacto | Acción | Owner |
|------|------|---------|--------|-------|
| {item} | Riesgo/Issue | {impacto} | {acción} | {nombre} |

### Plan Próximo Mes
1. {Actividad/milestone 1}
2. {Actividad/milestone 2}
3. {Actividad/milestone 3}

### Decisiones Pendientes del Cliente
| # | Decisión | Impacto si se retrasa | Deadline |
|---|---------|----------------------|----------|
| 1 | {decisión} | {impacto} | {fecha} |

### Presupuesto
| Concepto | Presupuestado | Gastado | Restante |
|----------|:------------:|:------:|:--------:|
| Total | ${total} | ${gastado} | ${restante} |
```

### 4. Post-Mortem Template

```markdown
# Post-Mortem: {Nombre del Proyecto}
## Fecha: {fecha} | Facilitador: {nombre}

### Datos del Proyecto
- **Cliente**: {nombre}
- **Servicio**: {tipo}
- **Duración planificada**: {X semanas}
- **Duración real**: {Y semanas}
- **Presupuesto planificado**: ${X}
- **Costo real**: ${Y}
- **Satisfacción del cliente**: {score /5}

### ¿Qué salió bien?
1. {Aspecto positivo 1}
2. {Aspecto positivo 2}
3. {Aspecto positivo 3}

### ¿Qué no salió bien?
1. {Problema 1}: {qué pasó, por qué, impacto}
2. {Problema 2}: {qué pasó, por qué, impacto}
3. {Problema 3}: {qué pasó, por qué, impacto}

### ¿Qué aprendimos?
1. {Lección 1}: {cómo la aplicaremos en el futuro}
2. {Lección 2}: {cómo la aplicaremos en el futuro}
3. {Lección 3}: {cómo la aplicaremos en el futuro}

### Action Items para Mejorar
| # | Acción | Owner | Deadline | Aplica a |
|---|--------|-------|----------|---------|
| 1 | {acción concreta} | {nombre} | {fecha} | {futuros proyectos / proceso / herramienta} |

### ¿Repetiríamos con este cliente?
{Sí / Sí con condiciones / No — y por qué}
```

---

## Métricas de Gestión de Proyectos

| Métrica | Target | Cómo Medir |
|---------|--------|-----------|
| On-time delivery rate | >90% | % de milestones entregados en fecha |
| Budget adherence | ±10% del presupuesto | Costo real vs presupuestado |
| Client satisfaction | >4.5/5 | Encuesta post-proyecto |
| Scope change rate | <15% | Items agregados vs scope original |
| Defect rate post-delivery | <5% | Bugs/issues reportados en primer mes |
| Sprint velocity consistency | ±15% variación | Story points completados por sprint |
| Team utilization | 70-85% | Horas facturables vs disponibles |
