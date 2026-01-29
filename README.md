# Procesamiento del Lenguaje Natural - Trabajo Final — RAG y agentes aplicados a *Cascadia*

## Descripción general
Este proyecto académico se centra en **técnicas de NLP aplicadas**, con énfasis en **RAG**, **agentes inteligentes** y **recuperación de información**, utilizando al juego *Cascadia* como dominio temático. Se integran **bases de datos de grafos**, **tabulares** y **vectoriales**, junto con modelos de lenguaje para **búsqueda semántica**, **clasificación de intención** y **orquestación de herramientas**. El objetivo es demostrar un pipeline completo de adquisición de información, organización estructural, recuperación y razonamiento sobre conocimiento textual diverso.

La implementación principal está contenida en un *notebook* con experimentos y evaluación de resultados, acompañado por un informe en PDF y el conjunto de datos preparados en texto y CSV. El foco es **comparar y validar técnicas de NLP** (búsqueda semántica, híbrida, reranking, clasificación e inferencia con LLMs) sobre un corpus del dominio, mostrando cómo estas piezas se combinan en soluciones de RAG y agentes.

## Alcance y contenido principal
El contenido del proyecto se organiza en los siguientes bloques:

### 1) Base de datos de grafos (conocimiento relacional)
- **Construcción de un grafo** con entidades y relaciones a partir de un archivo de triples (sujeto–relación–objeto). El grafo representa vínculos entre el juego, diseñadores, expansiones y conceptos relacionados.
- **Persistencia en Neo4j** mediante `py2neo`, con **visualización** y **consultas** básicas para explorar relaciones semánticas.
- **Apoyo exploratorio** mediante `networkx` y `matplotlib` para entender la estructura del grafo.

### 2) Base de datos tabular (estadística descriptiva)
- **Carga de estadísticas** asociadas al juego (por ejemplo: categorías, ratings y métricas globales) desde archivos CSV.
- **Consultas y resumen** de datos para describir el contexto cuantitativo del juego y sus características agregadas.

### 3) Base de datos vectorial (información textual y búsqueda semántica)
- **Limpieza y normalización** del texto.
- **Segmentación en chunks** y generación de **embeddings** con `SentenceTransformer`.
- **Construcción y persistencia de una colección en ChromaDB** para recuperar información mediante similitud semántica.
- **Búsqueda híbrida** combinando embeddings + BM25 (`rank_bm25`), con comparación de relevancia y diversidad.

### 4) Re-ranking de resultados
- **Reranking con cross-encoder** usando `FlagEmbedding` (modelo BGE) para reordenar candidatos.
- **Reranking con LLM** (Gemini) a partir de una política de selección basada en instrucción.

### 5) Clasificación de intención
- **Modelo clásico** con `LogisticRegression` + `TF-IDF` para clasificar preguntas.
- **Clasificador con LLM** (Gemini) para contrastar rendimiento, robustez y flexibilidad.

### 6) RAG (Retrieval-Augmented Generation)
- Implementación de un flujo **RAG** que combina: 
  - búsqueda híbrida,
  - reranking,
  - y generación de respuesta con un LLM.
- Se evalúan respuestas para consultas sobre reglas, objetivos del juego y mecánicas.

### 7) Agentes inteligentes con enfoque ReAct
- **Agente ReAct propio** (sin LangChain): planificación por pasos, uso de herramientas y justificación de acciones.
- **Agente con LangChain + Gemini** y herramientas externas (Wikipedia, búsqueda web) para consulta contextual.
- **Integración con Ollama** para el uso de modelos locales (ej. *phi-3*) como alternativa a modelos externos.

---

## Tecnologías y librerías principales
- **Python** como lenguaje base (ecosistema científico y de NLP).
- **Bases de datos y almacenamiento**: Neo4j + `py2neo`, ChromaDB.
- **Procesamiento y análisis**: `pandas`, `numpy`, `scikit-learn`, `langdetect`, `tqdm`.
- **NLP y embeddings**: `SentenceTransformer`, `TF-IDF`, `rank_bm25`.
- **LLMs y agentes**: Gemini (`google-genai`, `langchain_google_genai`), LangChain, Ollama.
- **Reranking**: `FlagEmbedding` (BGE reranker).
- **Búsqueda externa**: DuckDuckGo y Wikipedia (integradas como herramientas en agentes).

---

## Conjunto de datos y fuentes textuales
El corpus combina:
- **Reseñas de usuarios y críticas** de sitios especializados.
- **Manual y descripción oficial del juego**.
- **Datos tabulares de estadísticas y ratings**.
- **Relaciones estructuradas** para la construcción del grafo.

---

## Resultados
- Construcción de un **grafo semántico** funcional con relaciones verificables.
- Implementación de **búsqueda semántica e híbrida**, con comparación de precisión y cobertura.
- Evaluación de **reranking** con técnicas clásicas y LLMs.
- Comparación entre **clasificación tradicional y con LLMs** en tareas de intención.
- Integración de un pipeline **RAG completo**, demostrando utilidad para preguntas sobre mecánicas y reglas.
- Diseño de **agentes inteligentes** con herramientas externas, mostrando razonamiento paso a paso y acceso a fuentes complementarias.

---

## Entregables incluidos
- **Notebook principal** con todo el desarrollo experimental y las pruebas.
- **Informe final académico** y documentación complementaria en PDF.
- **Datos procesados** (textos, relaciones y estadísticas en CSV).
