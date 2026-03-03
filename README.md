# EntreVista AI 🤖💬

**Plataforma de entrevistas agénticas para América Latina** — IA que razona, repregunta y entrega evidencia estructurada al reclutador humano.

---

## 🎯 ¿Qué es EntreVista AI?

EntreVista AI es una plataforma SaaS que utiliza **IA agéntica** para conducir entrevistas de screening conversacionales vía **Telegram**, reemplazando chatbots de reglas estáticas con un agente inteligente que:

- 🧠 **Razona** sobre las respuestas del candidato en tiempo real
- 🔄 **Repregunta** de forma contextual y dinámica
- 📋 **Genera evidencia estructurada** con citas textuales para el reclutador
- 👤 **Mantiene al humano como decisor final** (Human-in-the-Loop)

> **JTBD:** *"Cuando mi equipo de reclutamiento está colapsado procesando cientos de aplicaciones con alta rotación, quiero un agente de IA que conduzca screenings conversacionales, adaptativos y 24/7 vía Telegram, para reducir el tiempo de contratación y entregar candidatos pre-evaluados con evidencia estructurada."*

---

## 🌎 Mercado Objetivo

| Segmento | Empresas | Sectores | Volumen |
|---|---|---|---|
| **BPO / Alto Volumen** | 200–5,000+ empleados | Contact centers, retail, logística | 500–5,000+ contrataciones/año |
| **Tech / SaaS** | 50–500 empleados | Software, fintech, startups | 50–300 contrataciones/año |

**Geografía MVP:** Colombia, México, Argentina

---

## 💡 Propuesta de Valor

> **En LATAM no existe un producto que combine razonamiento agéntico real + canal de mensajería nativo + output de evidencia estructurada, a un precio accesible por contratación exitosa.**

### Diferenciadores clave

| vs. Competidor | Ventaja EntreVista AI |
|---|---|
| **Magneto 365** | Razonamiento agéntico con repreguntas dinámicas (vs. flujos predefinidos) |
| **Webcand** | Conversación bidireccional adaptativa (vs. preguntas estáticas) |
| **Genomawork** | Evaluación dentro de un diálogo natural (vs. formato examen) |
| **Glider AI / HireVue** | LATAM-first, Telegram nativo, pricing por contratación (vs. enterprise global) |

---

## 🏗️ Estado del Proyecto

> ⚠️ **Fase actual: Especificación de producto** — No hay código fuente aún.

| Entregable | Estado |
|---|---|
| Investigación de mercado y dominio | ✅ Completo |
| Perfil de Cliente Ideal (ICP) | ✅ Completo |
| Análisis de mercado LATAM | ✅ Completo |
| Product Vision Board | ✅ Completo |
| PRD (13 segmentos) | ✅ Completo (v1.0) |
| Arquitectura técnica | ⏳ Pendiente |
| Backlog de ingeniería | ⏳ Pendiente |

---

## 📁 Estructura del Repositorio

```
entrev/
├── docs/                          # Documentos de investigación (inputs)
│   ├── overview.md                # Análisis profundo de plataformas agénticas,
│   │                              #   arquitectura, impacto operativo y marco
│   │                              #   regulatorio (2025-2026)
│   ├── icp.md                     # Perfil de Cliente Ideal (segmentos, dolores, deseos)
│   ├── mercado.md                 # Análisis de mercado HR Tech en LATAM
│   └── pvb.md                     # Product Vision Board v1.0
│
├── specs/                         # Especificaciones generadas (outputs)
│   └── prd.md                     # PRD completo v1.0 (aprobado)
│
├── ai-product-base.md             # Material de referencia: framework para productos AI
├── prompts-especificacion.md      # Metodología de co-creación (3 prompts secuenciales)
├── CLAUDE.md                      # Guía de contexto para asistentes AI
└── README.md                      # Este archivo
```

---

## 🔑 Principios No Negociables

| # | Principio | Regla |
|---|---|---|
| 1 | 🤝 **HITL** | La IA recomienda, el humano decide. Sin auto-reject. |
| 2 | 🔍 **Transparencia** | El candidato siempre sabe que habla con IA. |
| 3 | 📋 **Trazabilidad** | Cada puntaje tiene una cita textual de la transcripción. |
| 4 | 🛡️ **Anti-alucinación** | Si no sabe, escala a humano. Sin inventar datos. |
| 5 | 🔒 **Privacidad** | Solo datos profesionales. Nada biométrico ni emocional. |
| 6 | 💬 **Experiencia del candidato** | El candidato es usuario, no recurso. |

---

## 📊 Métricas Clave (Metas MVP a 90 días)

| Métrica | Antes | Meta |
|---|---|---|
| Time-to-screen | 2–5 días | < 1 hora |
| Candidatos screeneados/día/reclutador | ~20 | Ilimitado |
| Tasa de completación del screening | ~60% | ≥ 80% |
| Candidate NPS | N/A | ≥ 4.0/5.0 |
| Tasa de alucinación | N/A | < 1% |

**North Star Metric:** Contrataciones exitosas facilitadas por mes

---

## 🗺️ Roadmap 30/60/90 Días

| Fase | Qué se entrega | Hito |
|---|---|---|
| **Días 1–30** | Motor conversacional + guardrails + evaluación v1 | Agente funcional en Telegram + decisión de viabilidad del canal |
| **Días 31–60** | Dashboard HITL + rúbricas configurables + piloto #1 | Piloto con BPO en Colombia (200–300 candidatos) |
| **Días 61–90** | Iteración + segundo piloto + caso de estudio | Decisión informada sobre canal, modelo de negocio y calidad |

---

## 🧩 Modelo de Negocio

**Pago por contratación exitosa** — sin costo fijo. Solo se cobra cuando el producto entrega valor medible.

---

## 📝 Metodología de Co-Creación

El proyecto utiliza un proceso de **co-creación iterativa** con IA, definido en `prompts-especificacion.md`:

1. **Prompt 1 (PRD)** → `specs/prd.md` ✅
2. **Prompt 2 (Arquitectura)** → `specs/arquitectura.md` ⏳
3. **Prompt 3 (Backlog)** → `specs/backlog.md` ⏳

Cada prompt produce un segmento a la vez con revisión y aprobación humana antes de avanzar.

---

## 📚 Contexto de Mercado

- **HR Tech LATAM:** Mercado proyectado a $6,541M para 2030 (CAGR 15.5%)
- **Brecha agéntica:** Solo 14% de organizaciones en LATAM tiene IA agéntica en funcionamiento
- **Validación enterprise:** Workday adquirió Paradox en 2025 — lo conversacional agéntico es mainstream
- **Presión regulatoria:** EU AI Act (agosto 2026) + ley de IA ética Colombia

---

## 📄 Idioma

Toda la documentación está en **español** (mercado LATAM).

---

## 👥 Autores

- **Danny Bravo** — Product Lead
- **Claude AI** — AI Architect (co-creación)

---

*Proyecto desarrollado como parte del programa [Hardcore AI](https://hardcoreai30x.online/).*
