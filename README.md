# RAGent

Local RAG system using Ollama for LLM, Qdrant for vector storage, and Inngest for async workflows. Ingests PDFs, splits them into chunks, generates embeddings, and answers questions using retrieved context. Runs completely offline without external APIs.

## Main Files

- `main.py` - FastAPI server with Inngest functions for ingest and query
- `data_loader.py` - PDF chunking and embedding using sentence-transformers
- `vector_db.py` - Qdrant client for vector search
- `streamlit_app.py` - Web UI

## How to Run

Terminal 1 - Start Ollama:

```
ollama serve
```

Terminal 2 - Start Qdrant:

```
docker run -d --name qdrantRagDb -p 6333:6333 qdrant/qdrant
```

Terminal 3 - Start FastAPI:

```
uv run uvicorn main:app
```

Terminal 4 - Start Inngest:

```
npx inngest-cli@latest dev -u http://127.0.0.1:8000
```

Terminal 5 - Start Streamlit:

```
uv run streamlit run streamlit_app.py
```

## Usage Example

Ingest a PDF:

```json
{
  "pdf_path": "/Users/andreeamanole/Downloads/FIA2024examsubjects.pdf"
}
```

Response:

```json
{
  "ingested": 10
}
```

Query the PDF:

```json
{
  "question": "will the exam contain anything lstm related?"
}
```

Response:

```json
{
  "answer": "Yes, LSTM is mentioned as a potential solution for time series prediction.",
  "num_contexts": 5,
  "sources": ["/Users/andreeamanole/Downloads/FIA2024examsubjects.pdf"]
}
```

## Screenshots

![PDF Ingestion](demo1.png)

![Query Interface](demo2.png)
