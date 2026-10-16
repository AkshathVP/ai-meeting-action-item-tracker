# GraphRAG Item Extractor & Action Delegation Engine

An asynchronous Retrieval-Augmented Generation (GraphRAG) system built with **Python**, **Llama 3.3**, and **NetworkX**. Designed to automate cross-functional task delegation from raw meeting audio/transcripts and radically eliminate manual meeting follow-up overhead.

##  Key Architectural Achievements & Metrics
- Built an asynchronous Python pipeline that ingests batches of raw meeting transcripts and transforms unstructured meeting text into structured, consistently formatted records for further processing.
**High-Speed Async Ingestion:** Built using `asyncio` and Groq's high-speed inference API (`Llama-3.3-70b-versatile`),
- Applied Pydantic schema validation to enforce data integrity and data quality before graph construction, and modeled relationships between entities to track ownership and dependencies across meeting action items.
* Replaces standard flat vector search with a hybrid **NetworkX** knowledge graph.
- Produced interactive visualizations with PyVis to represent the constructed relationships, enabling reporting on blockers and task status while supporting data-driven decision-making.
---

##  Tech Stack
* **LLM & Inference:** Groq API (`llama-3.3-70b-versatile`), AsyncGroq
* **Graph Architecture:** NetworkX, PyVis (HTML interactive graphs)
* **Data Validation:** Pydantic (Structured JSON parsing)
* **Vector Search:** scikit-learn (TF-IDF Cosine Similarity for hybrid fallback)
* **Async Concurrency:** Python `asyncio`



---

## 📦 Installation & Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/AkshathVP/graphrag-item-extractor.git
   cd graphrag-item-extractor
