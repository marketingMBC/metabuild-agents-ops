# Stack Tecnologico de Meta Build City

> Documento maestro de tecnologias, frameworks y herramientas utilizadas por MBC.
> Ultima actualizacion: Febrero 2026

---

## 1. Desarrollo XR (Extended Reality)

### Game Engines

| Motor | Lenguaje | Uso Principal | Version |
|-------|----------|---------------|---------|
| Unity | C# | Recorridos virtuales, apps mobile AR, WebGL | 2023 LTS / 6000.x |
| Unreal Engine 5 | C++ / Blueprints | Visualizaciones de alta fidelidad, Pixel Streaming | 5.4+ |

**Criterio de seleccion**: Unity se prefiere para proyectos mobile/web y ciclos rapidos de desarrollo. Unreal Engine se utiliza cuando el cliente requiere calidad visual cinematografica o streaming remoto.

### WebXR

| Framework | Proposito | Notas |
|-----------|-----------|-------|
| Three.js | Renderizado 3D en navegador, base para viewers customizados | Maximo control, mayor complejidad |
| A-Frame | Prototipos rapidos WebXR, experiencias simples | Declarativo (HTML-like), ideal para demos |
| Babylon.js | Alternativa a Three.js con mejor soporte de physics | Buen soporte de PBR materials |

**Nota**: Para recorridos web se prioriza Three.js con React Three Fiber (R3F) para integracion con Next.js.

### Hardware Soportado

| Dispositivo | Tipo | Uso en MBC |
|-------------|------|------------|
| Meta Quest 3 | VR standalone | Recorridos inmobiliarios, training VR |
| Apple Vision Pro | Mixed Reality | Demostraciones premium, AR overlays |
| HTC Vive Pro 2 | VR tethered | Showrooms, presentaciones en oficina |
| HoloLens 2 | AR enterprise | Overlays en obra, inspecciones BIM |
| Mobile AR (iOS/Android) | AR mobile | Apps de visualizacion para compradores |

### Herramientas 3D

- **Blender 4.x**: modelado, UV mapping, baking de texturas. Herramienta principal open-source.
- **3ds Max**: cuando el cliente entrega archivos nativos de 3ds Max o se requiere interoperabilidad con Revit.
- **SketchUp**: importacion de modelos simples de arquitectos que trabajan en SketchUp.
- **Cinema 4D**: motion graphics y visualizaciones de marketing.
- **Substance Painter/Designer**: creacion de materiales PBR para real-time rendering.

### Scanning y Captura

| Herramienta | Tecnologia | Uso |
|-------------|-----------|-----|
| Matterport Pro3 | Structured light + LiDAR | Gemelos digitales de espacios existentes |
| LiDAR (iPhone 15 Pro / iPad Pro) | LiDAR nativo Apple | Captura rapida en terreno, point clouds |
| Polycam | Photogrammetry + LiDAR | Escaneo de objetos y espacios pequenos |
| Leica BLK360 | Laser scanning | Point clouds de alta precision para BIM |

### Streaming Remoto

- **Pixel Streaming (Unreal)**: renderizado en servidor GPU (AWS g5 instances), streaming via WebRTC al navegador del cliente. Ideal para visualizaciones pesadas sin descargar app.
- **Unity Render Streaming**: alternativa para proyectos Unity. Menor calidad que Pixel Streaming pero mas facil de configurar.
- **Infraestructura**: AWS EC2 g5.xlarge (1x NVIDIA A10G), auto-scaling basado en sesiones activas.

---

## 2. Inteligencia Artificial

### Lenguajes

| Lenguaje | Version | Uso |
|----------|---------|-----|
| Python | 3.10+ | ML training, data processing, backend AI services |
| TypeScript | 5.x | APIs REST, integraciones, frontend de dashboards |

### ML Frameworks

| Framework | Uso Principal | Notas |
|-----------|---------------|-------|
| PyTorch | Training de modelos custom (vision, NLP) | Preferido para investigacion y modelos custom |
| TensorFlow / TF Lite | Deployment en edge, modelos legacy | Usado para modelos en NVIDIA Jetson |
| scikit-learn | Modelos clasicos (regression, classification) | Analisis predictivo, feature engineering |
| XGBoost / LightGBM | Gradient boosting para datos tabulares | Prediccion de costos, scheduling |

### Computer Vision

| Herramienta | Uso en Construccion |
|-------------|---------------------|
| OpenCV | Preprocessing de imagenes, calibracion de camaras |
| YOLOv8 (Ultralytics) | Deteccion de objetos: trabajadores, EPP, equipos, materiales |
| Detectron2 | Segmentacion de instancias, analisis de progreso |
| Custom Models | Modelos fine-tuned con datos de obras chilenas |
| SAM (Segment Anything) | Segmentacion zero-shot para analisis rapido |

### NLP / LLM

| Herramienta | Uso |
|-------------|-----|
| LangChain | Orquestacion de pipelines RAG, chains, agents |
| Claude API (Anthropic) | Generacion de texto, analisis de documentos, chatbots |
| OpenAI API | GPT-4 como alternativa, embeddings (text-embedding-3) |
| Hugging Face | Modelos open-source, fine-tuning, inference API |
| ChromaDB / Pinecone | Vector stores para RAG |

### MLOps

| Herramienta | Funcion |
|-------------|---------|
| MLflow | Model registry, experiment tracking, model serving |
| DVC (Data Version Control) | Versionado de datasets y modelos |
| Weights & Biases | Experiment tracking visual, hyperparameter sweeps |
| Label Studio | Etiquetado de datos (imagenes de obra, documentos) |

### APIs y Data Processing

- **FastAPI**: API principal para servicios de AI. Async, auto-documentacion OpenAPI, validacion con Pydantic.
- **Flask**: APIs legacy o microservicios simples.
- **pandas / polars**: procesamiento de datos tabulares. polars para datasets grandes (>1GB).
- **Apache Spark**: procesamiento distribuido para datasets masivos (rare, solo en proyectos enterprise).
- **Celery + Redis**: procesamiento asincrono de tareas pesadas (training, batch inference).

---

## 3. Blockchain

### Networks

| Red | Tipo | Uso en MBC | Gas Estimado |
|-----|------|------------|--------------|
| Polygon PoS | L2 Ethereum | Red principal para contratos productivos | ~$0.01 USD/tx |
| Ethereum Mainnet | L1 | Activos de alto valor, tokenizacion inmobiliaria | ~$2-10 USD/tx |
| Arbitrum One | L2 Ethereum | Alternativa a Polygon para DeFi integrations | ~$0.05 USD/tx |
| Sepolia | Testnet L1 | Testing de contratos | Gratis |
| Mumbai / Amoy | Testnet L2 | Testing en Polygon | Gratis |

### Smart Contracts

| Herramienta | Funcion |
|-------------|---------|
| Solidity 0.8.x | Lenguaje principal de smart contracts |
| Hardhat | Framework de desarrollo, testing, deployment |
| Foundry (forge/cast) | Testing avanzado, fuzzing, gas profiling |
| OpenZeppelin Contracts | Libreria de contratos auditados (ERC-20, ERC-721, ERC-1155, Access Control) |

### Frontend Web3

| Herramienta | Funcion |
|-------------|---------|
| ethers.js v6 | Interaccion con blockchain desde frontend/backend |
| wagmi v2 | React hooks para Ethereum |
| RainbowKit | UI de conexion de wallet (MetaMask, WalletConnect) |
| viem | Alternativa moderna a ethers.js, tipado fuerte |

### Storage Descentralizado

| Herramienta | Uso |
|-------------|-----|
| IPFS (via Pinata) | Almacenamiento de documentos, imagenes, metadata NFT |
| Arweave | Almacenamiento permanente para certificados y registros criticos |

### Indexing y Querying

- **The Graph**: subgraphs custom para indexar eventos de contratos (pagos, trazabilidad, certificaciones).
- **Alchemy Enhanced APIs**: consultas rapidas de balance, transacciones, NFTs.

### Standards Implementados

| Standard | Uso en Construccion |
|----------|---------------------|
| ERC-20 | Tokens de utilidad para ecosistema MBC (futuro) |
| ERC-721 | Certificaciones unicas, licencias |
| ERC-1155 | Propiedad fraccionada, materiales trazables (multi-token) |
| ERC-4626 | Vaults para tokenizacion inmobiliaria (futuro) |

---

## 4. BIM (Building Information Modeling)

### Modelado

| Software | Version | Uso |
|----------|---------|-----|
| Autodesk Revit | 2024 / 2025 | Modelado BIM principal, familias parametricas |
| ArchiCAD | 27 | Alternativa a Revit, interoperabilidad IFC |
| Rhino + Grasshopper | 8 | Diseno parametrico, geometrias complejas |

### Coordinacion

| Software | Funcion |
|----------|---------|
| Navisworks Manage | Deteccion de interferencias (clash detection), 4D simulation |
| Solibri Model Checker | Validacion de modelos IFC, reglas de calidad |
| BIMcollab | Gestion de issues/BCF entre disciplinas |

### Plataformas Cloud

| Plataforma | Uso |
|------------|-----|
| Autodesk Construction Cloud (ACC) | Colaboracion, Document Management, Model Coordination |
| BIM 360 | Proyectos legacy, field management |
| Trimble Connect | Alternativa para clientes que usan Tekla |

### Automatizacion BIM

| Herramienta | Lenguaje | Uso |
|-------------|----------|-----|
| Dynamo | Visual programming / Python | Automatizacion dentro de Revit |
| pyRevit | Python / C# | Scripts y addins para Revit |
| Grasshopper | Visual programming | Diseno generativo en Rhino |
| Speckle | API | Interoperabilidad y automatizacion entre herramientas BIM |

### Viewers y Herramientas Web

| Herramienta | Uso |
|-------------|-----|
| IFC.js (That Open Company) | Viewer IFC en navegador, integrable en apps custom |
| xBIM | Toolkit .NET para procesamiento de IFC |
| BIMserver | Servidor open-source para modelos IFC |
| Forge Viewer (ACC) | Viewer embebido de Autodesk |

### Standards y Normativas

| Standard | Descripcion |
|----------|-------------|
| IFC 4.0 (ISO 16739) | Formato abierto de intercambio BIM |
| ISO 19650 | Gestion de informacion con BIM |
| PlanBIM Chile | Framework nacional chileno para implementacion BIM |
| LOD 100-500 | Niveles de desarrollo/detalle de modelos |
| BCF (BIM Collaboration Format) | Formato para comunicacion de issues entre herramientas |

---

## 5. Marketing / Growth

### CRM y Automatizacion

| Herramienta | Uso | Tier |
|-------------|-----|------|
| HubSpot | CRM, pipeline de ventas, email sequences | Free / Starter |
| Notion | CRM complementario, base de datos de leads | Team |

### Email Marketing

| Herramienta | Uso |
|-------------|-----|
| Mailchimp | Newsletters, campanas de email masivas |
| SendGrid | Emails transaccionales (notificaciones, reportes) |

### Analytics

| Herramienta | Uso |
|-------------|-----|
| Google Analytics 4 | Trafico web, conversiones, atribucion |
| Hotjar | Heatmaps, session recordings, feedback widgets |
| Mixpanel | Eventos de producto, funnels, retention |

### SEO

| Herramienta | Uso |
|-------------|-----|
| SEMrush | Keyword research, auditorias SEO, tracking de posiciones |
| Ahrefs | Analisis de backlinks, keyword gap analysis |
| Google Search Console | Monitoreo de indexacion, rendimiento en busqueda |

### Social Media y Ads

| Herramienta | Uso |
|-------------|-----|
| LinkedIn Sales Navigator | Prospeccion B2B, InMail campaigns |
| Buffer | Programacion de contenido social |
| Canva Pro | Diseno de contenido visual, templates de marca |
| Google Ads | SEM, display ads, remarketing |
| LinkedIn Ads | B2B advertising, lead gen forms |
| Meta Ads (FB/IG) | Campanas inmobiliarias, awareness |

### Video y Contenido

| Herramienta | Uso |
|-------------|-----|
| DaVinci Resolve | Edicion de video, color grading |
| After Effects | Motion graphics, animaciones de marca |
| Premiere Pro | Edicion de video (alternativa) |
| Midjourney / DALL-E | Generacion de conceptos visuales para presentaciones |

---

## 6. Infraestructura

### Cloud Providers

| Provider | Uso Principal | Servicios Clave |
|----------|---------------|-----------------|
| AWS | Infraestructura principal | EC2, S3, RDS, Lambda, SageMaker, CloudFront |
| GCP | ML workloads pesados | Vertex AI, Cloud GPUs, BigQuery |
| Vercel | Frontend hosting | Next.js deployments, Edge Functions |
| Cloudflare | CDN, DNS, security | R2 (storage), Workers, Pages |

### Servicios AWS Detallados

| Servicio | Uso en MBC |
|----------|------------|
| EC2 (g5.xlarge) | Pixel Streaming, GPU rendering |
| S3 | Almacenamiento de assets 3D, modelos ML, backups |
| RDS (PostgreSQL) | Base de datos relacional principal |
| Lambda | Funciones serverless, procesamiento de eventos |
| SageMaker | Training y deployment de modelos ML |
| CloudFront | CDN para apps web y assets estaticos |
| SES | Envio de emails transaccionales |
| Cognito | Autenticacion de usuarios |

### CI/CD

| Herramienta | Uso |
|-------------|-----|
| GitHub Actions | CI/CD principal: tests, linting, builds, deployments |
| Docker | Containerizacion de servicios |
| Docker Compose | Entornos de desarrollo local multi-servicio |

### Monitoring y Observabilidad

| Herramienta | Uso |
|-------------|-----|
| Sentry | Error tracking, performance monitoring |
| CloudWatch | Logs, metricas, alarmas de infraestructura AWS |
| Uptime Robot | Monitoreo de uptime de servicios publicos |

### Comunicacion

| Herramienta | Uso |
|-------------|-----|
| Slack | Comunicacion interna del equipo, integraciones |
| Discord | Comunidad MBC, soporte async |
| Zoom / Google Meet | Reuniones con clientes, presentaciones |
| Loom | Videos asincrono para demos y updates |

### Project Management

| Herramienta | Uso |
|-------------|-----|
| Notion | Wiki interno, documentacion, bases de datos |
| Linear | Issue tracking, sprints, roadmap |
| GitHub Projects | Tracking tecnico ligado a repos |
| Miro | Workshops, user journey mapping, brainstorming |

---

## 7. DevOps y Herramientas de Desarrollo

### Version Control

- **Git**: control de versiones para todo el codigo.
- **GitHub**: repositorios, pull requests, code review, Actions.
- **Branching strategy**: GitHub Flow (main + feature branches). Release branches para proyectos grandes.

### Containers

- **Docker**: todos los servicios se dockerizan para consistencia entre dev/staging/prod.
- **Docker Compose**: orchestracion local de multi-servicio (API + DB + Redis + worker).
- **ECR (AWS)**: registry privado de imagenes Docker.

### Infrastructure as Code

- **Terraform**: provisioning de infraestructura AWS cuando se requiere (no para todos los proyectos).
- **AWS CDK**: alternativa a Terraform para proyectos puramente AWS.
- **Serverless Framework**: para proyectos Lambda-heavy.

### IDEs y Herramientas de Desarrollo

| Herramienta | Uso |
|-------------|-----|
| VS Code | IDE principal para desarrollo general |
| Cursor | IDE con AI integrada para pair programming |
| Claude Code | CLI agent para desarrollo asistido por AI |
| Postman / Insomnia | Testing de APIs |
| pgAdmin / DBeaver | Administracion de bases de datos |

### Seguridad

- **Dependabot**: alertas de vulnerabilidades en dependencias.
- **GitHub Secret Scanning**: deteccion de secrets en codigo.
- **1Password / Bitwarden**: gestion de credenciales del equipo.
- **AWS IAM**: control de acceso granular a recursos cloud.
- **SSL/TLS**: Let's Encrypt via Cloudflare para todos los dominios.

---

## 8. Criterios de Seleccion de Tecnologia

Al evaluar nuevas herramientas o frameworks, MBC considera:

1. **Madurez**: tecnologia estable con comunidad activa y documentacion completa.
2. **Costo**: preferencia por open-source o tiers gratuitos hasta validar ROI.
3. **Interoperabilidad**: capacidad de integrarse con el stack existente.
4. **Talento**: disponibilidad de desarrolladores en Chile/LATAM con experiencia.
5. **Escalabilidad**: capacidad de crecer sin reescribir desde cero.
6. **Contexto chileno**: compatibilidad con normativas locales (PlanBIM, CMF, ley de datos).

---

## 9. Roadmap Tecnologico 2026

| Q1 2026 | Q2 2026 | Q3 2026 | Q4 2026 |
|---------|---------|---------|---------|
| Consolidar stack XR (Unity + Unreal) | Implementar Pixel Streaming en produccion | Pipeline CV completo para safety | Plataforma SaaS propia (v1) |
| Setup MLOps basico | Smart contracts en testnet | Deploy contratos en Polygon mainnet | Integracion BIM-blockchain |
| Definir arquitectura de microservicios | RAG pipeline para documentacion | Chatbot inmobiliario v2 con voice | AI dashboard para clientes |
| CI/CD para todos los repos | Monitoreo y alertas completo | ISO 27001 gap analysis | Certificacion ISO 27001 (inicio) |

---

*Este documento se actualiza trimestralmente. Responsable: CTO / Tech Lead de cada vertical.*
