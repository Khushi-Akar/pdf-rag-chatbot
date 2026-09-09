# Document Q&A — RAG Pipeline

A Retrieval-Augmented Generation (RAG) system that lets you upload a document and ask natural language questions about its content. Built as a command-line tool for now, with a UI and deployment planned next.

## How it works

1. **Document Ingestion** — PDF documents are parsed using PyPDF.
2. **Chunking** — Extracted text is split into smaller chunks for better retrieval accuracy.
3. **Embeddings** — Each chunk is converted into vector embeddings using Mistral AI's embedding model via HuggingFace.
4. **Vector Store** — Embeddings are stored in a local ChromaDB vector database.
5. **Retrieval** — When a user asks a question, the query is embedded and compared against stored vectors to find the most relevant chunks.
6. **Generation** — Retrieved chunks + the original query are sent to Mistral AI's LLM, which generates a context-aware answer.

## Tech Stack

- **Language:** Python
- **PDF Parsing:** PyPDF
- **Embeddings:** Mistral AI (via HuggingFace)
- **Vector Store:** ChromaDB
- **LLM:** Grok 
- **Package Management:** uv

## Project Structure

\`\`\`
├── document loaders/    # Document parsing and loading logic
├── src/                 # Core pipeline logic
├── chroma_db/           # Local vector store (gitignored)
├── create_database.py   # Script to build/populate the vector database
├── main.py               # Entry point — run this to ask questions
├── pyproject.toml
├── requirements.txt
└── .env.example          # Template for required environment variables
\`\`\`

## Setup

1. Clone the repo:
   \`\`\`bash
   git clone <your-repo-url>
   cd <repo-name>
   \`\`\`

2. Install dependencies using uv:
   \`\`\`bash
   uv sync
   \`\`\`

3. Copy the environment template and add your own API keys:
   \`\`\`bash
   cp .env.example .env
   \`\`\`
   Then fill in `.env` with your actual Mistral AI and HuggingFace credentials.

4. Build the vector database from your document:
   \`\`\`bash
   uv run create_database.py
   \`\`\`

5. Run the Q&A pipeline:
   \`\`\`bash
   uv run main.py
   \`\`\`

## Usage

Once running, you'll be prompted to enter a question. The system retrieves the most relevant chunks from your document and generates an answer using Grok.

## Roadmap

- [ ] Add a web UI for document upload and chat
- [ ] Deploy as a hosted app
- [ ] Support multiple document formats (currently PDF only)
- [ ] Add conversation history / follow-up question support

## License

MIT (or your preferred license)