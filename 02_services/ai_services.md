# Servicios de Inteligencia Artificial para Construcción

## Descripción del Servicio

Meta Build City lleva el poder de la **Inteligencia Artificial y Machine Learning** al corazón de las operaciones de construcción. Desarrollamos soluciones AI que transforman datos dispersos en insights accionables, automatizan tareas repetitivas y predicen problemas antes de que se conviertan en costos.

La industria de la construcción genera enormes volúmenes de datos — fotos de obra, documentos técnicos, registros de avance, datos de sensores — pero históricamente los ha subutilizado. Nuestros servicios AI desbloquean ese potencial.

## Propuesta de Valor

- **Reducción de 15-25% en sobrecostos** mediante predicción temprana de desviaciones
- **Ahorro de 10+ horas semanales** por equipo en generación de reportes
- **Detección proactiva de riesgos de seguridad** antes de que ocurran incidentes
- **Análisis de documentos técnicos 50x más rápido** que revisión manual

---

## Ofertas de Servicio

### 1. Computer Vision para Monitoreo de Obra

**Descripción:**
Sistemas de visión computacional que analizan imágenes y video de obra para tracking automático de avance, detección de incumplimientos de seguridad y documentación visual inteligente. Las cámaras de obra dejan de ser simples registros y se convierten en sensores inteligentes.

**Casos de Uso:**

**a) Progress Tracking (Seguimiento de Avance)**
- Comparación automática entre modelo BIM planificado y estado real de obra
- Porcentaje de avance por elemento constructivo (losas, muros, instalaciones)
- Generación automática de reportes de avance con evidencia visual
- Detección de desviaciones respecto al programa

**b) Safety Compliance (Cumplimiento de Seguridad)**
- Detección de EPP (Equipo de Protección Personal): casco, chaleco, arnés
- Identificación de zonas de riesgo no señalizadas
- Conteo de personas en zonas restringidas
- Detección de condiciones inseguras (andamios mal armados, materiales apilados incorrectamente)

**Deliverables:**
- Modelos de computer vision entrenados y desplegados
- Dashboard web en tiempo real con alertas configurables
- API de integración con sistemas de gestión de obra existentes
- Reportes automáticos diarios/semanales
- Reentrenamiento mensual del modelo con datos nuevos (primer trimestre)

**Timeline:** 6-10 semanas (dependiendo de cantidad de cámaras y escenarios)

**Stack:** Python, PyTorch, YOLOv8, OpenCV, FastAPI, Docker, AWS (EC2, S3, SageMaker), cámaras IP existentes o nuevas

---

### 2. Predictive Analytics (Analítica Predictiva)

**Descripción:**
Modelos de machine learning que aprenden de datos históricos de proyectos para predecir sobrecostos, atrasos en programa, problemas de calidad y otros riesgos. Transforma la gestión reactiva en gestión proactiva.

**Casos de Uso:**

**a) Predicción de Sobrecostos**
- Análisis de patrones en datos históricos de presupuesto vs. costo real
- Identificación de partidas con mayor probabilidad de desviación
- Alertas tempranas cuando indicadores sugieren tendencia al sobrecosto
- Escenarios what-if para evaluación de alternativas

**b) Predicción de Atrasos en Programa**
- Modelo predictivo basado en velocidad de avance real vs. planificada
- Factores climáticos, estacionales y de productividad
- Identificación de ruta crítica dinámica basada en datos reales
- Recomendaciones de mitigación priorizadas por impacto

**Deliverables:**
- Modelos predictivos calibrados con datos del cliente
- Dashboard ejecutivo con indicadores predictivos (semáforo de riesgo)
- Sistema de alertas automáticas por correo y notificaciones
- Reporte mensual de precisión del modelo y recalibración
- Documentación técnica y guía de interpretación

**Timeline:** 8-12 semanas (incluye recopilación y limpieza de datos históricos)

**Stack:** Python, scikit-learn, XGBoost, Prophet (forecasting), Pandas, PostgreSQL, Streamlit/Dash, AWS/GCP

---

### 3. NLP para Análisis de Documentos Técnicos

**Descripción:**
Procesamiento de lenguaje natural aplicado a especificaciones técnicas, contratos, bases de licitación, normativa y otros documentos de la industria. Extrae información clave, identifica inconsistencias y permite consultas en lenguaje natural sobre grandes volúmenes documentales.

**Casos de Uso:**

**a) Análisis de Especificaciones Técnicas**
- Extracción automática de requerimientos y materiales especificados
- Identificación de inconsistencias entre secciones o documentos
- Comparación entre EETT de distintas versiones (change tracking inteligente)
- Generación de resúmenes ejecutivos por disciplina

**b) Análisis de Contratos**
- Identificación de cláusulas de riesgo y penalizaciones
- Extracción de plazos, hitos y condiciones de pago
- Comparación contra templates de contrato estándar
- Alertas sobre cláusulas inusuales o potencialmente problemáticas

**c) Consulta Inteligente de Normativa**
- Chatbot que responde preguntas sobre NCh, OGUC, normativa sectorial
- Búsqueda semántica en base documental del proyecto
- Verificación de cumplimiento normativo automatizada

**Deliverables:**
- Sistema de análisis documental con interfaz web
- Chatbot de consulta sobre documentos del proyecto
- API de extracción de datos estructurados desde documentos
- Base de conocimiento indexada y searchable
- Capacitación al equipo legal/técnico del cliente

**Timeline:** 6-8 semanas

**Stack:** Python, LangChain, Claude API (Anthropic), OpenAI API, Pinecone/Weaviate (vector DB), FastAPI, OCR (Tesseract/AWS Textract), React frontend

---

### 4. Optimización de Cadena de Suministro

**Descripción:**
Algoritmos de optimización que mejoran la gestión de adquisiciones, inventario y logística de materiales en proyectos de construcción. Reduce desperdicios, optimiza tiempos de entrega y baja costos de almacenamiento.

**Casos de Uso:**
- Predicción de demanda de materiales por fase de proyecto
- Optimización de timing de órdenes de compra
- Identificación de proveedores alternativos basada en datos de rendimiento
- Detección de anomalías en precios de mercado
- Optimización de layout de bodega y logística interna de obra

**Deliverables:**
- Modelo de optimización calibrado para el proyecto/empresa
- Dashboard de gestión de suministros con recomendaciones AI
- Integración con ERP/sistema de adquisiciones existente
- Alertas de reposición inteligentes
- Reporte mensual de ahorros generados

**Timeline:** 8-10 semanas

**Stack:** Python, OR-Tools (Google), PuLP, Pandas, PostgreSQL, APIs de proveedores, Streamlit dashboard

---

### 5. Chatbots para Atención al Cliente Inmobiliario

**Descripción:**
Asistentes virtuales inteligentes especializados en atención al cliente para inmobiliarias y constructoras. Responden consultas sobre proyectos, programan visitas, califican leads y entregan información personalizada 24/7.

**Casos de Uso:**
- Atención de consultas en sitio web del proyecto inmobiliario
- Calificación automática de leads (presupuesto, timeline de compra, preferencias)
- Agendamiento automático de visitas a sala de ventas
- Seguimiento post-visita automatizado
- Atención de post-venta (estado de obra, entrega, garantías)

**Deliverables:**
- Chatbot desplegado en sitio web y WhatsApp Business
- Panel de administración para actualizar información del proyecto
- Integración con CRM del cliente (HubSpot, Salesforce u otro)
- Dashboard de métricas: leads generados, consultas atendidas, satisfacción
- Entrenamiento inicial con FAQ del proyecto + ajustes mensuales

**Timeline:** 3-5 semanas

**Stack:** LangChain, Claude API, FastAPI, WhatsApp Business API, React, PostgreSQL, HubSpot API

---

### 6. Automated Reporting (Reportes Automatizados)

**Descripción:**
Sistemas que recopilan datos de múltiples fuentes (ERP, planillas, fotos de obra, sensores) y generan reportes profesionales de forma automática. Libera al equipo de obra de horas dedicadas a compilar información en Excel y PowerPoint.

**Casos de Uso:**
- Informe semanal de avance de obra (generado automáticamente cada viernes)
- Reporte mensual a mandante con KPIs, fotos y análisis
- Dashboard ejecutivo para directorio con estado de todos los proyectos
- Reportes de seguridad con estadísticas y tendencias
- Informes de calidad con tracking de No Conformidades

**Deliverables:**
- Pipeline de datos automatizado conectado a fuentes del cliente
- Templates de reportes personalizados según destinatario
- Dashboard web interactivo con drill-down por proyecto
- Distribución automática por correo según calendario configurado
- Capacitación a equipo administrativo para gestión del sistema

**Timeline:** 4-6 semanas

**Stack:** Python, Pandas, Jinja2 (templates), WeasyPrint (PDF), Power BI/Streamlit, PostgreSQL, APIs de fuentes de datos, cron jobs/Airflow

---

## Requisitos de Datos y Proceso de Preparación

### Datos Necesarios (varía por servicio)
- **Computer Vision:** Acceso a cámaras de obra existentes o instalación de nuevas. Mínimo 2 semanas de imágenes históricas para entrenamiento.
- **Predictive Analytics:** Datos históricos de al menos 3-5 proyectos completados (costos, plazos, avance). Mientras más datos, mejores predicciones.
- **NLP:** Documentos técnicos en formato digital (PDF searchable idealmente). Mínimo 50-100 documentos para entrenamiento efectivo.
- **Supply Chain:** Registros de órdenes de compra, inventario, tiempos de entrega (idealmente 12+ meses).

### Proceso de Preparación de Datos

1. **Auditoría de Datos (Semana 1):** Identificamos qué datos existen, en qué formato y calidad.
2. **Limpieza y Estructuración (Semanas 2-3):** Normalización, eliminación de duplicados, manejo de datos faltantes.
3. **Feature Engineering (Semana 3-4):** Creación de variables derivadas relevantes para el modelo.
4. **Validación con Expertos (Semana 4):** El equipo del cliente valida que los datos procesados tienen sentido.
5. **Entrenamiento y Evaluación (Semanas 5-6):** Entrenamiento de modelos con datos preparados, evaluación de performance.

### Política de Datos
- Los datos del cliente son **propiedad exclusiva del cliente**
- Firmamos NDA antes de acceder a cualquier dato
- Utilizamos infraestructura cloud con encriptación en tránsito y en reposo
- No compartimos datos entre clientes ni los usamos para otros fines
- Al término del proyecto, los datos pueden ser eliminados de nuestros sistemas si el cliente lo solicita

---

## Stack Tecnológico Completo

| Categoría | Herramientas |
|-----------|-------------|
| Lenguajes | Python 3.11+, TypeScript |
| ML Frameworks | PyTorch, TensorFlow, scikit-learn, XGBoost |
| Computer Vision | OpenCV, YOLOv8, Detectron2, Segment Anything |
| NLP/LLM | LangChain, LlamaIndex, Claude API, OpenAI API |
| Vector Databases | Pinecone, Weaviate, ChromaDB |
| Backend | FastAPI, Django, Celery |
| Frontend | React, Next.js, Streamlit, Dash |
| Bases de Datos | PostgreSQL, MongoDB, Redis |
| Cloud | AWS (SageMaker, EC2, S3, Lambda), GCP (Vertex AI) |
| MLOps | MLflow, DVC, Docker, Kubernetes |
| Orquestación | Apache Airflow, Prefect |
| Visualización | Power BI, Streamlit, Plotly, D3.js |

---

## Diferenciadores

### 1. Modelos Específicos para Construcción
No aplicamos AI genérica. Nuestros modelos están entrenados con datos y contexto de la industria de la construcción chilena y latinoamericana. Entienden la diferencia entre una losa y un muro, entre un contrato EPC y uno por administración delegada.

### 2. Integración con Herramientas Existentes
No exigimos que el cliente cambie sus sistemas. Nos integramos con Procore, Primavera P6, MS Project, SAP, y los ERP y sistemas de gestión que ya usan las constructoras en Chile.

### 3. Enfoque Pragmático, No Académico
Entregamos soluciones que funcionan en obra, no papers de investigación. Cada modelo se valida con datos reales del cliente y se mide por su impacto en el negocio, no por métricas abstractas de accuracy.

### 4. Equipo Multidisciplinario
Nuestro equipo combina data scientists con experiencia en construcción: ingenieros civiles que programan, arquitectos que entienden machine learning, y profesionales BIM que hablan el lenguaje de los datos.

### 5. Escalabilidad Gradual
Proponemos partir con un piloto acotado (un proyecto, un caso de uso) y escalar gradualmente. No prometemos transformación digital instantánea — construimos confianza con resultados progresivos.

---

## Proceso de Trabajo

1. **Assessment Inicial (Semana 1):** Evaluación de madurez de datos, identificación de quick wins y oportunidades de alto impacto.
2. **Preparación de Datos (Semanas 2-4):** Recopilación, limpieza y estructuración de datos necesarios.
3. **Desarrollo de Modelo (Semanas 4-8):** Entrenamiento iterativo con validación continua del cliente.
4. **Piloto Controlado (Semanas 8-10):** Despliegue en un proyecto piloto con monitoreo intensivo.
5. **Evaluación y Ajuste (Semana 10-11):** Análisis de resultados del piloto, ajustes al modelo.
6. **Rollout (Semana 12+):** Despliegue en más proyectos, capacitación ampliada, soporte continuo.

---

*Meta Build City — Inteligencia artificial con los pies en la obra.*
