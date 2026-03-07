# Product Vision Board — Pajudometro

**Version:** 1.0
**Fecha:** 2026-03-06
**Basado en:** CLAUDE.md, Banco de Productos, Validacion, Critica

---

## 1. Vision

> **Democratizar la verificacion de discursos politicos en tiempo real en Colombia**, reemplazando la dependencia de fact-checks periodisticos asincrónicos con un agente de IA que transcribe, extrae afirmaciones verificables y emite veredictos con fuentes citadas — poniendo la auditoria civica directamente en el bolsillo del ciudadano.

---

## 2. Segmento Objetivo (Target Group)

### Segmento A: Ciudadano Informado
| Dimension | Detalle |
|---|---|
| **Perfil** | Colombianos 18–45, urbanos, digitalmente activos |
| **Comportamiento** | Consumen noticias politicas en redes sociales y TV |
| **Frustracion** | No tienen herramientas para verificar lo que escuchan en tiempo real |
| **Geografia MVP** | Colombia (Bogota, Medellin, Cali, Barranquilla) |
| **Contexto** | Ciclo electoral 2026 (legislativas marzo, presidenciales mayo) |
| **Canal** | App movil (iOS, Android) + Web |

### Segmento B: Periodistas y Fact-checkers
| Dimension | Detalle |
|---|---|
| **Perfil** | Redacciones independientes, verificadores de medios |
| **Organizaciones** | ColombiaCheck, La Silla Vacia, medios regionales |
| **Frustracion** | Proceso manual de transcripcion + verificacion toma horas/dias |
| **Volumen** | 10–50 discursos/semana durante campanas electorales |
| **Necesidad** | Pipeline automatizado que acelere su flujo de trabajo |

### Usuario diario
**Ciudadano curioso** — no es periodista, pero quiere saber si lo que dice un politico es verdad o mentira. Necesita respuestas rapidas, claras y con fuentes.

---

## 3. Necesidades (Needs / Pains)

### Ciudadano Informado
| Pain | Evidencia |
|---|---|
| **Verificacion inaccesible** | Solo 3 organizaciones hacen fact-checking sistematico en Colombia |
| **Asimetria temporal** | Las verificaciones se publican dias despues del discurso, cuando ya circuló |
| **Sobrecarga informativa** | 59% de colombianos preocupados por falsedades en internet (Reuters Institute) |
| **Desconfianza generalizada** | Politicos e influencers senalados como mayor peligro para la informacion veraz |

### Periodistas y Fact-checkers
| Pain | Evidencia |
|---|---|
| **Proceso manual lento** | Transcribir + investigar + redactar una verificacion toma 4–8 horas |
| **Capacidad limitada** | Equipos pequenos no pueden cubrir todos los discursos de campana |
| **Sin herramientas LATAM-native** | Full Fact y Factiverse operan en ingles/Europa, sin adaptacion a espanol colombiano |
| **Fragmentacion de fuentes** | No hay pipeline unificado que conecte transcripcion con bases de verificacion |

### JTBD

> **Cuando** escucho a un politico colombiano haciendo afirmaciones en un debate, entrevista o mitin, **quiero** grabar ese fragmento y obtener un analisis automatico de veracidad con fuentes verificables, **para** tomar decisiones informadas y no depender de que un medio lo verifique dias despues.

---

## 4. Producto (Product / Solution)

### One-Liner
**Pajudometro** es una app movil que funciona como un "Shazam para discursos politicos": graba audio de un politico colombiano, y un agente de IA transcribe, extrae afirmaciones, las fact-checkea contra fuentes confiables y devuelve un score de credibilidad con veredicto por cada claim.

### Capacidades clave del MVP

| # | Capacidad | Descripcion |
|---|---|---|
| 1 | **Captura de audio** | Grabacion desde microfono con auto-stop, upload a almacenamiento en la nube |
| 2 | **Agente de analisis agéntico** | Loop multi-turn con LLM que orquesta: transcripcion, extraccion de claims, identificacion de orador, fact-checking con fuentes |
| 3 | **Veredicto por claim** | Cada afirmacion clasificada como verdad / mentira / enganoso con explicacion y fuente verificable |
| 4 | **Score de veracidad (0–100)** | Gauge visual que resume la credibilidad del discurso completo |
| 5 | **Historial de grabaciones** | Registro de analisis pasados del usuario |
| 6 | **Rankings de politicos** | Leaderboard por veracidad acumulada basado en todas las grabaciones |
| 7 | **Procesamiento transparente** | Pantalla paso a paso con logs en tiempo real |

### Principios no negociables
1. **Agnóstico** — Misma pipeline para cualquier politico, sin filtros ideologicos
2. **Trazabilidad** — Cada veredicto tiene fuente verificable citada
3. **Anti-alucinacion** — Si no hay fuente verificable, se marca como no verificable
4. **Transparencia** — El usuario ve cada paso del analisis en tiempo real
5. **Privacidad** — Audio procesado en servidor, compliance con Ley 1581 de 2012

---

## 5. Valor de Negocio (Business Value)

### Modelo de negocio
**Freemium** — acceso gratuito con limite de grabaciones/mes. Tier premium para uso ilimitado + exportacion de reportes + acceso API.

### North Star Metric
**Discursos verificados por semana**

### KPIs clave (metas MVP a 90 dias)

| Categoria | KPI | Meta |
|---|---|---|
| **Activacion** | Tasa de completacion del flujo (grabar → ver resultados) | >=70% |
| **Activacion** | Tiempo de analisis end-to-end | <60 segundos |
| **Calidad** | Precision de transcripcion (WER) | <15% |
| **Calidad** | Claims con fuente verificable | >=80% |
| **Calidad** | Tasa de alucinacion en veredictos | <2% |
| **Retencion** | Usuarios que graban 2+ discursos en 7 dias | >=30% |
| **Engagement** | Grabaciones por usuario activo/semana | >=3 |

### Propuesta de ROI (para periodistas)

| Metrica de impacto | Antes (manual) | Despues (Pajudometro) |
|---|---|---|
| Tiempo por verificacion | 4–8 horas | <5 minutos |
| Discursos verificados/dia | 1–2 | Ilimitado |
| Cobertura de campana | Parcial (solo discursos principales) | Total (cualquier ciudadano graba) |
| Trazabilidad de fuentes | Notas del periodista | Estructurada + enlazada |

---

## 6. Diferenciacion (Competitive Advantage)

### Brecha de mercado

> **No existe un producto movil en LATAM que permita a un ciudadano grabar un discurso politico y obtener un fact-check automatico con IA en menos de un minuto, con veredicto por claim y fuentes citadas.**

### Posicionamiento vs. competidores

| Competidor | Limitacion clave | Diferenciador Pajudometro |
|---|---|---|
| **Full Fact AI** | Enfocado en redacciones, no B2C; inglés primero | Directo al ciudadano, espanol nativo, movil-first |
| **Factiverse Live** | Plataforma para periodistas, no consumidor final | App movil accesible para cualquier persona |
| **ColombiaCheck** | Manual, asincrono (dias de delay) | Automatico, resultado en <1 minuto |
| **Google Fact Check Tools** | API sin interfaz de usuario, requiere integracion tecnica | Experiencia end-to-end en una app |
| **ChatGPT / Copilot** | Generalista, sin pipeline de fact-checking estructurado | Agente especializado en verificacion con fuentes trazables |
| **ClaimBuster** | Deteccion de claims sin verificacion; ingles solamente | Pipeline completo: deteccion + verificacion + veredicto |

### Ejes de posicionamiento
```
Accesibilidad:    Solo periodistas  <--- --->  Cualquier ciudadano
Velocidad:        Dias (manual)     <--- --->  Segundos (automatico)

Pajudometro ocupa el cuadrante vacio: Ciudadano + Automatico
```

---

## 7. Contexto Estrategico

### Por que ahora?

| Tendencia | Implicacion |
|---|---|
| **Elecciones Colombia 2026** | Legislativas (marzo) y presidenciales (mayo) — pico de demanda de verificacion |
| **Alianza ColombiaCheck-CRC-MOE** | Reconocimiento oficial de la necesidad de herramientas tech contra desinformacion |
| **Modelos de transcripcion mejorados** | Nuevos modelos STT (2025) reducen WER significativamente en espanol |
| **Agentes de IA mainstream** | Tool-calling en LLMs permite pipelines de verificacion multi-paso confiables |
| **Mercado anti-desinformacion** | Proyectado a $4.9B para 2030, CAGR 42% |
| **59% colombianos preocupados** | Demanda ciudadana documentada por herramientas contra falsedades (Reuters Institute) |

### Decisiones estrategicas fundamentales

| Decision | Resolucion |
|---|---|
| Alcance geografico | Colombia-first (expandible a LATAM) |
| Segmento MVP | Ciudadano informado (B2C) |
| Plataforma | Flutter (iOS, Android, Web) |
| Backend | PostgreSQL + Auth + Storage en la nube |
| Modelo de negocio | Freemium |
| Idioma | Espanol colombiano |

### Top 3 riesgos

| Riesgo | Mitigacion |
|---|---|
| **Alucinacion en veredictos** | Cada claim requiere fuente verificable antes de emitir veredicto. Meta: <2% alucinacion |
| **Sesgo politico percibido** | Pipeline agnostico identico para todos los politicos. Transparencia total en fuentes. Sin filtros ideologicos |
| **Calidad de audio en entornos ruidosos** | Umbral de confianza en transcripcion; si es ambiguo, se marca como no verificable en vez de adivinar |

---

## 8. Roadmap de Alto Nivel (30/60/90 dias)

| Fase | Entregable principal | Hito |
|---|---|---|
| **Dias 1–30** | Flujo core: grabar → transcribir → extraer claims → fact-check → mostrar resultados | Agente funcional end-to-end con 3+ politicos verificados |
| **Dias 31–60** | Rankings de politicos + historial + mejora de UX de resultados + pruebas con usuarios reales | 50+ grabaciones reales analizadas con feedback cualitativo |
| **Dias 61–90** | Optimizacion de latencia + precision + segundo segmento (periodistas) + caso de estudio | Decision informada sobre modelo de negocio, calidad y canal de distribucion |

---

*Hardcore AI by 30X · Marzo 2026*
