# Crítica v2 del Product Vision Board — Pajudómetro
## Segunda ronda de análisis desde "De la Idea al Product Vision Board para Productos Agénticos"

**Fecha:** 2026-03-07
**Documento evaluado:** `docs/pvb.md` (v2.0, 2026-03-07)
**Marco de referencia:** `ai-product-base.md` (Hardcore AI — Estación 2)

---

## Veredicto General

El PVB v2.0 es un salto cualitativo respecto al v1.0. La incorporación del corpus legal como core del moat, el cambio a WhatsApp como canal, el B2B como centro de revenue y la inclusión de FTCEM/Discovery Debt resuelven las brechas estructurales más graves de la primera versión. Sin embargo, al pasar el documento con lupa por segunda vez, emergen **tensiones internas, asunciones frágiles y puntos ciegos** que podrían comprometer la ejecución si no se confrontan antes del PRD.

**Score general de madurez estratégica: 7/10** (v1.0 era ~4/10)

---

## 1. Test de Durabilidad Revisado: De 2/5 a 4/5 — Pero con un asterisco importante

El PVB afirma Durability Score de 4/5 basándose en que el corpus legal estructurado para RAG toma "3–6 meses de trabajo jurídico" para replicar. Esto es una mejora enorme, pero el argumento tiene una grieta:

**La grieta: La legislación colombiana es pública y finita.**

La Constitución tiene 380 artículos. El Código Civil, el Código Penal y las leyes orgánicas principales son documentos cerrados. No es un corpus que crece orgánicamente como los datos de Spotify o Duolingo. Un competidor motivado con un abogado y un ingeniero de RAG puede vectorizar ese mismo corpus en semanas, no meses. El trabajo "jurídico especializado" que el PVB describe es real pero es un **head start, no un moat permanente**.

**Lo que SÍ es durable (y el PVB debería enfatizar más):**
- El **knowledge graph político** — claims acumulados, promesas vs. cumplimiento, contradicciones históricas. Esto crece con cada uso y ES un flywheel real.
- Las **correcciones humanas** de periodistas — cada corrección es un dato de entrenamiento que mejora el sistema.
- La **interpretación contextual** — saber que cuando un político dice "vamos a acabar con los contratos de prestación de servicios" eso implica reformar el artículo X de la ley Y. Ese mapeo entre lenguaje coloquial político y corpus legal es el verdadero activo difícil de replicar.

**Recomendación:** Bajar el peso del corpus legal estático como moat (es un requisito de entrada, no una ventaja sostenida) y subir el peso del knowledge graph + correcciones como el flywheel verdadero. Reformular la narrativa: el moat no es "tenemos la Constitución vectorizada" (cualquiera puede), sino "tenemos 50,000 claims políticos colombianos cruzados contra ley, corregidos por periodistas, con historial longitudinal por político".

**Durability Score ajustado: 3.5/5** — El corpus estático es 2/5; el knowledge graph + correcciones es 5/5. El promedio depende de cuánto peso tenga cada uno en la ejecución real.

---

## 2. Las 3 Trampas Mortales — Estado en v2.0

### Trampa 1: Red Ocean Trap — ⚠️ Mejorado pero no resuelto

El PVB v2.0 ya no compite solo en "verificar claims" sino en "cruzar contra legislación colombiana". Esto estrecha el océano. Sin embargo, el documento base advierte que los gigantes no necesitan replicar tu producto exacto — les basta con hacer "good enough" para el 80% de los usuarios.

**Escenario no contemplado:** Google lanza una función de "verificar contra legislación local" en AI Overviews para mercados electorales. No necesita ser mejor que Pajudómetro — solo necesita existir gratis dentro de un producto que ya tiene 4 mil millones de usuarios. El PVB no tiene respuesta a este escenario.

**Contraargumento (a favor de Pajudómetro):** Colombia es un mercado demasiado pequeño para que Google invierta en legislación local. Esto es probablemente cierto, pero el PVB debería articularlo explícitamente como parte de la estrategia de "sobrevivir a los gigantes": la insignificancia del mercado colombiano ante Google/OpenAI ES una ventaja estratégica, no una debilidad.

### Trampa 2: Cool Demo Trap — 🟡 Significativamente mejorado

El cambio de <60 segundos a <5 minutos priorizando precisión es correcto. El FTCEM cubre los failure modes principales. Sin embargo, falta abordar un escenario concreto:

**El "último 20%" del cruce legal:** ¿Qué pasa cuando un claim político NO tiene una respuesta limpia en la legislación? La mayoría de las afirmaciones políticas son matizadas, no binarias. "Vamos a reducir impuestos a la clase media" no se verifica con un solo artículo — involucra interpretación de múltiples leyes, contexto presupuestal, y competencias constitucionales. El PVB asume que el RAG puede encontrar "el artículo exacto", pero la realidad legal es que muchos claims requieren **razonamiento jurídico interpretativo**, no solo retrieval.

**Riesgo real:** El agente va a ser excelente con claims factual-numéricos ("la inflación bajó al 3%") pero potencialmente mediocre con claims sobre propuestas de política pública. Si ≥40% de los claims políticos caen en la segunda categoría, el producto tiene un gap de calidad que el JTBD no anticipa.

**Recomendación:** Agregar una categoría de veredicto para claims de política pública: "Requiere reforma constitucional / Requiere ley ordinaria / Dentro de competencias del ejecutivo / Ambiguo — consulta legal necesaria". Esto es más honesto que forzar un verdad/mentira/engañoso en propuestas de campaña.

### Trampa 3: Platform Trap — 🟡 Mitigado, no eliminado

El corpus legal como data moat reduce la dependencia pura de APIs de terceros. Sin embargo, el PVB todavía depende de:
- **STT de terceros** (sin alternativa propia)
- **LLM de terceros** para el razonamiento (el más costoso y riesgoso)
- **WhatsApp Business API** para el canal principal de distribución

El documento base cita el caso de startups que vieron "sus unit economics implosionar en un solo quarter" cuando OpenAI ajustó pricing. El PVB no tiene contingencia si:
- Anthropic/OpenAI suben precios de API 2–3x (ha ocurrido)
- WhatsApp Business cambia términos de servicio o pricing para bots de alto volumen
- Whisper/Deepgram deprecan modelos de español

**Recomendación:** Agregar al FTCEM un failure mode de "platform dependency shock" con mitigación concreta (ej: model routing multi-proveedor, evaluación de modelos open-source como alternativa, plan B de canal si WhatsApp se encarece).

---

## 3. Moat Analysis Revisado

### Data Moat — 🟡 Mejor articulado, pero el flywheel tiene un problema de arranque en frío

El PVB describe un flywheel: más usuarios → más claims verificados → knowledge graph más completo → mejores respuestas → más usuarios. Esto es correcto en teoría, pero tiene un **cold start problem** que no se aborda:

**Día 1:** El knowledge graph tiene 0 claims. El corpus legal tiene la Constitución vectorizada. Un usuario envía audio, el agente hace RAG contra la Constitución y emite un veredicto. ¿Qué tan bueno es ese veredicto sin knowledge graph, sin correcciones acumuladas, sin historial del político?

Si la respuesta es "mediocre", entonces los primeros 1,000 usuarios tienen una experiencia inferior que puede matar la retención antes de que el flywheel arranque. El documento base advierte sobre esto cuando dice que "una vez que los usuarios experimentan AI que funciona bien en un contexto, lo esperan en todas partes".

**Recomendación:** Definir una estrategia de "seed data" para el knowledge graph:
- Pre-cargar con los claims verificados existentes de ColombiaCheck (si hay alianza)
- Crear manualmente un dataset de ~500 claims políticos colombianos con veredicto + fuente legal como ground truth para MVP
- Hacer "dog-fooding" intensivo con debates pasados (2022, 2018) para poblar el grafo antes de lanzar

### Trust Moat — 🟢 Bien planteado, pero la dependencia del prestige partner es una fragilidad

El PVB dice que ColombiaCheck/MOE como partner es "prerrequisito, no nice-to-have". Pero el Discovery Debt Log no incluye esta hipótesis:

**Hipótesis no trackeada: ColombiaCheck/MOE querrán asociarse con una herramienta AI automatizada.**

Estas organizaciones podrían ver a Pajudómetro como:
- Un aliado que les ahorra trabajo (best case)
- Un competidor que trivializa su oficio (worst case)
- Un riesgo reputacional si el agente falla y su nombre está asociado (medium case)

Si la respuesta de ColombiaCheck es "no, gracias", el PVB no tiene Plan B para legitimidad institucional. Esto es un riesgo existencial dado que la respuesta a P5 (cómo se rompe trust) depende enteramente de tener ese partner.

**Recomendación:** Agregar al Discovery Debt Log con Evidence Strength: Weak y Riesgo: Existencial. Definir al menos 2 alternativas: (a) universidades con facultad de derecho (ej: U. de los Andes, Externado), (b) observatorios de democracia independientes, (c) construir credibilidad propia sin partner (más lento pero más autónomo).

---

## 4. Economía — Stress-test de los números

### El modelo B2B subsidiando B2C es correcto, pero los números merecen escrutinio

El PVB dice: "20 seats de Redacción cubren ~1,000 usuarios free". Verifiquemos:

- 20 seats × $49/mes = $980/mes de revenue
- 1,000 usuarios free × 5 análisis/mes × $0.15–$0.30 = **$750–$1,500/mes de costo**
- Con el límite superior de costo ($0.30), 20 seats no cubren ni a 1,000 usuarios free

**El break-even es más apretado de lo que el PVB sugiere.** Y esto no incluye:
- Costos de infraestructura (vector DB, WhatsApp Business API fees, hosting)
- Costos de mantenimiento del corpus (actualización DANE, nuevas leyes)
- Costos de equipo (al menos 1 ingeniero + 1 abogado part-time para el corpus)

**Escenario más realista a 6 meses:**
- 5,000 usuarios free × 5 análisis/mes = 25,000 análisis × $0.20 promedio = **$5,000/mes en inferencia pura**
- 250 usuarios premium × $5 = $1,250/mes
- 30 seats B2B × $49–$199 = $1,470–$5,970/mes
- **Revenue total: $2,720–$7,220/mes vs. costos de al menos $7,000–$10,000/mes** (incluyendo infra + equipo mínimo)

Los márgenes siguen siendo negativos en el escenario más probable a 6 meses. El producto necesita o (a) más seats institucionales a $199, o (b) financiamiento externo que cubra la fase de construcción del flywheel, o (c) limitar más agresivamente el tier gratis.

**Recomendación:** Ser explícito en el PVB sobre la necesidad de financiamiento o grants para la fase pre-revenue. Un producto cívico anti-desinformación en contexto electoral puede acceder a grants de Google News Initiative, Meta Journalism Project, o fundaciones de democracia (USAID, NED). Esto no es solo un recurso económico — es distribución y legitimidad.

### El costo por análisis de $0.15–$0.30 puede estar subestimado

Para un flujo RAG multi-turn con razonamiento legal:
- STT (5 min audio): $0.03–$0.06
- Embedding del audio transcrito + query de búsqueda: $0.01
- RAG retrieval (3–5 consultas contra vector DB): $0.02–$0.05
- LLM reasoning (extracción de claims + 3–5 verificaciones independientes, cada una con contexto de ~8K tokens): si usamos Claude Sonnet, esto puede ser **$0.15–$0.40 solo en LLM**
- Validación post-generación (verificar que cada cita legal existe): $0.02–$0.05

**Total más realista: $0.25–$0.55 por análisis.** El PVB dice que prioriza Capability sobre Cost, pero los unit economics están calculados como si priorizara Cost.

**Recomendación:** Recalcular con el bound superior. Si el costo real es $0.40–$0.55, el tier gratis de 5 análisis/mes cuesta $2–$2.75/usuario/mes, y el break-even B2B necesita ~40 seats de Redacción por cada 1,000 free users, no 20.

---

## 5. Tensión interna: Capability vs. Discovery Debt

El PVB tiene una tensión no resuelta entre lo que promete y lo que puede validar:

**Lo que promete (sección 12):**
- Claims con fuente legal verificable: ≥85%
- Tasa de alucinación: <1%
- Tiempo de análisis: <5 minutos

**Lo que sabe (sección 14 — Discovery Debt):**
- "<1% alucinación en veredictos es alcanzable" → Evidence Strength: **Weak (sin benchmark)**
- "El corpus legal se puede estructurar para RAG efectivo en <30 días" → Evidence Strength: **Weak (estimación)**

Hay una brecha entre las metas de métricas y la evidencia de que son alcanzables. El documento base advierte: si tu Discovery Debt tiene múltiples items "Weak" con riesgo "Existencial", no estás listo para comprometerte con metas numéricas.

**Recomendación:** El PVB debería distinguir entre:
- **Metas de validación (primeros 30 días):** ¿Es técnicamente posible lograr <5% alucinación con nuestro stack? Si no, ¿qué necesitamos cambiar?
- **Metas de producto (90 días):** Solo fijables después de que las metas de validación se confirmen

Publicar metas numéricas antes de validar las hipótesis técnicas es el equivalente a decirle a un inversor "haremos $1M ARR" antes de tener un solo cliente.

---

## 6. Distribución — El punto más fuerte, con una brecha táctica

### Lo que está bien:
- WhatsApp como canal primary es una decisión excelente y diferenciada
- Output-as-distribution (tarjetas compartibles con artículo legal) es potencialmente viral
- El prestige partner como multiplicador de distribución está bien articulado

### La brecha: ¿Cómo llegan los primeros 1,000 usuarios al bot de WhatsApp?

El PVB no tiene una estrategia de adquisición de los primeros usuarios. Las tarjetas compartibles funcionan DESPUÉS de que alguien usa el producto. El prestige partner funciona DESPUÉS de la alianza. ¿Cómo se arranca?

**Opciones no exploradas:**
- **Cobertura de debates electorales en vivo:** El equipo de Pajudómetro hace live-fact-checking de un debate presidencial y publica resultados en X/Instagram en tiempo real. Cada tarjeta tiene el link al bot. Esto genera los primeros miles de usuarios en una sola noche.
- **Influencers políticos colombianos:** Creators como Daniel Samper, Juanpis González, o podcasters políticos usando el producto en sus contenidos.
- **Medios como canal:** Si ColombiaCheck o La Silla Vacía publican veredictos "powered by Pajudómetro", cada artículo suyo es un funnel.
- **QR codes en eventos electorales:** Presencia en debates universitarios, foros cívicos.

**Recomendación:** Agregar una sección de "Launch Playbook" o al menos definir la estrategia de adquisición de los primeros 1,000 usuarios en el roadmap de días 1–30.

---

## 7. FTCEM — Lo que falta

El FTCEM cubre 5 failure modes relevantes. Sin embargo, hay 3 escenarios no contemplados que el documento base señalaría:

### Failure Mode 6: Weaponización política
**Trigger:** Un partido político usa Pajudómetro selectivamente para atacar a opositores, compartiendo solo los veredictos negativos y omitiendo los positivos.
**Consequence:** El producto se percibe como herramienta de campaña negativa, no como auditoría neutral. Trust destruido.
**Early Warning:** Patrón de uso asimétrico (un bando político comparte 10x más que otro).
**Mitigation:** Las tarjetas compartibles siempre incluyen link al perfil completo del político (positivos y negativos). Rankings muestran el score total, no claims individuales.

### Failure Mode 7: Manipulación adversarial del input
**Trigger:** Alguien envía audio editado/deepfake de un político diciendo algo que nunca dijo, obtiene un veredicto de Pajudómetro, y lo comparte como "prueba".
**Consequence:** Pajudómetro se convierte involuntariamente en amplificador de desinformación — exactamente lo opuesto de su misión.
**Early Warning:** Detección de audio sintético, patrones de envío sospechoso (mismo audio enviado desde múltiples cuentas).
**Mitigation:** Disclaimer permanente: "Este análisis se basa en el audio proporcionado. Pajudómetro no verifica la autenticidad del audio." + En fase 2: integración de detección de deepfake audio.

### Failure Mode 8: Corpus legal desactualizado
**Trigger:** Se aprueba una reforma constitucional o una ley nueva que cambia el marco legal, y el corpus no se actualiza.
**Consequence:** Veredictos basados en legislación derogada o modificada. Desacreditación técnica.
**Early Warning:** Monitoreo de la Gaceta del Congreso y diarios oficiales.
**Mitigation:** Pipeline automatizado de actualización cuando se publican nuevas leyes + flag temporal "verificado contra legislación vigente a [fecha]".

---

## 8. Lo que el PVB v2.0 hace bien (reconocimiento explícito)

Sería deshonesto no señalar los avances significativos:

1. **El reframe del problema es correcto.** Pasar de "verificar claims" a "hacer accesible el conocimiento legal colombiano" cambia fundamentalmente la propuesta de valor y la durabilidad.

2. **El pivot a WhatsApp es estratégicamente superior.** Ir donde ya está la audiencia es la decisión correcta y demuestra pensamiento de distribución maduro.

3. **B2B como revenue center resuelve la economía conceptualmente.** La separación entre distribución (B2C) y monetización (B2B) es la estructura correcta.

4. **Capability sobre Speed es la prioridad correcta.** El cambio de <60s a <5min priorizando calidad es exactamente lo que el AI Decision Triangle recomienda para este caso de uso.

5. **El FTCEM existe y es relevante.** Los 5 failure modes son reales y las mitigaciones son razonables.

6. **El Discovery Debt Log es honesto.** Reconocer 6 hipótesis Weak con riesgo alto/existencial es señal de madurez estratégica, no de debilidad.

7. **Las 5 Preguntas Incómodas tienen respuestas articuladas.** No perfectas, pero demuestran pensamiento crítico sobre los riesgos del producto.

---

## 9. Resumen de ajustes recomendados antes del PRD

| # | Ajuste | Prioridad | Impacto |
|---|---|---|---|
| 1 | **Reformular el moat:** El corpus legal estático es requisito de entrada, no ventaja sostenida. El flywheel real es knowledge graph + correcciones humanas. | Alta | Cambia la narrativa estratégica |
| 2 | **Resolver cold start del knowledge graph:** Definir estrategia de seed data (pre-cargar claims de debates pasados). | Alta | Determina calidad de la experiencia MVP |
| 3 | **Recalcular unit economics con bound superior:** Costo por análisis probablemente $0.35–$0.55, no $0.15–$0.30. Ajustar break-even y tier gratis. | Alta | Afecta viabilidad financiera |
| 4 | **Agregar categoría de veredicto para propuestas de política pública:** Muchos claims no son verdad/mentira sino viabilidad legal. | Media | Honestidad del producto |
| 5 | **Agregar hipótesis de prestige partner al Discovery Debt:** ColombiaCheck puede decir que no. Necesitas Plan B. | Alta | Riesgo existencial de trust |
| 6 | **Agregar 3 failure modes al FTCEM:** Weaponización política, deepfake audio, corpus desactualizado. | Media | Completitud del análisis de riesgo |
| 7 | **Definir estrategia de primeros 1,000 usuarios:** Live-fact-checking de debate como launch event. | Media | Sin esto, el flywheel no arranca |
| 8 | **Contemplar grants/financiamiento como recurso explícito:** Google News Initiative, Meta Journalism Project, fondos de democracia. | Media | Realismo económico |
| 9 | **Agregar platform dependency shock al FTCEM:** Contingencia si APIs suben de precio o WhatsApp cambia términos. | Media | Resiliencia operativa |
| 10 | **Separar metas de validación (30 días) de metas de producto (90 días):** No comprometerse con <1% alucinación antes de validar técnicamente. | Media | Credibilidad de las metas |

---

## 10. Evaluación final por framework

| Framework | Score v1.0 | Score v2.0 | Nota |
|---|---|---|---|
| **Durability Test** | 2/5 | 3.5/5 | Corpus estático es temporal; knowledge graph es el moat real |
| **Red Ocean Trap** | Riesgo alto | Riesgo medio | Mercado colombiano es insignificante para gigantes (ventaja) |
| **Cool Demo Trap** | Riesgo alto | Riesgo medio-bajo | Capability sobre Speed es correcto; falta resolver claims ambiguos |
| **Platform Trap** | Riesgo crítico | Riesgo medio | Corpus legal reduce dependencia, pero STT/LLM/WhatsApp siguen siendo de terceros |
| **Data Moat** | Inexistente | En construcción | Flywheel articulado pero con cold start sin resolver |
| **Distribution Moat** | Débil | Bueno | WhatsApp + tarjetas compartibles + prestige partner |
| **Trust Moat** | Parcial | Sólido conceptualmente | Dependencia del partner es fragilidad |
| **Unit Economics** | Ausentes | Presentes pero optimistas | Recalcular con bound superior de costos |
| **5 Preguntas Incómodas** | Sin respuestas | Respondidas | P4 y P5 son las más fuertes |
| **FTCEM** | Ausente | 5 de 8 modes cubiertos | Faltan 3 escenarios críticos |

---

*Segunda ronda de crítica preparada aplicando los frameworks de "De la Idea al Product Vision Board para Productos Agénticos" (Hardcore AI — Estación 2)*
