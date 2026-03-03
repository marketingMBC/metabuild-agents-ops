# Decision Log — Meta Build City

Registro de decisiones clave de la empresa. Cada decisión se documenta con contexto, opciones evaluadas, decisión tomada y rationale.

---

## Formato

```
### [FECHA] — [TÍTULO]
- **Contexto**: ¿Por qué se necesitaba tomar esta decisión?
- **Opciones evaluadas**: ¿Qué alternativas se consideraron?
- **Decisión**: ¿Qué se decidió?
- **Rationale**: ¿Por qué se eligió esta opción?
- **Owner**: ¿Quién es responsable de la ejecución?
- **Status**: Implementada / En progreso / Pendiente
- **Revisión**: ¿Cuándo se revisará esta decisión?
```

---

## Decisiones

### 2026-02-12 — Implementación del sistema operativo con Claude Code

- **Contexto**: El equipo es pequeño (2-5 personas) y necesita maximizar productividad. Se requiere un sistema que automatice operaciones repetitivas.
- **Opciones evaluadas**:
  1. Contratar más personal → Alto costo, lento
  2. Usar herramientas SaaS separadas → Fragmentación, curva de aprendizaje
  3. Implementar sistema con Claude Code + sub-agentes → Bajo costo, integrado, escalable
- **Decisión**: Opción 3 — Sistema operativo basado en Claude Code con 5 sub-agentes especializados
- **Rationale**: Maximiza automatización con mínimo overhead. Los sub-agentes cubren ventas, contenido, ops, técnico y estrategia. Se puede iterar rápidamente.
- **Owner**: Equipo fundador
- **Status**: Implementada
- **Revisión**: 2026-05-12

### 2026-02-12 — Modelo de pricing multi-tier

- **Contexto**: Definir estructura de precios para los 5 servicios y sus combinaciones.
- **Opciones evaluadas**:
  1. Precio fijo por servicio → Simple pero inflexible
  2. Solo hourly rate → Transparente pero impredecible para el cliente
  3. Multi-tier: proyecto fijo + retainer + consulting + revenue share → Flexible, múltiples revenue streams
- **Decisión**: Opción 3 — Modelo multi-tier con foco en proyectos (60%) y retainers (25%)
- **Rationale**: Permite adaptar pricing al tipo de cliente y proyecto. Los retainers generan revenue recurrente. Revenue share alinea incentivos en proyectos grandes.
- **Owner**: Equipo fundador
- **Status**: Implementada
- **Revisión**: 2026-05-12

### 2026-02-12 — Foco geográfico inicial en Chile

- **Contexto**: Definir mercado geográfico de lanzamiento.
- **Opciones evaluadas**:
  1. LATAM completo desde día 1 → Demasiado disperso
  2. Solo Santiago → Muy limitado
  3. Chile completo, con prioridad Santiago → Balance entre foco y oportunidad
- **Decisión**: Opción 3 — Chile como mercado principal, con apertura a proyectos remotos en LATAM
- **Rationale**: Chile tiene el mercado de construcción más maduro de LATAM en adopción tecnológica (PlanBIM, normativas). Permite validar servicios antes de expandir.
- **Owner**: Equipo fundador
- **Status**: En progreso
- **Revisión**: 2026-08-12

---

## Template para Nueva Decisión

```markdown
### [YYYY-MM-DD] — [Título descriptivo]

- **Contexto**:
- **Opciones evaluadas**:
  1.
  2.
  3.
- **Decisión**:
- **Rationale**:
- **Owner**:
- **Status**: Pendiente
- **Revisión**: [fecha]
```

---

*Usar `/ops decision [tema]` para agregar una nueva entrada.*
