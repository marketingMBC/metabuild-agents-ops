# Stack de Inteligencia Artificial

> Documento tecnico detallado de las capacidades, metodologias y herramientas de AI/ML de Meta Build City.
> Verticales: Computer Vision, Analisis Predictivo, NLP/Documentacion, Chatbots Inmobiliarios.
> Ultima actualizacion: Febrero 2026

---

## 1. Computer Vision para Construccion

### 1.1 Object Detection

**Modelo principal**: YOLOv8 (Ultralytics) fine-tuned para construccion.

**Clases detectadas**:

| Categoria | Clases | Confianza Target |
|-----------|--------|-----------------|
| Personas | worker, visitor, supervisor | >= 85% |
| EPP | hard_hat, safety_vest, gloves, goggles, harness | >= 80% |
| Equipos | crane, excavator, forklift, scaffolding, formwork | >= 85% |
| Materiales | rebar_stack, concrete_bags, lumber, pipes | >= 75% |
| Zonas | restricted_zone, excavation, loading_area | >= 70% |
| Riesgos | open_edge, missing_guardrail, unsecured_load | >= 70% |

**Modelos disponibles**:

| Modelo | Tamano | Inference Time | Uso |
|--------|--------|---------------|-----|
| YOLOv8n-construction | 6 MB | 5 ms (GPU) | Edge deployment (Jetson Nano) |
| YOLOv8s-construction | 22 MB | 10 ms (GPU) | Edge deployment (Jetson Orin) |
| YOLOv8m-construction | 52 MB | 20 ms (GPU) | Cloud inference, balance precision/velocidad |
| YOLOv8l-construction | 87 MB | 35 ms (GPU) | Cloud inference, maxima precision |

**Training data**:
- Dataset base: COCO 2017 (transfer learning)
- Dataset custom: 15,000+ imagenes de obras chilenas etiquetadas
- Augmentations: rotation, flip, brightness/contrast, rain/fog simulation, cutout
- Split: 70% train, 15% validation, 15% test
- Etiquetado: Label Studio con equipo interno + revisores externos

### 1.2 Progress Monitoring

**Metodologia**:

```
Captura de imagenes (camaras fijas o drones)
    |
    v
Preprocessing: rectificacion, normalizacion, registro temporal
    |
    v
Comparacion temporal:
    - Image differencing entre capturas sucesivas
    - Segmentacion semantica de elementos construidos
    - Overlay con modelo BIM (render sintetico del avance esperado)
    |
    v
Calculo de avance:
    - Porcentaje de area construida vs planificada
    - Deteccion de elementos nuevos vs baseline
    - Volumetria estimada (si hay depth data)
    |
    v
Dashboard de avance:
    - Timeline visual con imagenes anotadas
    - Curva S real vs planificada
    - Alertas de desviacion (>10% atraso)
```

**Fuentes de imagenes**:
- Camaras fijas IP (Axis, Hikvision): captura cada 15 minutos
- Drones (DJI Mavic 3 Enterprise): vuelos semanales programados
- Camaras 360 (Insta360): captura panoramica periodica
- Smartphones: captura manual por supervisores

**Modelos utilizados**:
- Segmentacion semantica: DeepLabV3+ fine-tuned en elementos de construccion
- Change detection: Siamese network para detectar cambios entre capturas
- BIM comparison: rendering sintetico del avance esperado + IoU con realidad

### 1.3 Safety Compliance

**Detecciones de seguridad**:

| Tipo de Violacion | Deteccion | Respuesta |
|-------------------|-----------|-----------|
| Trabajador sin casco | Object detection (persona sin hard_hat) | Alerta inmediata al supervisor |
| Trabajador sin chaleco | Object detection (persona sin safety_vest) | Alerta inmediata al supervisor |
| Ingreso a zona restringida | Persona detectada dentro de polygon de zona | Alerta + registro de evento |
| Proximidad a equipos | Distancia persona-equipo < threshold | Alerta de proximidad |
| Trabajador en altura sin arnes | Persona en zona elevada sin harness detectado | Alerta critica |
| Acopio inseguro | Material fuera de zona de acopio designada | Alerta al encargado de bodega |

**Pipeline de safety monitoring**:

```
Camaras IP en obra (multiples angulos)
    |
    v
Edge Device (NVIDIA Jetson Orin Nano)
    |
    v
Inference pipeline:
    1. Person detection (YOLOv8)
    2. PPE detection (YOLOv8 EPP model)
    3. Zone compliance (polygon intersection)
    4. Proximity calculation (bounding box distance)
    |
    v
Event Classification:
    - CRITICAL: riesgo de accidente inmediato
    - WARNING: incumplimiento de norma
    - INFO: evento registrado para estadisticas
    |
    v
Notification System:
    - CRITICAL: push notification + sirena (si integrado)
    - WARNING: push notification + email
    - INFO: log en dashboard
    |
    v
Dashboard de seguridad:
    - Eventos en tiempo real
    - Estadisticas diarias/semanales
    - Tendencias de cumplimiento
    - Reportes para prevencionista
```

### 1.4 Data Pipeline Completo

```
[Captura]                    [Procesamiento]              [Inferencia]              [Resultado]

Camaras IP ----+             Image Queue  ----+           Model Server ----+        Dashboard
Drones --------+---> S3 ---> (Redis/SQS)  ----+---> GPU  (FastAPI)    ----+---->   Alertas
Smartphones ---+             Preprocessing ----+           Batch/RT    ----+        Reportes
                             (resize, norm)                                         API

[Storage]                    [MLOps]
S3 (raw images)              MLflow (model registry)
PostgreSQL (metadata)        DVC (dataset versioning)
TimescaleDB (time series)    W&B (experiment tracking)
```

### 1.5 Deployment Options

| Opcion | Hardware | Latencia | Costo | Uso |
|--------|----------|----------|-------|-----|
| Edge - Jetson Orin Nano | NVIDIA Jetson | <50ms | $500 USD (one-time) + energia | Obras con conectividad limitada |
| Edge - Jetson AGX Orin | NVIDIA Jetson | <20ms | $2,000 USD (one-time) | Multiples camaras, modelos complejos |
| Cloud - EC2 g5 | AWS EC2 g5.xlarge | 100-200ms (+ network) | ~$1.00 USD/hr | Obras con buena conectividad |
| Cloud - SageMaker | AWS SageMaker | 100-300ms | Pay-per-inference | Inference esporadica, auto-scaling |
| Hybrid | Jetson + AWS | Edge: <50ms, Cloud: batch | Combinado | Inference RT en edge, training en cloud |

---

## 2. Analisis Predictivo

### 2.1 Cost Prediction

**Objetivo**: predecir el costo final de un proyecto basado en datos historicos y variables del proyecto actual.

**Feature Engineering**:

| Feature | Tipo | Fuente |
|---------|------|--------|
| Superficie construida (m2) | Numerica | Proyecto BIM |
| Tipo de proyecto (vivienda, oficina, industrial) | Categorica | Brief |
| Ubicacion (comuna, region) | Categorica | Proyecto |
| N de pisos | Numerica | Proyecto BIM |
| Tipo de estructura (hormigon, acero, madera) | Categorica | Proyecto |
| Indice de precios de materiales | Numerica | INE / proveedores |
| Temporada (verano/invierno) | Categorica | Calendario |
| Complejidad arquitectonica (score 1-10) | Numerica | Evaluacion experta |
| Distancia a centro urbano (km) | Numerica | Geolocation |
| Historial de inflacion | Time series | Banco Central |

**Modelos**:

| Modelo | Uso | Metrica Principal |
|--------|-----|-------------------|
| XGBoost Regressor | Prediccion puntual de costo | MAPE < 10% |
| Quantile Regression (LightGBM) | Rangos de costo (P10, P50, P90) | Coverage > 90% |
| Neural Network (MLP) | Patrones complejos con muchas variables | MAPE < 8% |

**Risk Scoring**:
- Score 1-100 basado en probabilidad de sobrecosto
- Factores de riesgo identificados y cuantificados
- Recomendaciones automaticas de mitigacion
- Comparacion con proyectos similares historicos

### 2.2 Schedule Prediction

**Metodologia: Earned Value Analysis + ML**

```
Datos del proyecto:
    - Planned Value (PV) por actividad
    - Actual Cost (AC) por periodo
    - Earned Value (EV) calculado
    |
    v
Features derivadas:
    - SPI (Schedule Performance Index) = EV/PV
    - CPI (Cost Performance Index) = EV/AC
    - SPI trend (ultimas 4 semanas)
    - % de actividades criticas completadas
    - Weather forecast (proximas 2 semanas)
    - Historico de rendimiento del contratista
    |
    v
ML Model (LightGBM):
    - Output: probabilidad de atraso (0-100%)
    - Output: dias estimados de atraso/adelanto
    - Output: actividades con mayor riesgo de atraso
    |
    v
Alertas:
    - Verde: proyecto en schedule (SPI > 0.95)
    - Amarillo: riesgo moderado (SPI 0.85-0.95)
    - Rojo: atraso probable (SPI < 0.85)
```

### 2.3 Resource Optimization

**Demand Forecasting**:
- Predecir necesidad de mano de obra por especialidad para las proximas 2-4 semanas
- Input: programacion de actividades, rendimientos historicos, disponibilidad
- Output: dotacion recomendada por dia/semana por especialidad
- Modelo: Prophet (Facebook) para time series + ajustes manuales

**Crew Scheduling**:
- Optimizar asignacion de cuadrillas a actividades
- Considerar: skills, disponibilidad, restricciones de seguridad, preferencias
- Modelo: Linear programming (PuLP) o constraint satisfaction
- Output: planilla de asignacion optimizada

**Material Procurement**:
- Predecir necesidad de materiales basado en avance planificado
- Lead time de proveedores por material
- Output: calendario de pedidos optimizado para evitar atrasos y excesos de inventario

### 2.4 Data Sources

| Fuente | Datos | Integracion |
|--------|-------|-------------|
| ERP (SAP, Oracle, local) | Costos, ordenes de compra, contratos | API o export periodico |
| Project Management (Primavera, MS Project) | Programacion, avance, recursos | API o export (.xml, .mpp) |
| Weather API (OpenWeatherMap) | Pronostico y datos historicos | REST API |
| INE (Instituto Nacional de Estadisticas) | Indices de precios, inflacion | Web scraping / API |
| Proveedores | Cotizaciones, lead times, disponibilidad | Email parsing / portal |
| IoT sensores | Temperatura, humedad, vibracion | MQTT / API |
| Camaras | Imagenes de avance | Pipeline de CV (seccion 1) |

---

## 3. NLP para Documentacion

### 3.1 Document Analysis

**Tipos de documentos procesados**:

| Documento | Procesamiento | Output |
|-----------|---------------|--------|
| Contratos de construccion | Extraccion de clausulas clave, plazos, montos, penalidades | Resumen estructurado + alertas de riesgo |
| Especificaciones tecnicas (EETT) | Parsing de requerimientos por partida | Base de datos de requerimientos |
| RFI (Request for Information) | Clasificacion, routing, sugerencia de respuesta | Respuesta draft + referencias |
| Minutas de reunion | Extraccion de acuerdos, tareas, responsables | Lista de action items |
| Informes de avance | Extraccion de metricas, problemas, riesgos | Dashboard actualizado |
| Bases de licitacion | Analisis de requisitos, criterios de evaluacion | Checklist de cumplimiento |

### 3.2 RAG Pipeline (Retrieval-Augmented Generation)

**Arquitectura completa**:

```
[Ingestion Pipeline]

Documentos (PDF, DOCX, XLSX)
    |
    v
Document Loader (LangChain):
    - PyPDF / pdfplumber (PDF)
    - python-docx (DOCX)
    - openpyxl (XLSX)
    - Unstructured.io (formatos mixtos)
    |
    v
Text Splitter:
    - RecursiveCharacterTextSplitter
    - chunk_size: 1000 tokens
    - chunk_overlap: 200 tokens
    - Metadata: source, page, section
    |
    v
Embedding Model:
    - OpenAI text-embedding-3-small (1536 dims)
    - Alternativa: Cohere embed-v3 (1024 dims)
    |
    v
Vector Store:
    - ChromaDB (desarrollo, <100K docs)
    - Pinecone (produccion, >100K docs)
    - Metadata filtering: project, document_type, date
    |
    v
[Retrieval Pipeline]

User Query
    |
    v
Query Processing:
    - Query expansion (LLM rewrite)
    - Metadata filtering (proyecto, tipo de doc)
    |
    v
Retrieval:
    - Semantic search (cosine similarity, top-k=5)
    - Hybrid search: semantic + BM25 (keyword)
    - Re-ranking: Cohere Rerank o cross-encoder
    |
    v
Context Assembly:
    - Concatenar chunks relevantes
    - Agregar metadata (fuente, pagina)
    - Aplicar max context window
    |
    v
Generation:
    - LLM: Claude 3.5 Sonnet (primary) / GPT-4 (fallback)
    - System prompt con instrucciones especificas del dominio
    - Temperature: 0.1 (factual) / 0.7 (creative)
    |
    v
Response:
    - Respuesta generada con citas
    - Links a documentos fuente
    - Confidence score
```

### 3.3 Stack Detallado

| Componente | Herramienta | Version | Notas |
|------------|-------------|---------|-------|
| Orchestration | LangChain | 0.2.x | Chains, agents, retrieval |
| Vector Store (dev) | ChromaDB | 0.4.x | Open-source, local |
| Vector Store (prod) | Pinecone | Serverless | Managed, escalable |
| Embeddings | OpenAI text-embedding-3-small | - | Mejor costo/rendimiento |
| LLM (primary) | Claude 3.5 Sonnet | claude-3-5-sonnet | Mejor razonamiento |
| LLM (fallback) | GPT-4 Turbo | gpt-4-turbo | Backup |
| Re-ranking | Cohere Rerank | rerank-v3 | Mejora precision del retrieval |
| Document loading | Unstructured.io | 0.12.x | Soporte multi-formato |
| API | FastAPI | 0.109.x | Async, auto-docs |
| Cache | Redis | 7.x | Cache de queries frecuentes |
| Monitoring | LangSmith | - | Tracing de chains, evaluacion |

### 3.4 Use Cases Implementados

**Automated RFI Response**:
1. RFI llega por email o plataforma de gestion
2. NLP clasifica el tema (estructura, instalaciones, terminaciones, etc.)
3. RAG busca en documentos del proyecto (EETT, planos, contratos)
4. LLM genera respuesta draft con referencias
5. Ingeniero revisa, edita y envia
6. Tiempo promedio de respuesta: de 3 dias a 4 horas

**Contract Risk Analysis**:
1. Ingreso de contrato (PDF)
2. Extraccion de clausulas con LLM
3. Clasificacion de riesgo por clausula (alto/medio/bajo)
4. Comparacion con contratos benchmark
5. Reporte de riesgos con recomendaciones
6. Flags automaticos: penalidades excesivas, plazos irreales, ambiguedades

**Spec Compliance Checking**:
1. Input: especificaciones tecnicas del proyecto + propuesta del subcontratista
2. Extraccion de requerimientos de EETT
3. Matching con propuesta del subcontratista
4. Identificacion de brechas y no-conformidades
5. Reporte: cumple / no cumple / parcial por cada requerimiento

---

## 4. Chatbots Inmobiliarios

### 4.1 Arquitectura

```
[Canales de Entrada]

WhatsApp ----+
Web Widget --+---> Message Router (FastAPI)
Instagram ---+          |
                        v
              Intent Detection (LLM):
              - greeting, project_info, pricing,
              - availability, schedule_visit,
              - financing, complaint, other
                        |
                        v
              Knowledge Base Lookup:
              - Vector search en base de conocimiento del proyecto
              - Structured data query (disponibilidad, precios)
                        |
                        v
              Response Generation (Claude API):
              - System prompt con personalidad de marca
              - Contexto del proyecto y conversacion
              - Guardrails: no inventar datos, derivar a humano si necesario
                        |
                        v
              Response Delivery:
              - Formato adaptado al canal (WhatsApp tiene limites)
              - Rich media: imagenes, PDFs, links
              - CTA buttons (agendar visita, cotizar)
                        |
                        v
              [Si lead calificado]:
              - Crear/actualizar contacto en HubSpot
              - Notificar a ejecutivo comercial
              - Agendar follow-up automatico
```

### 4.2 Canales

| Canal | API | Capacidades | Notas |
|-------|-----|-------------|-------|
| WhatsApp Business | WhatsApp Cloud API (Meta) | Texto, imagenes, documentos, botones, listas | Canal principal en Chile |
| Web Widget | Custom (React + WebSocket) | Texto, imagenes, rich cards, video embed | Integrado en sitio del proyecto |
| Instagram DM | Instagram Graph API | Texto, imagenes, quick replies | Para campanas de awareness |
| Facebook Messenger | Messenger API | Texto, imagenes, carousels | Menor uso, pero disponible |

### 4.3 Knowledge Base

**Estructura de datos por proyecto**:

```json
{
  "project": {
    "name": "Edificio Los Alamos",
    "developer": "Inmobiliaria XYZ",
    "location": {
      "address": "Av. Principal 1234, Las Condes",
      "commune": "Las Condes",
      "city": "Santiago",
      "coordinates": [-33.4189, -70.5920]
    },
    "description": "Proyecto residencial de 15 pisos...",
    "delivery_date": "Q4 2027",
    "amenities": ["piscina", "gimnasio", "quincho", "sala multiuso"],
    "nearby": ["Metro Tobalaba (5 min)", "Mall Parque Arauco (10 min)"],
    "units": [
      {
        "type": "1D+1B",
        "area_m2": 35.5,
        "price_uf": 3200,
        "available": 12,
        "floor_plan_url": "https://...",
        "virtual_tour_url": "https://..."
      }
    ],
    "financing": {
      "reservation_uf": 50,
      "down_payment_percent": 10,
      "bank_financing": true,
      "subsidy_eligible": ["DS1", "DS19"]
    },
    "faq": [
      {
        "question": "Cual es la fecha de entrega?",
        "answer": "La entrega estimada es Q4 2027..."
      }
    ]
  }
}
```

### 4.4 Stack Tecnico del Chatbot

| Componente | Tecnologia | Notas |
|------------|-----------|-------|
| Backend | FastAPI (Python) | Async, webhook handling |
| LLM | Claude 3.5 Sonnet (Anthropic API) | Generacion de respuestas |
| Knowledge Retrieval | ChromaDB + structured DB | Hibrido: semantic + SQL |
| Database | PostgreSQL | Conversaciones, leads, analytics |
| Cache | Redis | Sesiones, rate limiting |
| Queue | Celery + Redis | Procesamiento async de mensajes |
| WhatsApp API | WhatsApp Cloud API | Webhook + send message |
| CRM Integration | HubSpot API | Crear/actualizar contactos |
| Hosting | AWS ECS (Fargate) | Serverless containers |
| Monitoring | Sentry + CloudWatch | Errors, latency, uptime |

### 4.5 Guardrails y Seguridad

**Reglas del chatbot**:
1. **Nunca inventar datos**: si no tiene la informacion, decir "No tengo esa informacion, te conecto con un ejecutivo".
2. **No dar asesoria legal/financiera**: derivar a profesionales.
3. **Detectar frustacion**: si el usuario expresa molestia, escalar a humano.
4. **Horario de escalamiento**: horario laboral derivar a humano, fuera de horario registrar para seguimiento.
5. **Datos sensibles**: no solicitar ni almacenar RUT, datos bancarios, contrasenas.
6. **Rate limiting**: max 30 mensajes por minuto por usuario.
7. **Content moderation**: filtrar mensajes ofensivos o spam.

**Escalamiento a humano**:
- Trigger automatico: 3+ intentos fallidos de respuesta, solicitud explicita, tema sensible
- Notificacion: push notification a ejecutivo via Slack/WhatsApp
- Handoff: contexto completo de la conversacion transferido al humano
- Follow-up: bot retoma si humano no responde en 30 minutos

### 4.6 Metricas del Chatbot

| Metrica | Target | Medicion |
|---------|--------|----------|
| Response time | < 5 segundos | P95 latency |
| Resolution rate | > 70% sin humano | Conversaciones resueltas / total |
| Lead capture rate | > 40% de conversaciones | Leads generados / conversaciones |
| CSAT | > 4.0/5.0 | Encuesta post-conversacion |
| Visit scheduling | > 15% de leads | Visitas agendadas / leads |
| Conversation length | 5-10 mensajes promedio | Mensajes por conversacion |
| Escalation rate | < 30% | Escalamientos / conversaciones |
| Uptime | 99.9% | Monitoreo continuo |

---

## 5. MLOps Pipeline

### 5.1 Pipeline Completo

```
[Data Collection]              [Training]                [Deployment]

Label Studio ----+             Cloud GPU ----+            FastAPI ----+
Camera feeds ---+---> DVC      (AWS/GCP)    |             SageMaker --+--> Monitoring
Manual upload --+    (versioned)|            v             Edge device-+    Dashboard
                     |         Training Script             |
                     v         (PyTorch/sklearn)           v
                Dataset v2.3   |                       Model Serving
                     |         v                       (REST API)
                     |     MLflow                          |
                     |     (experiment                     v
                     |      tracking)                  Predictions
                     |         |                           |
                     |         v                           v
                     +---> Model Registry             Alert System
                           (MLflow)                    (Sentry + custom)
                               |
                               v
                           Evaluation:
                           - Offline metrics (mAP, F1, MAPE)
                           - A/B testing (shadow mode)
                           - Human review (sample)
```

### 5.2 Versionado de Datos (DVC)

**Estructura**:
```
data/
  raw/               # Datos crudos (imagenes, CSVs)
  processed/         # Datos preprocesados
  annotations/       # Etiquetas (COCO JSON, YOLO txt)
  splits/            # Train/val/test splits

dvc.yaml             # Pipeline definitions
dvc.lock             # Pipeline lock file
```

**Remote storage**: AWS S3 bucket dedicado para datos de ML.

**Comandos frecuentes**:
```bash
dvc add data/raw/construction_images_v3/
dvc push                    # Subir datos al remote
dvc pull                    # Bajar datos del remote
dvc repro                   # Reproducir pipeline completo
dvc metrics show            # Ver metricas del ultimo run
dvc plots diff              # Comparar metricas entre versiones
```

### 5.3 Experiment Tracking (MLflow + W&B)

**MLflow** (model registry y serving):
- Tracking server: self-hosted en AWS EC2
- Artifact store: S3
- Model registry: staging -> production promotion
- Model serving: MLflow serve o export a ONNX

**Weights & Biases** (experiment tracking visual):
- Hyperparameter sweeps automaticos
- Visualizacion de metricas en tiempo real
- Comparacion de runs
- Artifacts: modelos, datasets, predicciones de ejemplo
- Reports: documentacion de experimentos

### 5.4 Model Evaluation

**Metricas por tipo de modelo**:

| Tipo de Modelo | Metricas | Threshold para Produccion |
|----------------|----------|--------------------------|
| Object Detection | mAP@0.5, mAP@0.5:0.95, precision, recall | mAP@0.5 >= 0.80 |
| Segmentacion | IoU, pixel accuracy, F1 | IoU >= 0.75 |
| Clasificacion | accuracy, F1, AUC-ROC | F1 >= 0.85 |
| Regression (costos) | MAPE, RMSE, R2 | MAPE <= 10% |
| NLP/RAG | relevance, faithfulness, answer correctness | relevance >= 0.8 |

**Evaluacion de modelos RAG (RAGAS framework)**:
- Faithfulness: la respuesta es fiel a los documentos recuperados?
- Answer relevance: la respuesta es relevante a la pregunta?
- Context precision: los documentos recuperados son relevantes?
- Context recall: se recuperaron todos los documentos necesarios?

### 5.5 Retraining Cadence

| Modelo | Frecuencia de Retraining | Trigger |
|--------|--------------------------|---------|
| YOLOv8 (safety) | Mensual | Nuevas clases, precision < threshold, datos nuevos |
| Progress monitoring | Trimestral | Nuevo tipo de proyecto |
| Cost prediction | Semestral | Actualizacion de datos de mercado |
| Chatbot (RAG) | Continuo | Nuevo proyecto inmobiliario |
| Schedule prediction | Trimestral | Feedback de predicciones pasadas |

---

## 6. Data Strategy

### 6.1 Data Collection Guidelines para Obras

**Protocolo de captura de imagenes**:
1. Camaras fijas: instalar en puntos estrategicos con vista panoramica
2. Configuracion: captura cada 15 minutos, resolucion minima 1920x1080
3. Almacenamiento: edge buffer de 48 horas + upload diario a S3
4. Metadata: timestamp, camera_id, project_id, weather conditions
5. Retention: imagenes crudas 6 meses, procesadas 2 anos, resultados permanente

**Protocolo de recoleccion de datos de proyecto**:
1. Estandarizar templates de reporte de avance
2. Integrar con ERP/PM tools via API cuando sea posible
3. Manual data entry como ultimo recurso (formularios validados)
4. Validacion automatica de datos al ingreso
5. Audit trail de modificaciones

### 6.2 Privacy y Security

**Datos personales**:
- Imagenes de trabajadores: anonimizar rostros antes de almacenar para training
- Datos de contacto (chatbot): encriptar en reposo (AES-256) y en transito (TLS 1.3)
- Cumplir con Ley 19.628 (proteccion de datos personales de Chile)
- Prepararse para nueva ley de datos personales (en tramitacion)

**Datos de proyecto**:
- Clasificar por nivel de confidencialidad (publico, interno, confidencial)
- Acceso basado en roles (RBAC) para todos los sistemas
- NDA con todos los clientes que entreguen datos
- Eliminacion de datos al termino del proyecto (segun acuerdo con cliente)

**Seguridad de modelos**:
- Modelos entrenados son propiedad de MBC (salvo acuerdo contrario)
- Datos de entrenamiento anonimizados
- No compartir modelos entre clientes sin consentimiento
- Model cards documentando training data, biases, limitaciones

### 6.3 Data Labeling Workflow

**Herramienta**: Label Studio (self-hosted)

**Proceso**:
1. **Data ingestion**: imagenes/documentos cargados a Label Studio
2. **Task creation**: definir tipo de anotacion (bbox, segmento, texto)
3. **Labeling**: equipo interno (2-3 etiquetadores)
4. **Review**: tech lead revisa muestra aleatoria (20%)
5. **Quality check**: inter-annotator agreement (IoU > 0.7 para bbox)
6. **Export**: formato COCO JSON o YOLO txt
7. **Versioning**: commit a DVC con metadata

**Guias de etiquetado**:
- Documento detallado por tipo de tarea
- Ejemplos positivos y negativos
- Casos edge documentados
- Actualizacion continua con feedback del modelo

---

## 7. Infraestructura de AI

### 7.1 Arquitectura de Deployment

```
[Internet]
    |
    v
[CloudFront CDN] --- [Route 53 DNS]
    |
    v
[ALB (Application Load Balancer)]
    |
    +---> [ECS Cluster (Fargate)]
    |         |
    |         +---> API Service (FastAPI)
    |         +---> Chatbot Service
    |         +---> RAG Service
    |
    +---> [SageMaker Endpoints]
    |         |
    |         +---> YOLOv8 Inference
    |         +---> Embedding Model
    |
    +---> [Edge Devices]
              |
              +---> Jetson Orin (per obra)
              +---> Local inference + sync

[Data Stores]
    +---> RDS PostgreSQL (structured data)
    +---> S3 (images, models, documents)
    +---> ElastiCache Redis (cache, sessions)
    +---> Pinecone (vectors)
    +---> TimescaleDB (time series)
```

### 7.2 Cost Estimates (USD/month)

| Servicio | Configuracion | Costo Estimado |
|----------|---------------|----------------|
| ECS Fargate (API) | 2 vCPU, 4GB RAM, 2 tasks | $150 |
| SageMaker (inference) | ml.g5.xlarge, serverless | $200-500 (segun uso) |
| RDS PostgreSQL | db.t3.medium, 100GB | $80 |
| S3 | 1 TB storage | $25 |
| ElastiCache Redis | cache.t3.micro | $15 |
| Pinecone | Serverless, 1M vectors | $70 |
| CloudWatch + Sentry | Basico | $50 |
| **Total estimado** | | **$600-900/month** |

**Nota**: costos escalan con numero de proyectos activos y volumen de inference.

---

*Este documento se actualiza con cada release de modelo o cambio de arquitectura. Responsable: AI/ML Lead.*
