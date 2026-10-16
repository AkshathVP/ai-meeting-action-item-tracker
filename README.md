# GraphRAG Item Extractor

An asynchronous Retrieval-Augmented Generation (GraphRAG) system built with **Python**, **Llama 3.3**, and **NetworkX**. Designed to extract structured action items, assignees, dependencies, and relationships from raw meeting transcripts to support meeting follow-up and reporting.

##  Key Architectural Achievements & Metrics
- Built an asynchronous Python pipeline that ingests batches of raw meeting transcripts and transforms unstructured meeting text into structured, consistently formatted records for further processing.
**High-Speed Async Ingestion:** Built using `asyncio` and Groq's high-speed inference API (`Llama-3.3-70b-versatile`),
- Applied Pydantic schema validation to enforce data integrity and data quality before graph construction, and modeled relationships between entities to track ownership and dependencies across meeting action items.
* * Combines TF-IDF similarity retrieval with **NetworkX** graph context for hybrid retrieval.
- Produced interactive visualizations with PyVis to represent the constructed relationships, enabling reporting on blockers and task status while supporting data-driven decision-making.
---

##  Tech Stack
* **LLM & Inference:** Groq API (`llama-3.3-70b-versatile`), AsyncGroq
* **Graph Architecture:** NetworkX, PyVis (HTML interactive graphs)
* **Data Validation:** Pydantic (Structured JSON parsing)
* **Retrieval:** scikit-learn (TF-IDF Vectorization and Cosine Similarity)
* **Async Concurrency:** Python `asyncio`



---

## 📦 Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/AkshathVP/graphrag-item-extractor.git
   cd graphrag-item-extractor
