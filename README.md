# AI Meeting Action Item Tracker

A Python pipeline that extracts meeting action items, owners, deadlines, dependencies, and entity relationships from transcript text. It uses Groq's Llama 3.3 model for structured extraction, Pydantic for validation, TF-IDF for text retrieval, NetworkX for graph relationships, and PyVis to export an interactive knowledge graph.

## Features

- **Asynchronous transcript processing** with Groq's `llama-3.3-70b-versatile` model.
- **Structured extraction** of tasks, assignees, deadlines, statuses, entities, and relationships, validated with Pydantic models.
- **Hybrid retrieval prototype** combining TF-IDF cosine similarity with linked graph context.
- **Interactive graph export** to an HTML file using PyVis.
- **Fallback demonstration data** when no API key is configured or the transcript input is empty.

## Architecture & Workflow

1. **Input:** Read meeting transcripts from `data/sample_transcripts.json`.
2. **Extraction:** When `GROQ_API_KEY` is available and transcripts are present, send transcript text to Groq asynchronously for JSON-formatted extraction.
3. **Validation:** Parse the response into `MeetingExtraction`, `ActionItem`, `Entity`, and `Relationship` Pydantic models.
4. **Indexing:** Build a directed NetworkX graph and a TF-IDF index over action-item descriptions and metadata.
5. **Querying:** Retrieve textually similar action items and expand related graph context using neighboring nodes.
6. **Visualization:** Export the graph to `interactive_knowledge_graph.html`.

## Tech Stack

- **Language:** Python
- **LLM / Inference:** Groq API, Llama 3.3 70B Versatile, `AsyncGroq`
- **Data validation:** Pydantic
- **Retrieval:** scikit-learn TF-IDF and cosine similarity
- **Graph:** NetworkX
- **Visualization:** PyVis
- **Concurrency / configuration:** `asyncio`, `python-dotenv`

## Project Structure

```text
ai-meeting-action-item-tracker/
├── data/
│   └── sample_transcripts.json   # Sample meeting transcripts
├── src/
│   ├── ingestion.py              # Async LLM extraction
│   ├── models.py                 # Pydantic data models
│   ├── graph_rag.py              # Graph construction and hybrid retrieval
│   └── visualize.py              # Interactive HTML graph export
├── .env.example                  # Environment variable template
├── main.py                       # Pipeline entry point
├── requirements.txt
└── README.md
```

## Setup

**Requirements:** Python 3.10+ recommended.

1. Clone the repository and enter the project directory:

   ```bash
   git clone https://github.com/AkshathVP/ai-meeting-action-item-tracker.git
   cd ai-meeting-action-item-tracker
   ```

2. Create and activate a virtual environment:

   ```bash
   python -m venv .venv
   ```

   Windows PowerShell:
   ```powershell
   .\.venv\Scripts\Activate.ps1
   ```

   macOS/Linux:
   ```bash
   source .venv/bin/activate
   ```

3. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

4. Configure the Groq API key. Copy `.env.example` to `.env` and replace the placeholder with your key:

   ```env
   GROQ_API_KEY=your_groq_api_key_here
   ```

   Keep `.env` private and do not commit API keys.

## Input Format

Add transcripts to `data/sample_transcripts.json` as a JSON array. Each record must include an `id` and the transcript `text`:

```json
[
  {
    "id": "MEETING_001",
    "text": "Priya will prepare the report by Friday. The design task depends on the API update."
  }
]
```

The model is prompted to return action items, entities, and relationships as JSON. The extracted action items include a task ID, description, assignee, optional deadline, status, and dependencies.

## Run

From the repository root:

```bash
python main.py
```

The script processes the sample transcripts when a Groq API key and non-empty input are available. Otherwise, it uses built-in fallback data to demonstrate graph construction and querying. It runs example hybrid queries in the terminal and writes `interactive_knowledge_graph.html` to the project root. Open that HTML file in a browser to explore the graph.

## Notes & Limitations

- This is a prototype pipeline, not a hosted web application; interaction is through the command line and exported HTML graph.
- Retrieval uses TF-IDF cosine similarity rather than embedding-based semantic search. Graph traversal adds connected context to retrieved tasks.
- Extraction quality depends on transcript clarity and the LLM response. Review extracted owners, dates, and dependencies before relying on them.
- The current script contains example queries and fallback records for demonstrating the pipeline; it does not provide a persistent database or a task-management integration.
