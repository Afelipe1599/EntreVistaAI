# Crítica del Product Vision Board — Pajudómetro
## Análisis desde el framework "De la Idea al Product Vision Board para Productos Agénticos"

**Fecha:** 2026-03-07
**Documento evaluado:** `docs/pvb.md` (v1.0, 2026-03-06)
**Marco de referencia:** `ai-product-base.md` (Hardcore AI — Estación 2)

---

## Veredicto General

El PVB de Pajudómetro es un documento bien estructurado que demuestra comprensión del problema y del contexto colombiano. Sin embargo, al pasarlo por los frameworks del documento base, emergen **brechas críticas** en moat, economics, durabilidad y estrategia de distribución que, si no se abordan, ponen en riesgo la viabilidad del producto más allá de un ciclo electoral.

---

## 1. Test de Durabilidad: ¿El Problema Sobrevive a GPT-5?

**Score: 2/5 — Riesgo alto de commoditización**

El documento base es explícito: los problemas de **OUTPUT** se commoditizan; los problemas de **WORKFLOW** persisten. Pajudómetro tiene un problema de durabilidad serio:

- **Lo que hace Pajudómetro es fundamentalmente un pipeline de outputs:** transcripción → extracción de claims → verificación → veredicto. Cada uno de estos pasos está siendo commoditizado activamente por modelos foundation.
- Ya hoy, un usuario puede grabar audio, pasarlo por Whisper (o el STT nativo de cualquier modelo), pegar la transcripción en ChatGPT/Claude/Gemini y pedir "verifica cada afirmación con fuentes". El resultado es comparable al flujo propuesto.
- Con GPT-5/Claude 5 y capacidades multimodales mejoradas (audio directo → análisis), el flujo completo podría ser un prompt de una línea en cualquier chatbot generalista.

**Lo que falta en el PVB:** Una respuesta honesta a "¿qué parte de nuestro valor NO puede replicarse con un prompt bien escrito en un modelo foundation?". El PVB compara contra competidores actuales (ColombiaCheck, Full Fact), pero no contra el competidor más peligroso: **ChatGPT con audio input + search en tiempo real**, que ya existe.

**Recomendación:** El problema durable no es "verificar claims" (output), sino construir la **infraestructura de conocimiento político colombiano** (workflow + data). Eso requiere un replanteamiento fundamental del moat.

---

## 2. Las 3 Trampas Mortales — ¿En cuáles cae Pajudómetro?

### Trampa 1: Red Ocean Trap — ⚠️ Riesgo medio-alto

El PVB posiciona a Pajudómetro en el cuadrante "Ciudadano + Automático" y afirma que nadie lo ocupa. Esto es parcialmente cierto **hoy**, pero ignora que:

- Google ya integra fact-checking en Search con AI Overviews
- Perplexity puede hacer fact-checking citado con un prompt
- Meta y Google tienen incentivos regulatorios para construir herramientas anti-desinformación en sus propias plataformas (donde ya vive el contenido)

El documento base advierte: "los startups están entrando en océanos rojos con wrappers AI cleveres, solo para ser aplastados cuando líderes replican su feature". La verificación automática de claims es exactamente el tipo de feature que un gigante puede replicar en una actualización.

### Trampa 2: Cool Demo Trap — ⚠️ Riesgo alto

El PVB describe un flujo que suena mágico: "graba → resultado en <60 segundos". El documento base advierte sobre el "último 20%": el gap entre un demo cool y un producto confiable.

Problemas concretos no abordados:
- **Audio en entornos reales:** mítines políticos, debates con crosstalk, TV con música de fondo. El PVB menciona "umbral de confianza" como mitigación, pero no modela qué porcentaje de grabaciones reales van a fallar ese umbral.
- **Verificación de claims ambiguos:** "Redujimos la pobreza" — ¿contra qué baseline? ¿Qué fuente es "la correcta"? El fact-checking profesional requiere contexto editorial que un agente no puede dar de forma confiable.
- **Meta <2% alucinación en veredictos:** Esto es extremadamente ambicioso. No hay benchmark de referencia para afirmar que es alcanzable con modelos actuales en español colombiano, sobre datos políticos que frecuentemente son matizados y no binarios.

### Trampa 3: Platform Trap — 🔴 Riesgo crítico

Pajudómetro es, por diseño, un wrapper sofisticado sobre APIs de terceros:
- STT de terceros (Whisper/Deepgram)
- LLM de terceros (el "agente de análisis agéntico")
- No se menciona ningún modelo propio ni fine-tuning

El documento base dice textualmente: "si todo lo que has construido es una capa delgada de UX sobre el modelo de otro y data pública, no estás construyendo un producto. Estás corriendo un experimento en tierra rentada."

**El PVB no tiene respuesta a esta pregunta.**

---

## 3. Moat Analysis — ¿Qué moat tiene realmente Pajudómetro?

Aplicando el framework de los 3 Moats:

### Data Moat — 🔴 Inexistente en el PVB actual

El PVB no articula qué data propietaria genera Pajudómetro que competidores no puedan obtener. Las grabaciones de los usuarios son audio público (discursos políticos). Las fuentes de verificación son públicas. Los veredictos son outputs de un LLM.

**¿Dónde podría existir?** En la acumulación de: (a) un dataset estructurado de claims políticos colombianos verificados con timestamp + fuente + veredicto + correcciones humanas, (b) patrones de verificación que mejoran con el uso, (c) un "knowledge graph" de promesas vs. realidad por político. Nada de esto está en el PVB.

### Distribution Moat — 🟡 Débil

El PVB propone una app móvil standalone. El documento base es claro: "Productos que se embeben en workflows se defienden mejor que standalone apps."

- Los colombianos consumen política en **WhatsApp, X, Instagram, TikTok y TV**. Una app separada compite por espacio en el teléfono contra estas plataformas.
- No hay estrategia de "output-as-distribution" (como ElevenLabs) ni de embeberse en un workflow existente.
- El "ranking de políticos" podría ser viral, pero no está articulado como estrategia de distribución.

### Trust Moat — 🟡 Mejor posicionado, pero insuficiente

Los principios no negociables (agnóstico, trazabilidad, anti-alucinación, transparencia) son correctos y alineados con el framework de Trust Moat. Sin embargo:

- No hay mención de auditoría externa o partnership con una entidad de fact-checking que valide la metodología
- No hay plan para manejar los casos donde el veredicto de Pajudómetro contradiga el de ColombiaCheck (esto va a pasar)
- No hay estrategia de "prestige moat" (como Harvey con Allen & Overy)

**Recomendación:** El moat más viable para Pajudómetro es un Trust Moat construido a través de alianza con ColombiaCheck/MOE/universidades, donde Pajudómetro se convierte en la **capa tecnológica** de una institución confiable, no en un actor independiente compitiendo por credibilidad.

---

## 4. Arena Competitiva — ¿Pioneer, Disruptor o Enhancer?

El PVB no define explícitamente su arena. Implícitamente se posiciona como **Pioneer (AI-Native)**: creando un mercado que no existía.

**Problema:** El mercado de fact-checking SÍ existe. Lo que Pajudómetro hace es usar AI para automatizar y democratizar un workflow existente. Eso lo hace un **Disruptor**, no un Pioneer.

Esto importa porque la estrategia cambia: un Disruptor debe demostrar que es **10x mejor** que el incumbent (ColombiaCheck manual). El PVB afirma "4-8 horas → <5 minutos", que suena a 10x, pero solo si la calidad es comparable. Si el veredicto automatizado tiene menor matiz/confiabilidad que un fact-check humano, no es 10x — es un producto diferente para un segmento diferente.

---

## 5. Economía Brutal — El Test de 10x

### Lo que el PVB no modela (y debería):

El documento base exige modelar economics a 100x escala. El PVB dice "Freemium" sin ningún número de costo.

**Estimación rápida de costos por análisis:**

| Componente | Costo estimado por análisis |
|---|---|
| STT (5 min de audio) | $0.03–$0.06 |
| LLM agente multi-turn (extracción + verificación + veredicto, ~10K tokens) | $0.05–$0.15 |
| Search/retrieval de fuentes | $0.01–$0.05 |
| **Total por análisis** | **~$0.10–$0.25** |

**A escala:**
- Meta de 3 grabaciones/usuario/semana × 10,000 usuarios activos = 30,000 análisis/semana
- Costo semanal: $3,000–$7,500
- Costo mensual: **$12,000–$30,000**

**Con modelo freemium:** Si solo 5% paga (500 usuarios pagos) y el tier premium cuesta ~$5/mes (mercado colombiano), eso es $2,500/mes de revenue contra $12K–$30K de costo. **Los márgenes son brutalmente negativos.**

El PVB necesita urgentemente:
- Definición de límites del tier gratuito (¿cuántos análisis gratis/mes?)
- Precio del tier premium validado contra willingness-to-pay en Colombia
- Modelo de costo por usuario que cierre con márgenes positivos
- Estrategia de monetización B2B (periodistas/medios) que subsidie el B2C

### El AI Decision Triangle

El PVB no define si optimiza para Cost, Capability o Speed. Implícitamente parece optimizar para **Speed** (<60 segundos), pero el caso de uso real demanda **Capability** (precisión del veredicto). Este conflicto no resuelto va a generar problemas de producto graves.

---

## 6. Las 5 Preguntas Incómodas — Aplicadas a Pajudómetro

### P1: ¿Qué si el problema desaparece en 12 meses por commoditización?

**Respuesta del PVB:** No existe.
**Realidad:** Con modelos multimodales que aceptan audio directo + hacen search en tiempo real, el "grabar y verificar" será un prompt genérico en 12–18 meses. El diferencial tiene que estar en otra parte.

### P2: ¿Quién es dueño de la data?

**Respuesta del PVB:** No abordada.
**Realidad:** Las fuentes de verificación son públicas (DANE, Banco de la República, medios). El audio es del usuario. No hay data propietaria. Un competidor con las mismas APIs tiene acceso a exactamente la misma información.

### P3: ¿Qué pasa si el producto falla públicamente?

**Respuesta del PVB:** Parcialmente cubierta (principios de anti-alucinación).
**Realidad:** En contexto electoral colombiano, un veredicto incorrecto de Pajudómetro podría: (a) ser utilizado como arma política ("la app dice que X es mentiroso"), (b) generar acusaciones de sesgo, (c) causar daño reputacional irreversible. El PVB no tiene un FTCEM (Failure mode, Trigger, Consequence, Early warning, Mitigation) documentado.

### P4: ¿Puede un competidor replicar esto en 6 semanas?

**Respuesta honesta: Sí.** Con Whisper + Claude/GPT + web search + una UI en Flutter, un equipo competente puede replicar el flujo core en semanas. El PVB no identifica ninguna barrera técnica o de data que lo impida.

### P5: Si tenemos éxito a escala, ¿cómo se rompe trust primero?

**Respuesta del PVB:** No abordada.
**Escenario más probable:** Un político demanda públicamente que el veredicto de Pajudómetro es "sesgado" o "incorrecto", genera controversia mediática, y sin respaldo institucional (ColombiaCheck, academia), Pajudómetro no tiene credibilidad para defenderse. El trust se rompe por legitimidad percibida, no por fallo técnico.

---

## 7. Elementos Faltantes vs. Template del Vision Board

El PVB no incluye varias secciones que el template del documento base exige:

| Sección del Template | Estado en PVB |
|---|---|
| Durability Score (1-5) | ❌ Ausente |
| Veto holder de confianza | ❌ Ausente |
| Moat primario (elegir UNO) | ❌ No definido explícitamente |
| Arena competitiva (Pioneer/Disruptor/Enhancer) | ❌ No definida |
| UX Paradigm (Assistant/Agent/Autonomous/Embedded) | ❌ No definido |
| AI Decision Triangle (Cost/Capability/Speed) | ❌ No definido |
| Modelo económico con números | ❌ Solo "Freemium" sin cifras |
| Costo estimado por usuario/mes | ❌ Ausente |
| Revenue por usuario/mes | ❌ Ausente |
| Gross margin proyectado | ❌ Ausente |
| Discovery Debt Log | ❌ Ausente |
| FTCEM (failure modes) | ❌ Ausente |

---

## 8. Lo Que el PVB Hace Bien

No todo es crítica. Hay elementos sólidos que vale la pena reconocer:

1. **Timing electoral:** El contexto de elecciones Colombia 2026 es genuinamente un catalizador de demanda. La urgencia es real.

2. **JTBD bien articulado:** "Cuando escucho a un político... quiero obtener un análisis automático... para tomar decisiones informadas" es claro y accionable.

3. **Principios no negociables:** Agnóstico, trazable, anti-alucinación, transparente. Están alineados con lo que el documento base llama Trust Moat.

4. **Segmentación dual:** Separar ciudadano informado vs. periodistas es correcto. El B2B (periodistas) es probablemente donde está el modelo de negocio viable.

5. **Propuesta de ROI para periodistas:** La tabla "antes vs. después" es convincente y concreta.

6. **Procesamiento transparente:** Mostrar los pasos del análisis en tiempo real es un diferenciador de UX que construye confianza.

---

## 9. Recomendaciones Prioritarias

### R1: Redefinir el moat como Data Moat basado en knowledge graph político
En lugar de competir en el pipeline (commoditizable), construir un **grafo de conocimiento político colombiano** que acumule: claims verificados, historial de promesas vs. cumplimiento, relaciones entre actores políticos, y correcciones humanas. Eso es data que no se puede comprar ni replicar con un prompt.

### R2: Resolver la economía ANTES de construir
Hacer las cuentas de costo por análisis, definir límites del tier gratis, y validar willingness-to-pay en Colombia. Si el modelo freemium B2C no cierra, pivotar a B2B-first (vender a medios y ONGs) y usar el B2C como canal de distribución, no como centro de revenue.

### R3: Buscar un "prestige partner" como ancla de trust
Aliarse con ColombiaCheck, MOE, o una universidad reconocida como auditor de la metodología. Sin respaldo institucional, un veredicto de IA sobre un político no tiene peso frente a la controversia pública.

### R4: Diseñar para distribución embebida, no standalone
En lugar de una app separada, considerar: bot de WhatsApp, extensión de Chrome para noticias online, integración con apps de noticias colombianas. Ir donde ya está la audiencia, no pedirles que descarguen otra app.

### R5: Completar las secciones faltantes del Vision Board
Llenar las 12 secciones ausentes identificadas en la sección 7, especialmente el FTCEM, el modelo económico con números, y la definición explícita de moat primario.

### R6: Preparar respuesta al "test de 6 semanas"
Articular qué tiene Pajudómetro que NO puede ser replicado en 6 semanas por un equipo con acceso a las mismas APIs. Si la respuesta honesta es "nada técnico", entonces el moat tiene que estar en data, distribución, o trust — y el PVB debe reflejar eso.

---

*Crítica preparada aplicando los frameworks de "De la Idea al Product Vision Board para Productos Agénticos" (Hardcore AI — Estación 2)*
