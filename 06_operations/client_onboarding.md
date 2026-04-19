# Proceso de Onboarding de Clientes — Meta Build City

> **Versión:** 2.0 | **Última actualización:** Febrero 2026
> **Objetivo:** Garantizar una experiencia de inicio fluida, profesional y consistente para cada nuevo cliente
> **Responsable principal:** Project Lead asignado

---

## Filosofía de Onboarding

Los primeros 14 días de la relación con un cliente definen la percepción que tendrán de MBC durante todo el proyecto. Un onboarding profesional genera confianza, establece expectativas claras y reduce fricciones futuras.

**Principio rector**: "Hacer que el cliente se sienta en buenas manos desde el primer minuto."

---

## Day 0: Contrato Firmado

El momento en que se firma el contrato es el punto de partida del onboarding. Estas tareas se ejecutan el mismo día o el día siguiente.

### Checklist Day 0

**Legal y Financiero**:
- [ ] Contrato de servicios completamente ejecutado (firmado por ambas partes)
- [ ] NDA firmado (si aplica — especialmente para proyectos con datos sensibles)
- [ ] Factura enviada para el pago inicial (según condiciones del contrato)
- [ ] Método de pago confirmado con el cliente (transferencia, factura, etc.)
- [ ] Orden de compra recibida (si el cliente lo requiere)

**CRM y Tracking**:
- [ ] Cliente creado/actualizado en CRM con status "Active Client"
- [ ] Deal movido a "Won" en el pipeline
- [ ] Información del contacto principal completada: nombre, cargo, email, teléfono
- [ ] Fuente del lead documentada (cómo nos conocieron)
- [ ] Valor del contrato y condiciones de pago registrados

**Comunicación Interna**:
- [ ] Canal de Slack creado: `#client-{nombre}` (minúsculas, sin espacios)
- [ ] Equipo asignado al proyecto notificado en Slack
- [ ] Brief interno compartido con el equipo (scope, timeline, contexto del cliente)
- [ ] Project Lead y Tech Lead confirmados

**Herramientas**:
- [ ] Proyecto creado en Notion/Linear con estructura estándar
- [ ] Carpeta compartida creada en Google Drive con estructura:

```
{Nombre Cliente} - {Nombre Proyecto}/
├── 01_Brief/           ← Project brief, propuesta firmada, contrato
├── 02_Requirements/    ← Documentos de requerimientos, specs
├── 03_Assets/          ← Assets del cliente (logos, fotos, modelos, data)
├── 04_Deliverables/    ← Entregables por fase
├── 05_Communication/   ← Meeting notes, reportes, presentaciones
└── 06_Admin/           ← Facturas, NDAs, documentos legales
```

---

## Day 1-2: Welcome

Las primeras 48 horas después de la firma son para dar la bienvenida formal y sentar las bases de comunicación.

### Checklist Day 1-2

**Welcome Email** (enviar dentro de las primeras 24 horas):
- [ ] Email de bienvenida enviado desde Project Lead al Client Champion

**Contenido del welcome email**:
```
Asunto: Bienvenido/a a MBC — Próximos pasos para {Nombre del Proyecto}

Estimado/a {Nombre},

¡Estamos muy contentos de comenzar a trabajar juntos en {nombre del proyecto}!

EQUIPO ASIGNADO:
- Project Lead: {nombre} — {email} — será tu punto de contacto principal
- Technical Lead: {nombre} — {email} — liderará la ejecución técnica
- {Otros roles si aplica}

CANALES DE COMUNICACIÓN:
- Email para comunicaciones formales y documentación
- {WhatsApp/Slack si aplica} para coordinación rápida
- Video calls semanales (te enviaremos invitación de calendario)

PRÓXIMOS PASOS:
1. Reunión de kickoff: {fecha y hora propuesta} — te enviaremos invitación
2. Necesitaremos de tu parte: {lista breve de lo que necesitamos del cliente}
3. Primer entregable esperado: {fecha y qué será}

ACCESO:
- Te hemos dado acceso a nuestra carpeta compartida: {link}
- Si necesitas acceso a alguna herramienta adicional, avísanos

¿Alguna pregunta antes del kickoff? No dudes en escribirme.

Saludos,
{Nombre del Project Lead}
Project Lead, Meta Build City
{teléfono} | {email}
```

**Setup de accesos**:
- [ ] Cliente agregado a carpeta compartida de Google Drive (permisos de editor en su carpeta)
- [ ] Cliente agregado a proyecto de Notion (si aplica — solo secciones cliente-facing)
- [ ] Invitación de calendario enviada para la reunión de kickoff
- [ ] Invitación de calendario enviada para sync semanal recurrente

**Recopilación de información**:
- [ ] Solicitar al cliente: logo, brand guidelines, contactos adicionales del equipo
- [ ] Solicitar accesos necesarios: plataformas, data, modelos BIM existentes, etc.
- [ ] Confirmar disponibilidad del Client Champion para el kickoff

---

## Day 3-5: Reunión de Kickoff

La reunión de kickoff es el momento más importante del onboarding. Aquí se alinean expectativas, se conocen las caras, y se establece el ritmo de trabajo.

### Pre-kickoff (preparación de MBC)

- [ ] Deck de kickoff preparado (ver estructura abajo)
- [ ] Roles internos claros: quién presenta qué
- [ ] Propuesta y scope revisados una vez más para tener todo fresco
- [ ] Lista de preguntas para el cliente preparada

### Agenda del Kickoff Meeting (60-90 minutos)

| # | Tema | Duración | Responsable |
|---|------|----------|------------|
| 1 | Presentaciones: quiénes somos, quiénes son ellos | 10 min | Project Lead |
| 2 | Revisión del scope y objetivos del proyecto | 10 min | Project Lead |
| 3 | Timeline y milestones clave | 10 min | Project Lead |
| 4 | Metodología de trabajo (cómo vamos a trabajar juntos) | 10 min | Tech Lead |
| 5 | Canales de comunicación y cadencia de reuniones | 5 min | Project Lead |
| 6 | Qué necesitamos del cliente (accesos, assets, info) | 10 min | Tech Lead |
| 7 | Definir key contacts y escalation path | 5 min | Project Lead |
| 8 | Preguntas del cliente | 10 min | Todos |
| 9 | Próximos pasos inmediatos y fechas | 5 min | Project Lead |
| 10 | Sign-off del project brief (si no se firmó antes) | 5 min | Ambas partes |

### Lo que Presentamos (MBC)

- **Scope del proyecto**: qué haremos, qué NO haremos (in/out of scope)
- **Timeline**: fases, milestones, fechas clave
- **Equipo**: quién es quién en MBC y qué hace cada persona
- **Metodología**: cómo trabajamos (sprints, demos, reviews)
- **Comunicación**: sync semanal, email para formales, Slack/WhatsApp para rápido
- **Expectativas**: qué necesitamos del cliente (tiempos de respuesta, accesos, decisiones)

### Lo que Recopilamos (del Cliente)

- [ ] Accesos y credenciales a plataformas, sistemas, servidores
- [ ] Brand assets: logos, paleta de colores, tipografía, brand guidelines
- [ ] Datos y modelos existentes: modelos BIM, planos, data sets, documentos técnicos
- [ ] Información de negocio: público objetivo, competencia, métricas actuales
- [ ] Contactos clave: quién aprueba, quién provee info técnica, quién es stakeholder
- [ ] Restricciones: deadlines externos, regulaciones, limitaciones técnicas

### Lo que Definimos Juntos

- [ ] Cadencia de comunicación: día y hora del sync semanal, formato
- [ ] Key contacts: quién contacta a quién para qué
- [ ] Escalation path: a quién escalar si hay blockers o problemas del lado del cliente
- [ ] Criterios de aceptación: cómo el cliente evaluará cada entregable
- [ ] Change request process: cómo manejar cambios de scope

### Post-kickoff

- [ ] Project brief firmado (sign-off) — si no se hizo antes
- [ ] Meeting notes del kickoff enviadas al cliente (mismo día)
- [ ] Accesos y assets recibidos verificados
- [ ] Sprint 1 / fase de discovery planificada
- [ ] Equipo interno alineado sobre hallazgos del kickoff

---

## Semana 1-2: Discovery

Las primeras 2 semanas post-kickoff son de inmersión en el problema del cliente.

### Checklist de Discovery

**Technical Discovery**:
- [ ] Revisión de sistemas y plataformas existentes del cliente
- [ ] Análisis de datos y modelos proporcionados
- [ ] Evaluación de constraints técnicos (hardware, software, integraciones)
- [ ] Identificación de dependencies externas (APIs, third-party tools)
- [ ] Evaluación de infrastructure necesaria (cloud, servidores, devices)

**Requirements Documentation**:
- [ ] Requerimientos funcionales documentados (qué debe hacer la solución)
- [ ] Requerimientos no-funcionales documentados (performance, seguridad, escalabilidad)
- [ ] User stories o casos de uso escritos
- [ ] Criterios de aceptación por requerimiento
- [ ] Priorización de requerimientos (MoSCoW: Must/Should/Could/Won't)
- [ ] Sign-off del cliente en documento de requerimientos

**Architecture/Approach**:
- [ ] Arquitectura técnica definida y documentada
- [ ] Stack tecnológico seleccionado y justificado
- [ ] Approach de desarrollo presentado al cliente
- [ ] Riesgos técnicos identificados con mitigación
- [ ] Prototipo o proof-of-concept (si la complejidad lo justifica)

**Planning**:
- [ ] Backlog completo creado con estimaciones
- [ ] Sprint 1 planificado con tareas, asignaciones y estimaciones
- [ ] Timeline detallado actualizado con fechas por sprint
- [ ] Risk register inicializado

---

## Ongoing: Gestión de la Relación durante el Proyecto

### Comunicación Regular

| Actividad | Frecuencia | Formato | Responsable |
|-----------|-----------|---------|------------|
| Sync semanal | Cada semana | Video call (30 min) | Project Lead |
| Sprint demo | Cada 2 semanas | Video call con screen share | Tech Lead |
| Status report | Mensual | Email + documento | Project Lead |
| Quarterly Business Review | Trimestral (retainers) | Presencial o video (60-90 min) | Project Lead + CEO |

### Gestión de Expectativas

**Reglas de comunicación con el cliente**:
- Siempre ser transparente sobre el status (buenas y malas noticias)
- Si hay un problema, comunicarlo proactivamente (no esperar a que el cliente pregunte)
- Nunca prometer lo que no se puede entregar
- Si hay un cambio de scope, documentarlo formalmente antes de ejecutar
- Responder emails/mensajes del cliente dentro de las 4 horas hábiles

### Change Request Process

Cuando el cliente pide algo que no está en el scope original:

1. Project Lead documenta el cambio solicitado
2. Tech Lead estima impacto en timeline y costo
3. Project Lead presenta al cliente: qué implica el cambio, costo adicional (si aplica), impacto en timeline
4. Si el cliente aprueba: actualizar scope, timeline, y presupuesto formalmente
5. Si no aprueba: documentar y continuar con scope original

**Template de change request**:
```
## Change Request #{número}
- Fecha: {fecha}
- Solicitado por: {nombre del cliente}
- Descripción del cambio: {qué se pide}
- Impacto en timeline: {+X días/semanas}
- Impacto en presupuesto: {+$X / sin impacto}
- Recomendación MBC: {aprobar / postergar / alternativa}
- Decisión del cliente: {aprobado / rechazado}
- Firma del cliente: _____________
```

---

## Offboarding: Cierre del Proyecto

Tan importante como el onboarding. Un cierre profesional genera referrals, testimonials y trabajo futuro.

### Final Delivery y Sign-off

- [ ] Entregable final completo según scope (verificado contra project brief)
- [ ] QA final pasado (ver quality_standards.md)
- [ ] Deploy a producción realizado
- [ ] Testing de aceptación (UAT) completado por el cliente
- [ ] Sign-off formal del cliente (email o documento firmado)
- [ ] Factura final enviada (si quedan pagos pendientes)

### Handoff Documentation

- [ ] Documentación técnica completa: arquitectura, código fuente, configuraciones, credenciales
- [ ] Documentación de usuario: guía de uso, FAQs, troubleshooting común
- [ ] Documentación de mantenimiento: cómo actualizar, monitorear, escalar, resolver problemas comunes
- [ ] Accesos transferidos al cliente: admin de plataformas, repositorios, credenciales
- [ ] Inventario de assets entregados: archivos, código, modelos, licencias

### Training Session

- [ ] Sesión de capacitación al equipo del cliente (1-3 horas según complejidad)
- [ ] Agenda de training preparada y compartida con anticipación
- [ ] Sesión grabada (con permiso) para referencia futura del cliente
- [ ] Materiales de training entregados: guía, slides, videos si aplica
- [ ] Q&A al final de la sesión

### Transición a Soporte/Mantenimiento

Si hay contrato de soporte:
- [ ] SLA (Service Level Agreement) definido y firmado
- [ ] Canales de soporte establecidos (email, Slack, ticketing)
- [ ] Equipo de soporte asignado y presentado al cliente
- [ ] Proceso de escalamiento definido
- [ ] Primera revisión de soporte agendada (30 días post-delivery)

Si NO hay contrato de soporte:
- [ ] Período de garantía definido (típicamente 30 días post-delivery para bugs)
- [ ] Cliente informado sobre qué está cubierto y qué no
- [ ] Propuesta de soporte/mantenimiento enviada para consideración futura

### Reunión de Cierre

- [ ] Reunión final con el cliente (30-45 min)
- [ ] Agenda: celebrar logros, revisar resultados, feedback mutuo, próximos pasos
- [ ] Preguntar: ¿qué hicimos bien? ¿qué podríamos mejorar?
- [ ] Discutir oportunidades futuras de trabajo

### Satisfaction Survey

- [ ] Encuesta de satisfacción enviada al Client Champion y stakeholders clave
- [ ] Formato: Google Form o TypeForm, 5-10 preguntas, 5 minutos para completar

**Preguntas de la encuesta**:
1. En una escala de 1-5, ¿qué tan satisfecho estás con el resultado del proyecto?
2. En una escala de 1-5, ¿qué tan bien cumplimos con los plazos acordados?
3. En una escala de 1-5, ¿cómo calificas la comunicación durante el proyecto?
4. En una escala de 1-5, ¿qué tan probable es que nos recomiendes a un colega? (NPS)
5. ¿Qué fue lo que más valoraste de trabajar con MBC?
6. ¿Qué podríamos haber hecho mejor?
7. ¿Hay algún otro proyecto o necesidad en la que podamos ayudarte?
8. ¿Podemos usar tu experiencia como caso de estudio? (Sí/No)

### Testimonial Request

- [ ] Si la satisfacción es alta (4+/5), pedir testimonial
- [ ] Ofrecer opciones: texto escrito, video corto (2 min), LinkedIn recommendation
- [ ] Facilitar: enviar preguntas guía para que sea fácil para el cliente

**Preguntas guía para testimonial**:
1. ¿Cuál era el desafío que tenían antes de trabajar con MBC?
2. ¿Cómo fue la experiencia de trabajar con nosotros?
3. ¿Qué resultados obtuvieron?
4. ¿Recomendarías a MBC? ¿A quién?

### Referral Ask

- [ ] Preguntar: "¿Conoces a alguien en tu red que pueda estar enfrentando un desafío similar?"
- [ ] No presionar: si dice que no, agradecer y seguir adelante
- [ ] Si refiere a alguien: contactar mencionando la referencia, enviar agradecimiento al referrer
- [ ] Registrar referral en CRM con fuente "Referral - {nombre del cliente}"

---

## Post-mortem Interno

Después de cada proyecto, hacer un post-mortem interno (ver template en project_management.md):

- [ ] Post-mortem agendado (máximo 1 semana después del cierre)
- [ ] Todo el equipo del proyecto participa
- [ ] Documentar: qué salió bien, qué salió mal, qué aprendimos
- [ ] Definir action items concretos para mejorar
- [ ] Agregar lecciones a la base de conocimiento (Notion)
- [ ] Actualizar templates y procesos si es necesario

---

## Onboarding Checklist — Vista Resumen

Para imprimir o tener a mano:

```
ONBOARDING — {Nombre del Cliente} — {Fecha}

DAY 0: CONTRATO FIRMADO
□ Contrato y NDA firmados
□ Factura inicial enviada
□ CRM actualizado (status: Active Client)
□ Canal Slack creado: #client-{nombre}
□ Proyecto creado en Notion/Linear
□ Carpeta compartida creada en Google Drive

DAY 1-2: WELCOME
□ Welcome email enviado
□ Accesos a herramientas compartidos con el cliente
□ Kickoff meeting agendado
□ Sync semanal recurrente agendado
□ Assets y accesos solicitados al cliente

DAY 3-5: KICKOFF
□ Deck de kickoff preparado
□ Kickoff meeting realizado
□ Scope, timeline, equipo, metodología presentados
□ Accesos, assets, info recopilada del cliente
□ Communication cadence definida
□ Project brief firmado (sign-off)
□ Meeting notes enviadas

SEMANA 1-2: DISCOVERY
□ Technical discovery completada
□ Requirements documentados y firmados
□ Arquitectura/approach presentado
□ Sprint 1 planificado
□ Risk register inicializado

OFFBOARDING (al final del proyecto)
□ Entrega final y sign-off del cliente
□ Documentación completa entregada
□ Training session realizada
□ Transición a soporte (si aplica)
□ Encuesta de satisfacción enviada
□ Testimonial solicitado
□ Referral ask realizado
□ Post-mortem interno completado
```
