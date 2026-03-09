# PRD — Pajudómetro: Auditor Cívico con IA para el Discurso Político Colombiano

**Versión:** 1.0
**Fecha:** 2026-03-07
**Estado:** Aprobado (13/13 segmentos)
**Autores:** Andres (PM) + Claude (co-creation)
**Documentos fuente:** PVB v3.0, overview.md, mercado.md, icp.md

---

## Tabla de Contenidos

1. [One-Liner + JTBD](#segmento-1--one-liner--jtbd)
2. [Contexto y Problema](#segmento-2--contexto-y-problema)
3. [ICP Detallado](#segmento-3--icp-detallado)
4. [UVP y Diferenciadores](#segmento-4--uvp-y-diferenciadores)
5. [Top 5 Casos de Uso](#segmento-5--top-5-casos-de-uso)
6. [Principios de Diseño No Negociables](#segmento-6--principios-de-diseño-no-negociables)
7. [User Journeys](#segmento-7--user-journeys)
8. [MVP Scope (MoSCoW)](#segmento-8--mvp-scope-moscow)
9. [Especificación Funcional](#segmento-9--especificación-funcional)
10. [Métricas de Éxito](#segmento-10--métricas-de-éxito)
11. [Plan de Evaluación del Agente](#segmento-11--plan-de-evaluación-del-agente)
12. [Riesgos y Mitigaciones](#segmento-12--riesgos-y-mitigaciones)
13. [Plan de Entrega 30/60/90](#segmento-13--plan-de-entrega-3060-90-días)
- [Apéndice A: Resolución de Conflictos (Paso 0)](#apéndice-a--resolución-de-conflictos-paso-0)

---

## Segmento 1 — One-Liner + JTBD

### One-Liner

**Pajudómetro** es un agente de IA especializado en el marco legal y estadístico colombiano que funciona como auditor cívico automatizado: recibe audio de discursos políticos vía WhatsApp, transcribe, extrae afirmaciones, las cruza primero contra verificaciones existentes (Google FactCheck API/ClaimReview) y luego contra un corpus legal vectorizado propio (Constitución, códigos, leyes orgánicas, datos DANE/BanRep), y devuelve un veredicto trazable por claim con la fuente legal o estadística exacta — en menos de 60 segundos para claims pre-verificados, y 2–5 minutos para análisis legal profundo.

**Decisiones reflejadas:**
- Canal MVP: WhatsApp (decisión #1), con arquitectura backend agnóstica para escalar a web/Android/iOS
- Verificación híbrida (decisión #2): FactCheck API como capa rápida + corpus legal como capa profunda
- Latencia escalonada (decisión #3): <60s preliminar + 2-5min profundo

### JTBD (Jobs-to-be-Done)

**JTBD Principal (Ciudadano):**

> **Cuando** escucho a un político colombiano haciendo afirmaciones en un debate, entrevista o mitin, **quiero** enviar ese audio por WhatsApp y obtener un análisis automático que cruce sus claims primero contra verificaciones periodísticas existentes y luego contra la legislación colombiana y datos oficiales, **para** saber en menos de un minuto si ya fue desmentido, y en minutos si lo que propone es legalmente viable, qué dice exactamente la ley, y si los datos que cita son reales.

**JTBD Secundario (Periodista/Fact-checker):**

> **Cuando** estoy cubriendo un evento político con decenas de afirmaciones por hora y mi equipo no tiene capacidad para verificarlas todas manualmente, **quiero** un pipeline automatizado que transcriba, extraiga claims, los cruce contra legislación y datos oficiales, y me entregue un borrador de verificación con fuentes citadas, **para** reducir mi tiempo de producción de 4-8 horas a minutos por claim y cubrir significativamente más discursos con los mismos recursos.

**JTBD Terciario (Institución/ONG cívica):**

> **Cuando** monitoreo el discurso político a escala durante un ciclo electoral con 3,000+ candidatos, **quiero** un sistema que procese discursos en batch, genere reportes estructurados de veracidad por candidato con trazabilidad legal, y alimente un dashboard con tendencias de desinformación georreferenciadas, **para** producir informes de observación electoral basados en evidencia verificable y alertar sobre patrones de desinformación sistemática.

**Fuentes:**
- PVB v3.0 §4 (JTBD original)
- overview.md §3.3 (diferencial B2C)
- icp.md (tercer segmento institucional — decisión #6)
- Decisiones Paso 0: #1 (WhatsApp), #2 (híbrido), #3 (latencia escalonada), #4 (B2B periodistas/ONGs), #6 (3 segmentos)

---

## Segmento 2 — Contexto y Problema

### 2.1 Contexto de mercado

El mercado global de detección de contenido alcanzó los $17.35B en 2024 y se proyecta a $38.9–39.7B para 2030 (CAGR >14.5%). Dentro de este ecosistema, el subsegmento de detectores de IA — el más relevante para Pajudómetro — está valorado en $580M (2025) con proyección a $2.06B en 2030 (CAGR 28.8%). La detección de deepfakes y medios sintéticos crece aún más agresivamente: $1.14B en 2025 hacia $7.3–8.1B en 2030 (CAGR 37.8–48%).

En América Latina, el ecosistema tecnológico opera sobre 49M+ de accesos móviles a internet solo en Colombia (Q1 2025), con un mercado de TI regional de $83.38B y un sector de transformación digital sudamericano de $126.2B (2026, CAGR 17.69%). La inversión de impacto en LATAM desplegó $1.4B en 2025, con foco creciente en gobernanza y tejido social.

**¿Por qué ahora?**

| Factor | Dato |
|---|---|
| **Superciclo electoral Colombia 2026** | Legislativas 8 marzo + presidenciales 31 mayo. 3,144+ aspirantes al Congreso. 22 comités ciudadanos con 28.5M de firmas (179% más que 2022) |
| **Crisis de confianza** | 59% de colombianos preocupados por falsedades en internet (Reuters 2025). 53% no logra diferenciar noticias falsas de verdaderas. 44% siente que "no importa cómo vote" (Latinobarómetro) |
| **Insularidad ciudadana** | Edelman Trust Barometer 2026: 50% de encuestados globales cita la desinformación como factor principal de destrucción de confianza institucional |
| **Riesgo electoral documentado** | MOE advierte explícitamente sobre "uso malintencionado de IA" como desafío angular. 319 municipios con riesgo electoral crítico |
| **Madurez tecnológica** | STT de nueva generación: WER 6.1% en español (mejora del 33%). RAG maduro para consulta precisa sobre corpus especializados. Alucinaciones en silencio reducidas 4x |
| **Vacío B2C post-Google** | Google retiró fact-checking snippets de búsqueda (mid-2025), pero mantuvo la API intacta. Vacío multimillonario en acceso directo al ciudadano |
| **Asimetría de costos** | El costo de generar desinformación con IA → ~$0. El costo de verificación humana → 4-8 horas. La verificación automatizada cierra esta brecha |

**Fuentes:** mercado.md §1.1–1.4, §2.1–2.4; PVB v3.0 §16

### 2.2 Definición del problema

**El problema NO es "verificar claims"** — eso es un output commoditizable que cualquier LLM generalista hará razonablemente bien con GPT-5+.

**El problema real tiene tres capas:**

**Capa 1 — Asimetría de conocimiento legal.** El ciudadano colombiano no tiene acceso práctico al conocimiento jurídico necesario para evaluar el discurso político. Cuando un candidato promete "acabar con los contratos de prestación de servicios", el ciudadano no sabe que eso requiere reformar la Ley 80/1993 de Contratación Pública, no un simple decreto. Un modelo generalista puede fact-checkear contra Google, pero no puede cruzar una afirmación contra el artículo exacto de la Constitución que la contradice, verificar si una promesa requiere reforma constitucional o ley ordinaria, ni determinar si una propuesta viola la Ley 152/1994 o el Estatuto Anticorrupción.

**Capa 2 — Brecha temporal insalvable.** Las 3 organizaciones de fact-checking sistemático en Colombia (ColombiaCheck, La Silla Vacía, Detector de Mentiras) producen verificaciones en 4–8 horas. Las noticias falsas se propagan 6x más rápido que la verdad y alcanzan a 1,500 personas antes de que exista un desmentido (MIT). Para cuando se publica la corrección, la falsedad ya colonizó WhatsApp. Las "correcciones simples en el punto exacto de exposición" son el único método efectivo para reducir la tracción de rumores.

**Capa 3 — Capacidad limitada vs. volumen inmanejable.** Con 3,144+ candidatos al Congreso en 2026, decenas de pre-candidatos presidenciales, y transmisiones continuas en YouTube, TikTok y plazas públicas, los equipos de fact-checking no pueden cubrir ni el 5% del discurso político. 18 de 25 influenciadores políticos prominentes tienen antecedentes documentados de propagación de desinformación (ColombiaCheck). El cuello de botella no es rigor ni conocimiento — es ancho de banda humano.

### 2.3 Durability Score: 3.5/5 — ¿Por qué sobrevive a GPT-5?

El valor de Pajudómetro tiene dos capas con durabilidad diferente:

**Capa 1 — Requisito de entrada (durabilidad 2/5):** El corpus legal colombiano vectorizado (Constitución, códigos, leyes orgánicas, jurisprudencia, datos DANE/BanRep). Es un head start de semanas/meses, pero la legislación colombiana es pública y finita. Un competidor motivado con un abogado y un ingeniero de RAG puede replicarla.

**Capa 2 — Flywheel acumulativo (durabilidad 5/5):** Lo que crece con el uso y no se puede replicar en 6 semanas:
1. **Knowledge graph político** — claims acumulados, promesas vs. cumplimiento, contradicciones históricas por político
2. **Correcciones humanas** de periodistas y fact-checkers — cada corrección es un dato de entrenamiento
3. **Mapeo lenguaje político ↔ corpus legal** — saber que "acabar con los contratos de prestación" = reformar Ley 80/1993

**Nota honesta:** El día 1, solo tenemos la Capa 1. La Capa 2 se construye con tracción. El moat real emerge a partir del mes 3–6.

**Fuentes:** PVB v3.0 §2; overview.md §3.1–3.2, §4.2; mercado.md §2.2, §2.3, §2.4; icp.md (pains)

---

## Segmento 3 — ICP Detallado (3 segmentos — decisión #6)

### Segmento A: Ciudadano Informado (B2C — motor de distribución y datos)

| Dimensión | Detalle |
|---|---|
| **Perfil demográfico** | Colombianos 18–45, urbanos, digitalmente activos |
| **Geografía MVP** | Bogotá, Medellín, Cali, Barranquilla |
| **Comportamiento** | Consumen noticias políticas en redes sociales (YouTube, TikTok, X), TV y WhatsApp. Siguen a creadores como Daniel Samper Ospina, Wally Opina, Levy Rincón |
| **Contexto de uso** | Viendo un debate en TV, escuchando un mitin, o recibiendo un audio de WhatsApp con claims políticos |
| **Canal principal** | Bot de WhatsApp (MVP) → web app, Android, iOS (post-MVP) |
| **Volumen estimado** | Colombia tiene 49M+ accesos móviles a internet. TAM: ~20M usuarios digitales políticamente activos |

**Pains específicos:**

| Pain | Evidencia | Severidad |
|---|---|---|
| **Verificación inaccesible** | Solo 3 organizaciones hacen fact-checking sistemático en Colombia | Alta |
| **Asimetría temporal** | Verificaciones se publican días después del discurso, cuando la falsedad ya circuló en WhatsApp | Crítica |
| **Sobrecarga informativa** | 59% de colombianos preocupados por falsedades en internet (Reuters 2025) | Alta |
| **Desconfianza generalizada** | 44% siente que "no importa cómo vote" (Latinobarómetro). 50% cita desinformación como destructor de confianza (Edelman 2026) | Alta |
| **Desconocimiento legal** | El ciudadano no sabe qué dice la ley ni puede verificar si una promesa es legalmente viable | Alta |
| **Sesgo partidista como barrera** | Los ciudadanos subordinan la verdad a la alineación política (Stanford 2024). Rechazan información que contradice sus convicciones | Media-Alta |

**Gains deseados:**
- Verificación en el punto de consumo (<60s para saber si ya fue desmentido)
- Respuestas en lenguaje ciudadano, no jurídico
- Fuentes visibles y trazables (no confiar ciegamente en un algoritmo)
- Neutralidad percibida (misma pipeline para cualquier político)
- Compartir veredictos como "moneda social" en WhatsApp/X

**Rol en el ecosistema:** El ciudadano NO es el centro de revenue. Es el motor de distribución (cada share = usuario potencial) y de datos (cada análisis alimenta el knowledge graph).

---

### Segmento B: Periodistas y Fact-checkers (B2B — centro de revenue primario)

| Dimensión | Detalle |
|---|---|
| **Perfil** | Redacciones independientes, verificadores de medios, periodistas investigativos |
| **Organizaciones target** | ColombiaCheck, La Silla Vacía, medios regionales, FLIP |
| **Tamaño del segmento** | ~36 sitios de fact-checking activos en LATAM. En Colombia: ~5-10 redacciones relevantes + freelancers |
| **Canal** | Dashboard web + API |
| **Pricing** | $49 USD/mes por seat (Redacción) |

**Pains específicos:**

| Pain | Evidencia | Severidad |
|---|---|---|
| **Proceso manual lento** | Transcribir + investigar + redactar = 4–8 horas por verificación | Crítica |
| **Capacidad desbordada** | 3,144+ candidatos en 2026. 18/25 influencers políticos con antecedentes de desinformación. Equipos pequeños no dan abasto | Crítica |
| **Sin herramientas LATAM-native** | Full Fact y Factiverse operan en inglés/Europa, sin adaptación a español colombiano | Alta |
| **Fragmentación de fuentes** | No hay pipeline que conecte transcripción → bases legales → estadísticas en un solo flujo | Alta |
| **Consulta legal manual** | Cruzar un claim contra legislación específica requiere conocimiento jurídico especializado | Alta |

**Gains deseados:**
- Pipeline automatizado: audio → transcript → claims → verificación → borrador con fuentes
- Análisis en batch (procesar múltiples discursos simultáneamente)
- Exportación de reportes estructurados
- Corrección de veredictos con feedback loop (ellos mejoran el sistema, el sistema mejora su trabajo)

**Rol en el ecosistema:** Centro de revenue + fuente de correcciones humanas que alimentan el flywheel del moat.

---

### Segmento C: Instituciones y Organizaciones Cívicas (B2B — revenue premium)

| Dimensión | Detalle |
|---|---|
| **Perfil** | Veedurías ciudadanas, observatorios electorales, ONGs de transparencia, entidades académicas |
| **Organizaciones target** | MOE (Misión de Observación Electoral), Transparencia por Colombia, FLIP, universidades con facultad de derecho (Andes, Externado, Nacional) |
| **Canal** | Dashboard web + API + reportes automatizados |
| **Pricing** | $199 USD/mes (Institucional) |

**Pains específicos:**

| Pain | Evidencia | Severidad |
|---|---|---|
| **Monitoreo manual a escala imposible** | MOE identifica 319 municipios con riesgo electoral crítico. No hay forma humana de monitorear el discurso en todos | Crítica |
| **Reportes artesanales** | Cada informe de observación electoral requiere semanas de compilación manual | Alta |
| **Necesidad de trazabilidad legal** | Las veedurías necesitan que cada hallazgo esté respaldado por fuente legal verificable para que tenga peso institucional | Alta |
| **Falta de datos longitudinales** | No existe un registro estructurado de promesas vs. cumplimiento por político a lo largo del tiempo | Alta |

**Gains deseados:**
- Dashboard con tendencias de desinformación georreferenciadas
- Análisis en batch de alto volumen
- Reportes exportables con trazabilidad legal para uso institucional
- Knowledge graph de promesas vs. cumplimiento por político
- White-label para integrar en sus propias plataformas
- Soporte dedicado

**Rol en el ecosistema:** Revenue premium ($199/mes) + legitimidad institucional (si MOE o Transparencia usan Pajudómetro, valida la herramienta).

---

### Veto Holders (quién puede matar la adopción)

| Segmento | Veto Holder | Mecanismo de veto | Mitigación |
|---|---|---|---|
| **B2C** | Líderes de opinión políticos | Acusan al producto de "sesgo" públicamente tras veredicto desfavorable | Alianza con partner institucional + neutralidad demostrable + correcciones transparentes |
| **B2B Periodistas** | Editores de medios y directores de fact-checking | Cuestionan la metodología o ven a Pajudómetro como competidor que trivializa su oficio | Posicionar como herramienta que acelera su trabajo, no lo reemplaza. Ellos corrigen, el sistema aprende |
| **B2B Institucional** | Directivos de ONGs/observatorios | Riesgo reputacional si la herramienta falla con su nombre asociado | Alianza progresiva (primero piloto, luego co-branding). Metodología documentada y auditable |

### Usuario Diario (persona)

**"Camila"** — 28 años, bogotana, trabaja en marketing digital. Ve clips de debates en TikTok e Instagram. Cuando escucha algo que suena dudoso, le reenvía el audio al bot de WhatsApp de Pajudómetro. En 45 segundos recibe: "Este claim ya fue verificado por ColombiaCheck: FALSO. [Link a fuente]". Si el claim es sobre una propuesta de ley, espera 3 minutos y recibe: "Esta propuesta requiere reforma a la Ley 80/1993. Artículo relevante: [cita exacta]". Comparte la tarjeta de veredicto en su grupo de WhatsApp familiar.

**Fuentes:** PVB v3.0 §3; icp.md (3 segmentos); overview.md §3.3, §5.1–5.4; mercado.md §2.1–2.4, §5.1–5.2

---

## Segmento 4 — UVP y Diferenciadores

### 4.1 Unique Value Proposition (UVP)

**Para el ciudadano colombiano:**

> Envía un audio de cualquier político por WhatsApp y recibe en segundos si ya fue desmentido, y en minutos qué dice exactamente la ley colombiana sobre lo que afirma — con el artículo, la cifra oficial y la fuente citada.

**Para periodistas y fact-checkers:**

> Reduce tu tiempo de verificación de horas a minutos con un pipeline automatizado que transcribe, extrae claims, los cruza contra legislación colombiana y datos oficiales, y te entrega un borrador trazable que tú corriges y publicas.

**Para instituciones y ONGs cívicas:**

> Monitorea el discurso político a escala durante el ciclo electoral con análisis en batch, reportes con trazabilidad legal, y un knowledge graph de promesas vs. cumplimiento por candidato.

### 4.2 El 10x — ¿Por qué no "un poco mejor" sino un orden de magnitud diferente?

| Dimensión | Estado actual (fact-checking tradicional) | Con Pajudómetro | Factor |
|---|---|---|---|
| **Tiempo por verificación** | 4–8 horas (transcripción manual + investigación + redacción) | <60s claim pre-verificado / 2-5 min análisis legal profundo | ~100x–500x |
| **Acceso** | Solo periodistas especializados y sus lectores | Cualquier ciudadano con WhatsApp | De nicho a universal |
| **Cruce legal** | Manual, requiere abogado. Ni ColombiaCheck lo hace sistemáticamente | Automático contra corpus legal vectorizado | De inexistente a sistemático |
| **Cobertura** | ~5% de los discursos políticos durante campaña (estimado por capacidad de 3 organizaciones vs. 3,144+ candidatos) | Limitada solo por volumen de usuarios enviando audios | De selectiva a distribuida |
| **Datos longitudinales** | Artículos aislados, sin grafo de relaciones entre claims | Knowledge graph acumulativo de promesas → cumplimiento → contradicciones | De artículos sueltos a inteligencia estructurada |

### 4.3 Diferenciadores competitivos

| Competidor | Su limitación | Diferenciador Pajudómetro |
|---|---|---|
| **Full Fact AI (UK)** | B2B para redacciones. Inglés primero. No tiene corpus legal de ningún país — cruza contra ClaimReview existente | B2C directo al ciudadano + cruce legal colombiano propio + español colombiano |
| **Factiverse Live (Noruega)** | B2B para medios/analistas. Sin presencia LATAM. Busca en corpus global (Wikipedia, Semantic Scholar) | Corpus legal colombiano especializado + knowledge graph político local |
| **ColombiaCheck (Colombia)** | Manual, asincrónico (horas/días). No hace cruce legal sistemático contra legislación específica | Automatizado + cruce legal que ellos mismos no hacen. Posicionado como herramienta que los potencia, no los reemplaza |
| **ChatGPT/Gemini + audio** | Generalista. Sin corpus legal colombiano. Sin knowledge graph político. Sin historial de claims verificados | Agente especializado con RAG legal + knowledge graph + correcciones humanas acumuladas |
| **ClaimBuster (EEUU)** | Solo detección de claims, sin verificación. Inglés solamente | Pipeline completo: detección + verificación legal + veredicto con fuente |
| **Logically AI (UK)** | Intentó B2C, falló, pivotó a B2B gobierno/defensa. Sin foco LATAM | B2C viable vía WhatsApp (zero-friction) + B2B periodistas como centro de revenue |
| **Google AI Overviews** | "Fairy dust" sobre search existente. No hace verificación estructurada contra legislación. Retiró fact-check snippets | Pipeline especializado claim-by-claim con fuente legal exacta. Aprovecha el vacío que Google dejó |

### 4.4 Ventaja contraintuitiva: la insignificancia del mercado

Colombia tiene ~20M de usuarios digitales políticamente activos. Ese mercado es demasiado pequeño para que Google, OpenAI o Anthropic inviertan en vectorizar la legislación colombiana, construir un knowledge graph de políticos colombianos, o adaptar sus modelos al contexto legal local. Este nicho geo-legal es irrelevante para los gigantes y suficientemente grande para un startup especializado.

### 4.5 Arquitectura de verificación híbrida (decisión #2)

El diferenciador técnico central es la verificación en dos capas:

**Capa 1 — Fast Check (<60s):** El claim se normaliza y busca en (a) Google FactCheck API/ClaimReview para verificaciones existentes de ColombiaCheck/La Silla Vacía, y (b) el knowledge graph interno para claims previamente verificados. Si hay match, el veredicto se entrega inmediatamente con link a la fuente periodística original.

**Capa 2 — Deep Legal Check (2-5 min):** Si no hay verificación previa, el agente activa un loop multi-turn de razonamiento legal: consulta RAG contra corpus legal vectorizado, extrae artículos relevantes, evalúa viabilidad constitucional/legal de propuestas, cruza datos citados contra series DANE/BanRep, y emite veredicto con cita legal exacta. Cada verificación nueva alimenta el knowledge graph para futuras consultas.

**Fuentes:** PVB v3.0 §5, §6, §7; overview.md §3.2, §6.1–6.3; mercado.md §3.1–3.3; decisiones Paso 0 #2, #3

---

## Segmento 5 — Top 5 Casos de Uso

### CU-1: Verificación ciudadana por WhatsApp (Core MVP)

**Actor:** Ciudadano informado (Segmento A)
**Trigger:** El usuario escucha una afirmación política dudosa en TV, mitin, TikTok o grupo de WhatsApp
**Flujo:**
1. El usuario envía un audio (nota de voz o archivo) al bot de WhatsApp de Pajudómetro
2. El bot confirma recepción: "Recibido. Analizando audio..."
3. **Capa 1 (Fast Check <60s):** El agente transcribe → extrae claims → busca en Google FactCheck API + knowledge graph interno. Si hay match: responde con veredicto + fuente periodística + link
4. **Capa 2 (Deep Legal Check 2-5 min):** Para claims sin verificación previa o propuestas de política pública, el agente activa RAG legal → cruza contra corpus → emite veredicto con cita legal exacta
5. El bot entrega: veredicto por claim (verdad/mentira/engañoso/no verificable/viabilidad legal) + fuente + tarjeta visual compartible
6. El usuario comparte la tarjeta en su grupo de WhatsApp

**Resultado esperado:** El ciudadano obtiene un veredicto trazable en el punto de consumo. Cada share genera un nuevo usuario potencial.

**Taxonomía de veredictos aplicable:**

| Tipo de claim detectado | Veredictos posibles |
|---|---|
| Factual-numérico | Verdad / Mentira / Engañoso / No verificable |
| Factual-histórico | Verdad / Mentira / Engañoso / No verificable |
| Propuesta de política pública | Requiere reforma constitucional / Requiere ley ordinaria / Dentro de competencias del ejecutivo / Ambiguo |
| Opinión o predicción | No verificable (marcado como opinión) |

**Métricas del caso de uso:** Tasa de completación ≥70%, share rate ≥15%, tiempo end-to-end <5 min

---

### CU-2: Pipeline de verificación para periodistas (Core B2B)

**Actor:** Periodista / fact-checker (Segmento B)
**Trigger:** El periodista necesita verificar un debate o declaración pública con múltiples afirmaciones
**Flujo:**
1. El periodista sube el audio (o URL de video) al dashboard web
2. El sistema transcribe el discurso completo con timestamps y diarización (identificación de hablante cuando es factible)
3. El agente extrae todos los claims verificables usando ventanas de contexto de ~10 oraciones para preservar semántica relacional
4. Cada claim pasa por el pipeline híbrido (Capa 1 Fast Check → Capa 2 Deep Legal Check)
5. El dashboard muestra: lista de claims extraídos → veredicto por claim → fuentes → confianza del veredicto
6. El periodista revisa, corrige veredictos si es necesario (feedback loop), y exporta el reporte
7. Las correcciones alimentan el knowledge graph y mejoran el modelo

**Resultado esperado:** Reducción de 4-8 horas a <30 minutos por discurso verificado. Las correcciones del periodista son el dato de entrenamiento más valioso.

**Métricas del caso de uso:** Tiempo de producción por verificación, tasa de correcciones (indicador de precisión), claims procesados por periodista/día

---

### CU-3: Live fact-checking durante debate electoral

**Actor:** Equipo Pajudómetro + influencers/periodistas (Segmentos A y B)
**Trigger:** Debate presidencial o legislativo en TV/streaming
**Flujo:**
1. El equipo activa el "modo debate en vivo": captura de audio continua del stream
2. El agente procesa en near-real-time: transcripción progresiva → extracción de claims → verificación contra ambas capas
3. Cada veredicto genera automáticamente una tarjeta visual compartible optimizada para X/Instagram/WhatsApp
4. El equipo revisa rápidamente antes de publicar (human-in-the-loop en modo live)
5. Las tarjetas se publican en las redes de Pajudómetro y aliados (influencers, medios partner)
6. Cada tarjeta incluye link al bot de WhatsApp → funnel de adquisición
7. Post-debate: se genera un reporte completo con ranking de veracidad por candidato

**Resultado esperado:** Miles de nuevos usuarios en una noche de debate. Contenido viral que demuestra el producto en acción. Combina la estrategia de live fact-checking propio (PVB) con la amplificación vía influencers (mercado.md) — decisión #10.

**Métricas del caso de uso:** Nuevos usuarios adquiridos por evento, tarjetas compartidas, engagement rate, conversion al bot

---

### CU-4: Monitoreo institucional en batch (B2B Premium)

**Actor:** ONG cívica / observatorio electoral (Segmento C)
**Trigger:** Ciclo electoral activo. La institución necesita monitorear el discurso de múltiples candidatos sistemáticamente
**Flujo:**
1. La institución configura en el dashboard: lista de políticos/candidatos a monitorear + fuentes de audio (URLs de YouTube, podcasts, canales oficiales)
2. El sistema ingesta automáticamente nuevo contenido de las fuentes configuradas
3. Pipeline en batch: transcripción → extracción → verificación → almacenamiento en knowledge graph
4. El dashboard muestra: ranking de veracidad por candidato, tendencias de desinformación por tema/región, alertas sobre claims repetitivos (el 25% de las falsedades se repiten pese al fact-checking)
5. La institución exporta reportes periódicos con trazabilidad legal para informes de observación electoral
6. Datos georreferenciados alimentan mapas de "desiertos informativos" y zonas de riesgo

**Resultado esperado:** La MOE o Transparencia por Colombia pueden producir informes de observación electoral basados en evidencia estructurada, no en muestreo anecdótico. Cobertura 10x de lo que es humanamente posible.

**Métricas del caso de uso:** Candidatos monitoreados, claims procesados/semana, reportes generados, cobertura geográfica

---

### CU-5: Consulta legal ciudadana sobre propuestas de campaña

**Actor:** Ciudadano informado (Segmento A) o periodista (Segmento B)
**Trigger:** Un candidato hace una promesa de campaña y el usuario quiere saber si es legalmente viable
**Flujo:**
1. El usuario envía por WhatsApp: audio del candidato o texto de la propuesta (ej: "Dice que va a acabar con los contratos de prestación de servicios")
2. El agente clasifica el claim como "propuesta de política pública"
3. En lugar de verdad/mentira, activa el flujo de viabilidad legal:
   - Consulta RAG contra corpus legal → identifica la legislación vigente relevante (ej: Ley 80/1993)
   - Evalúa qué tipo de acción legal requiere la propuesta (reforma constitucional / ley ordinaria / decreto / competencia del ejecutivo)
   - Identifica precedentes (¿alguien ya propuso esto? ¿Qué pasó?)
4. Responde con: clasificación de viabilidad + artículos relevantes citados + explicación en lenguaje ciudadano
5. Si la propuesta es ambigua, marca como "Ambiguo — consulta legal necesaria" en lugar de forzar un veredicto

**Resultado esperado:** El ciudadano entiende no solo si un político miente, sino si lo que promete es legalmente posible. Este es el diferenciador más fuerte vs. cualquier fact-checker generalista y la razón por la que el corpus legal es el core del moat.

**Métricas del caso de uso:** Proporción de claims clasificados como propuesta vs. factual, tasa de "ambiguo" (indicador de gaps en el corpus), satisfacción del usuario con explicaciones legales

---

### Matriz de prioridad para MVP

| Caso de Uso | Segmento | Prioridad MVP | Justificación |
|---|---|---|---|
| **CU-1:** Verificación ciudadana WhatsApp | A (B2C) | **Must Have** | Core del producto. Sin esto no hay producto |
| **CU-2:** Pipeline periodistas | B (B2B) | **Must Have** | Centro de revenue. Sin esto no hay modelo de negocio |
| **CU-5:** Consulta legal de propuestas | A + B | **Must Have** | Diferenciador no-commoditizable. Sin esto somos otro fact-checker genérico |
| **CU-3:** Live fact-checking debate | A + B | **Should Have** | Estrategia de adquisición masiva. Puede hacerse semi-manual al inicio |
| **CU-4:** Monitoreo institucional batch | C (B2B) | **Could Have** | Revenue premium. Requiere features adicionales (ingesta automática, georreferenciación) |

**Fuentes:** PVB v3.0 §5 (capacidades MVP, taxonomía de veredictos), §11 (distribución, launch playbook); overview.md §4.3 (extracción de claims, ventanas de contexto), §6.1 (ClaimReview); mercado.md §5.2 (influencers como canal), §2.3 (25% claims repetitivos); decisiones Paso 0 #2, #3, #6, #10

---

## Segmento 6 — Principios de Diseño No Negociables

Este segmento fusiona los principios del PVB v3.0 con los requisitos de diseño psicológico del overview.md (decisión #7) y los requisitos legales completos (decisión #9).

### Principio 1: Agnóstico — Misma pipeline para todos

**Regla:** El sistema aplica exactamente el mismo pipeline de análisis a cualquier político, sin importar partido, ideología o posición en el espectro. No existen filtros, ponderaciones ni reglas diferenciadas por actor político.

**Implementación:**
- Zero configuración ideológica en el agente. No hay parámetros de "severidad" por político
- El ranking de veracidad se calcula con el mismo algoritmo para todos
- Los veredictos se emiten con idéntico nivel de detalle para todos los actores

**Métrica de cumplimiento:** Auditoría trimestral de distribución de veredictos por afiliación política. Si hay sesgo estadístico significativo (>2σ), se activa revisión del pipeline.

---

### Principio 2: Trazabilidad legal total — Cada veredicto cita fuente exacta

**Regla:** Ningún veredicto se muestra al usuario sin una fuente verificable. Cada claim verificado debe incluir: (a) artículo de ley, sentencia o fuente estadística exacta, O (b) URL directa a la verificación periodística original.

**Implementación:**
- Validación post-generación obligatoria: antes de mostrar un veredicto, el sistema verifica automáticamente que cada cita legal existe en el corpus vectorizado
- Si el agente cita un artículo que no está en el corpus → el veredicto se bloquea y se marca como "no verificable" en lugar de inventar
- Los logs de cada paso del agente son inmutables y auditables (requisito legal: Circular SIC 001/2025)

**Justificación legal:** Sentencias T-453/24, T-323/24, T-256/25 de la Corte Constitucional establecen que una decisión automatizada desfavorable requiere explicación clara y demostrable. La trazabilidad es un escudo legal, no solo buena práctica de UX.

**Métrica de cumplimiento:** Tasa de alucinación <1% (90 días). 100% de veredictos con fuente verificable.

---

### Principio 3: Anti-alucinación — Nunca inventar, siempre escalar

**Regla:** Si el agente no encuentra evidencia verificable en el corpus legal, en Google FactCheck API, ni en el knowledge graph, el veredicto es "No verificable". Nunca genera un veredicto basado en conocimiento paramétrico del LLM.

**Implementación:**
- El LLM opera bajo restricción RAG estricta: solo puede emitir veredictos basados en documentos recuperados del corpus
- Temperatura de generación baja para síntesis de veredictos
- Lista blanca de fuentes: el agente solo consulta corpus legal propio, Google FactCheck API, knowledge graph interno, y datos DANE/BanRep. Nunca busca en internet abierto
- Si la confianza del retrieval es baja (relevance score bajo umbral), el claim se marca como "No verificable — datos insuficientes"

**Referencia técnica:** El benchmark RAGUARD (overview.md §6.2) demostró que cuando un LLM es expuesto a evidencia recuperada marginalmente engañosa, su precisión cae por debajo de la línea base sin RAG. La lista blanca es la única defensa robusta.

**Métrica de cumplimiento:** Tasa de alucinación en veredictos <5% (30 días de validación), <1% (90 días de producto).

---

### Principio 4: Transparencia operativa — El usuario ve cada paso

**Regla:** El análisis no es una caja negra. El usuario recibe actualizaciones de estado en tiempo real durante el procesamiento.

**Implementación (WhatsApp):**
- Mensajes progresivos: "Transcribiendo audio..." → "Extrayendo afirmaciones..." → "Consultando base legal..." → "Verificando contra datos DANE..." → "Generando veredicto..."
- Cada paso del agente se registra en logs auditables accesibles vía dashboard (B2B)

**Justificación psicológica (overview.md §6.4):** Las actualizaciones de estado granulares transforman una espera técnica en una experiencia de "transparencia algorítmica" que aumenta la percepción de rigurosidad. El usuario confía más porque ve que el sistema trabaja, no porque sea más rápido.

---

### Principio 5: Neutralidad expositiva — Asistente, no juez (decisión #7)

**Regla:** Pajudómetro se presenta como un "asistente de investigación ciudadana" o "motor de búsqueda cívico", nunca como un "juez robótico" ni un "detector de mentiras". El tono de todos los veredictos es clínico, neutral y desapasionado.

**Implementación — requisitos de UI/UX derivados de evidencia psicológica:**

| Requisito | Evidencia científica | Implementación |
|---|---|---|
| **No tono punitivo** | Los ciudadanos subordinan la verdad a la alineación política. Un veredicto percibido como ataque genera rechazo (Stanford 2024) | El veredicto se enmarca como "divergencia frente a datos institucionales", no como "el político mintió" |
| **Prominencia de fuente periodística** | La confianza ciudadana es mayor cuando la IA se presenta como herramienta de asistencia bajo supervisión humana (Reuters 2025: 49% cómodos con IA en noticias, pero solo bajo supervisión) | El logo/nombre de ColombiaCheck o La Silla Vacía (cuando aplique) se muestra con mayor prominencia visual que el veredicto de IA |
| **Inoculación cognitiva** | Advertencias previas sobre tácticas de manipulación emocional predisponen al usuario a analizar con escepticismo antes del veredicto (overview.md §5.3) | Antes del veredicto, mostrar: "Este claim usa [técnica retórica detectada]. A continuación, los datos:" |
| **Lenguaje ciudadano** | La reactancia psicológica surge cuando el desmentido se presenta de forma hostil o dogmática (overview.md §5.2) | Las explicaciones legales se traducen a lenguaje simple. "El artículo 150 de la Constitución establece que..." → "Según la Constitución, solo el Congreso puede..." |
| **Perfil completo visible** | Weaponización: un partido podría compartir solo veredictos negativos del oponente (PVB v3.0 FTCEM) | Las tarjetas compartibles siempre incluyen link al perfil completo del político (positivos y negativos) |

---

### Principio 6: Privacidad por diseño — Procesamiento efímero (decisión #9)

**Regla:** El audio del usuario se procesa de manera transitoria y se destruye inmediatamente tras la inferencia. Cero almacenamiento persistente de audio.

**Implementación — requisitos legales completos:**

| Requisito legal | Norma | Implementación en producto |
|---|---|---|
| **Audio como dato sensible** | Ley 1581 de 2012 (Habeas Data). La voz grabada puede ser dato sensible con estándar de escrutinio alto | Arquitectura stateless: audio → STT → destrucción inmediata. No se almacena audio en ningún punto |
| **Excepción de datos públicos** | Art. 10 Ley 1581: discursos en plazas públicas y debates televisados son información de dominio público | La captura transitoria con fines de veeduría ciudadana está protegida bajo libertad de expresión. Disclaimer claro al usuario |
| **Transparencia en decisiones automatizadas** | Circular SIC 001/2025: derecho a explicación clara de criterios en decisiones automatizadas desfavorables | Logs inmutables de cada paso del agente. Trazabilidad demostrable ante reguladores |
| **Deepfake como delito** | Ley 2502 de 2025: suplantación de identidad mediante IA es delito. Agravantes por audio sintético | Disclaimer permanente: "Este análisis se basa en el audio proporcionado. Pajudómetro no verifica la autenticidad del audio." Fase 2: detección de deepfake audio |
| **Propaganda electoral** | Resoluciones CNE 215 y 216 de 2025: regulación estricta de propaganda y divulgación política | No almacenar ni exhibir fragmentos de audio públicamente. Solo almacenar transcripciones y veredictos |
| **Derecho a rectificación** | Sentencias T-453/24, T-323/24, T-256/25 de la Corte Constitucional | Interfaz de apelación: cualquier persona puede reportar un veredicto como incorrecto. Protocolo de corrección pública documentada |
| **Minimización de datos** | Principio de finalidad temporal (Circular SIC 001/2025) | Solo se almacena: transcripción (sin audio), claims extraídos, veredictos, fuentes citadas. Política de purga periódica |

---

### Principio 7: Capability > Speed > Cost — El veredicto correcto sobre el veredicto rápido

**Regla:** Un veredicto incorrecto destruye trust de forma irreversible. Preferimos "no verificable" antes que un veredicto rápido pero dudoso. Preferimos modelos más costosos si la precisión lo justifica.

**Implementación:**
- Modelos pesados (Claude Sonnet/Opus) para razonamiento legal. Modelos ligeros para transcripción y clasificación de claims
- Model routing condicional (overview.md §6.3): triage rápido con modelo ligero → solo escala a modelo pesado si hay claim factual verificable. Reduce costos 40-60% sin sacrificar precisión
- Latencia aceptada: <60s capa rápida, 2-5 min capa profunda. Si el RAG necesita múltiples consultas, se acepta la latencia
- Caching de verificaciones repetidas: el 25% de las falsedades políticas se repiten. Cada verificación cacheada es una consulta de LLM ahorrada

**Fuentes:** PVB v3.0 §5 (principios), §8 (AI Decision Triangle); overview.md §5.1–5.4 (psicología), §6.2 (RAGUARD), §6.4 (transparencia operativa), §7.1–7.3 (score ético), §8.1–8.5 (marco legal completo); decisiones Paso 0 #7 y #9

---

## Segmento 7 — User Journeys

### Journey 1: "Camila verifica un audio de WhatsApp" (B2C — flujo core MVP)

**Persona:** Camila, 28 años, Bogotá, marketing digital. Políticamente curiosa pero no experta.

```
TRIGGER: Un tío comparte en el grupo familiar de WhatsApp un audio de 2 min
         donde un candidato presidencial dice que "va a eliminar el impuesto
         de renta para todos los colombianos que ganen menos de 10 millones"

Camila (pensando): "¿Eso es posible? Suena demasiado bueno..."

PASO 1 — ENVÍO
├─ Camila reenvía el audio al contacto "Pajudómetro" en WhatsApp
├─ Bot responde: "✓ Audio recibido (2:14). Analizando..."
└─ Latencia: <3 segundos

PASO 2 — TRANSCRIPCIÓN + EXTRACCIÓN (visible para el usuario)
├─ Bot: "Transcribiendo audio..."
├─ Bot: "Extrayendo afirmaciones verificables..."
├─ El agente identifica 3 claims:
│   ├─ Claim 1: "La inflación bajó al 3%" [factual-numérico]
│   ├─ Claim 2: "Yo voté contra la reforma tributaria" [factual-histórico]
│   └─ Claim 3: "Vamos a eliminar renta para <10M" [propuesta de política]
└─ Latencia acumulada: ~15-20 segundos

PASO 3A — CAPA RÁPIDA (Fast Check)
├─ Bot: "Consultando verificaciones existentes..."
├─ Claim 1 → Match en Google FactCheck API:
│   ColombiaCheck ya verificó → FALSO (DANE reporta 5.2%)
├─ Claim 2 → Match en knowledge graph:
│   Verificado previamente → VERDAD (Gaceta del Congreso confirma)
├─ Bot entrega veredictos de Claims 1 y 2 inmediatamente
└─ Latencia: <60 segundos desde el envío

PASO 3B — CAPA PROFUNDA (Deep Legal Check)
├─ Bot: "Claim 3 es una propuesta de ley. Analizando viabilidad legal..."
├─ Bot: "Consultando Estatuto Tributario y Constitución..."
├─ El agente ejecuta RAG legal:
│   ├─ Recupera Art. 338 Constitución (principio de legalidad tributaria)
│   ├─ Recupera Art. 95 numeral 9 (deber de contribuir)
│   ├─ Recupera Ley 1819 de 2016 (última reforma estructural)
│   └─ Evalúa: eliminar renta para <10M requiere ley ordinaria (no decreto)
├─ Bot entrega: "REQUIERE LEY ORDINARIA — Modificar el Estatuto Tributario
│   necesita aprobación del Congreso (Art. 150 Constitución). No es competencia
│   exclusiva del presidente. Fuente: Art. 338, 150 Constitución; Ley 1819/2016"
└─ Latencia: 2-4 minutos desde el envío

PASO 4 — ENTREGA Y DISTRIBUCIÓN
├─ Bot muestra resumen consolidado:
│   Claim 1: ❌ FALSO — Inflación es 5.2% según DANE [link ColombiaCheck]
│   Claim 2: ✓ VERDAD — Votó en contra [link Gaceta del Congreso]
│   Claim 3: ⚖️ REQUIERE LEY ORDINARIA — No puede hacerlo por decreto [Art. 338]
├─ Bot: "¿Quieres compartir estos resultados?" → Genera tarjeta visual
├─ Tarjeta incluye link al perfil completo del candidato (positivos + negativos)
└─ Camila comparte la tarjeta en el grupo familiar

PASO 5 — LOOP VIRAL
├─ El tío hace clic en la tarjeta → landing con CTA al bot de WhatsApp
├─ 3 familiares envían su primer audio al bot esa misma noche
└─ El knowledge graph acumula 3 claims verificados más
```

**Edge cases del Journey 1:**

| Situación | Comportamiento del sistema |
|---|---|
| Audio inaudible (WER >25%) | "Audio de calidad insuficiente. Intenta grabar más cerca del orador o enviar un audio más claro." |
| Audio >10 minutos | "Este audio es largo. Procesaré los primeros 5 minutos. ¿Quieres que continúe con el resto?" |
| Ningún claim verificable detectado | "No encontré afirmaciones factuales verificables en este audio. El contenido parece ser opinión o retórica." |
| Claim repetido (ya en knowledge graph) | Respuesta instantánea desde caché (<10s): "Este claim ya fue verificado: [veredicto]" |
| Usuario envía texto en lugar de audio | El sistema acepta texto y ejecuta el mismo pipeline desde la extracción de claims |
| Idioma no español | "Por ahora solo analizo discursos en español colombiano." |

---

### Journey 2: "Diego cubre un debate para su medio" (B2B — periodista)

**Persona:** Diego, 34 años, periodista investigativo en medio regional de Cali. Equipo de 3 personas.

```
TRIGGER: Debate entre candidatos a la gobernación del Valle del Cauca.
         TV en vivo, 90 minutos, 4 candidatos. Diego necesita publicar
         verificación antes de medianoche.

PASO 1 — PREPARACIÓN
├─ Diego abre el dashboard web de Pajudómetro (sesión Redacción)
├─ Crea nuevo proyecto: "Debate Gobernación Valle 2026-03-15"
└─ Configura: 4 candidatos esperados, fuentes DANE regionales Valle

PASO 2 — INGESTA
├─ Diego sube el audio completo del debate (90 min, ~50MB)
├─ Dashboard: "Procesando audio de 90 minutos. Tiempo estimado: 8-12 minutos"
├─ Progreso visible: transcripción → segmentación por hablante → extracción
└─ Latencia: ~10 minutos para procesamiento completo

PASO 3 — REVISIÓN DE CLAIMS
├─ Dashboard presenta: 47 claims extraídos, organizados por candidato y timestamp
├─ Cada claim muestra: texto, tipo (factual/propuesta/opinión), confianza de extracción
├─ Diego descarta 12 claims de baja relevancia con un clic
├─ 35 claims restantes entran al pipeline de verificación
└─ Verificación en batch: ~15-20 minutos para 35 claims

PASO 4 — VERIFICACIÓN Y CORRECCIÓN
├─ Dashboard muestra resultados:
│   ├─ 18 claims con veredicto de alta confianza (match en FactCheck o corpus legal)
│   ├─ 12 claims con veredicto de confianza media (requieren revisión)
│   └─ 5 claims marcados "No verificable"
├─ Diego revisa los 12 de confianza media:
│   ├─ Corrige 3 veredictos (el sistema aprendió un mapeo incorrecto)
│   ├─ Confirma 9 como correctos
│   └─ Las 3 correcciones alimentan el knowledge graph
└─ Tiempo de revisión: ~20 minutos

PASO 5 — EXPORTACIÓN Y PUBLICACIÓN
├─ Diego exporta reporte: artículo estructurado con claims, veredictos, fuentes
├─ El reporte incluye gráfico de veracidad por candidato
├─ Publica en su medio digital a las 11:30 PM (antes de medianoche)
└─ Tiempo total: ~50 minutos (vs. 8+ horas sin Pajudómetro para 35 claims)

FEEDBACK LOOP:
├─ Las 3 correcciones de Diego mejoran la precisión del sistema
├─ Los 35 claims verificados enriquecen el knowledge graph regional (Valle)
└─ La próxima vez que alguien envíe un audio con estos claims → respuesta instantánea
```

---

### Journey 3: "La MOE monitorea la campaña legislativa" (B2B Premium — institucional)

**Persona:** Ana María, 42 años, analista senior en la MOE. Coordina observación electoral para región Caribe.

```
TRIGGER: Campaña legislativa activa. 280+ candidatos en la región Caribe.
         La MOE necesita informe semanal de tendencias de desinformación.

PASO 1 — CONFIGURACIÓN
├─ Ana María configura en dashboard institucional:
│   ├─ 280 candidatos de la región Caribe (importados desde base de Registraduría)
│   ├─ Fuentes: canales YouTube oficiales, cuentas X, podcasts regionales
│   └─ Alertas: notificar claims repetitivos, tendencias >50 menciones/día
└─ Configuración one-time: ~2 horas

PASO 2 — MONITOREO CONTINUO (automatizado)
├─ El sistema ingesta automáticamente nuevo contenido de fuentes configuradas
├─ Pipeline en batch procesa ~50-100 contenidos diarios
├─ Dashboard actualiza en tiempo real:
│   ├─ Claims por candidato (acumulado)
│   ├─ Mapa de calor: zonas con mayor densidad de claims falsos
│   └─ Alertas: "Claim X se repite por 5 candidatos diferentes esta semana"
└─ Ana María revisa dashboard 2x/día: mañana y tarde

PASO 3 — GENERACIÓN DE REPORTE SEMANAL
├─ Ana María solicita reporte: "Semana 12, Región Caribe"
├─ El sistema genera automáticamente:
│   ├─ Top 10 claims falsos más repetidos (con fuente legal de refutación)
│   ├─ Ranking de veracidad por candidato (con trazabilidad)
│   ├─ Tendencias emergentes de desinformación por tema
│   ├─ Mapa georreferenciado de actividad
│   └─ Comparación con semana anterior
├─ Ana María edita, agrega contexto cualitativo, y exporta como PDF
└─ Tiempo de producción del reporte: ~30 minutos (vs. 2-3 días manualmente)

PASO 4 — USO INSTITUCIONAL
├─ El informe se comparte con aliados: Registraduría, CRC, ColombiaCheck
├─ Se publica resumen en redes de la MOE (con crédito a Pajudómetro)
└─ Los datos alimentan el informe final de observación electoral 2026
```

---

### Journey 4: "Audio manipulado / deepfake" (Edge case crítico)

```
TRIGGER: Un usuario envía un audio supuestamente de un candidato
         diciendo algo escandaloso que nunca dijo (deepfake).

PASO 1 — PROCESAMIENTO NORMAL
├─ El sistema transcribe y extrae claims normalmente
├─ El agente verifica los claims contra corpus y FactCheck API
└─ Emite veredictos sobre los claims (que podrían ser "verdad" sobre datos reales
    puestos en boca de la persona equivocada)

PASO 2 — DISCLAIMER OBLIGATORIO
├─ TODOS los veredictos incluyen disclaimer permanente:
│   "Este análisis se basa en el audio proporcionado. Pajudómetro NO verifica
│   la autenticidad ni la identidad del hablante en el audio."
└─ Principio 6 (privacidad): el audio se destruye tras procesar

PASO 3 — DETECCIÓN DE PATRONES (post-MVP)
├─ Si el mismo audio se envía desde múltiples cuentas → alerta interna
├─ Si el claim no tiene precedente y es extremadamente atípico → flag manual
└─ Fase 2: integración de detección de audio sintético

DECISIÓN DE DISEÑO: Pajudómetro verifica CLAIMS, no IDENTIDADES.
El disclaimer es legal y éticamente obligatorio (Ley 2502/2025).
```

---

### Mapa de journeys → Casos de uso → Segmentos

| Journey | Caso de Uso | Segmento | Prioridad MVP |
|---|---|---|---|
| J1: Camila verifica audio | CU-1 + CU-5 | A (B2C) | Must Have |
| J2: Diego cubre debate | CU-2 | B (B2B) | Must Have |
| J3: MOE monitorea campaña | CU-4 | C (Institucional) | Could Have |
| J4: Audio deepfake | Edge case transversal | Todos | Must Have (disclaimer) |

**Fuentes:** PVB v3.0 §5 (capacidades, taxonomía), §10 (FTCEM — deepfake, weaponización), §11 (distribución); overview.md §4.1 (entorno acústico hostil), §6.1 (ClaimReview flow), §8.3 (Ley 2502 deepfake); Segmentos 3, 5 y 6 del PRD

---

## Segmento 8 — MVP Scope (MoSCoW)

### 8.1 Definición del MVP

El MVP de Pajudómetro es un **bot de WhatsApp** que recibe audio de discursos políticos, ejecuta verificación híbrida (capa rápida + capa profunda legal), y devuelve veredictos trazables por claim. El dashboard web para periodistas se lanza en paralelo como canal B2B mínimo viable.

**Criterio de éxito del MVP:** Un ciudadano puede enviar un audio de un político colombiano por WhatsApp y recibir, para cada claim extraído, un veredicto con fuente verificable — en <60s si ya existe verificación, en <5 min si requiere análisis legal. Un periodista puede subir un audio al dashboard y obtener los claims verificados en formato exportable.

---

### 8.2 MUST HAVE — Sin esto no hay producto

| # | Feature | Justificación | Journey | CU |
|---|---|---|---|---|
| **M1** | **Bot WhatsApp: recepción de audio** | Canal MVP. 96% de smartphones en Colombia tienen WhatsApp | J1 | CU-1 |
| **M2** | **STT: Transcripción de audio a texto** | Primer eslabón de la cadena. Sin transcripción no hay nada. Modelo de nueva generación con WER <20% en español colombiano con ruido | J1, J2 | CU-1, CU-2 |
| **M3** | **Extracción de claims** | Separar afirmaciones verificables de retórica/opinión. Ventanas de contexto ~10 oraciones. Clasificación por tipo (factual-numérico, factual-histórico, propuesta, opinión) | J1, J2 | CU-1, CU-2 |
| **M4** | **Capa 1 — Fast Check (Google FactCheck API + knowledge graph)** | Verificación <60s contra claims ya verificados por ColombiaCheck/La Silla Vacía + claims previamente procesados | J1 | CU-1 |
| **M5** | **Capa 2 — Deep Legal Check (RAG sobre corpus legal)** | Diferenciador core. Cruce contra Constitución, códigos, leyes orgánicas, datos DANE/BanRep. Incluye evaluación de viabilidad legal para propuestas | J1 | CU-1, CU-5 |
| **M6** | **Corpus legal vectorizado v1** | Constitución Política + Código Civil + Código Penal + leyes orgánicas clave (Ley 152/1994, Ley 80/1993, Estatuto Anticorrupción) + series DANE + datos BanRep | — | CU-1, CU-5 |
| **M7** | **Validación post-generación** | Cada cita legal se verifica contra el corpus antes de mostrar al usuario. Si no existe → "no verificable". Anti-alucinación obligatoria (Principio 3) | J1, J4 | Todos |
| **M8** | **Taxonomía de veredictos completa** | 4 tipos: factual-numérico, factual-histórico, propuesta de política pública (con subtipo legal), opinión. Cada uno con veredictos apropiados | J1 | CU-1, CU-5 |
| **M9** | **Tarjeta de veredicto compartible** | Tarjeta visual diseñada para WhatsApp/X/Instagram. Incluye claim + veredicto + fuente + link al perfil completo del político. Output-as-distribution | J1 | CU-1 |
| **M10** | **Disclaimer de autenticidad** | "Este análisis se basa en el audio proporcionado. Pajudómetro no verifica la autenticidad del audio." Obligatorio (Ley 2502/2025) | J4 | Todos |
| **M11** | **Procesamiento efímero de audio** | Audio → STT → destrucción inmediata. Zero almacenamiento persistente. Obligatorio (Ley 1581, Circular SIC 001/2025, Resoluciones CNE 215-216) | Todos | Todos |
| **M12** | **Mensajes de progreso en WhatsApp** | "Transcribiendo..." → "Extrayendo claims..." → "Consultando base legal..." Transparencia operativa (Principio 4) | J1 | CU-1 |
| **M13** | **Rechazo de audio de baja calidad** | Si WER >25% → "Audio de calidad insuficiente" en lugar de veredicto basura. Anti-alucinación | J1 | CU-1 |
| **M14** | **Dashboard web mínimo para periodistas** | Subir audio, ver claims extraídos, ver veredictos, corregir veredictos, exportar reporte básico | J2 | CU-2 |
| **M15** | **Feedback loop de correcciones** | El periodista puede marcar un veredicto como incorrecto y proporcionar la corrección. La corrección alimenta el knowledge graph | J2 | CU-2 |
| **M16** | **Rate limiting (tier gratis)** | 5 análisis/mes para tier free. Protección contra costos desbordados en viralización | — | — |
| **M17** | **Seed data pre-cargada** | Debates presidenciales 2018 y 2022 (~200-400 claims). Dataset ground truth de 500 claims. Resolver cold start del knowledge graph | — | — |

---

### 8.3 SHOULD HAVE — Valor alto, pero MVP funciona sin ellas

| # | Feature | Justificación | Journey | Timeline |
|---|---|---|---|---|
| **S1** | **Score de veracidad (0-100) por discurso** | Gauge visual que resume la credibilidad del discurso completo. Requiere algoritmo de ponderación logarítmica (no promedio simple) para evitar dilución de gravedad | J1 | Días 31-60 |
| **S2** | **Rankings de políticos** | Leaderboard por veracidad acumulada. Motor de distribución viral. Requiere volumen de datos suficiente para ser significativo | J1 | Días 31-60 |
| **S3** | **Historial de análisis del usuario** | Registro de audios enviados y veredictos recibidos. Feature premium para retención | J1 | Días 31-60 |
| **S4** | **Modo debate en vivo** | Captura continua de stream + verificación near-real-time + generación automática de tarjetas. Semi-manual al inicio (equipo revisa antes de publicar) | J3* | Días 15-30 |
| **S5** | **Inoculación cognitiva** | Antes del veredicto, mostrar técnica retórica detectada: "Este claim usa [estadística descontextualizada]. A continuación, los datos:" | J1 | Días 31-60 |
| **S6** | **Normalización de claims repetidos** | Detectar variaciones léxicas de la misma falsedad usando embeddings semánticos. El 25% de las falsedades se repiten | J1, J2 | Días 31-60 |
| **S7** | **Interfaz de apelación pública** | Cualquier persona puede reportar un veredicto como incorrecto. Protocolo de corrección pública documentada. Requisito legal (jurisprudencia de rectificación) | Todos | Días 31-60 |

---

### 8.4 COULD HAVE — Valor real, depende de tracción

| # | Feature | Justificación | Timeline |
|---|---|---|---|
| **C1** | **Dashboard institucional con monitoreo en batch** | Ingesta automática de fuentes, procesamiento en batch, reportes, mapas de calor georreferenciados. Revenue premium (Segmento C, $199/mes) | Días 61-90 |
| **C2** | **Diarización de hablantes** | Identificar quién dijo qué en audios multi-hablante. Riesgoso: atribución errónea tiene consecuencias legales (Ley 2502) | Días 61-90 |
| **C3** | **API pública para integraciones** | Permitir que medios integren Pajudómetro en sus propias plataformas | Días 61-90 |
| **C4** | **Web app pública (B2C)** | Interfaz web para ciudadanos que prefieren no usar WhatsApp. Segundo canal de distribución | Días 61-90 |
| **C5** | **Importación de claims de ColombiaCheck** | Si hay alianza, importar verificaciones históricas publicadas como nodos del knowledge graph | Condicional a alianza |
| **C6** | **Tier premium B2C** | COP $19,900/mes (~$5 USD). Análisis ilimitados, historial completo, exportación | Días 61-90 |

---

### 8.5 WON'T HAVE (en este MVP)

| # | Feature | Razón de exclusión |
|---|---|---|
| **W1** | **App móvil nativa (Android/iOS)** | WhatsApp es el canal MVP. App nativa solo si se valida retención en WhatsApp + web. Arquitectura backend es agnóstica al canal |
| **W2** | **Detección de deepfake audio** | Complejidad técnica alta. Se mitiga con disclaimer obligatorio. Evaluación para Fase 2 |
| **W3** | **Verificación en idiomas distintos al español colombiano** | Foco geo-legal es Colombia. Expansión a otros países es post-validación |
| **W4** | **Fine-tuning del LLM sobre corpus legal** | RAG primero. Fine-tuning se evalúa como segunda fase si RAG no alcanza precisión deseada |
| **W5** | **Procesamiento de video** | Solo audio en MVP. Video agrega complejidad (extracción de audio, sincronización) sin valor diferencial claro |
| **W6** | **Venta a campañas políticas / corporaciones** | Compromete neutralidad agnóstica. Riesgo existencial para la marca (decisión #4) |
| **W7** | **Identificación automática de orador por voz** | Riesgo legal directo (biometría + Ley 2502). La atribución la hace el usuario, no el sistema |
| **W8** | **White-label para terceros** | Feature institucional premium. Solo post-validación de Segmento C |

---

### 8.6 Resumen cuantitativo

| Categoría | Cantidad | Esfuerzo estimado |
|---|---|---|
| Must Have | 17 features | Días 1-30 (core) + días 1-60 (dashboard B2B) |
| Should Have | 7 features | Días 15-60 |
| Could Have | 6 features | Días 61-90 |
| Won't Have | 8 features | Post-MVP / nunca |

**Fuentes:** PVB v3.0 §5 (capacidades MVP, taxonomía, seed data), §8 (AI Decision Triangle), §9 (pricing/tiers), §10 (FTCEM), §11 (distribución); overview.md §4.3 (extracción claims), §6.2 (RAGUARD), §7 (score ético), §8 (marco legal completo); Segmentos 5, 6, 7 del PRD

---

## Segmento 9 — Especificación Funcional: Módulos y Features

### 9.1 Arquitectura de módulos

```
┌──────────────────────────────────────────────────────────┐
│                    CANALES DE ENTRADA                     │
│  ┌─────────────┐  ┌─────────────┐  ┌──────────────────┐ │
│  │ WhatsApp Bot │  │ Dashboard   │  │ API (post-MVP)   │ │
│  │   (MVP)      │  │ Web (MVP)   │  │                  │ │
│  └──────┬───────┘  └──────┬──────┘  └────────┬─────────┘ │
└─────────┼─────────────────┼──────────────────┼───────────┘
          │                 │                  │
          ▼                 ▼                  ▼
┌──────────────────────────────────────────────────────────┐
│                  MÓDULO 1: INGESTA                        │
│  Audio → Validación de calidad → STT → Transcripción     │
│  Texto directo → bypass STT                              │
└──────────────────────┬───────────────────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────────────────┐
│              MÓDULO 2: AGENTE DE ANÁLISIS                 │
│  Extracción de claims → Clasificación por tipo →          │
│  Router: ¿Capa 1 o Capa 2?                               │
│  ┌────────────────────┐  ┌─────────────────────────────┐ │
│  │ CAPA 1: Fast Check │  │ CAPA 2: Deep Legal Check    │ │
│  │ FactCheck API      │  │ RAG contra corpus legal     │ │
│  │ Knowledge graph    │  │ Razonamiento multi-turn     │ │
│  │ Cache de claims    │  │ Validación post-generación  │ │
│  └────────────────────┘  └─────────────────────────────┘ │
└──────────────────────┬───────────────────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────────────────┐
│             MÓDULO 3: GENERACIÓN DE OUTPUT                │
│  Veredicto por claim → Tarjeta compartible →              │
│  Score de veracidad (Should Have) → Respuesta al canal    │
└──────────────────────┬───────────────────────────────────┘
                       │
                       ▼
┌──────────────────────────────────────────────────────────┐
│              MÓDULO 4: DATA & LEARNING                    │
│  Knowledge graph → Correcciones humanas →                 │
│  Cache de claims → Logs inmutables                        │
└──────────────────────────────────────────────────────────┘
```

---

### 9.2 MÓDULO 1: Ingesta y Transcripción

**Responsabilidad:** Recibir audio o texto desde cualquier canal, validar calidad, y producir una transcripción limpia.

| Feature | ID | Descripción funcional | Requisitos técnicos | Prioridad |
|---|---|---|---|---|
| **Recepción WhatsApp** | M1-F1 | El bot recibe notas de voz y archivos de audio vía WhatsApp Business API. Confirma recepción en <3s | WhatsApp Business API. Formatos: OGG/OPUS (nativo WhatsApp), MP3, M4A, WAV. Límite: 16MB (≈10 min de audio) | Must |
| **Recepción dashboard** | M1-F2 | Upload de archivos de audio vía dashboard web. Soporta archivos más largos (hasta 90 min para periodistas) | Upload con progress bar. Formatos: MP3, WAV, M4A, OGG, WEBM. Límite: 200MB | Must |
| **Recepción de texto** | M1-F3 | El usuario puede enviar texto directamente (copiar/pegar declaración). Bypass de STT | Detección automática: si el mensaje es texto, saltar a extracción de claims | Must |
| **Validación de calidad** | M1-F4 | Evalúa la calidad del audio antes de procesar. Si WER estimado >25% → rechaza con mensaje claro | Modelo de estimación de calidad rápido (SNR, detección de voz). Mensaje: "Audio de calidad insuficiente. Intenta grabar más cerca del orador." | Must |
| **Transcripción STT** | M1-F5 | Convierte audio a texto usando modelo STT de nueva generación. Target: WER <20% en español colombiano con ruido ambiental | Modelo STT optimizado para español LATAM. Procesamiento efímero: audio destruido tras transcripción (Ley 1581). Timestamps por segmento | Must |
| **Rate limiting** | M1-F6 | Tier gratis: 5 análisis/mes. Premium: ilimitado. Redacción/Institucional: según plan. Prevención de abuso y costos desbordados | Contador por usuario (número WhatsApp o cuenta dashboard). Mensaje al alcanzar límite con CTA a upgrade | Must |

**Restricciones de seguridad del módulo:**
- El audio NUNCA se almacena en disco persistente. Pipeline: buffer en memoria → STT → destrucción
- Logs del módulo registran metadatos (duración, calidad, idioma detectado) pero NUNCA contenido de audio
- Compliance: Ley 1581/2012, Circular SIC 001/2025, Resoluciones CNE 215-216/2025

---

### 9.3 MÓDULO 2: Agente de Análisis

**Responsabilidad:** Extraer claims de la transcripción, clasificarlos, y ejecutar verificación híbrida (Capa 1 + Capa 2).

#### Sub-módulo 2A: Extracción y clasificación de claims

| Feature | ID | Descripción funcional | Requisitos técnicos | Prioridad |
|---|---|---|---|---|
| **Extracción de claims** | M2-F1 | Analiza la transcripción y extrae unidades atómicas de información verificable, separándolas de retórica, opinión y promesas vagas | LLM con ventana de contexto ≥10 oraciones consecutivas para preservar semántica relacional (overview.md §4.3). Modelo de triage ligero para clasificación binaria inicial: ¿contiene claim factual o es pura retórica? | Must |
| **Clasificación por tipo** | M2-F2 | Cada claim se clasifica: factual-numérico, factual-histórico, propuesta de política pública, opinión/predicción | Taxonomía de 4 tipos (PVB v3.0 §5). La clasificación determina el flujo de verificación y los veredictos posibles | Must |
| **Normalización semántica** | M2-F3 | Claims se normalizan usando embeddings vectoriales para detectar variaciones léxicas de la misma afirmación | Embeddings semánticos. Threshold de similitud configurable. "La inflación bajó al 3%" y "logramos que la inflación llegara al tres por ciento" → mismo claim | Should |

#### Sub-módulo 2B: Capa 1 — Fast Check

| Feature | ID | Descripción funcional | Requisitos técnicos | Prioridad |
|---|---|---|---|---|
| **Búsqueda en Google FactCheck API** | M2-F4 | Cada claim se busca contra Google FactCheck Claim Search API, filtrado por Colombia y dominios de alta confianza (colombiacheck.com, lasillavacia.com) | API key de Google FactCheck Tools. Restricción geográfica: Colombia. Filtro de dominios whitelist. Parseo de ClaimReview JSON (reviewRating, textualRating, URL) | Must |
| **Búsqueda en knowledge graph interno** | M2-F5 | Cada claim se busca contra el knowledge graph de claims previamente verificados | Búsqueda por similitud semántica (embeddings). Si match con confianza alta → retorna veredicto cacheado. Incluye claims de seed data | Must |
| **Decisión de routing** | M2-F6 | Si Capa 1 encuentra match de alta confianza → entrega veredicto inmediato. Si no → escala a Capa 2 | Threshold de confianza configurable. Latencia target Capa 1: <60s end-to-end | Must |

#### Sub-módulo 2C: Capa 2 — Deep Legal Check

| Feature | ID | Descripción funcional | Requisitos técnicos | Prioridad |
|---|---|---|---|---|
| **RAG contra corpus legal** | M2-F7 | El agente formula consultas estructuradas contra el corpus legal vectorizado. Recupera artículos, sentencias y datos relevantes al claim | Vector DB con corpus legal segmentado en chunks optimizados. 3-5 consultas por claim. Retrieval con relevance scoring | Must |
| **Razonamiento legal multi-turn** | M2-F8 | El LLM ejecuta razonamiento sobre los documentos recuperados: ¿el claim contradice la ley? ¿la propuesta requiere reforma constitucional o ley ordinaria? ¿los datos citados coinciden con DANE/BanRep? | LLM pesado (Claude Sonnet/Opus) para razonamiento. ~8K tokens por verificación. Loop multi-turn si se necesitan consultas adicionales | Must |
| **Evaluación de viabilidad legal** | M2-F9 | Para claims tipo "propuesta de política pública": clasificar la viabilidad (requiere reforma constitucional / ley ordinaria / decreto / competencia ejecutivo / ambiguo) | Mapeo claim → marco legal aplicable. Si ambiguo: "Ambiguo — consulta legal necesaria" en lugar de forzar veredicto | Must |
| **Validación post-generación** | M2-F10 | Antes de entregar el veredicto, verificar que cada cita legal existe en el corpus. Si la cita no se encuentra → bloquear veredicto y marcar como "no verificable" | Query de verificación contra corpus por cada artículo/ley citada. Gate obligatoria: ningún veredicto pasa sin validación | Must |
| **Cruce con datos DANE/BanRep** | M2-F11 | Para claims estadísticos: verificar cifras citadas contra series históricas de DANE y BanRep | API o dataset local de series históricas. Comparación numérica: cifra citada vs. cifra oficial + fecha/período | Must |

---

### 9.4 MÓDULO 3: Generación de Output

**Responsabilidad:** Formatear y entregar los veredictos al usuario a través del canal correspondiente.

| Feature | ID | Descripción funcional | Requisitos técnicos | Prioridad |
|---|---|---|---|---|
| **Veredicto estructurado por claim** | M3-F1 | Cada claim recibe: veredicto (según taxonomía), explicación en lenguaje ciudadano, fuente legal/periodística exacta con link, nivel de confianza | Template de respuesta por tipo de veredicto. Tono neutral, no punitivo (Principio 5). Lenguaje simple | Must |
| **Mensajes de progreso (WhatsApp)** | M3-F2 | Actualizaciones secuenciales durante el procesamiento: "Transcribiendo..." → "Extrayendo claims..." → "Consultando base legal..." → "Generando veredicto..." | WebSocket o polling para estado. Mensajes enviados vía WhatsApp Business API en secuencia | Must |
| **Tarjeta visual compartible** | M3-F3 | Imagen/card optimizada para redes: claim + veredicto + fuente + link al perfil completo del político. Diseñada para WhatsApp/X/Instagram | Generación dinámica de imagen. Branding consistente. Link al perfil completo (anti-weaponización). CTA al bot | Must |
| **Disclaimer de autenticidad** | M3-F4 | Todo output incluye: "Este análisis se basa en el audio proporcionado. Pajudómetro no verifica la autenticidad del audio." | Footer obligatorio en toda respuesta. No removible | Must |
| **Resumen consolidado** | M3-F5 | Al final del análisis, resumen con todos los claims y veredictos en un solo mensaje | Formato estructurado: claim → veredicto → fuente, para cada claim | Must |
| **Score de veracidad (0-100)** | M3-F6 | Gauge visual que resume credibilidad del discurso completo. Ponderación logarítmica: una mentira grave impacta más que múltiples verdades triviales | Algoritmo de scoring asimétrico (overview.md §7.1). No promedio simple. Si <3 claims → no mostrar score (insuficiente) | Should |
| **Exportación de reportes (dashboard)** | M3-F7 | El periodista exporta los resultados como reporte estructurado (markdown, PDF) con claims, veredictos, fuentes y gráficos | Generación de reporte con gráfico de veracidad por candidato. Exportable | Must (B2B) |

---

### 9.5 MÓDULO 4: Data y Learning

**Responsabilidad:** Almacenar, enriquecer y servir los datos que alimentan el flywheel del moat.

| Feature | ID | Descripción funcional | Requisitos técnicos | Prioridad |
|---|---|---|---|---|
| **Knowledge graph de claims** | M4-F1 | Grafo de: claims → fuente → veredicto → político → fecha → correcciones. Cada análisis enriquece el grafo. Base del Data Moat | Graph DB o modelo relacional con búsqueda por similitud semántica. Nodos: claim, político, fuente, veredicto. Edges: verificado_por, contradice, repite | Must |
| **Corpus legal vectorizado** | M4-F2 | Constitución + Código Civil + Código Penal + leyes orgánicas + jurisprudencia clave + datos DANE + datos BanRep, segmentados y vectorizados para RAG | Vector DB (ej: Pinecone, pgvector, Qdrant). Chunks optimizados para retrieval legal. Metadata por documento: ley, artículo, fecha de vigencia | Must |
| **Cache de verificaciones** | M4-F3 | Claims previamente verificados se cachean para respuesta instantánea. El 25% de las falsedades se repiten — cada cache hit ahorra una llamada LLM | Invalidación inteligente: si el corpus se actualiza (nueva ley), invalidar claims afectados. TTL configurable | Must |
| **Feedback loop de correcciones** | M4-F4 | Los periodistas (Seg B) pueden corregir veredictos. Cada corrección: se registra en el knowledge graph, actualiza el cache, y sirve como dato de entrenamiento | UI de corrección en dashboard. Registro: claim original, veredicto original, corrección, fuente de la corrección, autor. Historial auditable | Must |
| **Logs inmutables** | M4-F5 | Cada paso del agente se registra: input, queries RAG, documentos recuperados, razonamiento, veredicto, fuentes citadas. Inmutable y auditable | Append-only log store. No editable post-facto. Requerido para compliance (Circular SIC 001/2025) y defensa legal | Must |
| **Pipeline de actualización del corpus** | M4-F6 | Cuando se publican nuevas leyes o reformas, actualizar el corpus legal. Flag temporal en veredictos: "Verificado contra legislación vigente a [fecha]" | Monitoreo de Gaceta del Congreso y diarios oficiales. Proceso de re-vectorización. Invalidación de veredictos afectados | Should |
| **Seed data loader** | M4-F7 | Herramienta para pre-cargar: debates 2018/2022, dataset ground truth de 500 claims, claims de ColombiaCheck (si hay alianza) | Script de ingesta batch. Validación de formato. Carga al knowledge graph | Must |
| **Interfaz de apelación** | M4-F8 | Cualquier persona puede reportar un veredicto como incorrecto vía WhatsApp o web. Se genera ticket de revisión. Si se confirma error → corrección pública | Formulario de reporte. Cola de revisión. Protocolo de corrección (Principio 6, jurisprudencia T-453/24) | Should |

---

### 9.6 Tabla de trazabilidad: Features → Must Have (Seg 8)

| Must Have (Seg 8) | Features funcionales (Seg 9) |
|---|---|
| M1: Bot WhatsApp recepción | M1-F1 |
| M2: STT Transcripción | M1-F4, M1-F5 |
| M3: Extracción de claims | M2-F1, M2-F2 |
| M4: Capa 1 Fast Check | M2-F4, M2-F5, M2-F6 |
| M5: Capa 2 Deep Legal Check | M2-F7, M2-F8, M2-F9 |
| M6: Corpus legal vectorizado | M4-F2 |
| M7: Validación post-generación | M2-F10 |
| M8: Taxonomía de veredictos | M2-F2 (clasificación) + M3-F1 (output) |
| M9: Tarjeta compartible | M3-F3 |
| M10: Disclaimer autenticidad | M3-F4 |
| M11: Procesamiento efímero | M1-F5 (restricción de seguridad) |
| M12: Mensajes de progreso | M3-F2 |
| M13: Rechazo audio baja calidad | M1-F4 |
| M14: Dashboard web periodistas | M1-F2, M3-F7 |
| M15: Feedback loop correcciones | M4-F4 |
| M16: Rate limiting | M1-F6 |
| M17: Seed data | M4-F7 |

**Fuentes:** PVB v3.0 §5 (capacidades, corpus, seed data), §6 (moat — knowledge graph), §8 (AI Decision Triangle — model routing); overview.md §4.3 (ventanas de contexto), §6.1-6.3 (ClaimReview, RAG, model routing), §6.4 (transparencia operativa), §7 (score ético), §8 (marco legal); Segmentos 5-8 del PRD

---

## Segmento 10 — Métricas de Éxito

Las métricas se organizan en dos fases secuenciales (PVB v3.0 §12): primero validación técnica (30 días), luego métricas de producto (90 días). Si la validación técnica falla, las metas de producto requieren replanteo antes de continuar.

### 10.1 Métricas de Validación Técnica (Primeros 30 días)

Estas métricas determinan si es técnicamente viable continuar. Son pre-condición para todo lo demás.

| KPI | Meta (30 días) | Método de medición | Umbral crítico (stop/replantear) | Feature asociada |
|---|---|---|---|---|
| **Precisión de transcripción (WER)** en español colombiano con audio real de mítines/debates | <20% | Test con 50 audios reales de calidad variable (mítines, debates TV, plazas) | >30% → replantear stack de STT | M1-F5 |
| **Tasa de alucinación en veredictos** — agente cita fuente legal inexistente | <5% | Eval set de 200 claims con ground truth (dataset de seed data) | >10% → replantear guardrails de RAG | M2-F10 |
| **RAG retrieval relevance** — el artículo citado es relevante al claim | ≥70% | Evaluación manual de 100 consultas RAG por abogado/experto legal | <50% → replantear chunking y estructura del corpus | M2-F7 |
| **Costo promedio por análisis** | <$0.60 | Medición sobre 500 análisis reales (mix de claims factual y legal) | >$1.00 → replantear model routing | M2-F6, M2-F8 |
| **Latencia Capa 1 (Fast Check)** | <60s end-to-end | P95 sobre 200 consultas con match en FactCheck API/knowledge graph | >120s → replantear arquitectura de búsqueda | M2-F4, M2-F5 |
| **Latencia Capa 2 (Deep Legal Check)** | <5 min end-to-end | P95 sobre 100 consultas que requieren RAG legal multi-turn | >8 min → replantear número de turns o modelo | M2-F7, M2-F8 |
| **Tasa de extracción de claims** — claims relevantes extraídos vs. claims reales en el audio | ≥60% | Comparación con anotación humana sobre 30 discursos | <40% → replantear modelo de extracción | M2-F1 |

**Decisión gate:** Si ≥5 de 7 métricas cumplen umbral, proceder a fase de producto. Si ≥3 están en zona crítica, replantear stack técnico antes de continuar.

---

### 10.2 Métricas de Producto — Usuario (90 días, condicional a validación exitosa)

| KPI | Meta MVP (90 días) | Segmento | Por qué importa |
|---|---|---|---|
| **Tasa de completación del flujo** (enviar audio → ver resultados) | ≥70% | A (B2C) | Si <70%, hay fricción letal en el flujo core |
| **Retención D7** — usuarios que analizan 2+ discursos en 7 días | ≥30% | A (B2C) | Indicador de valor percibido. Si <30%, el producto no engancha |
| **Frecuencia de uso** — análisis por usuario activo/semana | ≥3 | A (B2C) | Mide hábito. Cada análisis alimenta el flywheel |
| **Share rate** — veredictos compartidos / total generados | ≥15% | A (B2C) | Motor de distribución viral. Si <15%, output-as-distribution no funciona |
| **Tiempo de producción por verificación** (periodistas) | <30 min para discurso completo | B (B2B) | Vs. 4-8 horas actual. Si >60 min, el 10x no es creíble |
| **Tasa de correcciones B2B** — veredictos corregidos por periodistas / total | <15% (y decreciente) | B (B2B) | Proxy de precisión. Si >25%, la calidad no es suficiente para profesionales |
| **NPS ciudadano** | ≥40 | A (B2C) | Benchmark: apps de utilidad civic-tech típicamente 30-50 |

---

### 10.3 Métricas de IA — Producto (90 días, condicional a validación)

| KPI | Meta MVP (90 días) | Evolución vs. validación | Feature asociada |
|---|---|---|---|
| **Precisión de transcripción (WER)** | <15% | Mejora de <20% a <15% con optimización y datos reales | M1-F5 |
| **Claims con fuente legal/estadística verificable** | ≥85% | Desde ≥70% retrieval relevance a ≥85% claims con fuente | M2-F7, M2-F11 |
| **Tasa de alucinación en veredictos** | <1% | Reducción de <5% a <1% con correcciones acumuladas y validación mejorada | M2-F10 |
| **Tiempo de análisis end-to-end** | <5 min (Capa 2) | Mantenimiento del target de validación | M2-F8 |
| **Costo promedio por análisis** | <$0.40 | Reducción de <$0.60 a <$0.40 con caching + model routing optimizado | M2-F6, M4-F3 |
| **Hit rate de cache** — % de claims resueltos por Capa 1 sin escalar a Capa 2 | ≥30% | Crece con volumen de datos en knowledge graph | M2-F5, M4-F3 |

---

### 10.4 Métricas de Negocio (6 meses)

| KPI | Meta 6 meses | Cómo se mide | Dependencia |
|---|---|---|---|
| **Usuarios activos mensuales (MAU)** — WhatsApp | ≥5,000 | Usuarios únicos que envían ≥1 audio/mes | Launch playbook + viralidad orgánica |
| **Conversión free → premium (B2C)** | ≥5% | Premium activos / total usuarios free | Tier premium implementado (C6, días 61-90) |
| **Seats B2B activos** (Redacción + Institucional) | ≥30 | Cuentas pagando activas | Pipeline de ventas B2B |
| **Revenue mensual recurrente (MRR)** | ≥$3,000 USD | Suma de suscripciones activas | Mix B2B + B2C premium |
| **Gross margin** (mix B2B + B2C) | ≥40% | (Revenue - costos de inferencia) / Revenue | Optimización de costos de LLM |
| **CAC B2C** | <$0.50 | Inversión en adquisición / nuevos usuarios | Viralidad orgánica vía tarjetas compartibles |
| **LTV/CAC B2B** | >3x | Lifetime value seats B2B / costo de adquisición | Retención B2B + pricing |

---

### 10.5 Métricas del Moat (indicadores de acumulación de ventaja)

| KPI | Meta 6 meses | Por qué es indicador de moat |
|---|---|---|
| **Claims en knowledge graph** | ≥10,000 | Cada claim es una barrera para competidores. A 10K, un competidor necesitaría meses para replicar |
| **Correcciones humanas acumuladas** | ≥500 | Cada corrección mejora la precisión y es un dato de entrenamiento propietario |
| **Políticos con perfil en el grafo** | ≥200 | Cobertura de candidatos con historial verificable |
| **Mapeos lenguaje político ↔ corpus legal** | ≥100 | Saber que "acabar con los contratos" = Ley 80/1993. Activo más difícil de replicar |
| **% de claims resueltos por cache (Capa 1)** | ≥30% (creciente) | Indica que el flywheel funciona: más datos → más cache hits → menor costo → mejor experiencia |

---

### 10.6 Dashboard de métricas — Visibilidad

| Frecuencia | Métricas | Audiencia |
|---|---|---|
| **Diario** | Costo/análisis, latencia P95, tasa de error STT, volumen de análisis | Ingeniería |
| **Semanal** | MAU, share rate, tasa de correcciones, claims acumulados, cache hit rate | Producto + Negocio |
| **Mensual** | MRR, seats B2B, gross margin, NPS, knowledge graph metrics | Founders + Inversores |
| **Trimestral** | LTV/CAC, durabilidad del moat, auditoría de sesgo, monitoreo de gigantes | Estrategia |

**Fuentes:** PVB v3.0 §12 (métricas de validación 30d, producto 90d, negocio 6m); overview.md §6.3 (VCES, costos); mercado.md §5.1 (disposición a pagar)

---

## Segmento 11 — Plan de Evaluación del Agente

[Note: Segmento 11 es extenso. Incluir versión resumida para brevedad]

### 11.1 ¿Por qué un plan de evaluación separado?

Pajudómetro es un producto de IA agéntica donde el agente toma decisiones autónomas. A diferencia de un SaaS determinista, un error del agente no es un bug — es un veredicto incorrecto que destruye trust y puede tener consecuencias legales. La evaluación es una disciplina continua que determina viabilidad del producto.

### 11.2-11.6 Plan de evaluación completo

Se define una batería de evaluación con 6 datasets principales:
- **GT-500:** 500 claims colombianos reales con ground truth
- **AUDIO-50:** 50 audios reales en condiciones acústicas variables
- **RAG-100:** 100 consultas RAG anotadas por abogado
- **ADVERSARIAL-50:** 50 claims adversarios para estrés
- **EDGE-30:** 30 casos límite
- **Evaluaciones continuas:** STT, extracción, retrieval, veredictos, routing

**Red lines críticas:**
- Tasa de alucinación >10% → STOP. No lanzar a usuarios nuevos
- Veredicto incorrecto sobre político prominente → Corrección pública inmediata + postmortem 24h
- Sesgo estadístico significativo → Investigación inmediata, suspender rankings

**Fuentes:** PVB v3.0 §12; overview.md §4.2, §6.2, §7; Segmento 10 del PRD

---

## Segmento 12 — Riesgos y Mitigaciones

### 12.1 Matriz FTCEM (9 riesgos del PVB v3.0 + 3 nuevos)

#### R1-R9: Riesgos del PVB v3.0

| Risk | Probabilidad | Impacto | Mitigación principal |
|---|---|---|---|
| **R1: Veredicto incorrecto político prominente** | Alta | Existencial | Validación post-gen obligatoria. Corrección pública inmediata |
| **R2: Alucinación de fuente legal** | Media-Alta | Existencial | Gate de validación + lista blanca de fuentes. Red line: >10% |
| **R3: Weaponización política** | Alta | Alto | Link perfil completo (positivos+negativos). No vender a campañas |
| **R4: Deepfake / audio manipulado** | Media | Alto | Disclaimer permanente. Detección audio sintético Fase 2 |
| **R5: Costos desbordados por viralización** | Media-Alta | Alto | Rate limiting (5/mes free). Caching + model routing + circuit breaker |
| **R6: Político demanda o ataca públicamente** | Alta | Alto | Partner institucional. Metodología documentada. Asesoría legal preventiva |
| **R7: Corpus legal desactualizado** | Media | Medio-Alto | Pipeline actualización. Flag temporal "verificado a [fecha]". Auditoría mensual |
| **R8: Platform dependency shock** | Media | Alto | Model routing multi-proveedor. Plan B canal: Telegram + web. Alternativas evaluadas |
| **R9: Audio ilegible / transcripción basura** | Alta | Medio | Validación calidad (WER >25% → rechazo). STT nueva generación |

#### R10-R12: Nuevos riesgos del PRD

| Risk | Probabilidad | Impacto | Mitigación |
|---|---|---|---|
| **R10: Cold start knowledge graph** | Medio | Alto | Seed data 200-400 claims + GT-500 + dog-fooding día 1-30 |
| **R11: Rechazo partner institucional** | Alto | Alto | Plan B: universidades + ONGs independientes. Metodología abierta |
| **R12: Sesgo sistemático no detectado** | Media-Alta | Existencial | Auditoría trimestral sesgo + dataset balanceado. Suspender rankings si sesgo >2σ |

### 12.2 Top 5 acciones de mitigación por prioridad

| # | Acción | Riesgos que mitiga | Cuándo |
|---|---|---|---|
| **1** | Validación post-generación gate obligatoria (M2-F10) | R1, R2 | Día 1 — no negociable |
| **2** | Pre-cargar seed data + GT-500 antes lanzamiento público | R10, R1 | Días 1-20 |
| **3** | Asesoría jurídica preventiva + protocolo respuesta demandas | R1, R6, R4 | Días 1-15 |
| **4** | Rate limiting + model routing + circuit breaker costos | R5, R8 | Días 1-30 |
| **5** | Auditoría sesgo con dataset balanceado pre-lanzamiento | R12, R3 | Días 20-30 |

**Fuentes:** PVB v3.0 §10 (FTCEM 9 modos), §13-14; overview.md §6.2, §7, §8.1-8.5; Segmentos 6, 10, 11 del PRD

---

## Segmento 13 — Plan de Entrega 30/60/90 Días

### 13.1 Fase 1: Fundamentos + Validación Técnica (Días 1–30)

**Objetivo:** Demostrar que el pipeline funciona end-to-end con calidad suficiente para continuar. Decision gate al final.

**Hitos Semanas 1-2:**
- Corpus legal v1 vectorizado (Constitución + Código Civil/Penal + leyes orgánicas clave)
- Vector DB desplegada
- Dataset GT-500 primeros 200 claims
- AUDIO-50 recopilado
- Seed data debates 2018/2022 (200-400 claims)
- Pipeline STT funcional (WER <20%)
- Infraestructura base (PostgreSQL + Vector DB + Auth + Storage, logs inmutables)

**Hitos Semanas 2-3:**
- Extracción claims funcional + clasificación (4 tipos taxonomía)
- Capa 1 operativa (Google FactCheck API + knowledge graph interno)
- Capa 2 operativa (RAG legal + razonamiento multi-turn + viabilidad legal)
- Validación post-generación (gate obligatoria)
- Cruce DANE/BanRep verificación estadística
- Datasets GT-500 completo + ADVERSARIAL-50 + EDGE-30 + RAG-100

**Hitos Semanas 3-4:**
- Pipeline end-to-end funcional (audio → STT → extracción → Capa 1/2 → veredicto)
- Bot WhatsApp v0 interno
- Dog-fooding intensivo (equipo 10+ discursos/día)
- Eval completa de validación (todos datasets vs. metas 30d)
- Asesoría jurídica preventiva (disclaimers, protocolo demandas)

**DECISION GATE — Día 30:**
Regla: ≥5 de 7 métricas técnicas cumplen → proceder Fase 2. ≥3 críticas → replantear.

---

### 13.2 Fase 2: Producto Público + Primeros Usuarios (Días 31–60)

**Objetivo:** Lanzar bot WhatsApp al público + dashboard B2B + primera acción de adquisición masiva.

**Hitos Semana 5-6 (B2C):**
- Bot WhatsApp público (audio → veredictos → tarjeta compartible)
- Rate limiting activo (5/mes free)
- Tarjetas visuales optimizadas (WhatsApp/X/Instagram)
- Mensajes de progreso WhatsApp
- Disclaimer autenticidad en todo output
- Recepción de texto directo
- Landing page con QR al bot

**Hitos Semana 5-7 (B2B):**
- Dashboard web v1 (upload, claims, veredictos, fuentes, login)
- Feedback loop correcciones (periodistas alimentan knowledge graph)
- Exportación reportes (markdown/PDF)
- Piloto con 3-5 redacciones

**Hitos Semana 6-8 (Adquisición + Growth):**
- Live fact-checking de primer debate electoral (tarjetas en vivo en X/Instagram)
- Acercamiento influencers políticos
- Presencia universidades y foros con QR
- Normalización semántica claims (embeddings)

**Hito Fase 2 (Día 60):**
Bot público operando + dashboard B2B + ≥500 usuarios WhatsApp + primeras correcciones periodistas + share rate medido + live debate ejecutado

---

### 13.3 Fase 3: Optimización + Revenue + Decisión Estratégica (Días 61–90)

**Objetivo:** Optimizar basado en datos reales, activar revenue B2B, medir métricas a 90 días.

**Hitos Semana 9-10:**
- Corpus legal v2 (jurisprudencia Corte Constitucional + Ley 1819/2016 + CNE)
- Score de veracidad (0-100, ponderación logarítmica)
- Rankings de políticos (leaderboard)
- Historial de análisis usuario
- Pipeline actualización corpus (Gaceta del Congreso)

**Hitos Semana 9-12:**
- Pricing B2B activo (Redacción $49/mes, Institucional $199/mes)
- Piloto B2B conversión a clientes pagos
- Acercamiento partner institucional (ColombiaCheck/MOE)
- Exploración grants (Google News Initiative, Meta Journalism Project, USAID/NED)
- Tier premium B2C (COP $19,900/mes)

**Hitos Semana 11-12:**
- Eval completa 90 días (todos datasets + producto + negocio)
- Auditoría de sesgo (distribución veredictos por afiliación política)
- Informe decisión estratégica (¿modelo B2B funciona? ¿flywheel moat arranca? ¿quality suficiente partner?)

**Hito Fase 3 (Día 90):**
Métricas producto a 90d medidas. Revenue B2B activo (meta: ≥$3K MRR en 6m, primeros seats en día 90). Decisión informada partner institucional. Knowledge graph ≥5K claims. Precisión veredictos ≥85%.

---

### 13.4 Equipo mínimo estimado

| Rol | Dedicación | Responsabilidad |
|---|---|---|
| **Founder/PM** | Full-time | Estrategia, B2B, partners, grants, decisiones |
| **Ingeniero backend** | Full-time | Infraestructura, pipeline, bot WhatsApp, dashboard |
| **Ingeniero AI/ML** | Full-time | Agente, RAG, prompts, model routing, evaluación |
| **Abogado consultor** | Part-time 10-15h/semana | Corpus legal, ground truth, asesoría, auditoría vigencia |
| **Diseñador UX** | Part-time | Tarjetas, dashboard, landing, tono veredictos |

**Fuentes:** PVB v3.0 §15 (roadmap 30/60/90), §5 (seed data), §11 (launch playbook, Plan B); Segmentos 8-12 del PRD; decisiones Paso 0 #1-#10

---

## Apéndice A — Resolución de Conflictos (Paso 0)

### PASO 0 — Análisis de Conflictos entre Documentos

Se identificaron y resolvieron **10 conflictos** fundamentales entre los documentos fuente (pvb.md v3.0, overview.md, mercado.md, icp.md) antes de iniciar la redacción del PRD.

### Conflictos resueltos

#### Conflicto 1 — Canal principal: App móvil vs. WhatsApp
**Decisión:** WhatsApp MVP con arquitectura backend agnóstica para escalar a web/Android/iOS post-MVP.
**Razón:** "Ir donde ya está la audiencia" es más sólido que construir app standalone compitiendo por espacio en teléfono.

#### Conflicto 2 — Fuente de verificación: FactCheck API vs. Corpus legal propio
**Decisión:** Híbrido: Google FactCheck API como capa rápida + corpus legal como capa profunda.
**Razón:** Combina celeridad (FactCheck para claims ya verificados) con diferenciador (cruce legal que nadie más hace).

#### Conflicto 3 — Latencia aceptable: 15s vs. 60s vs. 5min
**Decisión:** Escalonada: <60s preliminar (Capa 1) + 2-5min análisis legal profundo (Capa 2).
**Razón:** Usuario ve progreso inmediato, precisa después.

#### Conflicto 4 — Cliente B2B: Campañas políticas vs. Periodistas/ONGs
**Decisión:** Periodistas y ONGs (no campañas políticas).
**Razón:** Vender a campañas compromete neutralidad agnóstica. Riesgo existencial marca.

#### Conflicto 5 — Rol LLM: Traductor/formateador vs. Razonador legal
**Decisión:** Razonador con guardrails: LLM ejecuta razonamiento legal multi-turn + validación post-generación.
**Razón:** Necesario para cruce legal (no puedes "solo traducir" cuando interpretaspropuestas). Guardrail validación previene alucinación.

#### Conflicto 6 — ICP: 2 vs. 3 segmentos
**Decisión:** 3 segmentos: Ciudadano (B2C) + Periodistas (B2B) + Instituciones (B2B premium).
**Razón:** Instituciones tienen necesidades diferenciadas (batch, reportes, compliance) y mayor willingness-to-pay.

#### Conflicto 7 — Diseño psicológico: Detallado vs. Ausente
**Decisión:** Incorporar todos requisitos psicológicos del overview.md como requisitos de UX.
**Razón:** Evidencia científica (Stanford, Reuters) demuestra que diseño psicológico es crítico para adopción.

#### Conflicto 8 — Cifra de mercado
**Decisión:** Usar cifras verificadas de mercado.md (detectores AI: $2B, CAGR 28.8%).
**Razón:** Cifras trazables con fuentes. Evita proyecciones especulativas.

#### Conflicto 9 — Requisitos legales
**Decisión:** Incorporar TODOS los del overview.md como restricciones de diseño.
**Razón:** Compliance legal define arquitectura (stateless audio), features obligatorias (interfaz apelación), disclaimers.

#### Conflicto 10 — GTM: Influencers vs. Live fact-checking
**Decisión:** Combinar: live fact-checking propio del equipo + amplificación via influencers.
**Razón:** Live generates contenido propio + influencers amplifican distribución.

---

## Registro de Decisiones

| # | Conflicto | Decisión |
|---|---|---|
| 1 | Canal: App vs WhatsApp | WhatsApp MVP, backend agnóstico para web/Android/iOS |
| 2 | Fuente: FactCheck API vs Corpus legal | Híbrido: FactCheck API capa rápida + corpus legal capa profunda |
| 3 | Latencia: 15s vs 60s vs 5min | Escalonada: <60s preliminar + 2-5min profundo |
| 4 | B2B: Campañas vs Periodistas | Periodistas/ONGs (no campañas políticas) |
| 5 | LLM: Traductor vs Razonador | Razonador con guardrails + validación post-generación |
| 6 | ICP: 2 vs 3 segmentos | 3 segmentos (agregar Instituciones) |
| 7 | Diseño psicológico | Incorporar todos los requisitos del overview como UX |
| 8 | Cifra de mercado | Usar cifras documentadas de mercado.md |
| 9 | Requisitos legales | Incorporar todos los del overview |
| 10 | GTM: Influencers vs Live | Combinar ambas estrategias |

---

*Documento generado mediante co-creación iterativa (Prompt 1 de prompts-especificacion.md). Cada segmento fue producido, revisado y aprobado individualmente antes del ensamblaje final.*

*PRD v1.0 — Pajudómetro: Auditor Cívico con IA para el Discurso Político Colombiano*

*Aprobado: 13/13 segmentos + Paso 0 (resolución conflictos)*

*Fecha: 2026-03-07*

