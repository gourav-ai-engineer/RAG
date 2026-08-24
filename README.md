<div align="center">

🚀 Production RAG Agent

Enterprise-Grade Retrieval-Augmented Generation Platform

Build intelligent AI-powered knowledge assistants that can ingest, process, index, search, and reason over private documents using Google Gemini, LangGraph, FastAPI, Next.js, PostgreSQL, and Qdrant.

<br />










<br />

🔍 Semantic Search · 🤖 AI Reasoning · 📄 Multi-Format Documents · 🧠 Conversational RAG

</div>

📖 Overview

Production RAG Agent is a full-stack, production-oriented Retrieval-Augmented Generation (RAG) platform for building intelligent AI assistants over private knowledge bases.

Instead of relying only on the internal knowledge of a Large Language Model (LLM), the system retrieves relevant information from uploaded documents and provides that context to the AI model before generating a response.

This helps produce answers that are:

🎯 More relevant

📚 Grounded in uploaded documents

🔎 Traceable through source citations

🧠 Context-aware

🛡️ Less prone to hallucination

The project also focuses on production engineering concerns such as deterministic chunking, duplicate detection, retry mechanisms, adaptive embedding batches, interrupted indexing recovery, multi-format document support, and health monitoring.

✨ Key Features

Feature

Description

🤖 AI-Powered Chat

Ask questions about your uploaded documents

📄 Multi-Format Support

PDF, DOCX, PPTX, XLSX, CSV, TXT, Markdown, and OCR-supported images

🔍 Semantic Search

Retrieve relevant document chunks using vector search

🧠 Conversational RAG

Context-aware multi-turn conversations

📚 Source Citations

Return relevant document sources with answers

🧩 LangGraph Workflow

Structured retrieval and generation workflow

⚡ Streaming Responses

Stream AI-generated responses in real time

🗂️ Document Management

Upload, inspect, index, and delete documents

🔁 Retry Mechanisms

Handle transient AI provider failures

📦 Docker Deployment

Containerized backend and infrastructure

❤️ Health Monitoring

Monitor Gemini, PostgreSQL, and Qdrant

🛡️ Duplicate Detection

Prevent unnecessary duplicate indexing

🏗️ System Architecture

The application follows a full-stack architecture where the Next.js frontend communicates with the FastAPI backend, which coordinates document processing, retrieval, databases, and Gemini-powered generation.

                              👤 USER
                                │
                                ▼
                    ┌──────────────────────┐
                    │  Next.js Frontend   │
                    │ React + TypeScript   │
                    └──────────┬───────────┘
                               │
                               │ REST / Streaming API
                               ▼
                    ┌──────────────────────┐
                    │   FastAPI Backend   │
                    │   Python + APIs     │
                    └──────────┬───────────┘
                               │
              ┌────────────────┼─────────────────┐
              │                │                 │
              ▼                ▼                 ▼
      ┌──────────────┐ ┌───────────────┐ ┌───────────────┐
      │ Google Gemini│ │  PostgreSQL   │ │    Qdrant     │
      │ LLM + Embed. │ │   Metadata    │ │ Vector Search  │
      └──────┬───────┘ └───────────────┘ └───────┬───────┘
             │                                   │
             └──────────────┬────────────────────┘
                            ▼
                  ┌──────────────────────┐
                  │  LangGraph RAG Flow  │
                  │                      │
                  │ Retrieve → Context   │
                  │         → Generate   │
                  └──────────────────────┘

🔹 Frontend

The frontend is built with Next.js, React, and TypeScript and provides the user interface for:

📄 Uploading documents

💬 Asking questions

📚 Viewing document sources

📊 Monitoring system health

🗂️ Managing indexed documents and collections

🔹 Backend

The backend is built with FastAPI and coordinates the application's core services:

Document ingestion

Parsing

Chunking

Embedding generation

Semantic retrieval

RAG orchestration

Conversation management

Health monitoring

🔹 PostgreSQL

PostgreSQL stores application metadata such as:

Document records

Processing state

Document metadata

Conversation information

🔹 Qdrant

Qdrant acts as the vector database.

It stores document embeddings and performs semantic similarity search to retrieve the most relevant chunks for a user query.

🔹 Google Gemini

Google Gemini is used for:

🧠 Embedding generation

🤖 Answer generation

📖 Context-grounded responses

The current configured generation model is:

gemini-3.6-flash

🔹 LangGraph

LangGraph orchestrates the RAG workflow:

User Query
    ↓
Retrieve Relevant Chunks
    ↓
Build Context
    ↓
Generate Answer
    ↓
Return Sources

🔄 How the RAG Pipeline Works

The complete workflow is divided into two major stages: document ingestion and question answering.

📥 Document Ingestion

Upload Document
      ↓
Validate File
      ↓
Parse Content
      ↓
Extract Metadata
      ↓
OCR (if required)
      ↓
Adaptive Chunking
      ↓
Generate Embeddings
      ↓
Store Vectors in Qdrant
      ↓
Store Metadata in PostgreSQL

💬 Question Answering

User Question
      ↓
Generate Query Embedding
      ↓
Semantic Search
      ↓
Retrieve Relevant Chunks
      ↓
Build Context with LangGraph
      ↓
Google Gemini Generates Answer
      ↓
Return Answer + Sources

📂 Supported Document Formats

Format

Supported

Processing

📕 PDF

✅

Native PDF parsing

📘 DOCX

✅

Word document parsing

📙 PPTX

✅

PowerPoint extraction

📗 XLSX

✅

Spreadsheet extraction

📊 CSV

✅

Structured data parsing

📄 TXT

✅

Text processing

📝 Markdown

✅

Markdown parsing

🖼️ Images

⚙️

OCR-based extraction where available

Each uploaded document can go through:

✓ File validation
✓ Content extraction
✓ Metadata extraction
✓ OCR when required
✓ Adaptive chunking
✓ Embedding generation
✓ Vector indexing
✓ Metadata storage
✓ Duplicate detection
✓ Resume-safe indexing

✂️ Adaptive Semantic Chunking

Large documents cannot efficiently be sent directly to an LLM.

The chunking pipeline supports:

📏 Configurable chunk sizes

🔄 Chunk overlap

🧩 Recursive chunk splitting

🆔 Deterministic chunk IDs

🔍 Duplicate chunk detection

♻️ Resume interrupted indexing

📚 Multi-format content processing

Why Deterministic Chunk IDs?

Deterministic IDs help the system:

Avoid duplicate vectors

Resume interrupted processing

Prevent unnecessary re-embedding

Maintain consistent document indexing

🔍 Retrieval-Augmented Generation

Instead of sending an entire document directly to the LLM:

1. User submits a question
           ↓
2. Question is converted into an embedding
           ↓
3. Qdrant performs semantic similarity search
           ↓
4. Relevant document chunks are retrieved
           ↓
5. LangGraph constructs the RAG context
           ↓
6. Google Gemini generates a grounded answer
           ↓
7. Relevant sources are returned

This approach helps:

Reduce hallucinations

Improve factual grounding

Handle large document collections

Return source-backed answers

Improve answer relevance

⚡ Resilient Embedding Pipeline

External AI providers can experience:

Rate limits

Temporary failures

Network interruptions

Request limits

Batch size restrictions

The embedding pipeline is designed to handle these challenges.

Features

✓ Dynamic batch sizing
✓ Exponential backoff
✓ Retry with jitter
✓ Adaptive batch reduction
✓ Concurrency control
✓ Duplicate-safe processing
✓ Resume-safe indexing
✓ Progress tracking

⚠️ Note: Large documents may require additional processing time when using API providers with rate limits.

💬 AI Chat

The chat interface supports:

🤖 Conversational RAG

⚡ Streaming responses

📝 Markdown rendering

💻 Code blocks

📋 Copy responses

📚 Source citations

🧠 Conversation context

The AI is instructed to remain grounded in the retrieved document context.

If relevant information is not available in the indexed documents, the system can indicate that the answer cannot be found in the available knowledge base.

📊 Dashboard

The application dashboard provides a high-level overview of the RAG system.

Monitor

🟢 Backend API status

🤖 Google Gemini connectivity

🐘 PostgreSQL connectivity

🔍 Qdrant connectivity

📄 Document statistics

🧩 Chunk statistics

💾 Storage information

📈 System health

🗂️ Document Management

The document management system supports:

📤 Upload documents

🔍 View indexed documents

🗑️ Delete documents

🔁 Duplicate detection

📊 Chunk statistics

📁 File metadata

⚙️ Indexing status

♻️ Already-indexed detection

🛠️ Technology Stack

🎨 Frontend

Next.js

React

TypeScript

Tailwind CSS

⚙️ Backend

Python

FastAPI

Pydantic

SQLAlchemy

Uvicorn

🤖 AI & RAG

Google Gemini

LangGraph

Retrieval-Augmented Generation

Semantic Embeddings

🗄️ Databases

PostgreSQL

Qdrant

📦 DevOps

Docker

Docker Compose

📸 Application Preview

🏠 Dashboard



📤 Upload Documents



📄 Documents



💬 AI Chat



🚀 Getting Started

1️⃣ Clone the Repository

git clone https://github.com/gourav-ai-engineer/RAG.git
cd RAG

2️⃣ Configure Environment Variables

Create the required environment files.

Frontend

Create:

.env

Use:

.env.example

Backend

Create:

backend/.env

Use:

backend/.env.example

Configure the required values, including:

GOOGLE_API_KEY
GEMINI_MODEL
POSTGRES_HOST
POSTGRES_PORT
POSTGRES_DB
POSTGRES_USER
POSTGRES_PASSWORD
QDRANT_HOST
QDRANT_PORT

Example:

GOOGLE_API_KEY=your_google_api_key
GEMINI_MODEL=gemini-3.6-flash

🔐 Never commit your real .env files or API keys to GitHub.

🐳 Start the Backend

Navigate to the backend directory:

cd backend

Start all backend services:

docker compose up --build

Run in detached mode:

docker compose up -d --build

Check running containers:

docker ps

Check logs:

docker compose logs -f

🩺 Check System Health

Once the backend is running:

curl http://localhost:8000/health

Expected response:

{
  "status": "ok",
  "gemini": "connected",
  "postgres": "connected",
  "qdrant": "connected"
}

🎨 Start the Frontend

Open another terminal in the project root.

Install dependencies:

npm install

Start the development server:

npm run dev

Open:

http://localhost:3000

🌐 Application Endpoints

Service

URL

🎨 Frontend

http://localhost:3000

⚙️ Backend API

http://localhost:8000

📚 Swagger Documentation

http://localhost:8000/docs

❤️ Health Endpoint

http://localhost:8000/health

🔍 Qdrant

http://localhost:6333

📁 Project Structure

Production-RAG-Agent/

├── app/
│   ├── chat/
│   ├── collections/
│   ├── dashboard/
│   ├── documents/
│   └── settings/
│
├── components/
│   ├── chat/
│   ├── collections/
│   ├── dashboard/
│   ├── documents/
│   ├── layout/
│   ├── settings/
│   └── ui/
│
├── lib/
│   ├── api/
│   ├── context/
│   ├── hooks/
│   └── types.ts
│
├── backend/
│   ├── app/
│   │   ├── api/
│   │   ├── db/
│   │   ├── schemas/
│   │   ├── services/
│   │   │   ├── embeddings/
│   │   │   ├── ocr/
│   │   │   └── parsers/
│   │   └── utils/
│   │
│   ├── alembic/
│   ├── tests/
│   ├── Dockerfile
│   ├── docker-compose.yml
│   └── requirements.txt
│
├── screenshots/
│
├── package.json
├── next.config.ts
├── README.md
└── LICENSE

🧪 Testing

The backend contains tests and validation scripts for:

Document upload

Duplicate detection

Chunking

Retrieval

Memory

Conversation quality

Deterministic IDs

Multi-format documents

OCR

Large document handling

Example:

cd backend
python test_all.py

🏭 Production Engineering Features

✓ Deterministic Chunk IDs
✓ Duplicate Document Detection
✓ Duplicate-safe Processing
✓ Resume Interrupted Indexing
✓ Adaptive Batch Embedding
✓ Exponential Backoff
✓ Retry with Jitter
✓ Dynamic Batch Reduction
✓ Similarity Threshold Filtering
✓ Streaming Responses
✓ Health Monitoring
✓ Multi-Format Parsing
✓ OCR Support
✓ Dockerized Deployment

🗺️ Roadmap

Future improvements planned for the platform:

Background workers

Asynchronous upload queue

Redis caching

Authentication

Multi-tenant architecture

Role-Based Access Control

Advanced observability

RAG evaluation pipeline

Automated benchmark suite

CI/CD pipeline

Kubernetes deployment

Hybrid search

Reranking

Query rewriting

Agentic workflows

🎓 Learning Objectives

This project demonstrates practical experience with:

🤖 Generative AI Engineering

📚 Retrieval-Augmented Generation

🔍 Semantic Search

🧠 AI Agents and LangGraph

🗄️ Vector Databases

📄 Document Processing Pipelines

⚡ Production FastAPI Development

🎨 Full-Stack AI Applications

🐳 Docker and Containerization

🗃️ PostgreSQL

🔎 Qdrant

☁️ AI API Integration

🏗️ Production Software Architecture

🤝 Contributing

Contributions are welcome!

Workflow

1. Fork the repository
        ↓
2. Create a feature branch
        ↓
3. Make your changes
        ↓
4. Run tests
        ↓
5. Commit changes
        ↓
6. Push your branch
        ↓
7. Open a Pull Request

Example:

git checkout -b feature/my-feature

git add .

git commit -m "feat: add my feature"

git push origin feature/my-feature

🔐 Security

Never commit:

.env
backend/.env
API keys
Database passwords
Private credentials

The repository includes .env.example files for configuration templates.

Before publishing changes, verify:

git status

And inspect tracked files:

git ls-files

📄 License

This project is licensed under the MIT License.

See the LICENSE file for details.

👨‍💻 Author

Gourav

M.Tech CSE (Artificial Intelligence) | AI Engineer | Software Developer

Areas of Interest

🤖 Artificial Intelligence

🧠 Generative AI

📚 RAG Systems

🔎 AI Search

🏗️ AI Agents

⚙️ Backend Engineering

💻 Full-Stack Development

🔬 Machine Learning

Repository

Production RAG Agent

⭐ If you find this project useful, consider giving the repository a star!

<div align="center">

🚀 Built to Explore Production-Grade AI Systems

Retrieval · Reasoning · Generation · Engineering

<br />

Made with ❤️ by Gourav

</div>