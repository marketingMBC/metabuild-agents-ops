# Pipeline de Ventas

## 1. Definición de Etapas del Pipeline

### Flujo general

```
Lead → Qualified → Discovery → Proposal → Negotiation → Closed Won / Closed Lost
```

### Detalle de cada etapa

| # | Etapa | Definición | Criterio de entrada | Criterio de avance | Probabilidad de cierre | Responsable |
|---|-------|-----------|--------------------|--------------------|----------------------|-------------|
| 1 | **Lead** | Contacto identificado con potencial interés. Puede venir de inbound (web, evento, referido) o outbound (prospección directa). | Empresa del sector AEC + contacto identificado con nombre y canal de contacto | Se logra agendar una llamada/reunión de descubrimiento | 10% | Marketing / SDR |
| 2 | **Qualified** | Lead calificado con BANT mínimo (Budget, Authority, Need, Timeline). Se confirmó que hay un dolor real y capacidad mínima de compra. | Interacción inicial confirma: (1) dolor relevante, (2) contacto tiene influencia, (3) empresa puede invertir | Discovery call agendada con decision maker o influenciador clave | 20% | SDR / Account Exec |
| 3 | **Discovery** | Llamada de descubrimiento realizada. Se entiende profundamente el dolor, el contexto, el proceso de decisión y el timeline del cliente. | Discovery call completada con notas registradas en CRM | Cliente solicita o acepta propuesta formal / demo técnica | 35% | Account Exec |
| 4 | **Proposal** | Propuesta formal entregada al cliente. Incluye alcance, pricing, timeline. Puede incluir demo técnica presencial. | Propuesta enviada + confirmación de recepción por el cliente | Cliente confirma que la propuesta está en evaluación activa / solicita ajustes | 50% | Account Exec |
| 5 | **Negotiation** | Cliente está evaluando activamente. Puede haber solicitudes de ajuste de precio, alcance, términos. Pueden estar comparando con otros proveedores. | Feedback recibido sobre la propuesta / reunión de negociación agendada | Acuerdo verbal o firma de contrato | 70% | Account Exec / CEO |
| 6a | **Closed Won** | Contrato firmado o orden de compra emitida. Deal cerrado exitosamente. | Firma de contrato / OC en Mercado Público / email de confirmación formal | N/A -- entrega a equipo de delivery | 100% | Account Exec |
| 6b | **Closed Lost** | Oportunidad no se concretó. Se registra motivo de pérdida para aprendizaje. | Rechazo explícito del cliente / 90 días sin respuesta después de propuesta | N/A -- mover a nurture list para reactivación futura | 0% | Account Exec |

---

## 2. Motivos de Closed Lost (Tracking)

| Código | Motivo | Acción de follow-up |
|--------|--------|---------------------|
| CL-01 | Sin presupuesto | Recontactar en Q4 (planificación anual) o cuando haya proyecto nuevo |
| CL-02 | Eligió competidor | Pedir feedback, ofrecer estar disponibles para futuro |
| CL-03 | Proyecto cancelado/postergado | Monitorear estado del proyecto, recontactar cuando se reactive |
| CL-04 | Timing inadecuado | Agendar follow-up en 3-6 meses |
| CL-05 | No responde | 3 intentos espaciados, luego mover a nurture (newsletter, eventos) |
| CL-06 | Decidió hacerlo interno | Ofrecer capacitación o servicio complementario |
| CL-07 | Alcance no match | Registrar qué servicio buscaban para ajustar oferta futura |

---

## 3. Pipeline Tracker

### Template de seguimiento

| # | Empresa | Contacto | Cargo | Segmento | Servicio principal | Etapa | Valor est. (USD) | Prob. | Valor ponderado | Fecha primer contacto | Expected close | Owner | Última actividad | Próxima acción |
|---|---------|----------|-------|----------|-------------------|-------|-------------------|-------|-----------------|----------------------|----------------|-------|-----------------|----------------|
| 1 | | | | | | | | | | | | | | |

### Ejemplos de deals en pipeline

| # | Empresa | Contacto | Cargo | Segmento | Servicio principal | Etapa | Valor est. (USD) | Prob. | Valor ponderado | Fecha primer contacto | Expected close | Owner | Última actividad | Próxima acción |
|---|---------|----------|-------|----------|-------------------|-------|-------------------|-------|-----------------|----------------------|----------------|-------|-----------------|----------------|
| 1 | Echeverría Izquierdo | Andrés Matte | Gerente de Innovación | Constructora | AI Monitoring + BIM | Discovery | $85,000 | 35% | $29,750 | 2025-01-15 | 2025-04-30 | RR | Discovery call 02/10 -- dolor claro en control de avance | Preparar demo AI monitoring para proyecto edificio Lo Barnechea |
| 2 | Fundamenta | Carolina Vial | Gerente Comercial | Inmobiliaria | XR Virtual Tours | Proposal | $22,000 | 50% | $11,000 | 2025-01-20 | 2025-03-15 | RR | Propuesta enviada 02/05 para proyecto "Parque Bicentenario" | Follow-up telefónico viernes 02/14 para feedback |
| 3 | Sabbagh Arquitectos | Felipe Sabbagh | Socio Director | Arquitectura | XR Visualization | Qualified | $12,000 | 20% | $2,400 | 2025-02-01 | 2025-05-30 | RR | Email intro enviado, aceptó reunirse | Agendar discovery call semana del 17/02 |
| 4 | MOP - Dirección de Arquitectura | Roberto Campos | Jefe División Edificación Pública | Gobierno | BIM Implementation | Lead | $60,000 | 10% | $6,000 | 2025-02-08 | 2025-09-30 | RR | Intercambiamos tarjetas en evento PlanBIM | Enviar email con propuesta de workshop BIM para funcionarios |
| 5 | Inmobiliaria Almagro | Martín Benavides | Gerente de Marketing | Inmobiliaria | XR + Marketing | Negotiation | $45,000 | 70% | $31,500 | 2024-12-10 | 2025-02-28 | RR | Reunión de negociación 02/07, pidieron ajuste de precio | Enviar propuesta revisada con descuento por paquete de 2 proyectos |

---

## 4. Métricas del Pipeline

### Dashboard de métricas

#### Pipeline total
| Métrica | Valor actual | Target mensual |
|---------|-------------|---------------|
| **Total pipeline value** (suma de todos los deals activos) | $224,000 | $300,000+ |
| **Weighted pipeline value** (suma de valor ponderado) | $80,650 | $100,000+ |
| **Cantidad de deals activos** | 5 | 10+ |
| **Deal promedio** | $44,800 | $35,000-$50,000 |

#### Conversion rates por etapa
| Transición | Rate actual | Target | Benchmark B2B tech |
|-----------|-----------|--------|-------------------|
| Lead → Qualified | -- | 40-50% | 30-40% |
| Qualified → Discovery | -- | 60-70% | 50-60% |
| Discovery → Proposal | -- | 50-60% | 40-50% |
| Proposal → Negotiation | -- | 40-50% | 30-40% |
| Negotiation → Closed Won | -- | 50-60% | 40-50% |
| **Overall Lead → Closed Won** | -- | **8-12%** | **5-10%** |

#### Velocidad del pipeline
| Métrica | Actual | Target |
|---------|--------|--------|
| Tiempo promedio Lead → Qualified | -- | < 2 semanas |
| Tiempo promedio Qualified → Discovery | -- | < 1 semana |
| Tiempo promedio Discovery → Proposal | -- | < 2 semanas |
| Tiempo promedio Proposal → Close | -- | < 4 semanas |
| **Ciclo total promedio** | -- | **2-4 meses** |

#### Métricas por segmento
| Segmento | Deals en pipeline | Valor total | Valor ponderado | Win rate |
|----------|------------------|-------------|-----------------|----------|
| Constructoras | 1 | $85,000 | $29,750 | -- |
| Inmobiliarias | 2 | $67,000 | $42,500 | -- |
| Arquitectura | 1 | $12,000 | $2,400 | -- |
| Gobierno | 1 | $60,000 | $6,000 | -- |
| **Total** | **5** | **$224,000** | **$80,650** | -- |

#### Métricas por servicio
| Servicio | Deals en pipeline | Valor total |
|----------|------------------|-------------|
| XR (tours, visualization, showrooms) | 3 | $79,000 |
| AI (monitoring, analytics) | 1 | $85,000 |
| BIM (implementation, coordination) | 1 | $60,000 |
| Marketing (digital, content) | 1 (paquete) | incl. en XR+Mktg |
| Blockchain | 0 | $0 |

---

## 5. Pipeline Review Semanal

### Agenda de reunión semanal de pipeline (30 min, lunes AM)

#### Participantes
- Account Executive (owner del pipeline)
- CEO / Head of Sales
- CTO (para validación técnica si es necesario)

#### Estructura

**1. Resumen del pipeline (5 min)**
- Total value / weighted value vs target
- Deals ganados y perdidos la semana anterior
- Nuevos leads ingresados

**2. Review deal-by-deal (15 min)**
- Solo deals en etapa Discovery, Proposal, o Negotiation (los que pueden cerrarse en 30-60 días)
- Por cada deal:
  - ¿Qué avanzó esta semana?
  - ¿Cuál es el next step concreto?
  - ¿Hay algún blocker?
  - ¿La probabilidad sigue siendo correcta? (ajustar si cambió algo)
  - ¿Necesita apoyo del CEO o CTO?

**3. Deals stalled / at risk (5 min)**
- Deals sin actividad en > 2 semanas
- Decisión: reactivar con acción concreta o mover a Closed Lost

**4. Forecast y acciones (5 min)**
- ¿Qué deals son realistas para cerrar este mes?
- ¿Hay suficiente pipeline para cumplir el target del mes/quarter?
- Si no: ¿qué acciones de generación de leads se necesitan?

### Template de notas de pipeline review

```
## Pipeline Review - [Fecha]

### Resumen
- Pipeline total: $[X] | Ponderado: $[Y]
- Deals activos: [N]
- Won esta semana: [deals] | Lost: [deals]
- Nuevos leads: [N]

### Deal Updates
1. [Empresa] - [Etapa] - $[Valor]
   - Update: [qué pasó]
   - Next: [próxima acción + fecha]
   - Risk: [si hay]

### Deals Stalled
- [Empresa] - última actividad [fecha] → Acción: [plan]

### Forecast
- Cierre probable este mes: $[X]
- Acciones necesarias: [lista]
```

---

## 6. Pipeline Health Indicators

### Indicadores de pipeline sano

| Indicador | Saludable | Alerta | Crítico |
|-----------|----------|--------|---------|
| Pipeline coverage (pipeline total / target revenue) | > 3x | 2-3x | < 2x |
| Deals activos | > 10 | 5-10 | < 5 |
| Deals en etapa avanzada (Proposal+) | > 3 | 1-3 | 0 |
| Nuevos leads por semana | > 3 | 1-3 | 0 |
| Deals stalled (> 3 semanas sin movimiento) | 0-1 | 2-3 | > 3 |
| Diversificación de segmentos | 3-4 segmentos | 2 segmentos | 1 segmento |
| Average deal age | < 60 días | 60-90 días | > 90 días |

### Acciones correctivas

| Problema | Acción |
|----------|--------|
| Poco pipeline total | Aumentar outbound: más eventos, más prospección LinkedIn, activar referidos |
| Muchos leads pero baja conversión a Qualified | Revisar targeting -- ¿estamos hablando con las personas correctas? |
| Deals se estancan en Discovery | Mejorar discovery call, asegurar que estamos hablando con decision makers |
| Deals se estancan en Proposal | Revisar calidad de propuesta, hacer follow-up más agresivo, ofrecer piloto |
| Alta tasa de Closed Lost | Analizar motivos, ajustar approach de venta, revisar pricing |
| Pipeline concentrado en 1 segmento | Diversificar esfuerzo de prospección a segmentos subatendidos |

---

## 7. Herramientas Recomendadas

### MVP (ahora)
- **Este archivo markdown** + spreadsheet en Google Sheets para tracking diario
- **Google Calendar** para recordatorios de follow-up
- **Gmail** con templates para emails de seguimiento

### Siguiente nivel (cuando haya 10+ deals activos)
- **HubSpot Free CRM** o **Pipedrive** ($15/user/mes) para gestión visual del pipeline
- **Calendly** para agendar reuniones sin fricción
- **Loom** para enviar videos personalizados de follow-up

### Escala (cuando haya equipo de ventas de 3+ personas)
- **HubSpot Sales Pro** ($90/user/mes) para sequences, reporting, forecasting
- **LinkedIn Sales Navigator** ($80/mes) para prospección
- **Gong/Chorus** para grabar y analizar llamadas de venta
