<div align="center">

# 🚀 Production RAG Agent

### Enterprise-Grade Retrieval-Augmented Generation Platform

Build AI-powered knowledge assistants capable of ingesting, indexing, retrieving, and reasoning over private documents using **Google Gemini, LangGraph, FastAPI, Next.js, PostgreSQL, and Qdrant**.

[![Python](https://img.shields.io/badge/Python-3.11+-blue?logo=python)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-Production-009688?logo=fastapi)](https://fastapi.tiangolo.com/)
[![Next.js](https://img.shields.io/badge/Next.js-15-black?logo=next.js)](https://nextjs.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6?logo=typescript)](https://www.typescriptlang.org/)
[![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?logo=docker)](https://www.docker.com/)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-Database-336791?logo=postgresql)](https://www.postgresql.org/)
[![Qdrant](https://img.shields.io/badge/Qdrant-Vector%20Database-red)](https://qdrant.tech/)
[![Google Gemini](https://img.shields.io/badge/Google-Gemini-orange?logo=google)](https://ai.google.dev/)

</div>

---

## 📌 Overview

**Production RAG Agent** is a full-stack, production-oriented Retrieval-Augmented Generation (RAG) platform for building intelligent AI assistants over private documents.

Instead of relying solely on an LLM's internal knowledge, the system:

1. Accepts and processes uploaded documents.
2. Extracts and chunks document content.
3. Generates semantic embeddings.
4. Stores vectors in Qdrant.
5. Stores document metadata in PostgreSQL.
6. Retrieves relevant information for user queries.
7. Uses Google Gemini to generate grounded responses.
8. Returns source references with the generated answer.

The project focuses on production engineering concepts such as resilient ingestion, deterministic chunking, duplicate detection, retry handling, crash recovery, and scalable vector search.

---

# ✨ Key Features

- 🤖 Enterprise-grade RAG architecture
- 📄 Multi-format document ingestion
- 🧠 Google Gemini integration
- 🔄 LangGraph-based AI workflow
- ⚡ FastAPI backend
- 🎨 Next.js + TypeScript frontend
- 🐘 PostgreSQL metadata storage
- 🔍 Qdrant vector database
- ✂️ Adaptive semantic chunking
- 🔁 Duplicate document detection
- ♻️ Resume-safe indexing
- 💬 Conversational AI chat
- 📚 Source citations
- 🐳 Dockerized deployment
- ❤️ Production health monitoring

---

# 🏗️ Architecture

```text
                           ┌───────────────┐
                           │     User      │
                           └───────┬───────┘
                                   │
                                   ▼
                     ┌─────────────────────────┐
                     │   Next.js Frontend      │
                     │   React + TypeScript    │
                     └───────────┬─────────────┘
                                 │
                          REST / Streaming API
                                 │
                                 ▼
                     ┌─────────────────────────┐
                     │    FastAPI Backend      │
                     └───────────┬─────────────┘
                                 │
          ┌──────────────────────┼──────────────────────┐
          │                      │                      │
          ▼                      ▼                      ▼
 ┌────────────────┐    ┌────────────────┐    ┌────────────────┐
 │ Google Gemini  │    │ PostgreSQL     │    │ Qdrant         │
 │ LLM + AI       │    │ Metadata       │    │ Vector Store   │
 └────────────────┘    └────────────────┘    └────────────────┘
          │
          ▼
 ┌──────────────────────────────┐
 │      LangGraph RAG Flow      │
 │                              │
 │ Retrieve → Context → Answer  │
 └──────────────────────────────┘
🧠 How the RAG Pipeline Works
                 DOCUMENT INGESTION
                         │
                         ▼
                ┌─────────────────┐
                │ Upload Document │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Validate File   │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Parse Content   │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Adaptive        │
                │ Chunking        │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Generate        │
                │ Embeddings      │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Store Vectors   │
                │ in Qdrant       │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Store Metadata  │
                │ in PostgreSQL   │
                └─────────────────┘


                    USER QUESTION
                         │
                         ▼
                ┌─────────────────┐
                │ Semantic Search │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Retrieve Best   │
                │ Document Chunks │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Build Context   │
                │ with LangGraph  │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Google Gemini   │
                │ Generate Answer │
                └────────┬────────┘
                         │
                         ▼
                ┌─────────────────┐
                │ Answer + Sources│
                └─────────────────┘
📄 Supported Document Formats

The system supports ingestion and indexing of:

Format	Supported
PDF	✅
DOCX	✅
PPTX	✅
XLSX	✅
CSV	✅
TXT	✅
Markdown	✅
Images / OCR	⚙️ Supported through OCR providers

Each uploaded document can go through:

File validation
Content extraction
Metadata extraction
OCR when required
Adaptive chunking
Embedding generation
Vector indexing
Metadata storage
Duplicate detection
✂️ Adaptive Semantic Chunking

The document processing pipeline includes production-oriented chunking capabilities.

Features
Recursive chunk splitting
Configurable chunk sizes
Chunk overlap
Deterministic chunk IDs
Duplicate detection
Resume interrupted indexing
Multi-format content processing

Deterministic chunk IDs help the system avoid creating duplicate vectors when documents are reprocessed.

🔍 Retrieval-Augmented Generation

Instead of sending an entire document directly to the LLM, the system follows this workflow:

The user submits a question.
The question is converted into an embedding.
Qdrant performs semantic similarity search.
The most relevant document chunks are retrieved.
LangGraph constructs the RAG context.
Google Gemini generates a grounded response.
Relevant sources are returned to the user.

This approach reduces hallucination and keeps responses grounded in the uploaded documents.

🔄 Resilient Embedding Pipeline

The embedding system is designed to handle external AI provider limitations.

Features
Dynamic batch sizing
Exponential backoff
Retry with jitter
Adaptive batch reduction
Concurrency control
Duplicate-safe processing
Resume-safe indexing
Progress tracking

Note: Large documents may require additional processing time when using API providers with rate limits or free-tier quotas.

💬 AI Chat

The AI chat interface supports:

Conversational RAG
Document-grounded responses
Streaming responses
Markdown rendering
Code blocks
Copy response functionality
Source citations
Conversation management

The system is designed to refuse unsupported questions when relevant information is not found in the indexed documents.

📁 Document Management

The document management system provides functionality for:

Uploading documents
Viewing indexed documents
Deleting documents
Duplicate detection
Already-indexed detection
Chunk statistics
Document metadata
Collection management
📊 Dashboard

The application dashboard provides system-level monitoring.

Health Monitoring
FastAPI backend status
Google Gemini connectivity
PostgreSQL connectivity
Qdrant connectivity
System Statistics
Total documents
Total chunks
Indexed collections
Storage information
🛠️ Technology Stack
Frontend
Next.js
React
TypeScript
Tailwind CSS
Backend
Python
FastAPI
LangGraph
SQLAlchemy
Pydantic
AI and Machine Learning
Google Gemini
Semantic Embeddings
Retrieval-Augmented Generation
Databases
PostgreSQL
Qdrant Vector Database
DevOps
Docker
Docker Compose
📸 Application Preview
Dashboard

Upload Documents

Document Management

AI Chat

🚀 Getting Started
Prerequisites

Make sure the following are installed:

Git
Docker Desktop
Node.js
npm
Google Gemini API Key
1️⃣ Clone the Repository
git clone https://github.com/gourav-ai-engineer/RAG.git
cd RAG
2️⃣ Configure Environment Variables

The project uses separate environment files for the frontend and backend.

Create environment files based on the provided examples.

Backend
cd backend
copy .env.example .env

Then configure the required values in:

backend/.env

Example:

GOOGLE_API_KEY=your_google_gemini_api_key

GEMINI_MODEL=gemini-3.6-flash

Never commit your real API keys or .env files to GitHub.

3️⃣ Start the Backend

From the backend directory:

docker compose up --build

This starts:

FastAPI backend
PostgreSQL
Qdrant

Verify the containers:

docker ps

The backend health endpoint should be available at:

http://localhost:8000/health

Expected example response:

{
  "status": "ok",
  "gemini": "connected",
  "postgres": "connected",
  "qdrant": "connected"
}
4️⃣ Start the Frontend

Open another terminal and navigate to the project root:

cd C:\projects\Production-RAG-Agent-main

Install dependencies:

npm install

Start the development server:

npm run dev

Open:

http://localhost:3000
🌐 Application URLs
Service	URL
Frontend	http://localhost:3000
Backend API	http://localhost:8000
API Documentation	http://localhost:8000/docs
Health Check	http://localhost:8000/health
Qdrant	http://localhost:6333
🧪 Health Check

You can test the backend directly from CMD:

curl http://localhost:8000/health

Example successful response:

{
  "status": "ok",
  "gemini": "connected",
  "postgres": "connected",
  "qdrant": "connected"
}
📂 Project Structure
Production-RAG-Agent/
│
├── app/                        # Next.js application pages
│   ├── chat/
│   ├── collections/
│   ├── dashboard/
│   ├── documents/
│   └── settings/
│
├── components/                 # Reusable frontend components
│   ├── chat/
│   ├── collections/
│   ├── dashboard/
│   ├── documents/
│   ├── layout/
│   └── ui/
│
├── lib/                        # Frontend utilities and API clients
│   ├── api/
│   ├── hooks/
│   └── context/
│
├── backend/
│   │
│   ├── app/
│   │   ├── api/                # FastAPI routes
│   │   ├── db/                 # Database models and connections
│   │   ├── schemas/            # Pydantic schemas
│   │   ├── services/           # Core application services
│   │   │   ├── embeddings/
│   │   │   ├── ocr/
│   │   │   └── parsers/
│   │   └── utils/
│   │
│   ├── alembic/                # Database migrations
│   ├── tests/                  # Automated tests
│   ├── Dockerfile
│   ├── docker-compose.yml
│   └── requirements.txt
│
├── screenshots/                # Application screenshots
│
├── package.json
├── next.config.ts
├── tsconfig.json
└── README.md
⚙️ Production Engineering Features

The project implements several engineering practices commonly required in production AI systems.

 Deterministic chunk IDs
 Duplicate document detection
 Resume interrupted indexing
 Adaptive batch embedding
 Exponential backoff
 Retry with jitter
 Dynamic batch reduction
 Similarity threshold filtering
 Streaming responses
 Source citations
 Health monitoring
 PostgreSQL metadata storage
 Qdrant vector search
 Dockerized services
🧪 Testing

The backend contains tests for multiple aspects of the system, including:

Document uploads
Duplicate detection
Adaptive chunking
Retrieval
Memory
Concurrent operations
ZIP bomb protection
Multi-format document parsing
Conversation quality

Run backend tests from the backend directory:

python -m pytest

Depending on your environment, individual test scripts can also be executed directly:

python test_retrieval.py
python test_duplicate.py
python comprehensive_audit.py
🗺️ Roadmap

Future improvements include:

 Background workers
 Asynchronous upload queue
 Redis caching
 User authentication
 Multi-tenant architecture
 Role-based access control
 Advanced observability
 Automated RAG evaluation
 CI/CD pipeline
 Kubernetes deployment
 Distributed workers
 Hybrid search
 Reranking pipeline
 Advanced document analytics
🎓 Learning Objectives

This project demonstrates practical experience with:

Retrieval-Augmented Generation
AI Engineering
Large Language Models
Google Gemini APIs
Vector Databases
Semantic Search
Document Processing
LangGraph Workflows
FastAPI Development
Full-Stack AI Applications
PostgreSQL
Docker
Production System Design
🔐 Security

Important security practices:

Never commit .env files.
Never expose API keys.
Use environment variables for secrets.
Validate uploaded files.
Apply file-size restrictions.
Restrict supported file formats.
Use database credentials securely in production.

Before publishing:

git status

Verify that files such as these are not being tracked:

.env
backend/.env
node_modules/
.venv/
__pycache__/

You can check tracked environment files using:

git ls-files | findstr /i ".env"

Only example environment files should normally appear:

.env.example
backend/.env.example
🤝 Contributing

Contributions are welcome.

To contribute:

Fork the repository.
Create a feature branch.
git checkout -b feature/your-feature-name
Make your changes.
Run tests.
Commit your changes.
git add .
git commit -m "feat: add your feature"
Push your branch.
git push origin feature/your-feature-name
Open a Pull Request.
📄 License

This project is licensed under the MIT License.

See the LICENSE file for details.

👨‍💻 Author
Gourav

AI Engineer | Software Engineer | M.Tech CSE (Artificial Intelligence)

Interests
Artificial Intelligence
Generative AI
Retrieval-Augmented Generation
AI Agents
Machine Learning
Backend Engineering
Distributed Systems
Production AI Systems
Tech Stack
Python
FastAPI
LangGraph
Next.js
TypeScript
PostgreSQL
Qdrant
Docker
Google Gemini
<div align="center">