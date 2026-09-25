# Caso de Estudio Capstone: Gobernanza de IA en el Sector de Salud Pública

**Curso:** Gobierno e Implementación de Sistemas de Gestión de IA basados en la Norma ISO/IEC 42001  
**Entidad Objeto de Estudio:** Ente Rector del Sector Salud (Organismo Público de Nivel Nacional)  
**Propósito:** Evaluar y diseñar la transición desde un entorno desgobernado (*As-Is*) hacia un Sistema de Gestión de Inteligencia Artificial (*To-Be*) alineado con estándares internacionales.

---

## 0. Fundamentos del Caso: Tipos de IA y Niveles de Autonomía

Para comprender el impacto del caso sin necesidad de formación técnica previa, es mandatorio dominar dos principios de diseño organizacional:

### Dimensión 1: El Tipo de Tareas que Ejecuta la IA
Las tres tipologías de Inteligencia Artificial conviven en una misma organización para propósitos distintos, y cada una exige controles específicos bajo un SGIA:
*   **IA Predictiva:** Analiza datos históricos para proyectar una probabilidad o un valor numérico. No genera texto ni mantiene conversaciones. *Ejemplo:* Estimar el riesgo de fraude en un reclamo.
*   **IA Generativa:** Produce contenido nuevo (resúmenes, documentos, imágenes) a partir de una instrucción (*prompt*). No toma decisiones ejecutivas autónomas. *Ejemplo:* Sintetizar un expediente clínico extenso.
*   **IA Agéntica:** Persigue un objetivo de alto nivel interactuando de manera autónoma con múltiples herramientas y entornos, decidiendo por sí misma los pasos intermedios. *Ejemplo:* Buscar pólizas, cruzar registros médicos y preparar recomendaciones analíticas complejas.

### Dimensión 2: El Nivel de Autonomía Delegado
El riesgo sistémico no reside en la tecnología utilizada, sino en el nivel de autonomía operativa que se le otorga. La norma **ISO/IEC 22989** define el vocabulario normativo del curso para el involucramiento humano:
*   **Human-in-the-loop (HITL):** La IA no puede actuar sin que un humano participe y valide cada decisión intermedia.
*   **Human-on-the-loop (HOTL):** La IA opera de forma autónoma pero bajo la supervisión activa de un humano con capacidad de intervenir y vetar el proceso.
*   **Human-in-command (HIC):** El humano mantiene la autoridad general sobre el ecosistema completo del sistema, controlando sus políticas rectoras.

A nivel pedagógico, para dotar de mayor granularidad a la auditoría, este caso implementa una escala complementaria de seis niveles (L1-L6), basada en la literatura de gobernanza empresarial (*Enterprise AI autonomy-levels framework, MDPI Information 17(7):646*):

| Nivel Pedagógico | Rol de la IA | Rol del Humano | Equivalente ISO/IEC 22989 |
| :--- | :--- | :--- | :--- |
| **L1 · Asistiva** | Provee información o análisis base | Ejecuta la acción final | Human-in-the-loop |
| **L2 · Consultiva** | Recomienda y ordena opciones | Decide y selecciona entre ellas | Human-in-the-loop |
| **L3 · Supervisada** | Toma la decisión técnica | Aprueba explícitamente antes de ejecutar | Human-in-the-loop (Límite crítico) |
| **L4 · Delegada** | Actúa sola dentro de reglas fijas | Monitorea de forma reactiva e interviene | Human-on-the-loop |
| **L5 · Autónoma** | Opera sin intervención en tiempo real | Fija los objetivos de antemano | Fuera de las 3 categorías estándar |
| **L6 · Orquestada** | Múltiples IA coordinadas entre sí | Gobierna el conjunto del ecosistema | Se aproxima a Human-in-command |

---

## 1. Contexto de la Organización

El **Ente Rector del Sector Salud** es una entidad del Poder Ejecutivo encargada de normar, conducir y fiscalizar la política nacional de salud pública. Su misión institucional es garantizar el acceso universal a la salud, la prevención de enfermedades y la gestión eficiente de los recursos médicos a nivel nacional.

La entidad interactúa diariamente con un ecosistema masivo, altamente fragmentado y descentralizado: hospitales públicos, redes de aseguramiento estatal, institutos especializados, clínicas privadas y registros de identidad ciudadana. Su principal desafío operativo es la **interoperabilidad semántica**: procesar, consolidar y auditar millones de Historias Clínicas Electrónicas (HCE), reportes de facturación, solicitudes de cobertura de seguros y registros de vigilancia epidemiológica que ingresan en formatos heterogéneos, no estructurados y de forma masiva.

---

## 2. Situación Actual / El Escenario AS-IS (El Problema)

Ante la intensa presión social y de mercado por acelerar la transformación digital, diversas direcciones generales comenzaron a desplegar soluciones de Inteligencia Artificial de forma aislada, autónoma y sin una gobernanza centralizada. Este fenómeno ha provocado la proliferación de **"Shadow Agents" (Agentes de IA en la sombra)** a lo largo de la institución:

*   **Fragmentación Operativa y Tecnológica:** La Oficina de Seguros Médicos programó scripts basados en modelos de lenguaje comerciales (LLMs) para automatizar la auditoría de reclamos. En paralelo, la Dirección de Epidemiología desplegó agentes de código abierto para extraer datos de brotes infecciosos desde textos libres provistos por hospitales regionales. Cada célula maneja sus propios contratos, prompts del sistema y conexiones API de manera independiente.
*   **Riesgo Crítico de Alucinación y Fallas Algorítmicas:** Al no existir un control o filtro central, los agentes de IA toman decisiones directas sobre datos sensibles. Se han detectado casos donde la IA altera o "alucina" diagnósticos oncológicos al resumir historias clínicas mal redactadas, o aprueba/rechaza financiamientos médicos basándose en lógicas erróneas. Al tratarse de un sector regulado, estas fallas exponen a la institución a severas contingencias legales, violaciones éticas y daños irreparables a la salud pública.
*   **Dispersión de Costos e Ineficiencia de Recursos:** La falta de una capacidad centralizada de enrutamiento provoca que consultas sencillas de texto (que podrían resolverse con modelos locales, pequeños y económicos) sean enviadas a APIs comerciales de costo elevado, disparando el gasto presupuestal de la entidad en más de un **300% de manera redundante**.
*   **Inexistencia de Evidencias e Incumplimiento Normativo:** La entidad no cuenta con un repositorio centralizado e inmutable de logs. Las decisiones que toman las IAs y la procedencia de los datos utilizados (*data lineage*) se guardan en archivos de texto planos locales en servidores dispersos, los cuales pueden ser modificados o borrados. Esto coloca a la institución en situación de incumplimiento total ante las fiscalizaciones de las **Autoridades Nacionales de Transformación Digital, Gobierno Digital y Protección de Datos Personales**, imposibilitando cualquier intento de certificar la norma **ISO/IEC 42001**.

### Diagnóstico desde la Perspectiva de la Autonomía
El fallo raíz de la organización no se debió al uso de tecnologías avanzadas, sino a la falta de definición y control de sus niveles de autonomía:
1.  **Caso A (Seguros):** Diseñado originalmente para operar en **L2 (Consultiva)**, escaló de facto a **L4 (Delegada)**, emitiendo aprobaciones y rechazos automáticos sin el consentimiento documentado de los auditores humanos.
2.  **Caso B (Resumen Clínico):** Concebido como una herramienta **L1 (Asistiva)**, el personal médico comenzó a leer y firmar los resúmenes sin contrastarlos con el expediente base, operando en la práctica como un **L3 (Supervisada)** no controlado.
3.  **Caso C (Epidemiología):** Desplegó capacidades agénticas complejas sin una delimitación de su perímetro instructivo, imposibilitando distinguir qué alertas sanitarias requería escalamiento inmediato a la dirección.

---

## 3. Justificación de la Propuesta de Solución TARGET (El To-Be)

Para erradicar el caos de los *Shadow Agents*, mitigar los riesgos de salud pública y garantizar el cumplimiento estricto del marco normativo nacional e internacional, la entidad ha determinado diseñar e implementar un **Sistema de Gestión de IA (SGIA)** bajo la norma **ISO/IEC 42001**.

La ingeniería del gobierno y su diseño operativo eficiente se materializan a través de un marco de diseño por **Abstracción Arquitectónica**. Este modelo consolida la antigua infraestructura dispersa en una jerarquía de **4 Capas Operativas orientadas a Capacidades y 1 Capa Transversal de Gobernanza Estricta**.

### Justificación de Ingeniería: ¿Cuándo se necesita un Agente frente a un Modelo Único?
Para optimizar recursos bajo ISO 42001 (Control de Costos y Eficiencia Sistemática), la arquitectura evalúa y clasifica la necesidad tecnológica según la complejidad del objetivo:
*   **Modelo Único (Predictivo o Generativo Puro):** Se utiliza cuando la tarea es lineal, atómica y su entrada está perfectamente estructurada o acotada. Se procesa en una sola iteración (*Single-shot interaction*), como clasificar un reclamo o resumir un bloque fijo de texto. No requiere planeación ni acceso dinámico a múltiples entornos externos.
*   **Sistema Agéntico (Multi-step Agentic System):** Es estrictamente obligatorio para tareas complejas y no lineales, como la Vigilancia Epidemiológica. Se justifica cuando el sistema persigue un **objetivo de alto nivel** donde los pasos intermedios no se pueden predefinir de forma estática. El agente requiere **autonomía iterativa** para ejecutar un ciclo de *Razonamiento → Acción → Observación*, interactuando dinámicamente con múltiples fuentes externas (Hospitales, Identidad, Aseguradoras) y adaptando su estrategia según las respuestas de su entorno.

---

## 4. Especificación Operativa del Modelo de Capas y Capacidades
![Arquitectura de IA Gobernada - ISO 42001] (arquitectura ia iso 42001.png)
La arquitectura se compone de los siguientes paquetes de funcionalidad encapsulados, asegurando que no existan brechas operacionales respecto a modelos de infraestructura previos, pero reduciendo radicalmente la carga cognitiva de la organización:

### 🏛️ Capa Transversal: Políticas Inyectadas y Gobernanza Operacional
*   **Capacidades:** Control de presupuesto financiero en tiempo real (límites de tokens/costo por invocación), *Guardrails* globales de seguridad, y la inyección de políticas organizacionales inviolables.
*   **Rol en el SGIA:** Actúa como una fuerza ortogonal que intercepta el ciclo de vida completo de cada consulta, bloqueando ejecuciones anómalas antes de que generen gastos o riesgos.

### 📦 Capa 1: Sistema de Contexto Acotado (Context Window Optimization)
*   **Capacidades:** Empaquetado de datos en contenedores de mínima exposición (*Paquetes de Contexto PC-nnn*), inyección por anclas de datos estructurados históricos y aislamiento del corpus gobernado de salud.
*   **Rol en el SGIA:** Reduce de forma proactiva la carga cognitiva del modelo, asegurando que solo ingrese información verídica y autorizada.

### 🧠 Capa 2: Núcleo de Razonamiento del Agente (Reasoning Core & Skills)
*   **Capacidades:** Orquestadores de flujos de IA, enrutador inteligente de modelos (derivando tareas simples a LLMs locales económicos y tareas complejas a modelos avanzados), y pasarelas estandarizadas bajo **Model Context Protocol (MCP)**.
*   **Rol en el SGIA:** Ejecuta el procesamiento predictivo, generativo o agéntico dentro de una celda controlada y desprovista de acceso directo libre a la red.

### ⚖️ Capa 3: Motor de Verificación Determinista (Deterministic Guardrails)
*   **Capacidades:** Validador matemático del grafo lógico de dependencias, evaluación sintáctica/semántica bajo reglas estrictas de negocio (*"Cuando → Entonces → Efecto"*) y generación inmutable de evidencias (Logs criptográficos).
*   **Rol en el SGIA:** Evalúa el output probabilístico del agente con código tradicional 100% auditable antes de permitir que la respuesta sea entregada a producción o al usuario.

### 👤 Capa 4: Interfaz de Gobernanza Operacional (Human-in-the-Loop - HITL)
*   **Capacidades:** Orquestación de la cola de excepciones humanas (`H-nnn`), consolas de auditoría clínica interactiva y captura de decisiones vinculantes del personal de salud.
*   **Rol en el SGIA:** Facilita el gobierno por excepción, garantizando que el control humano definitivo (*Human-on-the-loop* o *Human-in-the-loop*) se mantenga intacto según el nivel de autonomía asignado.

---

## 5. Mitigación de Riesgos en Tiempo de Ejecución (Los 3 Casos del SGIA)

La Capa Transversal mapea y restringe el comportamiento de los tres sistemas del caso Capstone, desactivando los desbordamientos de autonomía observados en el escenario *AS-IS*:

*   **Resolución del Caso A (Predictivo - Fraude en Seguros) ➔ Forzado en L2 (Consultiva):** La Capa Transversal detecta que el sistema es de nivel L2. La Capa 2 calcula la probabilidad de fraude, la Capa 3 verifica que no contenga código malicioso y, al llegar a la Capa 4, la arquitectura **bloquea cualquier despacho automático**. El resultado es inyectado exclusivamente como una sugerencia informativa en la pantalla del auditor de seguros humano.
*   **Resolución del Caso B (Generativo - Resúmenes Clínicos) ➔ Forzado en L1 (Asistiva):** El sistema procesa la HCE en las Capas 1 y 2. Al llegar a la Capa 3, el validador del grafo lógico contrasta semánticamente el resumen frente al historial médico original. Al detectar una discrepancia o la omisión/alucinación de un diagnóstico crítico (como una condición oncológica), el motor frena el flujo de forma determinista. Se estampa una marca de agua restrictiva y se despacha a la cola HITL del médico, impidiendo que el error impacte al paciente.
*   **Resolución del Caso C (Agéntico - Vigilancia Epidemiológica) ➔ Regulado en L4 (Delegada):** El agente de la Capa 2 coordina múltiples consultas dinámicas utilizando herramientas autenticadas con **MCP**. Si el agente, al procesar los datos de un brote, intenta declarar de forma autónoma una alerta sanitaria de cuarentena en una región, el motor de la Capa 3 identifica que dicha acción excede el rol L4 autorizado. El sistema clasifica el evento como **Fuera de Perímetro**, congela el presupuesto de tokens a través de la Capa Transversal y escala la decisión final al Director de Vigilancia Sanitaria en la Capa 4.

---

## 6. Fuentes Autoritativas y Sustento Científico

*   **Mitigación de la Carga Cognitiva:** Liu, N. F., Lin, K., Hewitt, J., Paranjape, A., Bevilacqua, M., Liang, P., & Potts, C. (Stanford University / UC Berkeley). *“Lost in the Middle: How Language Models Use Long Contexts”*.
*   **Arquitectura de Sistemas Agénticos y Guardrails:** Koenigstein, N. (O'Reilly Media). *“AI Agents: The Definitive Guide”*.
*   **Escala de Autonomía Empresarial:** *“Enterprise AI autonomy-levels framework”*, MDPI Information 17(7):646.
*   **Marcos Normativos Internacionales:** ISO/IEC 42001:2023 (SGIA) e ISO/IEC 22989 (Conceptos e Infraestructura de IA).

