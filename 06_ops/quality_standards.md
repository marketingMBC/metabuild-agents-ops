# Estándares de Calidad — Meta Build City

> **Versión:** 2.0 | **Última actualización:** Febrero 2026
> **Aplica a:** Todos los entregables de servicios MBC (XR, AI, Blockchain, Marketing Digital, BIM)
> **Responsable:** QA Lead / Project Lead (en ausencia de QA dedicado)

---

## Quality Philosophy

**"Entregar como si fuera para nosotros mismos."**

En MBC, la calidad no es una fase al final del proyecto ni la responsabilidad de una sola persona. Es una cultura que permea todo el proceso, desde el discovery hasta el handoff. Cada miembro del equipo es responsable de la calidad de su trabajo.

**Principios fundamentales**:

1. **Prevention over detection**: Es más barato evitar un defecto que encontrarlo y corregirlo después. Invertimos en hacer las cosas bien desde el principio.
2. **Quality is everyone's responsibility**: No existe un "equipo de QA" separado que sea dueño de la calidad. Cada developer, diseñador y project manager es co-responsable.
3. **Client perspective first**: La calidad se mide desde la perspectiva del usuario final y del cliente, no desde nuestra perspectiva técnica interna.
4. **Continuous improvement**: Cada proyecto nos enseña algo. Documentamos, aprendemos y mejoramos el proceso.

---

## Quality Dimensions

Todo entregable de MBC se evalúa en estas 6 dimensiones de calidad:

### 1. Functional (¿Funciona como se especificó?)

- El entregable cumple con todos los requerimientos funcionales documentados
- Cada feature funciona correctamente en los escenarios especificados
- Los edge cases están manejados apropiadamente
- No hay funcionalidades faltantes respecto al scope acordado

**Cómo verificar**: Testing funcional contra documento de requerimientos (traceability matrix).

### 2. Performance (¿Cumple los benchmarks de rendimiento?)

- Tiempos de carga dentro de los límites aceptables
- Rendimiento estable bajo condiciones normales de uso
- No hay memory leaks o degradación con el tiempo
- Benchmarks específicos por servicio (ver sección QA por servicio)

**Cómo verificar**: Testing de performance con herramientas específicas por plataforma.

### 3. Usability (¿Es intuitivo para el usuario final?)

- El usuario puede completar las tareas principales sin ayuda
- La interfaz es consistente y predecible
- Los mensajes de error son claros y útiles
- La navegación es lógica y eficiente
- Accesibilidad básica cumplida (contraste, tamaño de texto, etc.)

**Cómo verificar**: Testing de usabilidad con usuarios reales o representativos. Heuristic evaluation.

### 4. Reliability (¿Funciona consistentemente?)

- El sistema funciona de forma estable sin crashes ni errores inesperados
- Los datos se guardan y recuperan correctamente
- El sistema se recupera gracefully de errores
- Funciona en todas las plataformas/dispositivos especificados

**Cómo verificar**: Testing de estabilidad, testing en múltiples dispositivos/browsers, stress testing.

### 5. Security (¿Es seguro y protege los datos?)

- No hay vulnerabilidades conocidas sin parchear
- Los datos sensibles están encriptados (at rest y in transit)
- Autenticación y autorización implementadas correctamente
- Cumplimiento con regulaciones de protección de datos (Ley 19.628 Chile, GDPR si aplica)
- No hay credentials hardcodeados en el código

**Cómo verificar**: Security review, penetration testing (en proyectos críticos), code review enfocado en seguridad.

### 6. Maintainability (¿Se puede mantener después del handoff?)

- Código limpio, organizado y bien documentado
- Arquitectura modular y extensible
- Documentación técnica completa y actualizada
- Dependencias mínimas y bien justificadas
- Logs y monitoring implementados para debugging futuro

**Cómo verificar**: Code review por peer, revisión de documentación, checklist de maintainability.

---

## QA Process por Servicio

### XR (Realidad Extendida: VR/AR/MR)

**Device Testing Matrix**:

| Device / Plataforma | Priority | Testing Requerido |
|---------------------|:--------:|-------------------|
| Meta Quest 3 | Alta | Full testing |
| Meta Quest Pro | Media | Compatibility testing |
| Meta Quest 2 | Media | Compatibility testing |
| Apple Vision Pro | Baja (si aplica) | Compatibility testing |
| HoloLens 2 | Baja (si aplica) | Full testing |
| WebXR (Chrome/Edge) | Media | Browser testing |
| iOS (ARKit) | Alta (si aplica) | Full testing |
| Android (ARCore) | Alta (si aplica) | Full testing |
| Desktop (PC/Mac) | Alta (si aplica) | Full testing |

**Performance Benchmarks XR**:

| Métrica | Target VR (Quest) | Target AR (Mobile) | Target WebXR | Crítico |
|---------|:-----------------:|:------------------:|:------------:|:-------:|
| FPS (Frames Per Second) | >= 72 FPS | >= 30 FPS | >= 60 FPS | Sí — bajo FPS causa motion sickness |
| Load time (initial) | < 10 seg | < 5 seg | < 8 seg | Sí |
| Draw calls | < 200 | < 100 | < 150 | No |
| Polygon count (scene) | < 2M tris | < 500K tris | < 1M tris | No |
| Texture memory | < 1GB | < 256MB | < 512MB | No |
| App size | < 2GB | < 200MB | N/A | No |

**UX Testing Checklist XR**:
- [ ] Experiencia no causa motion sickness (no judder, no sudden movements)
- [ ] Locomotion es cómoda (teleport vs smooth, opciones de comfort)
- [ ] UI elements son legibles y alcanzables
- [ ] Interacciones son intuitivas (grab, point, click)
- [ ] Audio spatial funciona correctamente (si aplica)
- [ ] Tutorial/onboarding es claro para usuarios nuevos en XR
- [ ] Performance se mantiene estable durante toda la experiencia (no drops)
- [ ] Sesión de testing de al menos 15 min sin fatiga excesiva

### AI (Inteligencia Artificial / Machine Learning)

**Model Accuracy Metrics**:

| Métrica | Descripción | Target Mínimo | Ideal |
|---------|------------|:-------------:|:-----:|
| Precision | % de predicciones positivas que son correctas | >85% | >92% |
| Recall | % de positivos reales que el modelo detecta | >80% | >90% |
| F1 Score | Media armónica de precision y recall | >82% | >91% |
| Accuracy | % de predicciones totales correctas | >85% | >93% |
| AUC-ROC | Capacidad de discriminación del modelo | >0.85 | >0.95 |

**Nota**: los targets específicos se ajustan por caso de uso. Un modelo de detección de defectos en obra tiene diferentes requerimientos que un modelo de predicción de costos.

**AI QA Checklist**:
- [ ] Training data documentada: fuente, tamaño, distribución, preprocessing
- [ ] Model versioning implementado (MLflow, Weights & Biases, o equivalente)
- [ ] A/B testing realizado comparando modelo nuevo vs baseline
- [ ] Bias check: verificar que el modelo no tiene sesgos indeseados en los datos o resultados
- [ ] Edge cases probados: inputs inusuales, datos missing, outliers
- [ ] Performance en producción monitoreada (model drift detection)
- [ ] Latencia de inferencia aceptable para el caso de uso (< X ms)
- [ ] Fallback implementado: qué pasa si el modelo falla o no tiene confianza suficiente
- [ ] Documentación del modelo: arquitectura, hyperparámetros, métricas, limitaciones conocidas

### Blockchain / Smart Contracts

**Contract Auditing Checklist**:
- [ ] Código del smart contract revisado línea por línea por al menos 2 personas
- [ ] Vulnerabilidades conocidas verificadas (reentrancy, overflow, front-running, etc.)
- [ ] Testing de cada función con inputs válidos e inválidos
- [ ] Testing de edge cases y boundary conditions
- [ ] Access control verificado: ¿quién puede llamar cada función?
- [ ] Eventos (events) implementados para tracking y auditabilidad
- [ ] Upgradability strategy definida (si el contrato es upgradeable)

**Gas Optimization**:
- [ ] Gas usage por función medido y documentado
- [ ] Optimizaciones implementadas donde el costo es significativo
- [ ] Storage vs memory usage optimizado
- [ ] Batch operations donde sea posible (reducir transacciones individuales)

**Security Review**:
- [ ] Testing con herramientas automatizadas (Slither, Mythril, o equivalente)
- [ ] Auditoría externa para contratos que manejan fondos significativos (> $10K USD)
- [ ] Testnet deployment y testing antes de mainnet
- [ ] Multi-sig wallet para admin functions (si aplica)
- [ ] Emergency pause mechanism implementado
- [ ] Rate limiting para funciones críticas

### Marketing Digital

**Brand Consistency**:
- [ ] Colores de marca correctos (verificar hex codes)
- [ ] Tipografía correcta (font family, weights, sizes)
- [ ] Logo usado correctamente (versión, tamaño mínimo, clear space)
- [ ] Tono de voz alineado con brand guidelines del cliente
- [ ] Imágenes de calidad apropiada (resolución, composición)

**Grammar / Tone Review**:
- [ ] Ortografía revisada (español e inglés según corresponda)
- [ ] Gramática correcta
- [ ] Tono consistente con la marca y la audiencia
- [ ] CTAs claros y accionables
- [ ] No hay contenido placeholder o lorem ipsum en producción

**Analytics Tracking Verification**:
- [ ] Google Analytics 4 (o equivalente) configurado correctamente
- [ ] UTM parameters en todos los links de campaña
- [ ] Eventos de conversión definidos y funcionando
- [ ] Goals/objetivos configurados
- [ ] Tag Manager funcionando (si se usa)
- [ ] Pixel de remarketing activo (Facebook, LinkedIn, etc.)
- [ ] Datos de testing verificados en analytics antes de lanzar

### BIM (Building Information Modeling)

**Model Checking**:
- [ ] Verificación con Solibri Model Checker (o equivalente)
- [ ] Clash detection ejecutada y conflictos resueltos (0 hard clashes)
- [ ] Soft clashes identificados y documentados (tolerancias definidas)

**LOD (Level of Development) Verification**:
- [ ] LOD correcto según fase del proyecto y contrato
  - LOD 100: Conceptual (massing, ubicación)
  - LOD 200: Approximate geometry (tamaño, forma genérica)
  - LOD 300: Precise geometry (tamaño, forma, ubicación exacta)
  - LOD 350: LOD 300 + interfaces con otros sistemas
  - LOD 400: Fabrication-ready (detalle para fabricación)
  - LOD 500: As-built (verificado en campo)
- [ ] Cada elemento modelado al LOD especificado (no sobre-modelar ni sub-modelar)
- [ ] Información paramétrica completa según LOD (materiales, propiedades, clasificaciones)

**IFC Compliance**:
- [ ] Export a IFC verificado (IFC 2x3 o IFC4 según requerimiento)
- [ ] Información de clasificación correcta (UniClass, OmniClass, etc.)
- [ ] Propiedades del modelo intactas después de export
- [ ] Verificación en visor IFC independiente (BIMcollab Zoom, Solibri, xBIM)

**BIM Standards Compliance**:
- [ ] Naming conventions seguidas (archivos, views, familias/componentes)
- [ ] Worksets/structure organizados según estándar del proyecto
- [ ] Templates de proyecto aplicados correctamente
- [ ] Coordenadas compartidas configuradas correctamente
- [ ] BIM Execution Plan (BEP) cumplido

---

## Review Checklist — Todos los Proyectos

Este checklist aplica a TODOS los entregables de MBC, independiente del servicio.

### Pre-Delivery Review

- [ ] **Peer review completado**: otro miembro del equipo (no el autor) revisó el código/modelo/contenido
- [ ] **Tests passing**: todos los tests automatizados + manuales están pasando
- [ ] **Documentation complete**: documentación técnica y de usuario actualizada y completa
- [ ] **Requirements traceability**: cada requerimiento del cliente tiene un entregable que lo satisface (traceability matrix)
- [ ] **Performance benchmarks achieved**: métricas de performance dentro de los targets definidos
- [ ] **Security review completed**: no hay vulnerabilidades conocidas sin resolver
- [ ] **Deployment checklist followed**: el proceso de deploy está documentado y fue seguido paso a paso
- [ ] **Client UAT approved**: el cliente probó y aprobó el entregable en ambiente de staging

### Traceability Matrix (Template)

| # | Requerimiento | Descripción | Entregable | Testing | Status |
|---|--------------|------------|-----------|---------|--------|
| R1 | {req} | {descripción} | {feature/componente} | {cómo se probó} | Pass / Fail |
| R2 | {req} | {descripción} | {feature/componente} | {cómo se probó} | Pass / Fail |
| R3 | {req} | {descripción} | {feature/componente} | {cómo se probó} | Pass / Fail |

---

## Quality Metrics — KPIs

### Métricas Operacionales

| Métrica | Definición | Target | Cómo Medir |
|---------|-----------|--------|-----------|
| **Defect rate post-delivery** | % de bugs/issues reportados por el cliente en los 30 días post-delivery | <5% de los requerimientos | Conteo de issues / total requerimientos |
| **Client satisfaction** | Puntuación de encuesta post-proyecto | >4.5 / 5 | Encuesta de satisfacción |
| **On-time delivery** | % de milestones entregados en la fecha acordada | >90% | Fecha real vs fecha planificada |
| **Rework rate** | % de trabajo que tuvo que rehacerse por defectos de calidad | <10% | Horas de rework / horas totales |
| **First-pass yield** | % de entregables aprobados por el cliente sin correcciones | >80% | Entregables aprobados a la primera / total entregables |
| **Code/model peer review coverage** | % de código/modelos que pasaron por peer review | 100% | Reviews completados / items entregados |

### Tracking y Reporting

- **Por proyecto**: métricas actualizadas en cada sprint review
- **Mensual**: consolidado de métricas de calidad de todos los proyectos activos
- **Trimestral**: análisis de tendencias, comparación con trimestres anteriores, action items

### Dashboard de Calidad (Template)

```
QUALITY DASHBOARD — MBC — {Mes/Trimestre}

Proyectos activos: {#}
Proyectos entregados este período: {#}

| Proyecto | Defect Rate | Client Sat | On-Time | Rework Rate | First-Pass |
|----------|:----------:|:----------:|:-------:|:-----------:|:----------:|
| {proj 1} | {%}        | {x/5}      | {%}     | {%}         | {%}        |
| {proj 2} | {%}        | {x/5}      | {%}     | {%}         | {%}        |
| PROMEDIO  | {%}        | {x/5}      | {%}     | {%}         | {%}        |
| TARGET    | <5%        | >4.5       | >90%    | <10%        | >80%       |

Issues encontrados este período: {#}
Issues resueltos: {#}
Issues abiertos: {#}

Top issues:
1. {issue más frecuente}: {causa raíz} → {acción correctiva}
2. {segundo issue}: {causa raíz} → {acción correctiva}
```

---

## Continuous Improvement

### Post-Mortem después de Cada Proyecto

Obligatorio para todo proyecto. El post-mortem no es para buscar culpables, sino para aprender.

**Preguntas clave**:
1. ¿Qué salió bien que debemos repetir?
2. ¿Qué no salió bien que debemos evitar?
3. ¿Qué aprendimos que no sabíamos antes?
4. ¿Qué cambiaríamos si hiciéramos el proyecto de nuevo?
5. ¿Hay algo que debemos actualizar en nuestros procesos, templates o estándares?

**Output**: action items concretos con owner y deadline (ver template en project_management.md).

### Quarterly Quality Review

Cada trimestre, dedicar una sesión de 2-3 horas a revisar la calidad de forma transversal:

**Agenda**:
1. Revisar métricas de calidad del trimestre (30 min)
2. Analizar defectos recurrentes: ¿hay patrones? ¿qué servicio tiene más issues? (30 min)
3. Revisar feedback de clientes: ¿qué dicen las encuestas de satisfacción? (20 min)
4. Evaluar herramientas y procesos: ¿están funcionando? ¿hay algo que cambiar? (30 min)
5. Definir action items para el próximo trimestre (30 min)

### Lessons Learned Database

Mantener en Notion una base de datos de lecciones aprendidas:

| Fecha | Proyecto | Tipo | Lección | Impacto | Acción Tomada |
|-------|---------|------|---------|---------|---------------|
| {fecha} | {nombre} | Technical/Process/Communication | {qué aprendimos} | {alto/medio/bajo} | {qué cambiamos} |

**Regla**: cada post-mortem debe agregar al menos 1 lección a esta base de datos.

### Tool and Process Updates

Los estándares de calidad son un documento vivo. Se actualizan cuando:

- Un post-mortem identifica un gap en los estándares
- Adoptamos una nueva herramienta o tecnología
- Un cliente tiene un requerimiento que expone una carencia
- La quarterly review identifica una mejora necesaria
- Cambia una regulación o estándar de la industria (BIM, blockchain, seguridad)

**Proceso de actualización**:
1. Proponer cambio (cualquier miembro del equipo)
2. Revisar y discutir en el equipo
3. Aprobar el cambio (Tech Lead o CEO)
4. Actualizar este documento
5. Comunicar al equipo (Slack + reunión si es un cambio significativo)
6. Incrementar versión del documento

---

## Estándares por Tipo de Entregable — Quick Reference

### Código (Software, XR, AI, Smart Contracts)

- [ ] Código versionado en Git (GitHub)
- [ ] Convenciones de naming seguidas (por lenguaje/framework)
- [ ] Comentarios en secciones complejas
- [ ] No hay código muerto ni TODOs sin resolver en producción
- [ ] .gitignore configurado (no subir node_modules, .env, builds, etc.)
- [ ] README.md con instrucciones de setup y deployment
- [ ] Tests automatizados para funcionalidades críticas
- [ ] Peer review aprobado antes de merge a main

### Modelos 3D / BIM

- [ ] Archivo nombrado según convención del proyecto
- [ ] Modelo limpio: sin elementos duplicados, sin geometría basura
- [ ] Escala y coordenadas correctas
- [ ] LOD verificado contra especificación
- [ ] Export verificado (IFC, FBX, OBJ según necesidad)
- [ ] Archivo optimizado para su uso final (XR, rendering, coordinación)

### Documentos y Presentaciones

- [ ] Formato profesional con branding MBC (o del cliente si aplica)
- [ ] Ortografía y gramática revisada
- [ ] Contenido verificado contra fuentes
- [ ] Números y datos double-checked
- [ ] Versión final claramente marcada (no drafts)
- [ ] Exportado en formato correcto (PDF para entrega, editable para colaboración)

### Assets de Marketing

- [ ] Alineado con brand guidelines
- [ ] Resolución apropiada para el canal de distribución
- [ ] Copy revisado por tone and grammar
- [ ] Links verificados (no hay links rotos)
- [ ] Tracking implementado (UTMs, pixels)
- [ ] Responsive / adaptado para mobile
