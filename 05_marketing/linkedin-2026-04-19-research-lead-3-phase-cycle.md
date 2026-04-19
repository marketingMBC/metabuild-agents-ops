# LinkedIn Post — Research Lead autónomo: los 10 porqués del ciclo 3-phase task-driven

**Date:** 2026-04-19
**Task:** [M-19ABR] en Agent Task Queue (347a6b94-34ae-816c-a839-d77ece2eeffd)
**Channel:** LinkedIn (post de feed)
**Pillar:** AI Agents in Production
**Voice:** Rodrigo Requena Rivera (GM Meta Build City + Doctoral Candidate PUC)
**Length:** 1523 chars
**Status:** [DRAFT — Rodrigo envía]
**Cost:** $0.017595 (Claude Sonnet 4.5 via OpenRouter)

---

Mi Research Lead agent escribió 9500 palabras de mi tesis doctoral (Cap2 §2.1-2.5, 13-17 abr) a $0.046/día. Aquí los 10 porqués del ciclo 3-fases que realmente funciona.

La arquitectura es deliberadamente simple: scan 08:00 (Perplexity Sonar) → write 13:00 (Claude Sonnet 4.5) → review 19:00 (Gemini Flash), lunes a sábado. No hay magia, hay task-driven design.

El 13 de abril aprendí por qué esto importa. Sonar alucinó "morning routine" cuando el prompt decía "morning" literal: retornó contenido sobre rutinas matinales de longevidad en vez de Tech 4.0 research. Costo: 4 horas. Lección: keywords verbatim en Agent Task Queue de Notion, nunca improvisar.

Lo que funciona:
• Task Queue como contrato: el agente lee keywords exactas, no interpreta
• Feedback textual en bloques Notion editables (bidireccional, no VETO gate)
• Output contract: cada run = artefacto + Activity Log entry + Telegram notif
• Cap 3 v0.3 peer-reviewed con fuentes T1 (WoS, Scopus, IEEE)
• 5 secciones en español, $1.20/mes de costo operacional

No estoy vendiendo autonomía total. Estoy probando que los agentes escriben mejor cuando los tratas como coautores técnicos con scope preciso, no como asistentes mágicos.

Esto es parte de mi tesis doctoral en PUC Chile sobre Tech 4.0 + gestión de organizaciones.

¿Qué parte del ciclo scan→write→review te parece más frágil para producción académica o enterprise?

#AgenticAI #DoctoralResearch #Tech4punto0 #TaskDrivenDesign #AntiHallucination

---

## Metadata
- **Hook (200 chars):** "Mi Research Lead agent escribió 9500 palabras de mi tesis doctoral (Cap2 §2.1-2.5, 13-17 abr) a $0.046/día. Aquí los 10 porqués del ciclo 3-fases que realmente funciona."
- **Numbers cited:** 9500 palabras, $0.046/día, $1.20/mes, 13-17 abril, 4 horas, 08:00/13:00/19:00, Cap2 §2.1-2.5, Cap 3 v0.3
- **Personalization:** monograph real progress, anti-hallucination bug anecdote del 13 abr, PUC doctoral context, peer-reviewed T1 sources

## Review pending
Fase ANALYZE (Gemini Flash) ejecuta ahora con verdict PUBLISH / REVISE / KILL.
