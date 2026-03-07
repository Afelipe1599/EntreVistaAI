# Analisis Profundo de Plataformas de Verificacion Civica con IA: Arquitectura, Impacto Democratico y Marco Regulatorio en la Auditoria del Discurso Politico (2025-2026)

## 1. Introduccion al Paradigma de la Verificacion Civica Agentica

El ecosistema de la informacion publica ha experimentado una transformacion sin precedentes durante el periodo 2024-2026. La desinformacion ha dejado de ser una anomalia marginal para consolidarse como una tactica estructurada de coercion cognitiva, amplificada por arquitecturas algoritmicas de recomendacion en redes sociales y plataformas de mensajeria instantanea. Informes de inteligencia de mercado de 2026 estiman que el engano digital y la desinformacion representan un costo operativo para la economia global de aproximadamente $78 mil millones de dolares anuales, catalogando a la desinformacion impulsada por IA como una amenaza de $26 mil millones que esta reconfigurando las matrices de riesgo a nivel mundial.<sup>1</sup> La asimetria del problema es alarmante: las historias falsas se propagan a una velocidad seis veces mayor que la verdad, alcanzando rapidamente a cientos de miles de usuarios, mientras que los desmentidos tradicionales rara vez superan un alcance marginal.<sup>1</sup>

Sin embargo, el verdadero punto de inflexion no radica en la existencia de la desinformacion, sino en la evolucion de las herramientas disponibles para combatirla. La industria ha presenciado la transicion desde el fact-checking manual y asincrono — donde verificadores humanos publican correcciones dias despues de que una falsedad se viralizo — hacia la verificacion agentica en tiempo real. Un sistema de verificacion agentico no se limita a cruzar palabras clave contra una base de datos: actua como una entidad de software integrada que percibe audio en vivo, transcribe con precision clinica, extrae afirmaciones verificables separandolas de la retorica, consulta repositorios estructurados de fact-checks, y emite veredictos trazables con fuentes citadas — todo en cuestion de segundos.<sup>2</sup>

Este reporte de investigacion exhaustiva desglosa las funcionalidades, el impacto civico, la viabilidad comercial y el panorama regulatorio de los "Verificadores Civicos Agenticos". A traves de un analisis detallado de implementaciones reales entre 2025 y 2026, se evaluara como estas plataformas equilibran la velocidad computacional con la integridad epistemica, enmarcadas dentro del ciclo electoral colombiano y un entorno legal cada vez mas restrictivo.

## 2. Definicion y Delimitacion Conceptual: El Verificador Civico Agentico

Para alinear el concepto central de esta investigacion, es imperativo establecer una definicion tecnica de lo que constituye un "Verificador Civico Agentico". A diferencia de los buscadores de noticias o los chatbots de consulta generica, que se limitan a devolver resultados basados en coincidencia de keywords, el verificador agentico es un sistema de IA que asume la conduccion activa, adaptativa y analitica de un flujo de verificacion multi-paso.

En la practica, la arquitectura implica que el agente recibe una entrada de audio crudo, lo transforma en texto mediante modelos de transcripcion de ultima generacion, y ejecuta un analisis semantico profundo para separar las afirmaciones factuales verificables de la retorica politica, las opiniones, las promesas a futuro y las analogias. Utilizando el paradigma de llamadas a herramientas (Tool-calling), el agente formula consultas estructuradas contra repositorios externos de verificacion como la Google FactCheck Claim Search API, consume metadatos bajo el estandar ClaimReview de Schema.org, y sintetiza un veredicto clasificado (verdad, mentira o enganoso) con la cita textual de la fuente periodistica que respalda cada evaluacion.<sup>3</sup>

Esta capacidad de orquestar multiples herramientas especializadas a traves de turnos consecutivos, sin perder el contexto conversacional ni el objetivo de verificacion, es la esencia del comportamiento agentico. El resultado final no es una opinion probabilistica generada por un LLM, sino un output estructurado y auditable que conecta la voz del politico con el trabajo de periodistas de investigacion verificados, posicionando a la IA estrictamente como un conducto tecnologico de baja latencia.

| Dimension | Chatbot Tradicional | Verificador Agentico |
|---|---|---|
| **Entrada** | Texto escrito por el usuario | Audio capturado en vivo desde microfono |
| **Procesamiento** | Respuesta unica basada en prompt | Loop multi-turno con tool-calling (transcripcion, extraccion, verificacion, sintesis) |
| **Fuentes** | Conocimiento parametrico del LLM | APIs externas estructuradas (ClaimReview, Google FactCheck, DANE) |
| **Output** | Texto libre probabilistico | Veredicto clasificado + fuente citada + URL de respaldo |
| **Trazabilidad** | Nula (caja negra) | Total (cada paso registrado en logs auditables) |
| **Riesgo de alucinacion** | Alto (genera desde parametros) | Mitigado (restringido a fuentes externas verificadas) |

## 3. Eje A: Velocidad, Asimetria Informativa y el Valor Civico de la Verificacion en Tiempo Real

En el dominio de la auditoria del discurso publico, el impacto mas contundente de la IA agentica no reside en que "la IA decida" que es verdad. El verdadero paradigma de valor se fundamenta en como la IA comprime la latencia de verificacion de dias a segundos, cerrando la brecha temporal que permite a la desinformacion propagarse sin contrapeso.

### 3.1 La Brecha Temporal como Crisis Democratica

La verificacion periodistica tradicional, aunque rigurosa, opera de manera asincronica. Organizaciones como ColombiaCheck — certificada por la International Fact-Checking Network (IFCN) — y el Detector de Mentiras de La Silla Vacia han desarrollado metodologias exhaustivas y repositorios de desmentidos historicos.<sup>4</sup> Sin embargo, el proceso manual de transcribir un discurso, investigar las fuentes, redactar la verificacion y publicarla toma entre 4 y 8 horas, y en casos complejos, varios dias. Para cuando la correccion se publica, la falsedad original ya ha alcanzado a cientos de miles de ciudadanos en WhatsApp, TikTok y X.

En Colombia, esta brecha temporal adquiere dimensiones criticas. El 59% de los colombianos manifiesta una preocupacion explicita por la proliferacion de falsedades en el entorno digital, y los actores politicos e influenciadores partidistas son senalados como los principales vectores de riesgo para la informacion veraz.<sup>5</sup> Las plataformas de mensajeria cifrada de extremo a extremo dominan los canales de adquisicion de informacion politica, creando ecosistemas cerrados donde la desinformacion circula sin posibilidad de desmentido en tiempo real.<sup>6</sup>

### 3.2 Validacion Internacional: Full Fact AI y Factiverse

La viabilidad de comprimir esta latencia esta solidamente respaldada por el exito operativo de plataformas analogas en el ecosistema internacional.

**Full Fact AI (Reino Unido):** La plataforma lider global en verificacion asistida por IA proporciona infraestructura de fact-checking en tiempo real a mas de 45 organizaciones periodisticas y gubernamentales en mas de 30 paises.<sup>7</sup> Su sistema orquesta modelos avanzados de NLP para monitorear debates publicos de manera ininterrumpida, transcribir audio y video en tiempo real, e identificar afirmaciones verificables para cruzarlas con bibliotecas de comprobaciones previas. De cara a los procesos electorales de 2026, Full Fact ha expandido activamente el licenciamiento de sus herramientas hacia nuevas redacciones americanas, validando la exportabilidad global de estos sistemas.<sup>8</sup> Ademas, colabora en proyectos de escala continental como MediaVault y el Proyecto PAS en Europa, disenados como infraestructuras compartidas para rastrear narrativas enganosas interlingueisticas.<sup>9</sup>

**Factiverse (Noruega):** Tras levantar rondas de inversion superiores a un millon de euros y ser galardonada en TechCrunch Disrupt 2024, Factiverse programo para la primavera de 2026 el lanzamiento comercial de "Factiverse Live".<sup>10</sup> Esta solucion procesa hasta 150 horas de contenido audiovisual semanalmente de forma automatizada, con una latencia tan baja que en ocasiones interroga bases de datos globales (Wikipedia, Semantic Scholar, FactiSearch con 300,000+ fact-checks) devolviendo resultados incluso antes de que la afirmacion termine de ser articulada por el orador.<sup>11</sup>

### 3.3 El Diferencial B2C: Verificacion Distribuida en el Bolsillo del Ciudadano

A diferencia de Full Fact y Factiverse, cuyo modelo de negocio es primordialmente B2B orientado a redacciones periodisticas y agencias gubernamentales<sup>12</sup>, la propuesta del Pajudometro adopta una estrategia B2C. Al democratizar el acceso mediante una aplicacion movil nativa, se elimina la barrera de entrada: cualquier ciudadano actua como un auditor independiente, creando una red de verificacion distribuida en el punto exacto de consumo de la informacion. Las lecciones tecnicas de las plataformas B2B son el fundamento empirico que asegura que el pipeline propuesto es tecnologicamente ejecutable.

| Plataforma | Enfoque de Mercado | Mecanismo Central | Estado Operativo (2026) |
|---|---|---|---|
| **Full Fact AI (UK)** | B2B (Redacciones, ONGs) | Monitoreo continuo, STT en tiempo real, cruce con MediaVault | Despliegue global; 45+ orgs en 30 paises |
| **Factiverse Live (NOR)** | B2B (Medios, Analistas) | Busqueda semantica de baja latencia en FactiSearch (300k+ registros) | Lanzamiento Live en primavera 2026 |
| **ColombiaCheck (COL)** | ONG Periodistica | Verificacion manual, metodologia IFCN, repositorio de desmentidos | Operativo; alianza con MOE/CRC para elecciones 2026 |
| **Pajudometro (COL)** | B2C (Ciudadanos) | Captura in-situ, orquestacion agentica, consulta a APIs de FactCheck | Propuesta de MVP alineada con ciclo electoral |

## 4. Eje B: Precision Acustica, Transcripcion y Calidad de la Evidencia

Mientras que la primera ola de herramientas de fact-checking se centro en la cobertura y el volumen, la segunda ola se orienta hacia la precision clinica en cada eslabon de la cadena de verificacion. En un sistema agentico de auditoria politica, un error en la transcripcion — una negacion omitida, un numero distorsionado, un nombre propio mal interpretado — se propaga catastroficamente a traves de toda la cadena, produciendo veredictos alucinados que destruyen la credibilidad de la plataforma.

### 4.1 El Entorno Acustico Hostil del Discurso Politico

El contexto de uso de una app de verificacion civica es excepcionalmente hostil para el procesamiento de audio. Los usuarios grabaran a politicos en mitines en plazas publicas, en debates televisivos retransmitidos con eco, en recintos cerrados con acustica deficiente, o a traves de sistemas de megafonia distorsionados. En estos escenarios, la resistencia al ruido de fondo no es una caracteristica opcional: es el pilar de la confiabilidad del producto.

### 4.2 Evolucion de los Modelos de Transcripcion (STT)

A lo largo de 2025 y principios de 2026, la industria del reconocimiento automatico de voz (ASR) presencio un cambio de paradigma. Los nuevos modelos de transcripcion superan consistentemente a generaciones anteriores en metricas clave, especialmente en escenarios multilinguees y ambientes degradados.<sup>13</sup>

Para el idioma espanol (y sus variantes dialecticas latinoamericanas), las evaluaciones indican mejoras sustanciales en la Tasa de Error de Palabra (WER). Los modelos de ultima generacion alcanzan un WER de 6.1% en espanol, superando significativamente el 8.5% de modelos previos.<sup>14</sup> En entornos acusticamente ruidosos (SNR < 10dB) — equivalentes a una plaza publica llena de simpatizantes — los nuevos modelos logran un WER de 8.3%, una mejora del 33% frente al 12.5% de generaciones anteriores.<sup>14</sup>

Adicionalmente, las actualizaciones de diciembre 2025 introdujeron mejoras fundamentales en robustez algoritmica, reduciendo hasta en un factor de 4x las alucinaciones durante periodos de silencio prolongado en el audio — un fallo documentado donde el sistema inventaba texto para rellenar vacios acusticos, un riesgo inaceptable para una herramienta de auditoria politica.<sup>13</sup>

| Generacion de Modelo STT | WER en Espanol | Desempeno en Ruido (SNR < 10dB) | Relevancia para Verificacion Civica |
|---|---|---|---|
| **Modelos legacy (Whisper V3)** | 8.5% | 12.5% WER | Fuerte en entornos limpios; degradacion notable ante ruido y dialectos |
| **Modelos de nueva generacion (2025)** | 6.1% | 8.3% WER (mejora del 33%) | Precision semantica superior; comprension de terminologia politica |
| **Modelos optimizados (Dec 2025)** | Similar a version mayor | Alta robustez; alucinaciones en silencio reducidas 4x | Balance optimo entre latencia, costo y precision para audios cortos |
| **Alternativas streaming (ej. Deepgram Nova-3)** | < 5% (estimado) | Altamente resistente, optimizado para streaming | Excelente para arquitecturas multi-modelo de latencia ultra baja |

### 4.3 Extraccion de Afirmaciones y Ventanas de Contexto

Una vez obtenida una transcripcion limpia, el agente debe desentranar la retorica politica para aislar las unidades atomicas de informacion verificable. Los discursos politicos son amalgamas densas de opiniones, promesas a futuro, analogias y datos duros. La literatura en NLP aplicado al fact-checking subraya que la extraccion de afirmaciones (Claim Extraction) es el vector de falla mas comun en estos ecosistemas.<sup>15</sup>

Investigaciones presentadas en conferencias de la ACL concluyen que el analisis lineal fragmentado (oracion por oracion) destruye la semantica relacional del discurso. El tamano optimo de la ventana de contexto para preservar el significado relacional se situa alrededor de 10 oraciones continuas.<sup>16</sup> Ademas, un analisis masivo de desmentidos revela que casi el 25% de las afirmaciones politicas falsas se repiten de manera sistematica, desafiando las correcciones previas mediante variaciones matizadas.<sup>17</sup> El agente debe normalizar las afirmaciones extraidas utilizando incrustaciones vectoriales semanticas, asegurando que variaciones lexicas minimas de una misma mentira historica sean detectadas con precision.

## 5. Eje C: Psicologia Cognitiva, Sesgo Partidista y Barreras de Adopcion

El exito de cualquier herramienta de verificacion depende de la aceptacion por parte del usuario final. El diseno del MVP presupone una racionalidad ilustrada: asume que al presentar la falsedad de una declaracion mediante un veredicto estructurado, el ciudadano alterara su creencia. La evidencia cientifica contemporanea en ciencias del comportamiento destruye categoricamente esta hipotesis lineal.

### 5.1 La Prevalencia del Partidismo sobre la Verdad

Investigaciones conducidas por la Universidad de Stanford y publicadas a finales de 2024 en el _Journal of Experimental Psychology_ demostraron empiricamente que, en climas electorales altamente polarizados, la poblacion general subordina la verdad objetiva a la alineacion partidista.<sup>18</sup> Este sesgo opera independientemente del nivel de escolaridad o la capacidad de razonamiento logico.

El hallazgo mas relevante para la plataforma: los ciudadanos muestran una propension significativamente mayor a desestimar informacion objetivamente cierta que desafia sus convicciones ideologicas, frente a su disposicion para aceptar pasivamente narrativas falsas que las confirman.<sup>18</sup> En la practica, si la app devuelve un puntaje reprobatorio para el lider del usuario, el reflejo psicologico no sera cuestionar al politico, sino atacar la credibilidad del algoritmo.

### 5.2 Revaluacion del Efecto Contraproducente

Frente a la desinformacion, la comunidad cientifica habia advertido sobre el "efecto contraproducente" (Backfire Effect). Sin embargo, analisis longitudinales realizados entre 2024 y 2025 demuestran que este efecto es marginal y no justifica la abstencion de corregir falsedades.<sup>19</sup> La resistencia a la verificacion no emana de la correccion misma, sino de la "amenaza a la imagen social" (face threat) y la reactancia psicologica que surge cuando el desmentido se presenta de forma hostil o dogmatica.<sup>20</sup>

### 5.3 Implicaciones para el Diseno de Interfaz

Estos hallazgos imponen restricciones severas en el diseno de la UI y el tono del agente:

- **Neutralidad expositiva:** La presentacion del veredicto no debe exhibir un caracter punitivo. Las salidas deben ser neutrales, encuadrando la correccion como una divergencia estadistica frente a datos institucionales.<sup>20</sup>
- **Inoculacion cognitiva:** Integrar advertencias previas que indiquen que ciertos discursos emplean tacticas de manipulacion emocional actua como una inoculacion: predispone al usuario a analizar con escepticismo critico antes de recibir el veredicto duro.<sup>20</sup>
- **Posicionamiento como asistente, no como juez:** La app no debe promocionarse como un "juez robotico". Debe estructurarse como un motor de busqueda ultra-eficiente o "asistente de investigacion ciudadana", enfatizando el linaje humano de la verificacion.<sup>5</sup>
- **Prominencia de la fuente:** La pantalla de resultados debe priorizar visualmente la organizacion periodistica responsable (logo de ColombiaCheck, La Silla Vacia), posicionando a la IA como el conducto tecnologico, no como el autor del veredicto.

### 5.4 La Confianza Algoritmica en Colombia

Los datos del Reuters Institute 2025 revelan que aproximadamente el 49% de los encuestados globales se siente comodo con la IA en la seleccion de noticias, pero esta comodidad disminuye al 43% en redes sociales.<sup>5</sup> La audiencia colombiana muestra mayor apertura relativa a la IA en comparacion con Europa del Norte, pero mantiene desconfianza cuando la tecnologia produce informacion de manera autonoma con poca intervencion humana. Sin embargo, los ciudadanos manifiestan niveles sustancialmente mas altos de aceptacion cuando la IA se utiliza como herramienta de asistencia bajo supervision humana.<sup>5</sup>

## 6. Arquitectura Tecnica: Orquestacion Agentica, RAG y Prevencion de Alucinaciones

La ejecucion de un verificador civico agentico requiere una arquitectura que difiere radicalmente de las aplicaciones deterministas convencionales. Los LLMs son inherentemente probabilisticos y propensos a la alucinacion, por lo que los sistemas de nivel civico exigen infraestructuras de orquestacion complejas y guardrails rigurosos.

### 6.1 El Estandar ClaimReview y la Interoperabilidad de Datos

La infraestructura global de fact-checking ha evolucionado hacia la estandarizacion semantica a traves de la adopcion generalizada del esquema ClaimReview de Schema.org.<sup>21</sup> Las principales plataformas de verificacion en Colombia, incluyendo ColombiaCheck y el Detector de Mentiras de La Silla Vacia, incorporan este marcado de datos estructurados en sus articulos. ClaimReview encapsula metadatos vitales: autor de la afirmacion, la afirmacion literal evaluada, la URL del articulo, y la calificacion otorgada (reviewRating).<sup>22</sup>

El flujo de verificacion agentico se estructura asi:

1. **Extraccion Factual Rigurosa:** El modelo transforma la transcripcion coloquial en una entidad de busqueda canonica (ej. {"orador": "candidato X", "afirmacion_clave": "Tasa de inflacion es 4%"}).
2. **Llamada a la API (Tool-calling):** El agente invoca la Google FactCheck Claim Search API, aplicando restriccion geografica (Colombia) y filtrando por dominios de alta confianza (colombiacheck.com, lasillavacia.com).<sup>23</sup>
3. **Evaluacion de Resultados:** La API responde con objetos ClaimReview JSON. El agente extrae el reviewRating y la justificacion textual.<sup>22</sup>
4. **Sintesis Agnostica:** El agente reescribe la informacion en lenguaje ciudadano, incluyendo el enlace directo a la fuente periodistica original.

### 6.2 Robustez del Sistema RAG y Riesgos de Evidencia Enganosa

Los sistemas RAG comerciales asumen condiciones de recuperacion pristinas que no existen en el dominio politico.<sup>24</sup> El benchmark RAGUARD ha expuesto una vulnerabilidad critica: cuando un LLM es expuesto a evidencia recuperada marginalmente enganosa o tendenciosa, su precision cae drasticamente, rindiendo por debajo de las capacidades base del modelo sin informacion adicional.<sup>24</sup>

Si el agente utiliza motores de busqueda generalistas, es altamente probable que recupere articulos de blogs polarizados o noticias falsas disenadas para SEO, induciendo veredictos alucinados. La arquitectura debe estar restringida mediante una estricta lista blanca (whitelist) algoritmica: las herramientas de recuperacion solo deben consultar repositorios indexados de alta confiabilidad (DANE, Datos.gov.co, ColombiaCheck, La Silla Vacia).<sup>25</sup>

### 6.3 Enrutamiento de Modelos y Eficiencia VCES

La orquestacion de multiples turnos introduce el desafio de la latencia acumulada. Investigaciones de 2026 sobre el rendimiento comparativo de LLMs introducen la metrica VCES (Value-Cost-Execution-Speed), que demuestra un intercambio estructural entre velocidad de ejecucion y eficiencia de costos.<sup>26</sup>

Para mitigar el impacto financiero y optimizar la latencia, la arquitectura debe implementar un patron de enrutamiento condicional:

- **Enrutador de Triage (Modelo Ligero):** Clasificacion rapida binaria — ¿contiene el texto alguna afirmacion factual o es pura retorica politica? Si es retorica, el proceso se detiene.
- **Agente de Extraccion y Verificacion (Modelo Pesado):** Solo si el enrutador detecta un claim factual, la cadena se transfiere al modelo de mayor razonamiento para extraccion precisa y tool-calling contra APIs externas.

Este patron ha demostrado reducir el gasto en tokens entre un 40% y un 60% sin sacrificar la exactitud del veredicto.<sup>27</sup>

### 6.4 Transparencia Operativa y "Teatro Algoritmico"

La solucion a la latencia multi-turno desde la perspectiva UX consiste en inyectar actualizaciones de estado granulares en la interfaz a traves de conexiones bidireccionales (WebSockets). Mensajes secuenciales como "Transcribiendo audio...", "Aislando variables macroeconomicas...", "Consultando bases de datos de ColombiaCheck...", "Sintetizando veredicto..." transforman una espera tecnica en una experiencia de transparencia algoritmica que aumenta la percepcion ciudadana sobre la rigurosidad del analisis.<sup>26</sup>

## 7. Algoritmia de Calificacion Etica y el Diseno del Score de Veracidad

La inclusion de un Score de Veracidad (0-100) representado como un gauge, junto con rankings acumulados de politicos, es una estrategia de retencion potente. Sin embargo, la reduccion del discurso politico a una metrica unificadora conlleva riesgos eticos profundos.

### 7.1 La Falacia de la Dilucion de Gravedad

Un actor politico podria pronunciar intencionalmente diez afirmaciones triviales verdaderas y entremezclar una unica falsedad masiva. Un promedio aritmetico le otorgaria un 90%, encubriendo matematicamente el impacto de la desinformacion grave.<sup>28</sup>

### 7.2 Divergencias entre Verificadores Humanos

Estudios que comparan resoluciones de organizaciones como The Washington Post Fact Checker, PolitiFact y Snopes demuestran que, si bien el acuerdo en aseveraciones puramente facticas es alto, existen divergencias notables en la gradacion de la "enganosidad".<sup>29</sup>

### 7.3 Principios del Algoritmo de Calificacion

- **Asimetria en la Penalizacion:** Las afirmaciones clasificadas como "enganosas" (verdades a medias, omision de contexto, manipulacion de datos) representan el vector principal de la desinformacion moderna. La logica del puntaje debe penalizar de forma logaritmica las mentiras y enganosos, de modo que una sola mentira grave impacte el score mas que multiples verdades triviales.<sup>28</sup>
- **Clasificacion de Insuficiencia:** Si el agente no encuentra una verificacion periodistica previa exacta, no debe forzar una deduccion probabilistica. Debe clasificar la afirmacion como "No Verificable" o "Datos Insuficientes", blindando la app contra el riesgo de difamar algoritmicamente a un candidato.

## 8. Marco Regulatorio, Privacidad y Jurisprudencia Colombiana

El despliegue de una tecnologia que captura voz de ciudadanos, la procesa mediante modelos de IA de terceros y emite juicios de valor automatizados sobre su credibilidad interactua frontalmente con un marco legal riguroso y en constante evolucion.

### 8.1 La Voz como Dato Biometrico Sensible

Bajo la Ley Estatutaria 1581 de 2012, la voz humana grabada y procesada puede adquirir la categoria de dato sensible, sometida a un estandar de escrutinio excepcionalmente alto.<sup>30</sup> El tratamiento de datos sensibles exige autorizacion previa, libre, expresa e informada del titular — facticamente imposible cuando un ciudadano graba a un politico en una tarima.

Sin embargo, el Articulo 10 de la Ley 1581 establece excepciones donde no es necesaria la autorizacion, incluyendo el tratamiento de "datos de naturaleza publica".<sup>31</sup> La jurisprudencia ha establecido que los funcionarios publicos y candidatos politicos ven reducido el ambito de proteccion de su derecho a la intimidad frente al interes general, la libertad de informacion y el control democratico. Los discursos en plazas publicas, debates televisados y declaraciones ante medios constituyen informacion de dominio publico.<sup>32</sup>

Por consiguiente, la captura transitoria de esa voz con fines de veeduria ciudadana se encuentra protegida bajo la libertad de expresion y la excepcion de datos publicos. No obstante, el almacenamiento persistente generaria obligaciones complejas frente a la SIC, lo que exige una arquitectura "sin estado" (stateless) para el audio: procesamiento efimero, envio a la API de inferencia, y destruccion inmediata tras el analisis.<sup>33</sup>

### 8.2 Transparencia Algoritmica y Decisiones Automatizadas

La Circular Externa 001 de 2025 de la SIC establece el derecho a la "transparencia en decisiones automatizadas": un titular afectado por una decision automatizada desfavorable posee el derecho a recibir una explicacion clara sobre los criterios que condujeron al resultado.<sup>34</sup>

Cuando el sistema asigna una etiqueta publica de "Mentira" a un candidato, afecta directamente los derechos a la honra y el buen nombre. Ante una accion de tutela constitucional, la entidad desarrolladora tiene la carga de la prueba y debe demostrar paso a paso el proceso deductivo.<sup>35</sup> Por esto, cada veredicto debe estar acompanado de justificacion textual y citacion hipervinculada a la fuente periodistica: esto es un escudo legal de responsabilidad, no solo una buena practica de UI.

### 8.3 Ley 2502 de 2025: Tipificacion del Deepfake

La Ley 2502 de 2025 introduce reformas al Codigo Penal tipificando como delito la suplantacion de identidad mediante IA y estableciendo agravantes por la creacion de registros sonoros sinteticos que aparenten ser autenticos.<sup>36</sup> Si el modelo sufre una alucinacion y atribuye erroneamente una declaracion comprometedora a un candidato, la plataforma podria enfrentarse a demandas por calumnia y difamacion mediada algoritmicamente. La trazabilidad forense obliga a implementar disclaimers que certifiquen que la herramienta no certifica judicialmente la identidad del interlocutor.

### 8.4 Jurisprudencia sobre Rectificacion

La Corte Constitucional ha sido categorica respecto a la proteccion de derechos a la honra y rectificacion en plataformas digitales (Sentencias T-453/24, T-323/24, T-256/25).<sup>37</sup> Un fallo sistemico habilitara acciones de tutela por dano reputacional. La plataforma requiere una interfaz de apelacion directa (flagging) y protocolos de auditoria manual.

### 8.5 Legislacion Electoral

Las Resoluciones 215 y 216 de 2025 del CNE imponen regulaciones estrictas sobre la propaganda y divulgacion politica.<sup>38</sup> Si la app almacena y exhibe fragmentos de audio de mitines en formato publico, corre el riesgo de ser clasificada como canal no autorizado de propaganda extemporanea. La restriccion de grabacion corta y destruccion inmediata del audio es indispensable para blindar la plataforma.

## 9. Analisis de Viabilidad y Factibilidad de Despliegue

| Dimension | Nivel de Viabilidad | Nivel de Riesgo |
|---|---|---|
| **Transcripcion de audio en entornos ruidosos** | **Alta:** Modelos STT de nueva generacion reducen WER en 33% en ruido severo. Precision suficiente para fragmentos cortos de discurso politico. | **Medio:** Requiere umbral de confianza; audio inaudible debe marcarse como no verificable, no adivinarse. |
| **Extraccion de afirmaciones verificables** | **Alta:** Tool-calling estructurado permite separar retorica de datos factuales. Ventanas de contexto de 10 oraciones preservan semantica. | **Medio:** Discursos altamente retoricos o ironicos pueden generar falsos positivos en la extraccion. |
| **Verificacion via APIs (ClaimReview/Google FactCheck)** | **Alta:** Infraestructura madura (Schema.org, IFCN, ColombiaCheck). APIs publicas disponibles. | **Bajo:** Fuentes estructuradas y auditadas eliminan riesgo de contaminacion por SEO o blogs polarizados. |
| **Score de veracidad y rankings** | **Viable con precauciones:** Estrategia de retencion potente, pero requiere ponderacion logaritmica, no promedios simples. | **Medio:** Riesgo de dilucion de gravedad y percepcion de sesgo ideologico. |
| **Identificacion automatica del orador** | **Dificil:** Diarizacion acustica disponible pero propensa a errores en ambientes ruidosos multi-hablante. | **Critico:** Atribucion erronea de declaraciones a un politico constituye riesgo legal directo (Ley 2502/2025). |
| **Almacenamiento persistente de audio** | **Inviable legalmente:** Genera obligaciones de registro ante la SIC y riesgo bajo Ley 2502. | **Riesgo Alto:** Procesamiento efimero y destruccion inmediata es la unica via legalmente robusta. |

## 10. Requisitos Minimos para la Factibilidad Defendible

Para que el producto pueda ser desplegado sin incurrir en contingencias legales o crisis reputacionales en el horizonte electoral de 2026, su diseno debe integrar los siguientes requisitos:

**I. Externalizacion del Riesgo Epistemico (RAG y ClaimReview)**
El bucle agentico bajo ninguna circunstancia debe depender del conocimiento parametrico del LLM para formular juicios de veracidad. La arquitectura debe estructurarse obligatoriamente alrededor de llamadas a herramientas dirigidas a la Google FactCheck Claim Search API, consumiendo metadatos ClaimReview de entidades con aval metodologico (ColombiaCheck, La Silla Vacia). El agente funciona como traductor y formateador, no como generador de verdades.<sup>21</sup>

**II. Trazabilidad Total y Auditabilidad**
Cada veredicto debe estar vinculado a una fuente periodistica verificable con URL directa. Cada paso del agente debe registrarse en logs inmutables. Esta trazabilidad demuestra ante reguladores que el sistema es agnostico, objetivo y auditable — un escudo legal imprescindible frente a la SIC y las acciones de tutela constitucional.<sup>34</sup>

**III. Procesamiento Efimero de Audio**
Los archivos de audio deben ser procesados de manera transitoria y destruidos inmediatamente tras la inferencia. La arquitectura "sin estado" para datos biometricos garantiza cumplimiento con los principios de minimizacion de datos y finalidad temporal exigidos por la Circular 001/2025 y la Ley 1581.<sup>33</sup>

**IV. Algoritmia Etica del Score**
El algoritmo de calificacion debe abandonar promedios aritmeticos simples y aplicar penalizaciones asimetricas, ponderando logaritmicamente las afirmaciones falsas y enganosas. Si no existe verificacion previa exacta, el sistema debe clasificar como "No Verificable" en lugar de forzar una deduccion probabilistica.<sup>28</sup>

**V. Enrutamiento de Modelos para Sostenibilidad**
Para equilibrar costos operativos y latencia, el sistema debe implementar enrutamiento condicional: modelos ligeros para triage rapido, modelos pesados solo para extraccion compleja y sintesis final. Proyecciones para 50,000 llamadas mensuales estiman costos entre $200 y $800 dolares con arquitectura optimizada.<sup>27</sup>

**VI. Diseno Psicologicamente Informado**
La interfaz debe adoptar neutralidad expositiva, prominencia de fuentes periodisticas, inoculacion cognitiva previa, y posicionamiento como "asistente de investigacion", no como "juez". El objetivo es mitigar la reactancia psicologica y el rechazo partidista documentado en la literatura cientifica.<sup>18</sup>

En conclusion, el ecosistema algoritmico delineado tiene el potencial de transformarse en un contrapeso estructural a la desinformacion masiva. Su trascendencia no estara dictada exclusivamente por la sofisticacion del codigo, sino por su capacidad estrategica para operar de manera sostenible, navegar la psicologia humana fracturada por el tribalismo, y blindar su integridad bajo los dictamenes del Estado de Derecho. En la era de la IA generativa, defender la integridad institucional requiere enfrentar algoritmos ofuscadores con algoritmos auditores.

---

#### Obras citadas

1. The Velocity of Disinformation: 2026 Impact Report - Signal AI, fecha de acceso: marzo 3, 2026, [https://signal-ai.com/insights/resource/the-velocity-of-disinformation-2026-impact-report/](https://signal-ai.com/insights/resource/the-velocity-of-disinformation-2026-impact-report/)
2. Full Fact AI - AI-Powered Fact Checking Tools, fecha de acceso: marzo 3, 2026, [https://fullfact.ai/](https://fullfact.ai/)
3. Fact Check (ClaimReview) Markup for Search | Google Search Central, fecha de acceso: marzo 3, 2026, [https://developers.google.com/search/docs/appearance/structured-data/factcheck](https://developers.google.com/search/docs/appearance/structured-data/factcheck)
4. ColombiaCheck | Toolkit - Hive Mind, fecha de acceso: marzo 3, 2026, [https://en.hive-mind.community/tools/36,colombia-check](https://en.hive-mind.community/tools/36,colombia-check)
5. Colombia | Reuters Institute for the Study of Journalism, fecha de acceso: marzo 3, 2026, [https://reutersinstitute.politics.ox.ac.uk/digital-news-report/2025/colombia](https://reutersinstitute.politics.ox.ac.uk/digital-news-report/2025/colombia)
6. WhatsApp y desinformacion | Parte II - ColombiaCheck, fecha de acceso: marzo 3, 2026, [https://colombiacheck.com/chequeos/desinformacion-en-whatsapp-parte-ii](https://colombiacheck.com/chequeos/desinformacion-en-whatsapp-parte-ii)
7. Full Fact Report 2025, fecha de acceso: marzo 3, 2026, [https://fullfact.org/policy/reports/full-fact-report-2025/](https://fullfact.org/policy/reports/full-fact-report-2025/)
8. The UK's fact-checkers are sending their AI to help Americans cover elections - Poynter, fecha de acceso: marzo 3, 2026, [https://www.poynter.org/fact-checking/2025/the-uks-fact-checkers-are-sending-their-ai-to-help-americans-cover-elections/](https://www.poynter.org/fact-checking/2025/the-uks-fact-checkers-are-sending-their-ai-to-help-americans-cover-elections/)
9. Projects - Full Fact AI, fecha de acceso: marzo 3, 2026, [https://fullfact.ai/projects/](https://fullfact.ai/projects/)
10. Factiverse Live, fecha de acceso: marzo 3, 2026, [https://www.factiverse.ai/solutions/live](https://www.factiverse.ai/solutions/live)
11. Factiverse | Extract insights and mitigate organisational risks, fecha de acceso: marzo 3, 2026, [https://www.factiverse.ai/](https://www.factiverse.ai/)
12. Online Media | Factiverse Industry Cases, fecha de acceso: marzo 3, 2026, [https://www.factiverse.ai/industry-cases-media/online-media](https://www.factiverse.ai/industry-cases-media/online-media)
13. What's new in Azure OpenAI in Azure AI Foundry Models, fecha de acceso: marzo 3, 2026, [https://learn.microsoft.com/en-us/azure/foundry-classic/openai/whats-new](https://learn.microsoft.com/en-us/azure/foundry-classic/openai/whats-new)
14. OpenAI.fm: Ultimate Guide to OpenAI's Latest AI Voice Models - Monica, fecha de acceso: marzo 3, 2026, [https://monica.im/blog/openai-fm-text-to-speech-tts/](https://monica.im/blog/openai-fm-text-to-speech-tts/)
15. Claimify: Extracting high-quality claims from language model outputs - Microsoft Research, fecha de acceso: marzo 3, 2026, [https://www.microsoft.com/en-us/research/blog/claimify-extracting-high-quality-claims-from-language-model-outputs/](https://www.microsoft.com/en-us/research/blog/claimify-extracting-high-quality-claims-from-language-model-outputs/)
16. Optimising window size of semantic classification model for identification of in-text citations - PLOS One, fecha de acceso: marzo 3, 2026, [https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0309862](https://journals.plos.org/plosone/article?id=10.1371/journal.pone.0309862)
17. Un estudio revela que casi el 25% de las falsedades politicas se repiten pese al fact-checking - Laboratorio de Periodismo, fecha de acceso: marzo 3, 2026, [https://laboratoriodeperiodismo.org/un-estudio-revela-que-casi-el-25-de-las-falsedades-politicas-se-repiten-pese-al-fact-checking/](https://laboratoriodeperiodismo.org/un-estudio-revela-que-casi-el-25-de-las-falsedades-politicas-se-repiten-pese-al-fact-checking/)
18. Partisanship sways news consumers more than the truth - Stanford Report, fecha de acceso: marzo 3, 2026, [https://news.stanford.edu/stories/2024/10/new-study-shows-that-partisanship-trumps-truth](https://news.stanford.edu/stories/2024/10/new-study-shows-that-partisanship-trumps-truth)
19. The backfire effect after correcting misinformation is strongly associated with reliability - PMC, fecha de acceso: marzo 3, 2026, [https://pmc.ncbi.nlm.nih.gov/articles/PMC9283209/](https://pmc.ncbi.nlm.nih.gov/articles/PMC9283209/)
20. Fact-Checking News Use and Political Misperception - ResearchGate, fecha de acceso: marzo 3, 2026, [https://www.researchgate.net/publication/393915319](https://www.researchgate.net/publication/393915319)
21. ClaimReview - Schema.org Type, fecha de acceso: marzo 3, 2026, [https://schema.org/ClaimReview](https://schema.org/ClaimReview)
22. An API based on Claim Review - Full Fact GitHub, fecha de acceso: marzo 3, 2026, [https://fullfact.github.io/markup-investigation/docs/notes/06-claim-review-api-design/](https://fullfact.github.io/markup-investigation/docs/notes/06-claim-review-api-design/)
23. Fact Check Tools API - Google for Developers, fecha de acceso: marzo 3, 2026, [https://developers.google.com/fact-check/tools/api](https://developers.google.com/fact-check/tools/api)
24. Worse than Zero Shot? A Fact-Checking Dataset for Evaluating the Robustness of RAG Against Misleading Retrievals - arXiv, fecha de acceso: marzo 3, 2026, [https://arxiv.org/pdf/2502.16101](https://arxiv.org/pdf/2502.16101)
25. DANE - Departamento Administrativo Nacional de Estadistica, fecha de acceso: marzo 3, 2026, [https://www.dane.gov.co/](https://www.dane.gov.co/)
26. Both Ends Count! Just How Good are LLM Agents at Text-to-"Big SQL"? - arXiv, fecha de acceso: marzo 3, 2026, [https://arxiv.org/html/2602.21480v2](https://arxiv.org/html/2602.21480v2)
27. 50,000 LLM Calls Cost Less Than You Think: A 2026 Pricing Reality Check - Inkeep, fecha de acceso: marzo 3, 2026, [https://inkeep.com/blog/50-000-llm-calls-cost-less-than-you-think-a-2026-pricing-rea](https://inkeep.com/blog/50-000-llm-calls-cost-less-than-you-think-a-2026-pricing-rea)
28. AI in the Age of Fake (Imagined) Content - Stimson Center, fecha de acceso: marzo 3, 2026, [https://www.stimson.org/2026/ai-in-the-age-of-fake-imagined-content/](https://www.stimson.org/2026/ai-in-the-age-of-fake-imagined-content/)
29. Cross-checking journalistic fact-checkers - PMC, fecha de acceso: marzo 3, 2026, [https://pmc.ncbi.nlm.nih.gov/articles/PMC10368232/](https://pmc.ncbi.nlm.nih.gov/articles/PMC10368232/)
30. Ley 1581 de 2012 - Funcion Publica, fecha de acceso: marzo 3, 2026, [https://www.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=49981](https://www.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=49981)
31. LEY 1581 DE 2012 - SUIN-Juriscol, fecha de acceso: marzo 3, 2026, [https://www.suin-juriscol.gov.co/viewDocument.asp?ruta=Leyes/1684507](https://www.suin-juriscol.gov.co/viewDocument.asp?ruta=Leyes/1684507)
32. El contexto actual del derecho de la imagen en Colombia - U. Externado, fecha de acceso: marzo 3, 2026, [https://revistas.uexternado.edu.co/index.php/propin/article/view/4602/5519](https://revistas.uexternado.edu.co/index.php/propin/article/view/4602/5519)
33. SIC, Externa No. 001 de 2025, 19-sep-2025 - Centro de Estudios Regulatorios, fecha de acceso: marzo 3, 2026, [https://www.cerlatam.com/normatividad/sic-externa-no-001-de-2025-19-sep-2025/](https://www.cerlatam.com/normatividad/sic-externa-no-001-de-2025-19-sep-2025/)
34. La Superintendencia de Industria y Comercio emite instrucciones sobre el tratamiento de datos personales en el sector fintech, fecha de acceso: marzo 3, 2026, [https://sedeelectronica.sic.gov.co/noticias/la-superintendencia-de-industria-y-comercio-emite-instrucciones-sobre-el-tratamiento-de-datos-personales-en-el-sector-fintech](https://sedeelectronica.sic.gov.co/noticias/la-superintendencia-de-industria-y-comercio-emite-instrucciones-sobre-el-tratamiento-de-datos-personales-en-el-sector-fintech)
35. Proteccion de datos en Colombia: sanciones, nuevas reglas de la SIC e impacto de la IA - Holland & Knight, fecha de acceso: marzo 3, 2026, [https://www.hklaw.com/es/news/intheheadlines/2025/08/data-protection-in-colombia-sanctions-new-sic-rules](https://www.hklaw.com/es/news/intheheadlines/2025/08/data-protection-in-colombia-sanctions-new-sic-rules)
36. Ley 2502 de 2025 - Alcaldia Mayor de Bogota, fecha de acceso: marzo 3, 2026, [https://www.alcaldiabogota.gov.co/sisjur/normas/Norma1.jsp?i=188454](https://www.alcaldiabogota.gov.co/sisjur/normas/Norma1.jsp?i=188454)
37. Sentencia T-453 de 2024 - Corte Constitucional, fecha de acceso: marzo 3, 2026, [https://www.corteconstitucional.gov.co/relatoria/2024/t-453-24.htm](https://www.corteconstitucional.gov.co/relatoria/2024/t-453-24.htm)
38. Resolucion 215 de 2025 Consejo Nacional Electoral, fecha de acceso: marzo 3, 2026, [https://www.alcaldiabogota.gov.co/sisjur/normas/Norma1.jsp?i=190897&dt=S](https://www.alcaldiabogota.gov.co/sisjur/normas/Norma1.jsp?i=190897&dt=S)
39. Registraduria, CRC, MOE y Colombiacheck anunciaron alianza para combatir la desinformacion - MOE, fecha de acceso: marzo 3, 2026, [https://moe.org.co/en/registraduria-crc-moe-y-colombiacheck-anunciaron-alianza-para-combatir-la-desinformacion-en-las-elecciones-de-2026-via-ifm-noticias/](https://moe.org.co/en/registraduria-crc-moe-y-colombiacheck-anunciaron-alianza-para-combatir-la-desinformacion-en-las-elecciones-de-2026-via-ifm-noticias/)
40. Elecciones legislativas de Colombia de 2026 - Wikipedia, fecha de acceso: marzo 3, 2026, [https://es.wikipedia.org/wiki/Elecciones_legislativas_de_Colombia_de_2026](https://es.wikipedia.org/wiki/Elecciones_legislativas_de_Colombia_de_2026)
41. Industrialized Deception: The Collateral Effects of LLM-Generated Misinformation - arXiv, fecha de acceso: marzo 3, 2026, [https://arxiv.org/html/2601.21963v2](https://arxiv.org/html/2601.21963v2)
42. Introducing next-generation audio models in the API - OpenAI, fecha de acceso: marzo 3, 2026, [https://openai.com/index/introducing-our-next-generation-audio-models/](https://openai.com/index/introducing-our-next-generation-audio-models/)
43. AI-driven disinformation: policy recommendations for democratic resilience - PMC, fecha de acceso: marzo 3, 2026, [https://pmc.ncbi.nlm.nih.gov/articles/PMC12351547/](https://pmc.ncbi.nlm.nih.gov/articles/PMC12351547/)
44. Datos Abiertos Colombia, fecha de acceso: marzo 3, 2026, [https://www.datos.gov.co/](https://www.datos.gov.co/)
45. LATAM-GPT and the Rise of Regional AI - Medium, fecha de acceso: marzo 3, 2026, [https://medium.com/@delimiterbob/latam-gpt-and-the-rise-of-regional-ai-3b9fbc51a35b](https://medium.com/@delimiterbob/latam-gpt-and-the-rise-of-regional-ai-3b9fbc51a35b)
46. Suplantar identidad con IA ya es delito en Colombia - U. Central, fecha de acceso: marzo 3, 2026, [https://www.ucentral.edu.co/noticentral/suplantar-identidad-ia-ya-es-delito-colombia-asi-se-sancionara](https://www.ucentral.edu.co/noticentral/suplantar-identidad-ia-ya-es-delito-colombia-asi-se-sancionara)
47. Corte Constitucional emite sentencia sobre derecho al buen nombre en redes sociales - Fenalco, fecha de acceso: marzo 3, 2026, [https://www.fenalco.com.co/blog/juridico-2/corte-constitucional-emite-sentencia-sobre-derecho-al-buen-nombre-en-las-redes-sociales-269](https://www.fenalco.com.co/blog/juridico-2/corte-constitucional-emite-sentencia-sobre-derecho-al-buen-nombre-en-las-redes-sociales-269)
48. The Full Price Tag: What AI Agents Actually Cost - ProSkale, fecha de acceso: marzo 3, 2026, [https://proskale.com/the-full-price-tag-what-ai-agents-actually-cost-and-what-the-quote-wont-tell-you/](https://proskale.com/the-full-price-tag-what-ai-agents-actually-cost-and-what-the-quote-wont-tell-you/)
