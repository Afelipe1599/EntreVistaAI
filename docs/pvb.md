# Product Vision Board — Pajudómetro

**Versión:** 3.0
**Fecha:** 2026-03-07
**Basado en:** CLAUDE.md, Banco de Productos, Validación, Crítica v1 y v2 (ai-product-base.md)

---

## 1. Visión

> **Democratizar la auditoría cívica del discurso político en Colombia** mediante un agente de IA especializado que cruza automáticamente las afirmaciones de los políticos contra el corpus legal y estadístico colombiano — convirtiendo datos públicos dispersos en veredictos trazables que cualquier ciudadano puede consultar desde su celular.

---

## 2. Problema (que persiste post-GPT-5)

### Definición del dolor

El problema NO es "verificar claims" (output commoditizable). El problema es que **el conocimiento legal y estadístico colombiano está fragmentado, desactualizado y es inaccesible para el ciudadano común** — y los políticos explotan esa asimetría de información.

Un modelo generalista puede fact-checkear contra Google, pero NO puede:

- Cruzar una afirmación contra el artículo exacto de la Constitución Política de 1991 que la contradice o respalda
- Verificar si una promesa de campaña requiere reforma constitucional, ley ordinaria o decreto
- Rastrear si un dato citado por un político contradice la cifra oficial del DANE del trimestre pasado
- Determinar si una propuesta viola la Ley 152 de 1994 (Orgánica del Plan de Desarrollo) o el Estatuto Anticorrupción

### Durability Score: 3.5/5

**¿Por qué sobrevive a GPT-5?** El valor tiene dos capas con durabilidad diferente:

**Capa 1 — Requisito de entrada (durabilidad 2/5):** La base de conocimiento legal colombiano vectorizada (Constitución, Código Civil, Código Penal, leyes orgánicas, jurisprudencia, datos DANE/BanRep). Es un head start de semanas/meses, pero la legislación colombiana es pública y finita — un competidor motivado con un abogado y un ingeniero de RAG puede replicarla.

**Capa 2 — Flywheel acumulativo (durabilidad 5/5):** El verdadero moat que crece con el uso:
1. El **knowledge graph político** — claims acumulados, promesas vs. cumplimiento, contradicciones históricas por político. Cada análisis lo enriquece. A los 6 meses, un competidor tendría que replicar miles de verificaciones.
2. Las **correcciones humanas** de periodistas y fact-checkers — cada corrección es un dato de entrenamiento que mejora la precisión. Los competidores no tienen este feedback loop.
3. El **mapeo entre lenguaje coloquial político y corpus legal** — saber que cuando un político dice "vamos a acabar con los contratos de prestación de servicios" eso implica reformar artículos específicos de leyes específicas. Ese mapeo contextual es el activo más difícil de replicar.

**Nota honesta:** El día 1, solo tenemos la Capa 1. La Capa 2 se construye con tracción. El moat real emerge a partir del mes 3–6 de operación.

---

## 3. Segmento Objetivo (Target Group)

### Segmento A: Ciudadano Informado


| Dimensión           | Detalle                                                                       |
| ------------------- | ----------------------------------------------------------------------------- |
| **Perfil**          | Colombianos 18–45, urbanos, digitalmente activos                              |
| **Comportamiento**  | Consumen noticias políticas en redes sociales y TV                            |
| **Frustración** | No tienen herramientas para verificar lo que escuchan en tiempo real          |
| **Geografía MVP**   | Colombia (Bogotá, Medellín, Cali, Barranquilla)                               |
| **Contexto**        | Ciclo electoral 2026 (legislativas marzo, presidenciales mayo)                |
| **Canal principal** | Bot de WhatsApp + Web app (no app standalone — ir donde ya está la audiencia) |


### Segmento B: Periodistas y Fact-checkers (B2B — centro de revenue)


| Dimensión          | Detalle                                                        |
| ------------------ | -------------------------------------------------------------- |
| **Perfil**         | Redacciones independientes, verificadores de medios            |
| **Organizaciones** | ColombiaCheck, La Silla Vacía, medios regionales               |
| **Frustración**    | Proceso manual de transcripción + verificación toma horas/días |
| **Volumen**        | 10–50 discursos/semana durante campañas electorales            |
| **Necesidad**      | Pipeline automatizado que acelere su flujo de trabajo          |
| **Canal**          | Dashboard web + API                                            |


### Veto holder de confianza

**¿Quién puede matar la adopción aunque el end-user ame el producto?**

- **Para B2C:** Líderes de opinión políticos que acusen al producto de "sesgo" públicamente
- **Para B2B:** Editores de medios y directores de fact-checking que cuestionen la metodología
- **Mitigación:** Alianza con partner institucional que valide la metodología (ver sección 8)

### Usuario diario

**Ciudadano curioso** — no es periodista, pero quiere saber si lo que dice un político es verdad o mentira. Necesita respuestas rápidas, claras y con fuentes. Le envía un audio por WhatsApp y recibe el análisis en el mismo chat.

---

## 4. Necesidades (Needs / Pains)

### Ciudadano Informado


| Pain                          | Evidencia                                                                                   |
| ----------------------------- | ------------------------------------------------------------------------------------------- |
| **Verificación inaccesible**  | Solo 3 organizaciones hacen fact-checking sistemático en Colombia                           |
| **Asimetría temporal**        | Las verificaciones se publican días después del discurso, cuando ya circuló                 |
| **Sobrecarga informativa**    | 59% de colombianos preocupados por falsedades en internet (Reuters Institute)               |
| **Desconfianza generalizada** | Políticos e influencers señalados como mayor peligro para la información veraz              |
| **Desconocimiento legal**     | El ciudadano no sabe qué dice la ley ni puede verificar si una promesa es legalmente viable |


### Periodistas y Fact-checkers


| Pain                              | Evidencia                                                                                  |
| --------------------------------- | ------------------------------------------------------------------------------------------ |
| **Proceso manual lento**          | Transcribir + investigar + redactar una verificación toma 4–8 horas                        |
| **Capacidad limitada**            | Equipos pequeños no pueden cubrir todos los discursos de campaña                           |
| **Sin herramientas LATAM-native** | Full Fact y Factiverse operan en inglés/Europa, sin adaptación a español colombiano        |
| **Fragmentación de fuentes**      | No hay pipeline unificado que conecte transcripción con bases legales y estadísticas       |
| **Consulta legal manual**         | Cruzar un claim contra legislación específica requiere conocimiento jurídico especializado |


### JTBD

> **Cuando** escucho a un político colombiano haciendo afirmaciones en un debate, entrevista o mitin, **quiero** enviar ese audio y obtener un análisis automático que cruce sus claims contra la ley colombiana y datos oficiales, **para** saber no solo si miente, sino qué dice exactamente la ley o los datos sobre lo que afirma.

---

## 5. Producto (Product / Solution)

### One-Liner

**Pajudómetro** es un agente de IA especializado en el marco legal y estadístico colombiano que actúa como auditor cívico: recibe audio de un discurso político, transcribe, extrae afirmaciones, las cruza contra su base de conocimiento legal (Constitución, códigos, leyes, datos DANE) y devuelve un veredicto por claim con la fuente legal o estadística exacta.

### Base de conocimiento propietaria (el core del moat)


| Corpus                            | Contenido                                                                                        | Uso por el agente                                   |
| --------------------------------- | ------------------------------------------------------------------------------------------------ | --------------------------------------------------- |
| **Constitución Política de 1991** | 380 artículos + actos legislativos                                                               | Verificar viabilidad constitucional de propuestas   |
| **Código Civil**                  | Régimen de obligaciones, contratos, familia                                                      | Cruzar claims sobre derechos civiles                |
| **Código Penal**                  | Tipos penales, penas, agravantes                                                                 | Verificar claims sobre justicia y seguridad         |
| **Leyes orgánicas**               | Ley 152/1994 (Plan de Desarrollo), Ley 136/1994 (Municipios), Estatuto Anticorrupción            | Verificar viabilidad legal de promesas de gobierno  |
| **Jurisprudencia clave**          | Sentencias de la Corte Constitucional con mayor impacto                                          | Contexto interpretativo de derechos                 |
| **Datos DANE**                    | Series históricas de pobreza, empleo, inflación, PIB                                             | Verificar claims estadísticos                       |
| **Banco de la República**         | Indicadores macroeconómicos, tasas, reservas                                                     | Verificar claims económicos                         |
| **Knowledge graph político**      | Claims verificados + historial de promesas vs. cumplimiento por político (se acumula con el uso) | Contexto longitudinal, detección de contradicciones |


**Método de integración:** RAG (Retrieval-Augmented Generation) sobre corpus vectorizado + actualizaciones periódicas de datos DANE/BanRep. El fine-tuning se evalúa como segunda fase para mejorar el razonamiento legal.

### Estrategia de seed data (resolver cold start)

El knowledge graph tiene 0 claims el día 1. Sin datos acumulados, la experiencia MVP depende solo del RAG legal estático, que es insuficiente para construir retención. Para arrancar el flywheel antes del lanzamiento:

| Acción | Contenido | Timeline |
|---|---|---|
| **Pre-carga debates pasados** | Analizar debates presidenciales 2018 y 2022 con el agente, generando ~200–400 claims verificados como base del grafo | Días 1–15 |
| **Dataset ground truth** | Crear manualmente 500 claims políticos colombianos con veredicto + fuente legal, validados por abogado. Sirve como eval set Y como seed data | Días 1–20 |
| **Claims de ColombiaCheck** | Si hay alianza, importar verificaciones históricas ya publicadas como nodos del knowledge graph | Días 15–30 (condicional a alianza) |
| **Dog-fooding intensivo** | El equipo analiza 10+ discursos/día durante las primeras 2 semanas para detectar gaps y poblar el grafo | Días 1–14 |

### Capacidades clave del MVP


| #   | Capacidad                       | Descripción                                                                                                                                           |
| --- | ------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1   | **Captura de audio**            | Grabación desde micrófono o envío de audio por WhatsApp                                                                                               |
| 2   | **Agente de análisis agéntico** | Loop multi-turn con LLM que orquesta: transcripción → extracción de claims → consulta RAG contra corpus legal/estadístico → fact-checking → veredicto |
| 3   | **Veredicto legal por claim**   | Cada afirmación clasificada con: verdad / mentira / engañoso / no verificable / **viabilidad legal** (para propuestas) + explicación + **artículo o fuente legal/estadística exacta** |
| 4   | **Score de veracidad (0–100)**  | Gauge visual que resume la credibilidad del discurso completo                                                                                         |
| 5   | **Historial de grabaciones**    | Registro de análisis pasados del usuario                                                                                                              |
| 6   | **Rankings de políticos**       | Leaderboard por veracidad acumulada (distribución viral)                                                                                              |
| 7   | **Procesamiento transparente**  | Pantalla paso a paso con logs en tiempo real                                                                                                          |


### Principios no negociables

1. **Agnóstico** — Misma pipeline para cualquier político, sin filtros ideológicos
2. **Trazabilidad legal** — Cada veredicto cita artículo de ley, sentencia o fuente estadística exacta
3. **Anti-alucinación** — Si no hay fuente verificable en el corpus, se marca como "no verificable" (nunca inventa)
4. **Transparencia** — El usuario ve cada paso del análisis en tiempo real
5. **Privacidad** — Audio procesado en servidor, compliance con Ley 1581 de 2012 (Habeas Data)

### Taxonomía de veredictos

No todas las afirmaciones políticas son verdad/mentira. Los claims sobre propuestas de campaña requieren un veredicto diferente al de claims factuales. Forzar verdad/mentira en propuestas de política pública es deshonesto y erosiona trust.

| Tipo de claim | Veredictos posibles | Ejemplo |
|---|---|---|
| **Factual-numérico** | Verdad / Mentira / Engañoso / No verificable | "La inflación bajó al 3%" → Mentira (DANE reporta 5.2%) |
| **Factual-histórico** | Verdad / Mentira / Engañoso / No verificable | "Yo voté contra esa ley" → Verdad (Gaceta del Congreso lo confirma) |
| **Propuesta de política pública** | Requiere reforma constitucional / Requiere ley ordinaria / Dentro de competencias del ejecutivo / Ambiguo — consulta legal necesaria | "Vamos a acabar con los contratos de prestación de servicios" → Requiere ley ordinaria (modifica Ley 80/1993 de Contratación Pública) |
| **Opinión o predicción** | No verificable (marcado como opinión, no como claim factual) | "Colombia será potencia en 2030" → Opinión, no verificable |

---

## 6. Moat Primario

### Selección: Data Moat (con Trust Moat como refuerzo)

**Data Moat — dos capas con durabilidad diferente:**

| Componente | Tipo | Durabilidad | Descripción |
|---|---|---|---|
| **Corpus legal vectorizado** | Requisito de entrada | 2/5 | Constitución + códigos + leyes + jurisprudencia, estructurados para RAG. Head start de semanas, pero replicable por un competidor motivado. Es necesario pero no suficiente como moat. |
| **Knowledge graph político** | **Flywheel (core del moat)** | **5/5** | Cada análisis alimenta un grafo de claims → fuente → veredicto → correcciones. Más usuarios = más claims = grafo más completo = mejores respuestas. A los 6 meses, un competidor tendría que replicar miles de verificaciones. |
| **Correcciones humanas** | **Flywheel (core del moat)** | **5/5** | Periodistas y fact-checkers del segmento B corrigen veredictos. Cada corrección es un dato de entrenamiento. Los competidores no tienen este feedback loop. |
| **Mapeo lenguaje político ↔ corpus legal** | **Flywheel (core del moat)** | **4/5** | Saber que "acabar con los contratos de prestación" = reformar Ley 80/1993. Se aprende con uso y correcciones. Difícil de replicar sin operación real. |
| **Datos estadísticos actualizados** | Mantenimiento | 3/5 | Series DANE y BanRep actualizadas periódicamente. Ventaja operativa, no moat per se. |


**Trust Moat — como refuerzo:**


| Elemento                       | Estrategia                                                                              |
| ------------------------------ | --------------------------------------------------------------------------------------- |
| **Partner institucional**      | Alianza con ColombiaCheck o MOE como auditor de metodología (Prestige Moat à la Harvey) |
| **Auditoría pública**          | Metodología documentada y publicada para escrutinio                                     |
| **Correcciones transparentes** | Si un veredicto es corregido, se publica la corrección con explicación                  |


### Test de 6 semanas: ¿Puede un competidor replicar esto con las mismas APIs?

**El pipeline (transcribir → extraer → verificar):** Sí, replicable en semanas.
**El corpus legal estructurado para RAG:** No. Requiere trabajo jurídico especializado para estructurar, indexar y optimizar chunks de legislación colombiana para consulta por agentes. Estimado: 3–6 meses.
**El knowledge graph político con correcciones:** No. Se construye con uso. Cada semana de operación amplía la ventaja.

---

## 7. Arena Competitiva y Posicionamiento

### Arena: Disruptor (AI-Disrupted)

Pajudómetro NO crea un mercado nuevo (el fact-checking existe). Usa AI para reimaginar un workflow existente haciéndolo 10x más rápido y accesible. La estrategia es de **Disruptor**, no de Pioneer.

**El 10x:** 4-8 horas → <5 minutos + acceso universal (no solo periodistas) + cruce legal automático que ni los fact-checkers hacen manualmente de forma sistemática.

### UX Paradigm: Agent (actor autónomo dentro de límites)

El agente ejecuta tareas autónomamente (transcribir, buscar, verificar, emitir veredicto) pero dentro de límites estrictos:

- Solo consulta su corpus verificado (nunca inventa fuentes)
- Si no encuentra evidencia, dice "no verificable" (nunca adivina)
- El usuario NO está en el loop durante el análisis, pero puede ver cada paso en tiempo real

### Sobrevivir a los gigantes


| Gigante                      | Su limitación                                                                           | Nuestra estrategia                                     |
| ---------------------------- | --------------------------------------------------------------------------------------- | ------------------------------------------------------ |
| **ChatGPT/Gemini con audio** | Generalista, sin corpus legal colombiano, sin knowledge graph político                  | Especialización profunda en contexto colombiano        |
| **Google AI Overviews**      | Fairy dust sobre search existente, no hace verificación estructurada contra legislación | Pipeline especializado claim-by-claim con fuente legal |
| **Meta (WhatsApp)**          | Incentivo conflictivo (la desinformación genera engagement)                             | Complementamos su plataforma, no competimos            |

**Ventaja contraintuitiva:** La insignificancia del mercado colombiano para Google/OpenAI ES una ventaja estratégica. Ningún gigante va a invertir en vectorizar la legislación colombiana ni en construir un knowledge graph de políticos colombianos para un mercado de ~20M de usuarios digitales. Este nicho geo-legal es demasiado pequeño para ellos y suficientemente grande para nosotros.


### Posicionamiento vs. competidores


| Competidor          | Limitación clave                                                  | Diferenciador Pajudómetro                                                  |
| ------------------- | ----------------------------------------------------------------- | -------------------------------------------------------------------------- |
| **Full Fact AI**    | Enfocado en redacciones, no B2C; inglés primero                   | Directo al ciudadano, español colombiano, cruce legal                      |
| **Factiverse Live** | Plataforma para periodistas, no consumidor final                  | Bot WhatsApp accesible para cualquier persona                              |
| **ColombiaCheck**   | Manual, asincrónico (días de delay)                               | Automático + cruce contra corpus legal que ellos no hacen sistemáticamente |
| **ChatGPT + audio** | Sin corpus legal colombiano, sin historial de claims por político | Agente especializado con RAG legal + knowledge graph                       |
| **ClaimBuster**     | Detección de claims sin verificación; inglés solamente            | Pipeline completo con verificación legal                                   |


---

## 8. AI Decision Triangle

### Optimización primaria: Capability (precisión del veredicto)


| Dimensión        | Decisión     | Justificación                                                                                     |
| ---------------- | ------------ | ------------------------------------------------------------------------------------------------- |
| **Capability** ⭐ | Prioridad #1 | Un veredicto incorrecto destruye trust. En contexto político, la precisión no es negociable.      |
| **Speed**        | Prioridad #2 | <5 minutos es aceptable (no necesita ser <60 segundos si eso compromete calidad).                 |
| **Cost**         | Prioridad #3 | Aceptamos costos más altos por análisis si la calidad es superior. Optimizamos con model routing. |


### Trade-offs aceptados

- Usamos modelos más costosos (Claude Sonnet/Opus) para el razonamiento legal, modelos baratos para transcripción y clasificación
- Preferimos "no verificable" antes que un veredicto rápido pero dudoso
- Aceptamos latencia de 2–5 minutos si el RAG legal necesita múltiples consultas

---

## 9. Modelo Económico

### Estrategia: B2B-first con B2C como canal de distribución

El B2C (ciudadano) genera volumen, datos y distribución. El B2B (medios/ONGs) genera revenue.

### Pricing


| Tier                  | Precio                    | Incluye                                                            | Público                       |
| --------------------- | ------------------------- | ------------------------------------------------------------------ | ----------------------------- |
| **Gratis (WhatsApp)** | $0                        | 5 análisis/mes, veredictos básicos                                 | Ciudadano                     |
| **Premium**           | COP $19,900/mes (~$5 USD) | Análisis ilimitados, historial completo, exportación               | Ciudadano power user          |
| **Redacción**         | $49 USD/mes por seat      | API, dashboard, análisis en batch, reportes exportables, prioridad | Periodistas/medios            |
| **Institucional**     | $199 USD/mes              | Todo Redacción + white-label, volumen, soporte dedicado            | ONGs, observatorios, partidos |


### Unit economics estimados (escenario conservador y optimista)

| Componente del costo por análisis | Optimista | Conservador |
|---|---|---|
| STT (5 min audio) | $0.03 | $0.06 |
| Embedding + query de búsqueda | $0.01 | $0.02 |
| RAG retrieval (3–5 consultas contra vector DB) | $0.02 | $0.05 |
| LLM reasoning (extracción + 3–5 verificaciones, ~8K tokens c/u) | $0.15 | $0.40 |
| Validación post-generación (verificar citas legales contra corpus) | $0.02 | $0.05 |
| **Total por análisis** | **$0.23** | **$0.58** |

| Métrica | Optimista | Conservador |
|---|---|---|
| Costo usuario free/mes (5 análisis) | $1.15 | $2.90 |
| Revenue usuario free/mes | $0 | $0 |
| Revenue usuario premium/mes | ~$5 | ~$5 |
| Revenue seat Redacción/mes | $49 | $49 |
| **Break-even B2C (premium por cada 1,000 free):** | 60 (~6% conversión) | 150 (~15% conversión — improbable) |
| **Break-even real (seats B2B por cada 1,000 free):** | 24 seats | 60 seats |

### El pricing escala a 10x usuarios?

**Con B2C solo:** No. Los márgenes son negativos a escala en ambos escenarios.
**Con B2B subsidiando B2C (escenario optimista):** Sí. 50 seats institucionales a $199/mes = $10K/mes, suficiente para subsidiar ~8,000 usuarios free.
**Con B2B subsidiando B2C (escenario conservador):** Requiere ~100 seats B2B o financiamiento externo para cubrir la base free. Necesitamos optimizar agresivamente costos de LLM (model routing, caching de verificaciones repetidas).

### Gross margin proyectado (mix B2B+B2C)

**Meta a 12 meses:** 35–50% (inferior a SaaS tradicional, aceptable para AI product en fase temprana)

### Financiamiento de la fase pre-revenue

Un producto cívico anti-desinformación en contexto electoral puede acceder a fuentes de financiamiento no-dilutivas:

| Fuente | Relevancia | Monto estimado |
|---|---|---|
| **Google News Initiative** | Grants para herramientas de fact-checking | $10K–$50K |
| **Meta Journalism Project** | Fondos para combatir desinformación | $10K–$30K |
| **USAID / NED** | Programas de fortalecimiento democrático en LATAM | $20K–$100K |
| **Fondo Colombia en Paz** | Apoyo a proyectos de transparencia | TBD |

Estos grants no solo cubren runway — aportan legitimidad y distribución (ser "apoyado por Google News Initiative" es un trust signal).

---

## 10. FTCEM — Failure Modes


| Failure Mode                                       | Trigger                                                        | Consequence                                                           | Early Warning                                                                 | Mitigation                                                                                             |
| -------------------------------------------------- | -------------------------------------------------------------- | --------------------------------------------------------------------- | ----------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **Veredicto incorrecto sobre político prominente** | Claim ambiguo + fuente desactualizada en corpus                | Controversia mediática, acusaciones de sesgo, pérdida masiva de trust | Spike en reportes de "veredicto incorrecto" por usuarios                      | Corrección pública inmediata + escalación a partner institucional + revisión del corpus                |
| **Alucinación de fuente legal**                    | LLM genera artículo de ley inexistente                         | Desacreditación del producto, potencial daño legal                    | Alertas automáticas cuando el agente cita artículos no presentes en el corpus | Validación post-generación: cada cita legal se verifica contra el corpus antes de mostrar al usuario   |
| **Audio ilegible / transcripción basura**          | Mitin ruidoso, audio de TV con música de fondo, mala grabación | Usuario recibe análisis de un texto que no refleja lo que se dijo     | WER > 25% en transcripción                                                    | Auto-reject con mensaje: "Audio de calidad insuficiente. Intenta grabar más cerca del orador."         |
| **Costos desbordados**                             | Viralización sin control de tier gratis                        | Factura de inferencia de 5-6 cifras mensuales                         | Monitoreo diario de costo/análisis + alertas a 80% del presupuesto            | Rate limiting dinámico + cola de procesamiento en picos + reducción de contexto en tier free           |
| **Político demanda o ataca públicamente**          | Veredicto desfavorable a figura con poder mediático            | Presión legal/mediática, efecto intimidatorio                         | Menciones en medios/redes señalando al producto                               | Partner institucional respalda metodología + documentación legal previa + asesoría jurídica preventiva |
| **Weaponización política** | Un partido usa Pajudómetro selectivamente para atacar opositores, compartiendo solo veredictos negativos y omitiendo positivos | El producto se percibe como herramienta de campaña negativa, no como auditoría neutral. Trust destruido | Patrón de uso asimétrico (un bando político comparte 10x más que otro) | Las tarjetas compartibles siempre incluyen link al perfil completo del político (positivos y negativos). Rankings muestran score total, no claims aislados |
| **Deepfake / audio manipulado** | Alguien envía audio editado o deepfake de un político diciendo algo que nunca dijo, obtiene veredicto de Pajudómetro, y lo comparte como "prueba" | Pajudómetro se convierte en amplificador involuntario de desinformación — lo opuesto de su misión | Detección de audio sintético, patrones de envío sospechoso (mismo audio desde múltiples cuentas) | Disclaimer permanente: "Este análisis se basa en el audio proporcionado. Pajudómetro no verifica autenticidad del audio." + Fase 2: integración de detección de deepfake audio |
| **Corpus legal desactualizado** | Se aprueba reforma constitucional o ley nueva que cambia el marco legal, y el corpus no se actualiza a tiempo | Veredictos basados en legislación derogada o modificada. Desacreditación técnica | Monitoreo de la Gaceta del Congreso y diarios oficiales | Pipeline automatizado de actualización cuando se publican nuevas leyes + flag temporal: "Verificado contra legislación vigente a [fecha]" |
| **Platform dependency shock** | Anthropic/OpenAI suben precios de API 2–3x, o WhatsApp Business cambia términos/pricing para bots de alto volumen | Unit economics implosionan, canal principal se encarece o cierra | Monitoreo mensual de pricing de proveedores + alertas si costo/análisis sube >20% | Model routing multi-proveedor (Claude + GPT + modelos open-source como Llama), evaluación trimestral de alternativas open-source para LLM y STT. Plan B de canal: Telegram + web si WhatsApp se encarece |


---

## 11. Distribución

### Estrategia: Embedded, no standalone


| Canal                | Justificación                                                       | Prioridad          |
| -------------------- | ------------------------------------------------------------------- | ------------------ |
| **Bot de WhatsApp**  | 96% de smartphones en Colombia tienen WhatsApp. Zero fricción.      | MVP — Prioridad #1 |
| **Web app**          | Dashboard para periodistas + landing para SEO                       | MVP — Prioridad #2 |
| **Rankings virales** | Leaderboard de políticos = output-as-distribution (à la ElevenLabs) | MVP — Prioridad #3 |
| **App móvil**        | Solo si validamos retención en WhatsApp + Web                       | Post-MVP           |


### Output-as-distribution

Cada veredicto genera una **tarjeta visual compartible** ("Fulano dijo X → FALSO según Art. 123 de la Constitución") diseñada para WhatsApp/X/Instagram. Cada share es un nuevo usuario potencial.

### Prestige partner

Buscar alianza con **ColombiaCheck** o la **MOE (Misión de Observación Electoral)** como validador de la metodología. En un mercado donde la credibilidad es todo, un respaldo institucional es más valioso que cualquier feature técnico.

**Riesgo:** Estas organizaciones podrían ver a Pajudómetro como competidor que trivializa su oficio, o como riesgo reputacional si el agente falla con su nombre asociado.

**Plan B si ColombiaCheck/MOE dicen no:**

| Alternativa | Viabilidad | Trade-off |
|---|---|---|
| **Universidades con facultad de derecho** (U. de los Andes, Externado, U. Nacional) | Alta — interés académico en AI + derecho | Menos reconocimiento público que ColombiaCheck, pero alta credibilidad técnica |
| **Observatorios de democracia independientes** (Transparencia por Colombia, FLIP) | Media — alineamiento de misión | Menor alcance mediático |
| **Construir credibilidad propia sin partner** — publicar metodología abierta + invitar auditorías independientes | Siempre disponible | Más lento, pero más autónomo. Requiere track record de 6+ meses sin errores graves |

### Launch playbook: primeros 1,000 usuarios

Las tarjetas compartibles y el prestige partner funcionan DESPUÉS de tener usuarios. La adquisición inicial requiere una estrategia específica:

| Táctica | Descripción | Timeline |
|---|---|---|
| **Live-fact-checking de debate electoral** | El equipo hace fact-checking en vivo de un debate presidencial/legislativo y publica tarjetas en X/Instagram en tiempo real. Cada tarjeta tiene link al bot de WhatsApp. Potencial: miles de usuarios en una noche. | Primer debate disponible |
| **Influencers políticos colombianos** | Acercamiento a creators como Daniel Samper Ospina, podcasters políticos, youtubers de análisis. Ellos usan el producto en su contenido. | Días 15–30 |
| **Medios como canal** | Si hay alianza B2B, cada artículo de ColombiaCheck/La Silla Vacía "powered by Pajudómetro" es un funnel. | Días 31–60 |
| **Universidades y foros cívicos** | Presencia en debates universitarios con QR code al bot. Audiencia joven y políticamente activa. | Días 15–45 |

---

## 12. Métricas de Éxito

### User Metrics


| KPI                                                            | Meta MVP (90 días) |
| -------------------------------------------------------------- | ------------------ |
| Tasa de completación del flujo (enviar audio → ver resultados) | ≥70%               |
| Usuarios que analizan 2+ discursos en 7 días                   | ≥30%               |
| Grabaciones por usuario activo/semana                          | ≥3                 |
| Share rate (veredictos compartidos/total generados)            | ≥15%               |


### AI-Specific Metrics — Validación técnica (primeros 30 días)

Estas metas determinan si es técnicamente viable continuar. Si no se alcanzan, requieren replanteo de stack o approach antes de fijar metas de producto.

| KPI | Meta de validación (30 días) | Método |
|---|---|---|
| Precisión de transcripción (WER) en español colombiano con audio real | <20% | Test con 50 audios reales de mítines/debates |
| Tasa de alucinación en veredictos (cita fuente legal inexistente) | <5% | Eval set de 200 claims con ground truth |
| RAG retrieval relevance (el artículo citado es relevante al claim) | ≥70% | Evaluación manual de 100 consultas RAG |
| Costo promedio por análisis | <$0.60 | Medición sobre 500 análisis reales |

### AI-Specific Metrics — Producto (90 días, condicional a validación exitosa)

| KPI | Meta MVP (90 días) |
|---|---|
| Precisión de transcripción (WER) en español colombiano | <15% |
| Claims con fuente legal/estadística verificable | ≥85% |
| Tasa de alucinación en veredictos (cita fuente inexistente) | <1% |
| Tiempo de análisis end-to-end | <5 minutos |
| Costo promedio por análisis | <$0.40 |


### Business Metrics


| KPI                             | Meta 6 meses |
| ------------------------------- | ------------ |
| Conversión free → premium (B2C) | ≥5%          |
| Seats B2B activos               | ≥30          |
| Revenue mensual                 | ≥$3,000 USD  |
| Gross margin (mix B2B+B2C)      | ≥40%         |


---

## 13. Riesgos Críticos (Las 5 Preguntas Incómodas)

### P1: ¿Qué si el problema desaparece en 12 meses por commoditización?

**Respuesta:** El pipeline de análisis sí es commoditizable. El corpus legal colombiano estructurado y el knowledge graph político NO lo son. Cada mes de operación amplía la ventaja en data. Si GPT-5 hace fact-checking genérico mejor, Pajudómetro sigue siendo el único con cruce legal colombiano especializado.

### P2: ¿Quién es dueño de la data?

**Respuesta:** El corpus legal es público pero nuestra estructuración es propietaria. El knowledge graph político es generado por uso (propio). Las correcciones humanas son propias. No dependemos de una fuente única que pueda revocar acceso. Riesgo bajo.

### P3: ¿Qué pasa si el producto falla públicamente?

**Respuesta:** Un veredicto incorrecto sobre un político prominente sería amplificado por medios y redes. Mitigación: (1) partner institucional respalda, (2) corrección pública inmediata documentada, (3) validación automática de cada cita legal antes de mostrar, (4) asesoría jurídica preventiva.

### P4: ¿Puede un competidor replicar en 6 semanas?

**Respuesta:** El pipeline (STT + LLM + verificación): sí. El corpus legal estructurado para RAG: no (3–6 meses de trabajo jurídico). El knowledge graph con historial de claims y correcciones: no (se construye con uso acumulado).

### P5: Si tenemos éxito a escala, ¿cómo se rompe trust primero?

**Respuesta:** Un político con poder mediático acusa a Pajudómetro de "sesgo ideológico" después de un veredicto desfavorable. Sin respaldo institucional, no tenemos credibilidad para defendernos. Por eso el prestige partner (ColombiaCheck/MOE) es prerrequisito, no nice-to-have.

---

## 14. Discovery Debt Log


| Hipótesis                                                          | Evidence Strength              | Método de Validación                    | Riesgo si estamos equivocados    | Owner              | Recheck  |
| ------------------------------------------------------------------ | ------------------------------ | --------------------------------------- | -------------------------------- | ------------------ | -------- |
| Los colombianos usarán WhatsApp para verificar discursos           | Weak (asunción)                | Piloto con 100 usuarios en campaña      | Existencial (canal equivocado)   | Producto           | Semana 4 |
| Periodistas pagarán $49/mes por el pipeline                        | Weak (benchmarks de mercado)   | Entrevistas con 10 redacciones          | Alto (modelo de revenue)         | Business           | Semana 6 |
| WER <15% es alcanzable en español colombiano con audio real        | Medium (benchmarks de Whisper) | Test con 50 audios reales de mítines    | Alto (calidad core del producto) | Ingeniería         | Semana 2 |
| El corpus legal se puede estructurar para RAG efectivo en <30 días | Weak (estimación)              | Sprint de estructuración con abogado    | Alto (timeline del MVP)          | Ingeniería + Legal | Semana 3 |
| <1% alucinación en veredictos es alcanzable                        | Weak (sin benchmark)           | Eval set de 200 claims con ground truth | Existencial (trust)              | AI/ML              | Semana 4 |
| Tarjetas de veredicto se comparten orgánicamente                   | Weak (asunción)                | Tracking de share rate en piloto        | Medio (distribución)             | Growth             | Semana 8 |
| ColombiaCheck/MOE querrán asociarse con herramienta AI automatizada | Weak (asunción)               | Reunión exploratoria con directivos     | Existencial (trust sin respaldo) | Founder            | Semana 4 |
| El mercado colombiano es demasiado pequeño para que Google/OpenAI inviertan en legislación local | Medium (inferencia lógica) | Monitoreo de lanzamientos de gigantes en LATAM | Alto (competencia de gigante) | Producto | Trimestral |


---

## 15. Roadmap de Alto Nivel (30/60/90 días)


| Fase           | Entregable principal                                                                                                                         | Hito                                                                                    |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- |
| **Días 1–30**  | Corpus legal vectorizado + agente RAG funcional + bot WhatsApp con flujo core (audio → veredicto con fuente legal)                           | Agente end-to-end verificando claims contra Constitución y DANE                         |
| **Días 31–60** | Rankings de políticos + tarjetas compartibles + dashboard web periodistas + pruebas con 50+ usuarios reales                                  | Feedback cualitativo + primeras correcciones al corpus + share rate medido              |
| **Días 61–90** | Optimización de precisión + segundo corpus (Código Penal, leyes orgánicas) + piloto B2B con 3 redacciones + acercamiento a ColombiaCheck/MOE | Decisión informada sobre modelo de negocio, métricas de calidad y partner institucional |


---

## 16. Contexto Estratégico

### ¿Por qué ahora?


| Tendencia                              | Implicación                                                                                          |
| -------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| **Elecciones Colombia 2026**           | Legislativas (marzo) y presidenciales (mayo) — pico de demanda de verificación                       |
| **Alianza ColombiaCheck-CRC-MOE**      | Reconocimiento oficial de la necesidad de herramientas tech contra desinformación                    |
| **Modelos de transcripción mejorados** | Nuevos modelos STT (2025) reducen WER significativamente en español                                  |
| **RAG maduro**                         | Las técnicas de retrieval-augmented generation permiten consulta precisa sobre corpus especializados |
| **Mercado anti-desinformación**        | Proyectado a $4.9B para 2030, CAGR 42%                                                               |
| **59% colombianos preocupados**        | Demanda ciudadana documentada por herramientas contra falsedades (Reuters Institute)                 |


### Decisiones estratégicas fundamentales


| Decisión       | Resolución                                         | Justificación                                |
| -------------- | -------------------------------------------------- | -------------------------------------------- |
| Canal MVP      | Bot WhatsApp + Web (no app nativa)                 | Ir donde ya está la audiencia, zero fricción |
| Revenue center | B2B (periodistas/ONGs), B2C como distribución      | Unit economics no cierran con B2C solo       |
| Moat primario  | Data Moat (corpus legal + knowledge graph)         | Único activo no replicable en 6 semanas      |
| Optimización   | Capability > Speed > Cost                          | Un veredicto incorrecto mata el producto     |
| Backend        | PostgreSQL + vector DB + Auth + Storage en la nube | RAG requiere base vectorial                  |
| Idioma         | Español colombiano (regionalismos, contexto local) | Especialización como barrera                 |


---

*Hardcore AI by 30X · Marzo 2026*