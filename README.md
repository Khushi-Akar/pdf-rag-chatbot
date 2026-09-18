# Document Q&A — RAG Pipeline

A Retrieval-Augmented Generation (RAG) system that lets you upload a document and ask natural language questions about its content. Available as a **live web app** (via Streamlit) and as a command-line tool.

## 🚀 Live Demo

Try it now — no setup required:

**[https://pdf-rag-chatbot-mirhaybmd5f3pg6sivyn5d.streamlit.app/](https://pdf-rag-chatbot-mirhaybmd5f3pg6sivyn5d.streamlit.app/)**

Upload a PDF and start asking questions directly in your browser.

## How it works

1. **Document Ingestion** — PDF documents are parsed using PyPDF.
2. **Chunking** — Extracted text is split into smaller chunks for better retrieval accuracy.
3. **Embeddings** — Each chunk is converted into vector embeddings using Mistral AI's embedding model via HuggingFace.
4. **Vector Store** — Embeddings are stored in a local ChromaDB vector database.
5. **Retrieval** — When a user asks a question, the query is embedded and compared against stored vectors to find the most relevant chunks.
6. **Generation** — Retrieved chunks + the original query are sent to the LLM, which generates a context-aware answer.

## Tech Stack

* **Language:** Python
* **Web UI / Deployment:** Streamlit ([live app](https://pdf-rag-chatbot-mirhaybmd5f3pg6sivyn5d.streamlit.app/))
* **PDF Parsing:** PyPDF
* **Embeddings:** Mistral AI (via HuggingFace)
* **Vector Store:** ChromaDB
* **LLM:** Groq
* **Package Management:** uv

## Project Structure

```
├── document loaders/   # Document parsing and loading logic
├── src/                # Core pipeline logic
├── chroma_db/          # Local vector store (gitignored)
├── create_database.py  # Script to build/populate the vector database
├── main.py              # CLI entry point — run this to ask questions
├── app.py                # Streamlit app entry point (web UI)
├── pyproject.toml
├── requirements.txt
└── .env.example          # Template for required environment variables
```

## Option 1: Use the Hosted App

Just open the live demo link above, upload your PDF, and start chatting — nothing to install.

> Note: on the free Streamlit tier the app may take a few seconds to "wake up" if it hasn't been used recently.

## Option 2: Run Locally (CLI or Streamlit)

### Setup

1. Clone the repo:
   ```bash
   git clone <repo-url>
   cd <repo-folder>
   ```
2. Install dependencies using uv:
   ```bash
   uv sync
   ```
3. Copy the environment template and add your own API keys:
   ```bash
   cp .env.example .env
   ```
   Then fill in `.env` with your actual Mistral AI and HuggingFace credentials.
4. Build the vector database from your document:
   ```bash
   uv run create_database.py
   ```

### Run the CLI version

```bash
uv run main.py
```

You'll be prompted to enter a question. The system retrieves the most relevant chunks from your document and generates an answer.

### Run the Streamlit app locally

```bash
uv run streamlit run app.py
```

This launches the same web UI as the hosted demo, but running on your own machine.

## Roadmap

* [x] Add a web UI for document upload and chat
* [x] Deploy as a hosted app (Streamlit)
* [ ] Support multiple document formats (currently PDF only)
* [ ] Add conversation history / follow-up question support

## License

MIT (or your preferred license)
