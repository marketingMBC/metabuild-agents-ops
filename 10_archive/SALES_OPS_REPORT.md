# MetaBuild Smart — Reporte Estratégico de Sales Ops & Revenue
## Head of Sales Ops & Revenue Strategist Report

**Fecha:** 2026-02-12
**Analista:** Claude (Sales Ops AI)
**Fuentes de datos:**
- CRM Lite (`crm_lite.md`) — 8 contactos estructurados
- Pipeline (`pipeline.md`) — 5 deals activos
- Base Notion (`contacts_data.json`) — 45 contactos de eventos y networking
- Enrichment Data (`contact_report.json`) — 30 organizaciones scrapeadas
- Feria CSV (`Base de datos - Metabuild City.xlsx`) — 39 organizaciones de ferias

**Total de registros analizados:** 92 organizaciones únicas, ~75 contactos con nombre identificado

---

# FASE 1 — AUDITORÍA DE LA BASE DE CONTACTOS

## 1.1 Estado General de la Base

| Fuente | Registros | Con Email | Con Teléfono | Con Cargo | Con Pain/Interés | Completitud |
|--------|-----------|-----------|--------------|-----------|-------------------|-------------|
| CRM Lite | 8 | 8 (100%) | 8 (100%) | 8 (100%) | 8 (100%) | **95%** |
| Notion DB | 45 | 31 (69%) | 5 (11%) | 28 (62%) | 35 (78%) | **45%** |
| Feria CSV | 39 | ~10 (26%) | ~5 (13%) | ~20 (51%) | ~30 (77%) | **35%** |

### Completitud Global Promedio: **48%** — ALERTA ROJA

## 1.2 Campos Críticos Faltantes

| Campo | % Vacío | Impacto | Recomendación |
|-------|---------|---------|---------------|
| **Email** | 35% | ALTO — no se puede hacer outreach | Enriquecer vía LinkedIn Sales Nav o scraping |
| **Teléfono** | 75% | MEDIO — WhatsApp es canal clave en Chile | Solicitar en primera interacción |
| **Cargo** | 38% | ALTO — no sabemos si es decision maker | Investigar LinkedIn antes de contactar |
| **Segmento/Industria** | 60% (Notion) | ALTO — no se puede segmentar | Clasificar manualmente cada contacto |
| **Sitio web** | 40% | BAJO — es complementario | Buscar vía Google |
| **Fecha reunión** | 90% | MEDIO — no hay tracking de timing | Registrar en próxima interacción |

## 1.3 Inconsistencias Detectadas

### Duplicados entre fuentes (10 organizaciones)
| Organización | CRM | Notion | Feria | Contactos Distintos | Acción |
|---|---|---|---|---|---|
| Echeverría Izquierdo | Andrés Matte | Rodrigo (pivelic@ei.cl) | Rodrigo | 2 contactos reales | **OPORTUNIDAD**: 2 puertas de entrada a la misma empresa |
| Inmobiliaria Almagro | Martín Benavides | Francisca Gonzalez | Francisca | 2 contactos reales | **OPORTUNIDAD**: Martín=Marketing, Francisca=Innovación → multi-thread |
| Holo | — | Daniel Quevedo | Daniel Quevedo | 1 contacto | Consolidar en un solo registro |
| Ingevec | — | J.T. Poblete | J.T. Poblete | 1 contacto | Consolidar |
| Wbuild | — | Daniel Pardo | Daniel Pardo | 1 contacto | Consolidar |
| CChC | — | Eduardo Hernández | Eduardo Hernández | 1 contacto | Consolidar |
| Un Techo Para Chile | — | Jose Segovia | Jose Segovia | 1 contacto | Consolidar |
| Minverso | — | Matías | Matías | 1 contacto | Consolidar |
| Loping | — | Iván | Iván | 1 contacto | Consolidar |
| Imova | — | Daniel Iribarren | Daniel Iribarren | 1 contacto | Consolidar |

### Problemas de calidad de datos
1. **Emails con errores**: `plagges@sentiovr.com (ejecutivo comercial` — contiene texto extra en el campo email
2. **Contactos sin nombre**: 8 registros en Notion sin campo "Contacto" (COMPITE, Mutual de seguridad, iBIM, EDIFICA, CYGEM, etc.)
3. **Emails genéricos vs personales**: `comprascorporativa@mutual.cl`, `ventas@edifica.cl`, `contacto@cipycs.cl` — baja tasa de respuesta esperada
4. **Clasificación Hot/Warm/Cold inconsistente**: Novatec tiene un dolor urgente (accidente laboral) pero está como `#Warm`. Debería evaluarse como `#Hot`.
5. **Fechas obsoletas**: Los registros del CRM están con fechas de 2025. Si estos son datos reales, llevan ~12 meses sin actualización.
6. **Status en Notion poco informativo**: Mayoría en "Sin empezar" o vacío — no hay distinción entre los que se contactaron vs no.

## 1.4 Leads Ocultos de Alto Potencial

Estos contactos están "enterrados" en la base pero tienen señales fuertes:

| # | Organización | Contacto | Señal Oculta | Score Preliminar |
|---|---|---|---|---|
| 1 | **ETAC** (grúas) | Santiago Urrutia | Mencionaron que EI necesita capacitación para riggers → referral directo a deal activo de $85K | HIGH |
| 2 | **Francisca Gonzalez** (Almagro) | Francisca | 2do contacto en Almagro, lado innovación/calidad. Quiere VR para capacitación de administración de edificios → necesidad concreta | HIGH |
| 3 | **Parque Cordillera** | Carlos | CLIENTE EXISTENTE que ya tiene metaverso construido. Upsell de modelo Sponsor → revenue recurrente | HIGH |
| 4 | **MK** (cerámicos) | Carolina Cortes | Gerente Visual de proveedor de materiales. VR/AR para visualización de productos cerámicos en obra → caso de uso concreto | MEDIUM |
| 5 | **Claro LAB 5G** | Sebastián Guerrero | 5G + XR es combo natural. Potencial partnership tecnológico con Claro | MEDIUM |
| 6 | **NUEVO PUDAHUEL** | Eduardo Gallego | Aeropuerto = infraestructura de gran escala + presupuesto alto | MEDIUM |
| 7 | **Mutual de Seguridad** | (sin nombre) | Prevención de riesgos + XR safety training → alineación perfecta con servicio existente | MEDIUM |

## 1.5 Evaluación de la Clasificación Hot/Warm/Cold Actual

| Clasificación Actual | Contactos | Evaluación | Ajustes Necesarios |
|---|---|---|---|
| Hot (3) | Matte, Vial, Benavides | **Correcta** — deals activos con presupuesto confirmado | Mantener |
| Warm (2) | Sabbagh, Undurraga | **Parcialmente correcta** — Novatec (accidente reciente) debería ser HOT por urgencia del dolor | Subir Novatec a Hot |
| Cold (2) | Campos, Pérez-Cotapos | **Correcta** — sin respuesta o interacción mínima | Mantener |
| Sin clasificar (~75) | Todos los de Notion/Feria | **PROBLEMA GRAVE** — 85% de la base sin clasificar | Aplicar scoring (Fase 2) |

---

# FASE 2 — MODELO DE SCORING INTELIGENTE (0-100)

## 2.1 Metodología de Scoring

| Factor | Peso | Rango | Criterios |
|--------|------|-------|-----------|
| **Nivel de Relación** | 0-25 | Negociación activa=25, Propuesta enviada=20, Discovery=15, Meeting/call=12, Contacto bueno en evento=10, Email exchange=7, Contacto breve=3, Sin contacto=0 |
| **Tamaño Empresa / Potencial de Gasto** | 0-20 | Enterprise (>500 emp)=20, Mid-market (50-500)=15, PYME (10-50)=10, Startup/Micro=5, Desconocido=3 |
| **Alineación con Industria** | 0-20 | Construcción/Inmobiliaria directa=20, Infraestructura/adyacente=15, Educación-construcción=12, Tech-construcción=10, Otro relevante=5, Sin relación=0 |
| **Dolor Detectado** | 0-20 | Dolor explícito + presupuesto=20, Dolor explícito=15, Interés concreto=10, Interés genérico=5, Ninguno=0 |
| **Madurez Digital** | 0-10 | Ya usa XR/AI/BIM=10, Explorando activamente=7, Tiene algo de tech=5, Tradicional=3, Desconocido=2 |
| **Capacidad de Pago** | 0-5 | Presupuesto confirmado=5, Empresa grande=4, Mediana=3, Pequeña/desconocida=2, ONG/startup=1 |

### Umbrales de clasificación
| Rango | Clasificación | Significado |
|-------|---------------|-------------|
| **75-100** | **HOT** | Oportunidad activa, prioridad máxima, acción en <7 días |
| **55-74** | **WARM** | Potencial real, requiere nurturing activo, acción en 2-4 semanas |
| **35-54** | **COLD** | Potencial futuro, nurturing pasivo (newsletter, contenido) |
| **0-34** | **ARCHIVE** | Sin potencial comercial directo, mantener en red |

## 2.2 Scoring Completo — Top Tier (Clientes Potenciales Directos)

### SEGMENTO HOT (75-100)

| # | Score | Organización | Contacto | Cargo | Industria | Servicio Probable | Valor Est. | Justificación |
|---|-------|---|---|---|---|---|---|---|
| 1 | **90** | Inmobiliaria Almagro | Martín Benavides | Gerente Marketing | Inmobiliaria | XR Tours + Marketing | $45,000 | Negociación activa, presupuesto aprobado, pidió descuento por volumen |
| 2 | **87** | Echeverría Izquierdo | Andrés Matte | Gte. Innovación | Constructora | AI Monitoring + BIM | $85,000 | Discovery completa, dolor claro, presupuesto $100K aprobado |
| 3 | **85** | Fundamenta | Carolina Vial | Gte. Comercial | Inmobiliaria | XR Virtual Tours | $22,000 | Propuesta enviada, demo exitosa ("esto es lo que necesitamos") |
| 4 | **77** | Inmobiliaria Almagro | Francisca Gonzalez | Sub Gte. Innovación | Inmobiliaria | XR Training | $25,000 | 2do contacto en Almagro, necesidad concreta (VR capacitación edificios) |
| 5 | **75** | Parque Cordillera | Carlos | Jefe Operaciones | Parques | Metabuild HUB Sponsor | $15,000 | Cliente existente, upsell, relación construida, metaverso ya operativo |

### SEGMENTO WARM (55-74)

| # | Score | Organización | Contacto | Cargo | Industria | Servicio Probable | Valor Est. | Justificación |
|---|-------|---|---|---|---|---|---|---|
| 6 | **72** | Novatec | Patricio Undurraga | Gte. Operaciones | Constructora | XR Safety Training | $35,000 | Accidente reciente → dolor urgente. Receptivo. CORFO posible. |
| 7 | **69** | Ingevec Construcción | Jose T. Poblete | Gte. Innovación | Constructora | Publicidad + XR | $30,000 | Gran constructora, Gte Innovación interesado, quiere suscripción publicidad |
| 8 | **65** | Sabbagh Arquitectos | Felipe Sabbagh | Socio Director | Arquitectura | XR Visualization | $12,000 | Socio director interesado, proyecto hospital, reunión aceptada |
| 9 | **63** | CChC | Eduardo Hernández | Jefe Innovación | Gremio Construc. | Alianza / Eventos XR | $20,000 | Gatekeeper de la industria. Un partnership abre puertas masivas |
| 10 | **62** | Diplomado Const. 4.0 UC | Rodrigo Reyes | Jefe de Programa | Educación-Const. | XR Educación | $12,000 | Quiere hacer clase en metaverso + modelar aula 3D. Credibilidad UC |
| 11 | **60** | MOP | Roberto Campos | Jefe Div. Edificación | Gobierno | BIM Implementation | $60,000 | Gran valor pero ciclo largo. Mercado Público. Trabajar como lead a 6+ meses |
| 12 | **60** | ETAC | Santiago Urrutia | Gte. Innovación | Grúas (Construc.) | XR Training + Ads | $15,000 | Conexión directa con EI (deal de $85K). Riggers = caso uso safety training |
| 13 | **60** | Salfacorp | Ignacio Pérez-Cotapos | Subgte. Innovación | Constructora | AI + BIM + Blockchain | $80,000 | Enorme potencial pero sin respuesta aún. Buscar otro ángulo |
| 14 | **58** | Echeverría Izquierdo | Rodrigo (Pivelic) | Gte. Innovación | Constructora | XR + BIM | — | 2do contacto en EI, refuerza deal de $85K. Multi-threading |
| 15 | **58** | Un Techo Para Chile | Jose Segovia | Depto. Innovación | ONG/Social | XR Donaciones | $8,000 | Alto valor de PR y social impact. Newsletter + RRSS exposure |

### SEGMENTO COLD (35-54)

| # | Score | Organización | Contacto | Industria | Notas |
|---|-------|---|---|---|---|
| 16 | 53 | NUEVO PUDAHUEL | Eduardo Gallego | Infraestructura | Aeropuerto, alto presupuesto potencial, interés genérico |
| 17 | 52 | Mutual de Seguridad | (sin nombre) | Prev. Riesgos | Alineación perfecta con XR Safety. Necesita contacto |
| 18 | 50 | Wbuild | Daniel Pardo | PropTech/Blockchain | Startup, CEO simpático pero sin deal concreto |
| 19 | 50 | ECCUC | Benjamín Navarrete | Educación UC | Director Docencia, dio espacio para presentar en charla blockchain |
| 20 | 48 | iBuilder | Rolando Cáceres | TI Construcción | Fundador, competitor parcial pero potencial partner/cliente |
| 21 | 48 | MK (cerámicos) | Carolina Cortes | Materiales Constr. | Gerente Visual. VR para visualización de cerámicos |
| 22 | 47 | EDIFICA | (sin nombre) | Feria Construcción | Canal de eventos, no cliente directo |
| 23 | 45 | Montessori Educ | Alfonso Barek | Educación (Ecuador) | VR tours para colegio. Internacional. Timing no inmediato |
| 24 | 45 | Diplomado Blockchain UC | Jaime Navón | Educación UC | Red de alumni en CS, blockchain collaboration |
| 25 | 45 | Magister en Construcción UC | Agustín Delgado | Educación UC | Jefe Programa, ideas sociales (viviendas Techo), Semana I |
| 26 | 43 | Yelli | Gustavo Urrutia | Blockchain RE | Startup, Real Estate + blockchain |
| 27 | 42 | DECON UC | Camilo Guzmán | Educación UC | Laboratorio, quiere mejorar experiencia estudiantil |
| 28 | 41 | HAIKENLAB | Susana Castro | Tech/Financ. | Financiamiento proyectos virtuales, FILL 2025 |
| 29 | 40 | INNOVEX | Javier González | Tech | Contacto FILL 2025, genérico |
| 30 | 40 | CITIC | María José Torres | Tech | Contacto FILL 2025, genérico |

### PARTNERS / ALIADOS (Track Separado)

| # | Organización | Contacto | Cargo | Tipo | Valor Estratégico |
|---|---|---|---|---|---|
| P1 | Hildebrandt Gruppe | Werner Hildebrandt | Socio Director | Referral cruzado | ALTO — Lean + Tech combo. Fuente de referrals |
| P2 | Holo | Daniel Quevedo | CEO | Co-opetitor XR | MEDIO — Puede referir o subcontratar |
| P3 | Imova | Daniel Iribarren | Gte. Comercial | Aliado VR | ALTO — Desarrollo VR, validó idea, quiere colaborar |
| P4 | Minverso | Matías | Co-fundador | Aliado XR Minería | MEDIO — Mismo desarrollo pero para minería |
| P5 | Sentio VR | Chaitanya Ravi | CEO | Tool partner | MEDIO — Suscripción gratuita a cambio de exposure |
| P6 | Lucid Dreams | Cristóbal Baixas | CEO | Aliado VR | BAJO — Contacto de evento |
| P7 | Naum | Francisco Díaz | — | Aliado VR Minería | BAJO — VR para minería |
| P8 | U de Talca | Ana Esther Feldman | Vicerrectoría Innov. | Academic partner | MEDIO — Fondos + estudiantes VR |
| P9 | CIPYCS | Heleny | Ventas | Dev VR partner | BAJO — Ofrecieron servicio, potencial subcontratación |

### ARCHIVE / BAJA PRIORIDAD (<35)

| Organización | Razón |
|---|---|
| Sorgard Team | No empáticos, sin capacidad ni interés |
| Party Rumble | Desarrolladores gaming, no construcción |
| Vulcano Services | Startup muy temprana, blockchain genérico |
| Romeo Sports | Viajes/deporte, sin relación a construcción |
| DRIFT360 | Interés en tours pero sin datos de empresa |
| Betterfly | Seguros de vida, no es cliente sino proveedor |
| Cadena Group | Consultor blockchain genérico, sin datos |
| Travel Security | Eventos cripto/viajes, no construcción |
| Magazine21 | Periodismo, posible PR channel pero no cliente |
| La Obra UC | Voluntariado, sin presupuesto |
| COMPITE | Asesoría PYMEs genérica |
| TechDesign | Sin información suficiente |
| CYGEM | Sin información suficiente |
| Claro LAB 5G | Contacto UC, partnership tech a largo plazo |

---

# FASE 3 — ESTRATEGIA POR SEGMENTO

## 3.1 Segmento HOT (Score 75-100) — 5 contactos

### Perfil
- Deals activos o con necesidad confirmada
- Decision makers identificados
- Presupuesto confirmado o muy probable
- Timeline: 0-30 días para cierre o avance significativo

### Estrategia

| Dimensión | Definición |
|-----------|-----------|
| **Canal recomendado** | WhatsApp/Teléfono directo → Email formal → Reunión presencial |
| **Tipo de mensaje** | Personalizado, orientado a resolver SU dolor específico |
| **Approach** | Consultivo, urgente pero no agresivo. Mostrar que entendemos su problema |
| **Frecuencia** | 2-3 touchpoints/semana hasta definición |

### Secuencia de 3 pasos para HOT

| Paso | Timing | Canal | Acción |
|------|--------|-------|--------|
| **1** | Día 0 | WhatsApp/Teléfono | Mensaje directo retomando última conversación. "Hola [Nombre], ¿cómo vas con [tema específico]? Tengo [entregable/propuesta/demo] listo para ti." |
| **2** | Día 2-3 | Email formal | Enviar propuesta revisada / material prometido / demo personalizada. Incluir deadline suave: "Idealmente me gustaría confirmar antes del [fecha] para asegurar disponibilidad del equipo." |
| **3** | Día 5-7 | Llamada + seguimiento email | "Quería asegurarme de que recibiste [X]. ¿Hay algo que pueda aclarar o ajustar? ¿Cuándo podríamos cerrar los detalles?" |

### Acciones inmediatas por contacto HOT

| Contacto | Acción Específica | Deadline |
|---|---|---|
| Martín Benavides (Almagro) | Enviar propuesta revisada con descuento paquete 2 proyectos | HOY |
| Andrés Matte (EI) | Preparar y enviar demo AI monitoring personalizada para Lo Barnechea | 48h |
| Carolina Vial (Fundamenta) | Follow-up telefónico para feedback de propuesta enviada | HOY |
| Francisca Gonzalez (Almagro) | Contactar vía email/WhatsApp para agendar reunión sobre VR training | Esta semana |
| Carlos (Parque Cordillera) | Presentar modelo Sponsor monetización del metaverso existente | Esta semana |

---

## 3.2 Segmento WARM (Score 55-74) — 10 contactos

### Perfil
- Interés confirmado pero sin deal formal
- Algunos con dolor detectado, otros con interés genérico
- Timeline: 30-90 días para avance a HOT

### Estrategia

| Dimensión | Definición |
|-----------|-----------|
| **Canal recomendado** | Email personalizado → LinkedIn → Teléfono/WhatsApp para agendar |
| **Tipo de mensaje** | Value-first: contenido relevante + oferta de conversar |
| **Approach** | Educativo y consultivo. Posicionarse como experto, no como vendedor |
| **Frecuencia** | 1 touchpoint/semana por 3-4 semanas |

### Secuencia de 3 pasos para WARM

| Paso | Timing | Canal | Acción |
|------|--------|-------|--------|
| **1** | Día 0 | Email personalizado | Contenido de valor relevante a su dolor/interés. No vender. "Vi este caso de [industria similar] que me recordó nuestra conversación. [Link/adjunto]" |
| **2** | Día 7 | LinkedIn + Email | Interactuar con su contenido en LinkedIn. Email: invitación a demo gratuita o workshop. "Estamos organizando [X], creo que te puede interesar." |
| **3** | Día 14 | WhatsApp/Teléfono | Contacto directo para agendar. "Hola [Nombre], ¿tendríamos 20 min esta semana para mostrarle algo que preparamos pensando en [su empresa]?" |

### Acciones inmediatas por contacto WARM

| Contacto | Acción Específica | Deadline |
|---|---|---|
| Novatec (Undurraga) | Enviar caso estudio XR Safety Training + info CORFO | Esta semana |
| Ingevec (Poblete) | Proponer reunión para presentar modelo de suscripción | 2 semanas |
| Sabbagh (Felipe) | Agendar discovery call (ya aceptó reunirse) | Esta semana |
| CChC (Hernández) | Proponer workshop XR para socios de la CChC | 2 semanas |
| Diplomado UC (Reyes) | Coordinar piloto de clase en metaverso | 2 semanas |
| MOP (Campos) | Enviar email + propuesta workshop BIM gratuito | Esta semana |
| ETAC (Urrutia) | Conectar con deal EI (capacitación riggers) | 2 semanas |
| Salfacorp (Pérez-Cotapos) | 2do intento: email con artículo AI en construcción | Esta semana |
| EI-Rodrigo (Pivelic) | Contactar para reforzar deal con Andrés Matte | 2 semanas |
| Techo (Segovia) | Proponer piloto VR para evento de donaciones | 3 semanas |

---

## 3.3 Segmento COLD (Score 35-54) — 15 contactos

### Perfil
- Contacto establecido pero sin interés confirmado
- Potencial futuro pero no inmediato
- Faltan datos para evaluar correctamente

### Estrategia

| Dimensión | Definición |
|-----------|-----------|
| **Canal recomendado** | Email automatizado (newsletter) + LinkedIn engagement pasivo |
| **Tipo de mensaje** | Contenido educativo, tendencias de industria, casos de éxito |
| **Approach** | Awareness y posicionamiento. Que piensen en MBC cuando tengan la necesidad |
| **Frecuencia** | 1 touchpoint/mes (newsletter) + engagement orgánico en LinkedIn |

### Secuencia de 3 pasos para COLD

| Paso | Timing | Canal | Acción |
|------|--------|-------|--------|
| **1** | Día 0 | Email (newsletter signup) | Agregar a lista de newsletter. Primer email: "Bienvenido a la comunidad MBC" con contenido de valor |
| **2** | Día 30 | Email + LinkedIn | Newsletter mensual con tendencias AEC + casos de éxito. Conectar en LinkedIn si no está conectado |
| **3** | Día 60 | Email de reactivación | "Hola [Nombre], hace tiempo conversamos sobre [tema]. Tenemos novedades que creo te interesan: [nuevo case study / evento / oferta]" |

---

# FASE 4 — GENERACIÓN DE OUTREACH

## 4.1 Email Template 1 — Constructoras & Inmobiliarias (HOT/WARM)

```
Asunto: [Nombre], una idea para [problema específico] en [nombre proyecto/empresa]

Estimado/a {{Nombre}},

{{Conexión personal: "Después de nuestra conversación en [evento/reunión]..."
O "Me referió [nombre]..." O "Vi el proyecto [X] que están desarrollando..."}}

En Meta Build City trabajamos con constructoras e inmobiliarias como
{{empresa similar o segmento}} para resolver exactamente ese desafío:
{{dolor detectado: "la falta de visibilidad de avance en tiempo real" /
"la baja velocidad de venta en sala" / "los riesgos de seguridad en obra"}}.

{{Resultado concreto}}: Nuestros clientes han logrado {{métrica: "reducir
incidentes un 40% con XR Safety Training" / "aumentar conversión en sala
de ventas un 25% con Virtual Tours" / "ahorrar 15 hrs/semana en reportes
con AI Monitoring"}}.

¿Tendría 20 minutos esta semana para mostrarle cómo esto aplicaría
a {{empresa del contacto}}? Puedo hacer una demo personalizada con datos
de su {{tipo de proyecto}}.

{{Propuesta de horario: "¿Le acomoda el jueves a las 10 o el viernes
a las 15?"}}

Quedo atento,
Rodrigo Requena
Meta Build City — Tecnología 4.0 para Construcción
+56 9 XXXX XXXX | metabuildcity.com
```

**Variables dinámicas:**
- `{{Nombre}}`: Nombre del contacto
- `{{Conexión personal}}`: Cómo lo conociste
- `{{Dolor detectado}}`: Del campo "Resumen breve" o notas
- `{{Resultado concreto}}`: Case study relevante al dolor
- `{{empresa del contacto}}`: Nombre de su empresa
- `{{tipo de proyecto}}`: Edificio, obra civil, vivienda social, etc.

---

## 4.2 Email Template 2 — Follow-up con Valor (WARM → HOT)

```
Asunto: Caso de éxito: cómo {{empresa similar}} resolvió {{problema}}

Hola {{Nombre}},

Te comparto un caso que me recordó nuestra conversación:

{{empresa similar}} enfrentaba {{problema similar al del contacto}}.
Implementamos {{servicio MBC}} y en {{timeframe}} lograron:
- {{Resultado 1}}
- {{Resultado 2}}
- {{Resultado 3}}

{{Enlace al case study o video demo}}

Si esto te hace sentido para {{empresa del contacto}}, me encantaría
mostrarte cómo se vería implementado en su contexto.

¿Cuándo podríamos conversar 15 minutos?

Saludos,
Rodrigo
```

---

## 4.3 Email Template 3 — Reactivación (COLD → WARM)

```
Asunto: {{Nombre}}, ¿sigue en pie el interés en {{tema}}?

Hola {{Nombre}},

Hace {{tiempo}} conversamos sobre {{tema/servicio}} para
{{empresa del contacto}}. Quería retomar el contacto porque
tenemos novedades:

{{Novedad relevante:
- "Acabamos de completar un proyecto similar con [empresa conocida]"
- "Lanzamos un nuevo servicio de [X] que se alinea con lo que discutimos"
- "Hay un evento de la CChC sobre [tema] donde estaremos presentando"
- "CORFO acaba de abrir una línea de financiamiento para innovación en construcción"
}}

{{Invitación suave: "Si el timing es mejor ahora, me encantaría retomar
la conversación. Si no, quedo disponible cuando sea oportuno."}}

Saludos cordiales,
Rodrigo
Meta Build City
```

---

## 4.4 Scripts WhatsApp (3 variantes)

### WhatsApp Script 1 — Retomar conversación (HOT)
```
Hola {{Nombre}}! 👋 Soy Rodrigo de Meta Build City.

¿Cómo va todo con {{tema/proyecto}}?

Tengo {{la propuesta revisada / la demo / el material}} que
quedamos de enviar. ¿Te lo mando por acá o prefieres por email?

También quería saber si podemos agendar {{próximo paso: reunión /
demo / llamada}} para esta semana. ¿Qué día te acomoda?
```

### WhatsApp Script 2 — Primer contacto post-evento (WARM)
```
Hola {{Nombre}}, soy Rodrigo de Meta Build City 🏗️

Nos conocimos en {{evento}}. Me quedó dando vueltas lo que
conversamos sobre {{tema}}.

Preparé {{algo de valor: un mini análisis / una propuesta
preliminar / un caso de estudio}} que creo te puede interesar.
¿Te lo comparto?

Quedo atento!
```

### WhatsApp Script 3 — Referido/Introducción (WARM)
```
Hola {{Nombre}}, soy Rodrigo de Meta Build City.

{{Referente}} me sugirió contactarte porque {{razón}}.

Nosotros en MBC nos especializamos en {{servicio relevante}}
para la industria de la construcción, y creo que podemos
aportar valor a {{empresa}}.

¿Tendrías 15 min esta semana para una breve llamada?
```

---

## 4.5 Script de Llamada Telefónica

```
APERTURA (30 seg):
"Hola {{Nombre}}, habla Rodrigo Requena de Meta Build City.
¿Tiene un minuto? [Esperar]

Lo llamo porque {{contexto: nos conocimos en X / me referido Y /
vi que están trabajando en Z}}."

GANCHO (30 seg):
"Nosotros en MBC ayudamos a {{tipo de empresa}} a resolver
{{dolor genérico del segmento}} usando {{servicio}}.

Por ejemplo, {{resultado de caso similar en 1 frase}}."

PREGUNTA DE CALIFICACIÓN (1 min):
"Cuénteme, ¿cómo están manejando actualmente {{problema}}
en {{empresa}}? ¿Es algo que les preocupa?"

[ESCUCHAR - tomar notas]

PROPUESTA (30 seg):
"Interesante. Basado en lo que me cuenta, creo que podríamos
{{propuesta concreta}}.

¿Le haría sentido agendar una reunión de 30 minutos donde le
muestre {{demo / propuesta / caso}} aplicado a su contexto?"

CIERRE:
"¿Qué día de la próxima semana le acomodaría? Tengo
disponibilidad el {{día}} a las {{hora}} o el {{día}} a las {{hora}}.

Perfecto, le envío una invitación de calendario ahora mismo.
Muchas gracias {{Nombre}}, hablamos el {{día}}."

SI NO TIENE TIEMPO:
"Entiendo perfectamente. ¿Le puedo enviar un email breve con
la información? Así lo revisa cuando pueda y vemos si vale la
pena conversar."
```

---

## 4.6 Mensaje LinkedIn

```
CONEXIÓN (si no están conectados):
"Hola {{Nombre}}, soy Rodrigo de Meta Build City. Nos dedicamos
a tecnología 4.0 para la industria de la construcción en Chile.

{{Contexto: "Vi tu perfil y noté que [algo relevante]" /
"Nos conocimos en [evento]" / "[Referente] me sugirió conectar"}}.

Me encantaría tenerte en mi red para compartir contenido relevante
del sector. ¡Saludos!"

MENSAJE POST-CONEXIÓN (si ya conectados):
"Hola {{Nombre}}! Noté que en {{empresa}} están {{actividad
relevante: desarrollando proyecto X / explorando innovación / etc}}.

En MBC estamos trabajando con empresas como la tuya en
{{servicio relevante}}. Tengo un {{caso de estudio / artículo /
invitación}} que creo te interesaría.

¿Te lo comparto por acá o prefieres una breve llamada?"
```

---

# FASE 5 — SISTEMA DE FOLLOW-UP (Estructura Notion)

## 5.1 Database Properties para Notion CRM

### Properties del Database Principal ("Pipeline MBC")

| Property | Tipo | Opciones / Formato | Obligatorio |
|---|---|---|---|
| **Contacto** | Title | Nombre completo | SI |
| **Organización** | Text | Nombre empresa | SI |
| **Email** | Email | — | SI |
| **Teléfono** | Phone | +56 9 XXXX XXXX | NO |
| **LinkedIn** | URL | — | NO |
| **Cargo** | Text | — | SI |
| **Segmento** | Select | Constructora / Inmobiliaria / Arquitectura / Gobierno / Educación / Tech / ONG / Otro | SI |
| **Score** | Number | 0-100 | SI |
| **Clasificación** | Formula | `if(prop("Score") >= 75, "🔥 HOT", if(prop("Score") >= 55, "🟡 WARM", if(prop("Score") >= 35, "❄️ COLD", "📦 ARCHIVE")))` | AUTO |
| **Stage** | Select | Lead / Qualified / Discovery / Proposal / Negotiation / Closed Won / Closed Lost / Partner | SI |
| **Servicio** | Multi-select | XR Tours / XR Training / XR Visualization / AI Monitoring / AI Analytics / BIM Implementation / BIM Coordination / Blockchain / Marketing Digital / Paquete | SI |
| **Valor Estimado** | Number (USD) | — | NO |
| **Valor Ponderado** | Formula | `prop("Valor Estimado") * if(prop("Stage") == "Lead", 0.1, if(prop("Stage") == "Qualified", 0.2, if(prop("Stage") == "Discovery", 0.35, if(prop("Stage") == "Proposal", 0.5, if(prop("Stage") == "Negotiation", 0.7, if(prop("Stage") == "Closed Won", 1, 0))))))` | AUTO |
| **Fuente** | Select | Evento / LinkedIn / Referido / Web / Outbound / Mercado Público | NO |
| **Evento** | Select | FILL 2025 / EtMDay 2025 / CFF2025 / Expo Travel / Expo Edifica / PlanBIM / Otro | NO |
| **Owner** | Person | — | SI |
| **Dolor Detectado** | Text (long) | Descripción del pain point | NO |
| **Último Contacto** | Date | — | SI |
| **Próxima Acción** | Text | Descripción de next step | SI |
| **Fecha Próxima Acción** | Date | — | SI |
| **Días sin Contacto** | Formula | `dateBetween(now(), prop("Último Contacto"), "days")` | AUTO |
| **Alerta Inactividad** | Formula | `if(prop("Días sin Contacto") > 21, "🚨 URGENTE", if(prop("Días sin Contacto") > 14, "⚠️ ALERTA", if(prop("Días sin Contacto") > 7, "👀 REVISAR", "✅ OK")))` | AUTO |
| **Notas** | Text (long) | Resumen de interacciones | NO |
| **Email Enviado** | Checkbox | — | NO |
| **Demo Realizada** | Checkbox | — | NO |
| **Propuesta Enviada** | Checkbox | — | NO |
| **Created** | Created time | Auto | AUTO |
| **Last Edited** | Last edited time | Auto | AUTO |

## 5.2 Vistas Recomendadas

### Vista 1: "Pipeline Board" (Kanban por Stage)
- **Tipo:** Board
- **Group by:** Stage
- **Sort:** Score (descending)
- **Filter:** Stage != "Closed Lost" AND Stage != "Partner"
- **Columnas visibles:** Contacto, Organización, Valor Estimado, Score, Alerta Inactividad

### Vista 2: "Prioridad Semanal" (Table filtrada)
- **Tipo:** Table
- **Filter:** `Fecha Próxima Acción <= Today + 7 days` OR `Alerta Inactividad contains "URGENTE" OR "ALERTA"`
- **Sort:** Score (descending), luego Fecha Próxima Acción (ascending)
- **Columnas:** Contacto, Organización, Stage, Score, Clasificación, Próxima Acción, Fecha Próxima Acción, Alerta Inactividad

### Vista 3: "Dashboard Métricas" (Table con cálculos)
- **Tipo:** Table
- **Group by:** Stage
- **Cálculos por grupo:** Count, Sum(Valor Estimado), Sum(Valor Ponderado)
- **Filter:** Stage != "Closed Lost"

### Vista 4: "Contactos por Segmento" (Board)
- **Tipo:** Board
- **Group by:** Segmento
- **Sort:** Score (descending)

### Vista 5: "Follow-up Tracker" (Calendar)
- **Tipo:** Calendar
- **Date property:** Fecha Próxima Acción
- **Colores:** Por Clasificación (HOT=rojo, WARM=amarillo, COLD=azul)

### Vista 6: "Partners & Aliados"
- **Tipo:** Table
- **Filter:** Stage == "Partner"
- **Columnas:** Contacto, Organización, Tipo alianza, Valor estratégico, Próxima Acción

## 5.3 Cadencia de Tracking Semanal

### Lunes (15 min) — Pipeline Review
```
Checklist:
□ Revisar Vista "Prioridad Semanal" → ¿Qué acciones tienen deadline esta semana?
□ Revisar alertas de inactividad → ¿Algún contacto lleva >14 días sin interacción?
□ Actualizar stages de deals que avanzaron o retrocedieron
□ Registrar actividades de la semana pasada que no se registraron
```

### Miércoles (10 min) — Mid-week Check
```
Checklist:
□ ¿Se ejecutaron las acciones del lunes? Si no, reprogramar
□ ¿Llegó algún nuevo lead? Agregar al pipeline con score
□ ¿Algún HOT necesita escalación o apoyo?
```

### Viernes (10 min) — Cierre Semanal
```
Checklist:
□ Actualizar "Último Contacto" de todos los deals tocados esta semana
□ Definir prioridades de la próxima semana
□ ¿Pipeline coverage > 3x del target? Si no, planear generación de leads
```

---

# FASE 6 — AUTOMATIZACIÓN (Flujo n8n)

## 6.1 Arquitectura del Flujo

```
┌─────────────────────────────────────────────────────────┐
│                    n8n WORKFLOW: MBC CRM                │
│                                                         │
│  ┌──────────┐    ┌──────────┐    ┌──────────────────┐  │
│  │ TRIGGER  │───>│ EVALUATE │───>│ ACTION           │  │
│  │ (cron/   │    │ (check   │    │ (email/slack/    │  │
│  │  webhook)│    │  rules)  │    │  notion update)  │  │
│  └──────────┘    └──────────┘    └──────────────────┘  │
└─────────────────────────────────────────────────────────┘
```

## 6.2 Flujos Propuestos

### Flujo 1: Alerta de Inactividad Automática
```
TRIGGER: Cron job cada lunes 8:00 AM
│
├─> NOTION API: Query database where "Días sin Contacto" > 14
│   AND Stage NOT IN ("Closed Won", "Closed Lost", "Partner")
│
├─> IF matches > 0:
│   ├─> SLACK/EMAIL: Enviar alerta a owner
│   │   "⚠️ Tienes {{count}} contactos inactivos hace >14 días:
│   │    {{lista con nombre, empresa, días sin contacto, stage}}"
│   │
│   └─> NOTION: Actualizar campo "Alerta Inactividad" = "⚠️ ALERTA"
│
└─> IF Días sin Contacto > 30 AND Stage == "Lead":
    └─> NOTION: Mover Stage a "Closed Lost"
        + Agregar nota: "Auto-cerrado por inactividad 30+ días"
```

### Flujo 2: Follow-up Automático Post-Evento
```
TRIGGER: Webhook cuando se agrega nuevo contacto a Notion con Event != null
│
├─> WAIT: 24 horas (no contactar el mismo día del evento)
│
├─> IF Email existe:
│   ├─> GMAIL: Enviar email Template 1 (personalizado según evento y segmento)
│   └─> NOTION: Actualizar "Email Enviado" = true, "Status" = "Email enviado"
│
├─> WAIT: 5 días
│
├─> IF Status todavía == "Email enviado" (no respondió):
│   ├─> GMAIL: Enviar email Template 2 (follow-up con valor)
│   └─> NOTION: Agregar nota "2do email enviado"
│
├─> WAIT: 7 días más
│
└─> IF Status todavía sin cambio:
    └─> SLACK: Notificar "{{Contacto}} de {{Empresa}} no respondió
         después de 2 emails. ¿Intentar WhatsApp/llamada?"
```

### Flujo 3: Recordatorio de Próxima Acción
```
TRIGGER: Cron job diario 8:30 AM
│
├─> NOTION API: Query where "Fecha Próxima Acción" == HOY
│
├─> FOR EACH match:
│   └─> SLACK/EMAIL:
│       "📋 Hoy tienes pendiente:
│        {{Próxima Acción}} con {{Contacto}} de {{Organización}}
│        Stage: {{Stage}} | Score: {{Score}} | Valor: ${{Valor Estimado}}"
│
└─> NOTION API: Query where "Fecha Próxima Acción" == AYER AND acción no completada
    └─> SLACK: "🚨 OVERDUE: La acción con {{Contacto}} estaba programada
         para ayer y no se registró completada."
```

### Flujo 4: Cambio de Stage → Notificación
```
TRIGGER: Notion webhook on property change (Stage)
│
├─> IF new Stage == "Proposal":
│   └─> SLACK: "🎯 {{Contacto}} de {{Organización}} avanzó a PROPOSAL!
│        Valor: ${{Valor}}. Próxima acción: {{Próxima Acción}}"
│
├─> IF new Stage == "Negotiation":
│   └─> SLACK: "🔥 {{Contacto}} en NEGOTIATION! Valor: ${{Valor}}.
│        ¿Necesita apoyo del CEO?"
│
├─> IF new Stage == "Closed Won":
│   ├─> SLACK: "🎉🎉 DEAL CERRADO! {{Organización}} - ${{Valor}}!
│        Iniciar onboarding."
│   └─> Trigger flujo de onboarding automático
│
└─> IF new Stage == "Closed Lost":
    ├─> SLACK: "😔 Deal perdido: {{Organización}}. Motivo: {{nota}}"
    └─> NOTION: Mover a vista "Reactivación futura" con reminder en 90 días
```

### Flujo 5: Resumen Semanal Automático
```
TRIGGER: Cron job viernes 17:00
│
├─> NOTION API: Aggregate pipeline data
│   - Total pipeline value
│   - Weighted pipeline value
│   - Deals por stage (count + value)
│   - Nuevos leads esta semana
│   - Deals movidos esta semana
│   - Contactos con alerta de inactividad
│
└─> SLACK/EMAIL: Enviar reporte semanal formateado
    "📊 PIPELINE SEMANAL MBC
     Total: ${{total}} | Ponderado: ${{weighted}}
     HOT: {{count_hot}} deals (${{value_hot}})
     Deals avanzados: {{moved_forward}}
     Alertas: {{inactive_count}} contactos inactivos

     TOP 3 prioridades próxima semana:
     1. {{deal_1}}
     2. {{deal_2}}
     3. {{deal_3}}"
```

## 6.3 Stack Técnico Recomendado

| Componente | Herramienta | Costo |
|---|---|---|
| Automatización | n8n (self-hosted) o n8n Cloud | Gratis (self) / $20/mes (cloud) |
| CRM | Notion (ya en uso) | Gratis / $10/mes |
| Email | Gmail + Gmail API | Gratis |
| Notificaciones | Slack o Telegram | Gratis |
| Enriquecimiento | Apollo.io o Hunter.io | $49/mes (opcional) |
| Scheduling | Calendly | Gratis |

---

# FASE 7 — REPORTE FINAL EJECUTIVO

## 7.1 Resumen Estratégico

### Estado actual del pipeline

| Métrica | Valor Actual | Target | Estado |
|---|---|---|---|
| Total registros en base | 92 organizaciones | — | — |
| Contactos con nombre | ~75 | — | — |
| Pipeline value (deals activos CRM) | $224,000 | $300,000 | 🟡 75% |
| Weighted pipeline value | $80,650 | $100,000 | 🟡 81% |
| Deals activos en CRM | 5 | 10+ | 🔴 50% |
| Pipeline coverage (vs target $25K/mes) | 2.7x | >3x | 🟡 Close |
| Contactos HOT | 5 | 5+ | 🟢 100% |
| Contactos WARM con potencial | 10 | 15+ | 🟡 67% |
| Completitud de datos | 48% | 80%+ | 🔴 Crítico |

### Diagnóstico en una frase
> **MBC tiene una base de contactos rica en relaciones pero pobre en datos estructurados. El pipeline tiene deals de alto valor pero es frágil (5 deals = alta concentración de riesgo). La oportunidad más grande es activar los ~45 contactos de Notion que están dormidos, especialmente los 10 WARM que podrían generar $250K+ adicionales en pipeline.**

## 7.2 Top 15 Leads Priorizados

| Rank | Org | Contacto | Score | Stage | Valor | Servicio | Acción Inmediata |
|------|-----|----------|-------|-------|-------|----------|------------------|
| 1 | **Inmob. Almagro** | Martín Benavides | 90 | Negotiation | $45K | XR + Marketing | Enviar propuesta revisada con descuento HOY |
| 2 | **Echeverría Izquierdo** | Andrés Matte | 87 | Discovery | $85K | AI + BIM | Demo AI personalizada en 48h |
| 3 | **Fundamenta** | Carolina Vial | 85 | Proposal | $22K | XR Tours | Follow-up telefónico HOY |
| 4 | **Inmob. Almagro** | Francisca Gonzalez | 77 | Lead | $25K | XR Training | Contactar para agendar reunión |
| 5 | **Parque Cordillera** | Carlos | 75 | Client (upsell) | $15K | HUB Sponsor | Presentar modelo de monetización |
| 6 | **Novatec** | Patricio Undurraga | 72 | Lead | $35K | XR Safety | Caso estudio + info CORFO |
| 7 | **Ingevec** | Jose T. Poblete | 69 | Lead | $30K | Suscripción + XR | Proponer reunión modelo suscripción |
| 8 | **Sabbagh Arq.** | Felipe Sabbagh | 65 | Qualified | $12K | XR Visualization | Agendar discovery call |
| 9 | **CChC** | Eduardo Hernández | 63 | Lead | $20K | Workshop XR | Proponer workshop para socios CChC |
| 10 | **Diplomado UC** | Rodrigo Reyes | 62 | Lead | $12K | XR Educación | Coordinar piloto clase en metaverso |
| 11 | **MOP** | Roberto Campos | 60 | Lead | $60K | BIM Implementation | Email + workshop BIM gratuito |
| 12 | **ETAC** | Santiago Urrutia | 60 | Lead | $15K | XR Training | Conectar con deal EI (riggers) |
| 13 | **Salfacorp** | Ignacio Pérez-Cotapos | 60 | Lead | $80K | AI + BIM | Email con artículo AI construcción |
| 14 | **EI (2do contacto)** | Rodrigo Pivelic | 58 | Lead | — | Refuerzo deal | Contactar para multi-thread |
| 15 | **Techo** | Jose Segovia | 58 | Lead | $8K | XR Social | Piloto VR evento donaciones |

### Valor total Top 15: **$464,000** (pipeline potencial si todos avanzan)
### Valor ponderado estimado: **$142,000**

## 7.3 Plan de Acción a 14 Días

### Semana 1 (Días 1-7): ACTIVACIÓN

| Día | Acción | Target | Canal | Entregable |
|-----|--------|--------|-------|------------|
| **D1 (Hoy)** | Enviar propuesta revisada Almagro | Martín Benavides | Email + WhatsApp | Propuesta PDF con pricing paquete |
| **D1** | Follow-up Fundamenta | Carolina Vial | Teléfono | Llamada directa para feedback |
| **D2** | Preparar demo AI monitoring | Andrés Matte (EI) | Email | Demo personalizada con datos Lo Barnechea |
| **D2** | Contactar Francisca Gonzalez (Almagro) | Francisca | Email | Email personalizado sobre VR training |
| **D3** | Enviar demo AI a EI | Andrés Matte | Email + WhatsApp | Link a demo + propuesta de reunión |
| **D3** | Agendar discovery Sabbagh | Felipe Sabbagh | Email/Teléfono | Propuesta de 3 horarios |
| **D4** | Email + caso estudio Novatec | Patricio Undurraga | Email | Caso XR Safety + brochure CORFO |
| **D4** | Contactar Carlos (Parque Cordillera) | Carlos | WhatsApp | Propuesta modelo Sponsor |
| **D5** | Email reactivación Salfacorp | Ignacio Pérez-Cotapos | Email | Artículo AI en construcción + propuesta breve |
| **D5** | Email MOP workshop BIM | Roberto Campos | Email formal | Invitación a workshop BIM gratuito |
| **D6-7** | Preparar contenido para WARM | Batch | — | 2 case studies, 1 artículo blog |

### Semana 2 (Días 8-14): NURTURING & EXPANSION

| Día | Acción | Target | Canal | Entregable |
|-----|--------|--------|-------|------------|
| **D8** | Follow-up a todos los que no respondieron S1 | Varios | Email/WhatsApp | 2do touchpoint personalizado |
| **D8** | Proponer workshop CChC | Eduardo Hernández | Email | Propuesta de workshop XR para socios |
| **D9** | Contactar Ingevec | Jose T. Poblete | Email + LinkedIn | Propuesta modelo suscripción |
| **D9** | Conectar ETAC con deal EI | Santiago Urrutia | WhatsApp | Info sobre capacitación riggers |
| **D10** | Coordinar piloto Diplomado UC | Rodrigo Reyes | Email | Propuesta de clase en metaverso |
| **D10** | Enviar propuesta Techo | Jose Segovia | Email | Propuesta piloto VR donaciones |
| **D11** | Limpiar base Notion | — | Notion | Completar campos vacíos top 30 contactos |
| **D12** | Configurar 1er flujo n8n | — | n8n | Flujo de alertas de inactividad |
| **D13** | Enviar newsletter inaugural | Lista COLD (15) | Email | Newsletter con contenido de valor |
| **D14** | Pipeline review completa | — | Interno | Actualizar CRM, scores, y proyecciones |

### KPIs de la quincena

| Métrica | Target |
|---|---|
| Emails enviados (personalizado) | 15 |
| Llamadas realizadas | 8 |
| Reuniones agendadas | 5 |
| Propuestas enviadas | 3 |
| Deals avanzados de stage | 3 |
| Nuevos leads agregados al pipeline | 5 |

## 7.4 Riesgos Identificados

| Riesgo | Probabilidad | Impacto | Mitigación |
|--------|-------------|---------|------------|
| **Concentración**: 3 deals (EI, Almagro, Fundamenta) = 68% del pipeline | ALTA | ALTO | Activar urgente los 10 WARM para diversificar |
| **Datos incompletos**: 48% completitud promedio | ALTA | MEDIO | Sprint de enriquecimiento de datos (LinkedIn + scraping) |
| **Single-threaded**: Mayoría de deals tiene 1 solo contacto | MEDIA | ALTO | Identificar 2do contacto en empresas grandes (ya hecho con EI y Almagro) |
| **No hay CRM real**: Markdown funciona pero no escala | MEDIA | MEDIO | Migrar a Notion pipeline + n8n en los próximos 14 días |
| **Ciclo largo gobierno**: MOP puede tomar 6+ meses | ALTA | BAJO | Trabajar como pipeline a largo plazo, no depender para revenue corto |
| **Sin case studies formales**: Difícil convencer sin pruebas | MEDIA | ALTO | Documentar caso Parque Cordillera como primer case study formal |
| **Equipo pequeño**: 2-5 personas para ejecutar todo | ALTA | ALTO | Priorizar deals HOT, automatizar lo posible, usar partners para delivery |

## 7.5 Métricas a Monitorear (Semanal)

### Dashboard Mínimo Viable

| Categoría | Métrica | Fórmula | Target |
|---|---|---|---|
| **Volume** | Total pipeline value | Suma de Valor Estimado (deals activos) | >$300K |
| **Volume** | Weighted pipeline value | Suma de Valor Ponderado | >$100K |
| **Volume** | # deals activos | Count (Stage != Closed) | >10 |
| **Velocity** | Deals avanzados/semana | Count(stage changes forward) | >2/semana |
| **Velocity** | Avg days in stage | Promedio días en cada stage | <21 días |
| **Conversion** | Lead→Qualified rate | Qualified / Total Leads | >40% |
| **Conversion** | Proposal→Won rate | Won / Proposals sent | >30% |
| **Activity** | Touchpoints/semana | Emails + calls + meetings | >15 |
| **Activity** | Contactos con actividad reciente (<14d) | Count(Último Contacto > Today-14) | >80% de HOT+WARM |
| **Health** | Pipeline coverage | Pipeline value / Monthly target revenue | >3x |
| **Health** | # contactos con alerta inactividad | Count(Días sin contacto > 14) | 0 (HOT), <3 (WARM) |
| **Health** | Diversificación de segmentos | # segmentos con deals | >3 segmentos |

## 7.6 Decisiones Estratégicas Documentadas

| # | Decisión | Rationale | Alternativas Consideradas |
|---|----------|-----------|--------------------------|
| D1 | Usar scoring 0-100 en vez de solo Hot/Warm/Cold | Permite priorización más granular y decisiones data-driven | Solo usar clasificación textual (menos preciso) |
| D2 | Consolidar 4 fuentes en 1 Notion DB | Elimina duplicados, centraliza tracking, permite automatización | Mantener múltiples fuentes (caótico, error-prone) |
| D3 | Clasificar partners en track separado | No son ventas directas, tienen métricas diferentes | Mezclar con pipeline de ventas (confunde métricas) |
| D4 | Priorizar constructoras/inmobiliarias sobre educación | Mayor capacidad de pago, dolor más claro, ciclo más corto | Enfocarse en educación UC (menor revenue pero credibilidad) |
| D5 | Proponer n8n self-hosted | Costo cero, control total, ya existe experiencia en Python/automation | Zapier ($49/mes, más fácil pero más caro y limitado) |
| D6 | No eliminar contactos COLD, mover a newsletter | Pueden reactivarse con trigger adecuado (nuevo proyecto, nuevo presupuesto) | Eliminar para simplificar base (pierde oportunidades futuras) |
| D7 | Documentar Parque Cordillera como primer case study | Es el único proyecto completado, validación social necesaria | Esperar un deal más grande (demora, pierde momentum) |

---

# ANEXOS

## Anexo A: Contactos Completos con Score (Tabla Maestra)

| # | Score | Clasificación | Organización | Contacto | Email | Teléfono | Cargo | Segmento | Stage | Servicio | Valor Est. | Fuente |
|---|-------|---------------|---|---|---|---|---|---|---|---|---|---|
| 1 | 90 | HOT | Inmob. Almagro | Martín Benavides | mbenavides@almagro.cl | +56954321098 | Gte. Marketing | Inmobiliaria | Negotiation | XR+Marketing | $45,000 | CRM |
| 2 | 87 | HOT | Echeverría Izquierdo | Andrés Matte | amatte@ei.cl | +56987654321 | Gte. Innovación | Constructora | Discovery | AI+BIM | $85,000 | CRM |
| 3 | 85 | HOT | Fundamenta | Carolina Vial | cvial@fundamenta.cl | +56976543210 | Gte. Comercial | Inmobiliaria | Proposal | XR Tours | $22,000 | CRM |
| 4 | 77 | HOT | Inmob. Almagro | Francisca Gonzalez | Fgonzalezs@almagro.cl | — | Sub Gte. Innovación | Inmobiliaria | Lead | XR Training | $25,000 | Notion |
| 5 | 75 | HOT | Parque Cordillera | Carlos | — | — | Jefe Operaciones | Parques | Client | HUB Sponsor | $15,000 | Notion |
| 6 | 72 | WARM | Novatec | Patricio Undurraga | pundurraga@novatec.cl | +56943210987 | Gte. Operaciones | Constructora | Lead | XR Safety | $35,000 | CRM |
| 7 | 69 | WARM | Ingevec | Jose T. Poblete | jpoblete@ingevec.cl | — | Gte. Innovación | Constructora | Lead | Suscripción+XR | $30,000 | Notion |
| 8 | 65 | WARM | Sabbagh Arq. | Felipe Sabbagh | fsabbagh@sabbagharchitects.cl | +56965432109 | Socio Director | Arquitectura | Qualified | XR Viz | $12,000 | CRM |
| 9 | 63 | WARM | CChC | Eduardo Hernández | ehernandez@cchc.cl | — | Jefe Innovación | Gremio | Lead | Workshop XR | $20,000 | Notion |
| 10 | 62 | WARM | Diplomado C4.0 UC | Rodrigo Reyes | rodreyes@uc.cl | — | Jefe Programa | Educación | Lead | XR Educ | $12,000 | Notion |
| 11 | 60 | WARM | MOP | Roberto Campos | rcampos@mop.gov.cl | — | Jefe Div. Edif. | Gobierno | Lead | BIM | $60,000 | CRM |
| 12 | 60 | WARM | ETAC | Santiago Urrutia | santiago.urrutia@gruasyequipos.cl | — | Gte. Innovación | Grúas | Lead | XR Training | $15,000 | Notion |
| 13 | 60 | WARM | Salfacorp | Ignacio Pérez-Cotapos | iperez@salfacorp.com | +56921098765 | Subgte. Innovación | Constructora | Lead | AI+BIM | $80,000 | CRM |
| 14 | 58 | WARM | Echeverría Izquierdo | Rodrigo Pivelic | pivelic@ei.cl | — | Gte. Innovación | Constructora | Lead | XR+BIM | — | Notion |
| 15 | 58 | WARM | Techo | Jose Segovia | jose.segovia@techo.org | — | Depto. Innovación | ONG | Lead | XR Social | $8,000 | Notion |

## Anexo B: Data Enrichment desde Scraping (Contactos con datos enriquecidos)

| Organización | Emails Encontrados | Teléfonos | LinkedIn | Instagram |
|---|---|---|---|---|
| iBuilder | soporte@ibuilder.com, ventas@builder.cl + 8 más | +56931897172 + 13 más | linkedin.com/company/icbuilder | @ibuilder.latam |
| CChC | — | 56223763300 | Sí | @camarachilenadelaconstruccion |
| JUMP UC | jumpchile@uc.cl, claudia.zanartu@uc.cl + 3 | — | — | @jump_chile |
| Un Techo | info.chile@techo.org + 6 más | +56228387300 | Sí | @techochile |
| Holo | contacto@holo.cl | +56942900992 | linkedin.com/company/holo-xr | @holo.xr |
| EDIFICA | ventas@edifica.cl | +56994496237 | — | @Expoedifica |
| Inmob. Almagro | — | 223726666, 228406666 | — | @inmobiliariaalmagro |
| Wbuild | — | +56947303170 | linkedin.com/company/wbuild-io | @wbuild.io |
| Sentio VR | hello@sentiovr.com | 56621522084 | — | @sentiovr |
| Minverso | contacto@metaverso.cl | +56971334886 | linkedin.com/company/minverso | @minversocl |
| COMPITE | contacto@compite.cl | +56962047015 | linkedin.com/company/compite-spa | @compite.cl |
| CIPYCS | contacto@cipycs.cl | +56929420170 | linkedin.com/company/cipycs | @cipycs |
| DECON UC | decon@uc.cl | +56955044567 | — | — |
| ETAC | — | 56224842100 | linkedin.com/company/gruasyequiposcruzdelsur | @gruasyequiposcruzdelsur |

---

**FIN DEL REPORTE**

*Generado por Claude — Head of Sales Ops & Revenue Strategist*
*Fecha: 2026-02-12*
*Próxima revisión: 2026-02-26 (14 días)*
