# Estandares de Entrega Tecnica

> Estandares obligatorios para todos los entregables tecnicos de Meta Build City.
> Aplica a: XR, AI/ML, Blockchain, Marketing Digital, BIM.
> Ultima actualizacion: Febrero 2026

---

## 1. Estandares Generales

### 1.1 Codigo

**Reglas obligatorias para todo codigo entregado**:

| Estandar | Requisito | Herramienta de Verificacion |
|----------|-----------|----------------------------|
| Documentacion | Todas las funciones publicas documentadas (JSDoc, docstrings, Natspec) | Linter rules |
| Testing | >= 80% coverage para critical paths, >= 60% coverage general | Jest, pytest, Hardhat test |
| Version Control | Historial limpio de commits, mensajes descriptivos | Git, GitHub |
| Linting | Codigo pasa linter sin warnings | ESLint, Pylint, Solhint |
| Formatting | Formato consistente segun configuracion del proyecto | Prettier, Black, forge fmt |
| Security | Sin secrets en codigo, dependencias sin vulnerabilidades criticas | GitHub Secret Scanning, Dependabot |
| Type Safety | TypeScript strict mode, Python type hints, Solidity NatSpec | tsc, mypy, solc |

**Branching strategy**:
- `main`: codigo en produccion, protegido
- `develop`: integracion de features (para proyectos grandes)
- `feature/*`: una branch por feature/task
- `hotfix/*`: fixes urgentes en produccion
- Pull Request obligatorio para merge a main/develop
- Minimo 1 reviewer aprobado para merge

**Commit messages**:
```
<type>(<scope>): <description>

[body]

[footer]
```

Tipos: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`, `build`, `ci`

### 1.2 Documentacion

**Documentos obligatorios en todo proyecto**:

| Documento | Contenido | Formato | Responsable |
|-----------|-----------|---------|-------------|
| README.md | Overview, setup, uso, arquitectura | Markdown | Tech Lead |
| ARCHITECTURE.md | Diagramas, decisiones de diseno, componentes | Markdown + diagramas | Tech Lead |
| API.md / OpenAPI spec | Endpoints, parametros, ejemplos | Markdown o Swagger | Backend Dev |
| USER_GUIDE.md | Manual de uso para usuario final | Markdown o PDF | PM + Tech Lead |
| DEPLOYMENT.md | Pasos de deployment, configuracion, variables de entorno | Markdown | DevOps / Dev |
| CHANGELOG.md | Historial de cambios por version | Markdown | Todo el equipo |
| MAINTENANCE.md | Procedimientos de mantenimiento, troubleshooting | Markdown | Tech Lead |

**Estandares de documentacion**:
- Escrita en espanol (con terminos tecnicos en ingles cuando sea estandar de la industria)
- Diagramas en Mermaid (renderizable en GitHub) o draw.io
- Screenshots actualizados con cada release
- Versionada junto al codigo (misma branch)

### 1.3 Paquete de Handoff

**Estructura estandar de entrega**:

```
/[proyecto-nombre]/
|
|-- /src/                    # Codigo fuente completo
|   |-- /frontend/
|   |-- /backend/
|   |-- /contracts/          # (si aplica)
|   |-- /ml/                 # (si aplica)
|
|-- /docs/
|   |-- README.md
|   |-- ARCHITECTURE.md
|   |-- API.md
|   |-- USER_GUIDE.md / USER_GUIDE.pdf
|   |-- DEPLOYMENT.md
|   |-- MAINTENANCE.md
|   |-- CHANGELOG.md
|
|-- /builds/                 # Builds compilados listos para deploy
|   |-- /web/
|   |-- /mobile/
|   |-- /vr/
|
|-- /assets/                 # Assets originales (3D, imagenes, etc.)
|
|-- /config/
|   |-- .env.example         # Template de variables de entorno (SIN valores reales)
|   |-- docker-compose.yml
|   |-- Dockerfile
|
|-- /tests/                  # Suite de tests
|
|-- /scripts/                # Scripts de utilidad (deployment, migration, etc.)
|
|-- CREDENTIALS.md           # Instrucciones para acceder a credenciales (via 1Password/vault)
```

**Entrega de credenciales**:
- NUNCA en archivos de texto plano o email
- Via 1Password vault compartido con el cliente
- O transferencia presencial con instrucciones de rotacion
- Documentar que credenciales existen y donde estan (sin los valores)

---

## 2. Estandares por Linea de Servicio

### 2.1 XR (Extended Reality)

**Entregables obligatorios**:

| Entregable | Formato | Descripcion |
|------------|---------|-------------|
| Builds optimizados | APK (Quest), HTML5 (Web), EXE (Desktop) | Un build por plataforma target |
| Proyecto fuente | Unity Project / Unreal Project completo | Listo para abrir y compilar |
| Asset library | FBX, textures (PNG/JPG), materials | Organizados por categoria |
| Deployment guide | Markdown / PDF | Pasos para desplegar en cada plataforma |
| Performance report | PDF / Spreadsheet | FPS, load times, file sizes por plataforma |
| User manual | PDF | Guia para el usuario final de la experiencia |

**Requisitos tecnicos de builds**:

| Plataforma | Frame Rate Min | Load Time Max | File Size Max | Formato |
|------------|---------------|---------------|---------------|---------|
| Meta Quest 3 | 72 FPS (P95) | 15 segundos | 2 GB | APK |
| Web (desktop) | 60 FPS (P95) | 10 segundos | 100 MB (initial) | HTML5 + assets |
| Web (mobile) | 30 FPS (P95) | 15 segundos | 50 MB (initial) | HTML5 + assets |
| Desktop VR | 90 FPS (P95) | 10 segundos | 10 GB | EXE + data |
| Pixel Streaming | 60 FPS (server) | 5 seg (stream start) | N/A | Server deployment |

**Requisitos de proyecto fuente**:
- Compila sin errores en la version del engine especificada
- Estructura de carpetas organizada y documentada
- Assets no utilizados eliminados (clean project)
- Scripts comentados en funciones principales
- README dentro del proyecto con instrucciones de build

### 2.2 AI/ML (Inteligencia Artificial)

**Entregables obligatorios**:

| Entregable | Formato | Descripcion |
|------------|---------|-------------|
| Modelos entrenados | .pt (PyTorch), .onnx, .tflite | Modelo listo para inference |
| Training data documentation | Markdown + JSON | Descripcion del dataset, split, augmentations |
| API endpoints | FastAPI + OpenAPI spec | Documentacion de endpoints de inference |
| Monitoring setup | Dashboard config + alertas | Dashboards y alertas configuradas |
| Retraining guide | Markdown | Pasos para reentrenar con nuevos datos |
| Model card | Markdown (template estandar) | Metricas, limitaciones, sesgos, datos de training |
| Evaluation report | PDF / Markdown | Metricas detalladas en test set |

**Model Card (template obligatorio)**:

```markdown
# Model Card: [Nombre del Modelo]

## Overview
- Tipo: [Object Detection / Classification / Regression / NLP]
- Arquitectura: [YOLOv8m / XGBoost / etc.]
- Version: [v1.2.0]
- Fecha de training: [2026-02-01]

## Intended Use
- Proposito: [Deteccion de EPP en obras de construccion]
- Usuarios: [Prevencionistas de riesgo, supervisores de obra]
- Limitaciones: [No funciona en condiciones de poca luz, no detecta EPP parcialmente oculto]

## Training Data
- Dataset: [construction_safety_v3]
- Tamano: [15,000 imagenes]
- Fuentes: [Obras en Santiago y Valparaiso, 2024-2026]
- Etiquetado: [Label Studio, 3 anotadores, inter-annotator agreement 0.85]
- Sesgo conocido: [Mayoría de imagenes diurnas, sub-representacion de obras nocturnas]

## Metrics (Test Set)
- mAP@0.5: 0.87
- Precision: 0.89
- Recall: 0.84
- Inference time: 20ms (GPU), 150ms (CPU)

## Ethical Considerations
- Imagenes anonimizadas (rostros blurred)
- No se utiliza para identificacion individual
- Resultados deben ser validados por humano
```

**Requisitos de API**:
- Documentacion OpenAPI completa y actualizada
- Rate limiting configurado
- Authentication (API key o OAuth2)
- Error handling estandarizado (codigos HTTP + mensajes claros)
- Health check endpoint (/health)
- Version endpoint (/version)
- Logging de requests (sin datos sensibles)

### 2.3 Blockchain

**Entregables obligatorios**:

| Entregable | Formato | Descripcion |
|------------|---------|-------------|
| Contratos auditados | .sol + ABI JSON | Codigo fuente + ABI compilado |
| Deployment scripts | TypeScript (Hardhat) | Scripts reproducibles de deployment |
| Block explorer verification | Link verificado | Contrato verificado en Etherscan/Polygonscan |
| Admin keys handoff | 1Password vault | Multi-sig setup, owner keys |
| Subgraph (si aplica) | GraphQL schema + mappings | Subgraph deployado en The Graph |
| Frontend dApp | Next.js build | Interfaz web para interactuar con contratos |
| Audit report | PDF | Resultados de auditoria (interna o externa) |

**Requisitos de smart contracts**:
- Codigo verificado en block explorer
- Tests con >= 95% coverage
- Slither report: 0 high/medium findings
- Natspec documentation completa
- Emergency pause implementado
- Multi-sig para funciones admin
- Eventos para todos los cambios de estado

**Deployment documentation**:
```markdown
# Deployment Record

## Contracts

| Contract | Network | Address | Tx Hash | Block |
|----------|---------|---------|---------|-------|
| MilestonePayment (Proxy) | Polygon | 0x1234...abcd | 0xabcd...1234 | 45678901 |
| MilestonePayment (Impl) | Polygon | 0x5678...efgh | 0xefgh...5678 | 45678900 |

## Admin Roles

| Role | Address | Type | Description |
|------|---------|------|-------------|
| DEFAULT_ADMIN | 0xABCD...1234 | Gnosis Safe (2/3) | Admin principal |
| PAUSER | 0xEFGH...5678 | EOA | Emergency pause |
| OPERATOR | 0xIJKL...9012 | Backend service | Oracle updates |

## Verification

All contracts verified on Polygonscan:
- [MilestonePayment Proxy](https://polygonscan.com/address/0x1234...abcd#code)
- [MilestonePayment Implementation](https://polygonscan.com/address/0x5678...efgh#code)
```

### 2.4 Marketing Digital

**Entregables obligatorios**:

| Entregable | Formato | Descripcion |
|------------|---------|-------------|
| Brand assets | AI/SVG + PNG | Logos, paleta de colores, tipografias |
| Campaign configurations | Export de plataforma | Configuraciones de Google Ads, LinkedIn Ads, Meta Ads |
| Analytics setup | Documentacion + accesos | GA4, Hotjar, Mixpanel configurados |
| Content calendar | Notion / Spreadsheet | Planificacion de contenido 3+ meses |
| Performance report | PDF / Dashboard | Metricas de campanas, ROI, recomendaciones |
| SEO audit | PDF | Estado actual, keywords, recomendaciones |
| Social media assets | Canva templates + exports | Templates de marca para redes sociales |

**Requisitos de analytics**:
- Google Analytics 4 configurado con eventos custom
- Conversion tracking para formularios y CTAs
- UTM parameters estandarizados para todas las campanas
- Dashboard de metricas clave (Google Looker Studio o custom)
- Reportes mensuales automatizados

**Estructura de campana documentada**:
```markdown
# Campana: [Nombre]

## Objetivo
[Brand awareness / Lead generation / Conversions]

## Plataformas
- Google Ads: [Search / Display / YouTube]
- LinkedIn Ads: [Sponsored Content / InMail]
- Meta Ads: [Feed / Stories / Reels]

## Presupuesto
- Total: $X USD/mes
- Distribucion: Google X%, LinkedIn X%, Meta X%

## Targeting
- Audiencia: [descripcion detallada]
- Geolocalizacion: [Chile / Santiago / etc.]
- Exclusiones: [competidores, etc.]

## Metricas Target
- CPL: < $X USD
- CTR: > X%
- Conversion Rate: > X%

## Assets
- [link a carpeta de creatividades]
- [link a landing pages]
```

### 2.5 BIM (Building Information Modeling)

**Entregables obligatorios**:

| Entregable | Formato | Descripcion |
|------------|---------|-------------|
| Archivos nativos | .rvt (Revit) / .pln (ArchiCAD) | Modelos en formato nativo del software |
| Exportacion IFC | .ifc (IFC 4.0) | Modelo en formato abierto estandar |
| Model documentation | PDF / Markdown | Estructura del modelo, familias, parametros |
| Clash reports | HTML / PDF (Navisworks) | Reportes de deteccion de interferencias |
| Coordination logs | Spreadsheet / Notion | Registro de reuniones de coordinacion y resoluciones |
| LOD specification | PDF | Nivel de desarrollo por disciplina y etapa |
| BIM Execution Plan (BEP) | PDF | Plan de ejecucion BIM del proyecto |

**Requisitos de modelos BIM**:

| Requisito | Estandar | Verificacion |
|-----------|----------|-------------|
| Formato IFC | IFC 4.0 (ISO 16739-1:2018) | IFC validator (buildingSMART) |
| Clasificacion | OmniClass o Uniformat | Verificar en model checker |
| Parametros | Segun BEP del proyecto | Checklist de parametros |
| Coordenadas | Punto base del proyecto documentado | Verificar en coordinacion |
| Niveles | Nomenclatura estandar (N+XX o como BEP) | Verificar en modelo |
| Familias | Parametricas, bien nombradas | Review manual |
| Warnings | 0 warnings criticos en Revit | Revisar lista de warnings |
| File size | Optimizado (purgar elementos no usados) | Audit del modelo |

**Compliance con PlanBIM Chile**:
- Roles y responsabilidades BIM definidos
- BEP alineado con estandar PlanBIM
- Entregables segun lo definido en Solicitud de Informacion (SDI)
- Clasificacion segun sistema adoptado (OmniClass preferido)
- Niveles de informacion segun tabla de NDI de PlanBIM

**Clash Detection Report (template)**:
```markdown
# Reporte de Interferencias - [Proyecto] - [Fecha]

## Resumen

| Disciplinas | Clashes Detectados | Resueltos | Pendientes | Nuevos |
|-------------|-------------------|-----------|------------|--------|
| EST vs MEP | 45 | 38 | 5 | 2 |
| ARQ vs EST | 12 | 12 | 0 | 0 |
| MEP vs MEP | 23 | 15 | 6 | 2 |
| **Total** | **80** | **65** | **11** | **4** |

## Clashes Pendientes (Detalle)

### CL-001: Ducto HVAC vs Viga nivel 3
- **Disciplinas**: Mecanica vs Estructura
- **Ubicacion**: Eje C-3, Nivel 3
- **Severidad**: Alta
- **Responsable**: Ing. Mecanico
- **Plazo**: 2026-02-20
- **Imagen**: [screenshot]
- **Propuesta de solucion**: Rerouting de ducto por debajo de viga
```

---

## 3. Quality Gates

### Gate 1: Design Review

**Cuando**: Al finalizar la fase de diseno/arquitectura, antes de iniciar desarrollo.

**Criterios de aprobacion**:

| Criterio | Verificador | Artefacto |
|----------|-------------|-----------|
| Arquitectura tecnica documentada | Tech Lead | ARCHITECTURE.md + diagramas |
| Stack tecnologico justificado | Tech Lead | Decision records |
| Estimacion de esfuerzo validada | PM + Tech Lead | Timeline + resource plan |
| Riesgos tecnicos identificados | Tech Lead | Risk register |
| Mockups/wireframes aprobados | Cliente | Figma / Miro boards |
| BEP aprobado (si BIM) | BIM Manager | BIM Execution Plan |
| Scope of Work firmado | PM | SoW document |

**Proceso**:
1. Tech Lead presenta arquitectura al equipo
2. Peer review interno (1-2 horas)
3. Ajustes basados en feedback
4. Presentacion al cliente (simplificada)
5. Sign-off del cliente en enfoque tecnico

### Gate 2: Development Review

**Cuando**: Al completar el desarrollo core (antes de QA formal).

**Criterios de aprobacion**:

| Criterio | Verificador | Metrica |
|----------|-------------|---------|
| Code review completado | Peer developer | 100% PRs revisados |
| Unit tests pasan | CI/CD (GitHub Actions) | 0 failures |
| Integration tests pasan | CI/CD | 0 failures |
| Coverage minimo alcanzado | CI/CD | >= 80% critical, >= 60% general |
| Linting sin errores | CI/CD | 0 errors |
| Build exitoso en todas las plataformas | CI/CD | Builds generados |
| Performance benchmarks iniciales | Developer | Dentro de targets |
| API documentation actualizada | Backend Dev | OpenAPI spec up to date |

### Gate 3: Testing / QA

**Cuando**: Al completar QA interno, antes de entregar al cliente para UAT.

**Criterios de aprobacion**:

| Criterio | Verificador | Metrica |
|----------|-------------|---------|
| QA checklist completado | QA Engineer | 100% items verificados |
| 0 bugs criticos | QA Engineer | Bug tracker limpio |
| 0 bugs high severity | QA Engineer | Bug tracker limpio |
| Performance benchmarks cumplidos | QA Engineer | Dentro de targets por plataforma |
| Security review completada | Tech Lead | Checklist de seguridad aprobado |
| Cross-platform testing | QA Engineer | Testeado en todos los targets |
| Accessibility verificada | QA Engineer | Checklist de accesibilidad |
| Regression testing (si update) | QA Engineer | No regresiones detectadas |

**QA Checklist generico**:
- [ ] Funcionalidad: todas las features funcionan segun spec
- [ ] Compatibilidad: funciona en todos los dispositivos/browsers target
- [ ] Performance: FPS, load time, memoria dentro de limites
- [ ] Usabilidad: flujos intuitivos, feedback claro al usuario
- [ ] Error handling: errores manejados gracefully, mensajes claros
- [ ] Data integrity: datos se guardan y recuperan correctamente
- [ ] Security: autenticacion, autorizacion, input validation
- [ ] Edge cases: comportamiento correcto con datos vacios, extremos, invalidos
- [ ] Localizacion: textos correctos en todos los idiomas soportados
- [ ] Offline behavior: comportamiento correcto sin conectividad (si aplica)

### Gate 4: Staging / UAT

**Cuando**: Cliente realiza User Acceptance Testing en ambiente de staging.

**Criterios de aprobacion**:

| Criterio | Verificador | Artefacto |
|----------|-------------|-----------|
| Deploy en staging exitoso | DevOps / Dev | URL/build de staging funcionando |
| Demo al cliente completada | PM | Minuta de reunion |
| Feedback del cliente recopilado | PM | Lista de feedback items |
| Feedback incorporado | Dev team | PRs merged |
| Re-test de items de feedback | QA | Verificacion de fixes |
| Sign-off del cliente | Cliente | Email / documento firmado |

**Proceso de UAT**:
1. PM coordina sesion de UAT con cliente (presencial o remoto)
2. Cliente prueba la experiencia siguiendo script de testing
3. Cliente documenta feedback (PM facilita)
4. Equipo prioriza feedback: must-fix vs nice-to-have vs future
5. Implementar must-fix items
6. Re-demo al cliente
7. Obtener sign-off formal

### Gate 5: Production / Go-Live

**Cuando**: Deployment final a produccion y handoff al cliente.

**Criterios de aprobacion**:

| Criterio | Verificador | Artefacto |
|----------|-------------|-----------|
| Deployment checklist completado | DevOps / Dev | Checklist firmado |
| Monitoring configurado y funcionando | DevOps | Dashboard de monitoring |
| Alertas configuradas | DevOps | Alert rules activas |
| Backup configurado | DevOps | Backup schedule verificado |
| Documentacion completa | Tech Lead | Todos los docs del paquete de handoff |
| Training del cliente completado | PM + Tech Lead | Sesion realizada, materiales entregados |
| Credenciales transferidas | Tech Lead | Via vault seguro |
| SLA acordado | PM | Documento de SLA firmado |
| Post-mortem programado | PM | Fecha agendada (2-4 semanas post-launch) |

**Deployment Checklist**:
- [ ] Backup de estado actual de produccion (si es update)
- [ ] Variables de entorno configuradas
- [ ] Base de datos migrada (si aplica)
- [ ] SSL/TLS configurado y verificado
- [ ] DNS apuntando correctamente
- [ ] CDN configurado y cacheando correctamente
- [ ] Health check endpoints respondiendo
- [ ] Logs fluyendo a sistema de monitoring
- [ ] Alertas disparando correctamente (test alert)
- [ ] Rollback plan documentado y testeado
- [ ] Performance verificada en produccion
- [ ] Smoke tests pasando en produccion

---

## 4. Review Process

### 4.1 Peer Review para Codigo

**Reglas de code review**:
- Todo codigo pasa por Pull Request (no direct push a main/develop)
- Minimo 1 reviewer aprobado (2 para cambios criticos)
- Reviewer no puede ser el autor del PR
- PR debe tener descripcion clara del cambio y por que
- CI/CD debe pasar antes de merge (tests, linting, build)
- Resolver todos los comentarios antes de merge (o marcar como "won't fix" con justificacion)

**Que revisar**:
1. **Correctitud**: el codigo hace lo que dice que hace?
2. **Legibilidad**: es facil de entender? nombres claros? comentarios donde necesarios?
3. **Mantenibilidad**: sera facil de modificar en el futuro? DRY? SOLID?
4. **Performance**: hay bottlenecks obvios? queries N+1? loops innecesarios?
5. **Security**: input validation? SQL injection? XSS? secrets hardcoded?
6. **Testing**: los tests cubren los casos importantes? edge cases?
7. **Documentation**: funciones publicas documentadas? README actualizado?

### 4.2 Technical Lead Approval

**Requiere aprobacion del Tech Lead**:
- Cambios de arquitectura (nueva dependencia, nuevo servicio, cambio de patron)
- Cambios de infraestructura (nuevo servicio cloud, cambio de config)
- Cambios de schema de base de datos
- Nuevos endpoints publicos
- Cambios en smart contracts (cualquier cambio)
- Cambios que afectan performance significativamente
- Cambios de seguridad (autenticacion, autorizacion, encriptacion)

**Proceso**:
1. Developer crea PR con tag `needs-architecture-review`
2. Tech Lead revisa dentro de 24 horas laborales
3. Si aprobado, merge normal
4. Si requiere cambios, feedback detallado en PR
5. Si requiere discusion, agendar meeting de 30 minutos

### 4.3 Client Sign-off

**Puntos de sign-off del cliente**:

| Punto | Documento | Metodo |
|-------|-----------|--------|
| Scope of Work | SoW firmado | Firma digital (DocuSign / HelloSign) |
| Design approval (Gate 1) | Email de aprobacion | Email del contacto designado |
| UAT approval (Gate 4) | Acta de recepcion parcial | Firma digital |
| Final delivery (Gate 5) | Acta de recepcion final | Firma digital |
| SLA agreement | Contrato de soporte | Firma digital |

### 4.4 Post-Mortem

**Se realiza para TODOS los proyectos** (2-4 semanas despues del go-live).

**Agenda del post-mortem** (1-2 horas):

1. **Timeline review** (15 min):
   - Planificado vs real (tiempo, costo)
   - Milestones: on-time, delayed, why?

2. **What went well** (20 min):
   - Tecnologias que funcionaron
   - Procesos que ayudaron
   - Colaboracion efectiva

3. **What didn't go well** (20 min):
   - Problemas tecnicos enfrentados
   - Proceso que falto
   - Comunicacion que fallo
   - Scope creep

4. **Lessons learned** (15 min):
   - Que hariamos diferente?
   - Que debemos mantener?
   - Que debemos mejorar?

5. **Action items** (10 min):
   - Acciones concretas para mejorar
   - Responsables y deadlines
   - Updates a templates/procesos/documentacion

**Documento de post-mortem**:
- Guardado en Notion, base de datos de post-mortems
- Accesible a todo el equipo
- Referenciado en proyectos futuros similares
- Revisado trimestralmente para identificar patrones

---

## 5. SLA Standards

### 5.1 Tiempos de Respuesta

| Canal | Tiempo de Primera Respuesta | Horario |
|-------|----------------------------|---------|
| Email | 24 horas habiles | Lunes a Viernes, 9:00-18:00 CLT |
| Slack (canal de soporte) | 4 horas habiles | Lunes a Viernes, 9:00-18:00 CLT |
| Telefono (emergencia) | 1 hora | 24/7 (solo para incidentes criticos) |
| Ticket (Linear) | 24 horas habiles | Lunes a Viernes, 9:00-18:00 CLT |

### 5.2 Tiempos de Resolucion de Bugs

| Severidad | Descripcion | Tiempo de Resolucion | Ejemplo |
|-----------|-------------|---------------------|---------|
| **Critico** | Sistema caido, data loss, security breach | 24 horas | App no carga, datos comprometidos |
| **Alto** | Feature principal no funciona, workaround no disponible | 48 horas | Pagos no procesan, login falla |
| **Medio** | Feature secundaria no funciona, workaround disponible | 1 semana (5 dias habiles) | Reporte no exporta, filtro no funciona |
| **Bajo** | Issue cosmetico, mejora menor | Siguiente sprint (2-4 semanas) | Typo en UI, alineacion de elementos |

**Proceso de escalamiento**:
1. Bug reportado por cliente (email/Slack/ticket)
2. PM clasifica severidad (dentro de 4 horas)
3. Dev asignado (dentro de 2 horas de clasificacion)
4. Fix desarrollado, testeado, deployado
5. Cliente notificado de resolucion
6. Verificacion de fix por cliente
7. Ticket cerrado

### 5.3 Uptime

**Para soluciones hospedadas por MBC**:

| Servicio | Uptime Target | Downtime Max/Mes | Monitoreo |
|----------|---------------|-------------------|-----------|
| Web apps | 99.5% | 3.6 horas | Uptime Robot + CloudWatch |
| APIs | 99.5% | 3.6 horas | Health checks cada 1 min |
| VR streaming | 99.0% | 7.3 horas | Custom monitoring |
| Dashboards | 99.0% | 7.3 horas | Uptime Robot |
| Chatbots | 99.9% | 43 minutos | Health checks + alertas |

**Exclusiones de SLA**:
- Mantenimiento programado (notificado con 48 horas de anticipacion)
- Force majeure (desastres naturales, ataques DDoS masivos)
- Issues causados por terceros (AWS outage, API de WhatsApp down)
- Cambios realizados por el cliente sin coordinacion con MBC

**Compensacion por incumplimiento de SLA**:
- 99.0%-99.5%: credito del 10% de la tarifa mensual de hosting
- 98.0%-99.0%: credito del 25% de la tarifa mensual
- <98.0%: credito del 50% de la tarifa mensual
- Credito maximo: 50% de la tarifa mensual
- Aplicable solo a downtime no excluido

### 5.4 Mantenimiento Programado

**Calendario de mantenimiento**:

| Tipo | Frecuencia | Ventana | Contenido |
|------|-----------|---------|-----------|
| Updates menores | Mensual | Martes 22:00-02:00 CLT | Patches de seguridad, bug fixes, minor updates |
| Updates mayores | Trimestral | Sabado 22:00-06:00 CLT | Feature updates, dependency upgrades, DB migrations |
| Security patches | As needed (criticos: 24h) | ASAP | Vulnerabilidades criticas |
| Infrastructure | Semestral | Sabado 22:00-06:00 CLT | OS updates, scaling, optimization |

**Proceso de mantenimiento**:
1. Notificacion al cliente 48 horas antes (updates mayores: 1 semana)
2. Backup completo antes de iniciar
3. Ejecutar actualizaciones en staging primero
4. Verificar en staging
5. Ejecutar en produccion
6. Smoke tests post-actualizacion
7. Notificacion de completitud al cliente
8. Monitoreo intensivo por 24 horas post-update

### 5.5 End of Support

**Cuando un proyecto sale de soporte activo**:
1. Notificacion 90 dias antes del fin de soporte
2. Handoff completo de conocimiento al equipo del cliente (o nuevo proveedor)
3. Documentacion actualizada y entregada
4. Credenciales rotadas y transferidas
5. Desactivacion de accesos MBC a sistemas del cliente
6. Periodo de gracia de 30 dias para consultas post-handoff
7. Archivado del proyecto en sistemas internos de MBC

---

## 6. Templates y Checklists

### 6.1 Template de Inicio de Proyecto

```markdown
# [Nombre del Proyecto] - Kickoff

## Informacion General
- Cliente: [nombre]
- Contacto principal: [nombre, email, telefono]
- Tipo de proyecto: [XR / AI / Blockchain / Marketing / BIM / Mixto]
- Fecha de inicio: [YYYY-MM-DD]
- Fecha estimada de entrega: [YYYY-MM-DD]
- Presupuesto: [USD/UF]

## Equipo MBC
- PM: [nombre]
- Tech Lead: [nombre]
- Developers: [nombres]
- QA: [nombre]

## Repositorios
- GitHub: [URL]
- Notion: [URL del workspace del proyecto]
- Figma: [URL]

## Ambientes
- Development: [URL]
- Staging: [URL]
- Production: [URL]

## Canales de Comunicacion
- Slack: [canal]
- Reuniones: [frecuencia, dia, hora]

## Quality Gates Programados
- Gate 1 (Design): [fecha]
- Gate 2 (Development): [fecha]
- Gate 3 (Testing): [fecha]
- Gate 4 (UAT): [fecha]
- Gate 5 (Production): [fecha]
```

### 6.2 Checklist de Cierre de Proyecto

- [ ] Todos los quality gates aprobados
- [ ] Acta de recepcion firmada por el cliente
- [ ] Paquete de handoff completo y entregado
- [ ] Credenciales transferidas de forma segura
- [ ] Training del cliente completado
- [ ] SLA definido y firmado (si aplica soporte post-entrega)
- [ ] Post-mortem realizado
- [ ] Lecciones aprendidas documentadas
- [ ] Proyecto archivado en sistemas internos
- [ ] Facturacion final emitida
- [ ] Feedback del cliente recopilado (NPS/CSAT)

---

*Este documento es la referencia de calidad de Meta Build City. Se revisa y actualiza semestralmente. Responsable: CTO + Tech Leads de cada vertical.*
