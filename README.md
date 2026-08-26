<div align="center">

🚀 Production RAG Agent

Enterprise-Grade Retrieval-Augmented Generation (RAG) Platform

Build AI-powered knowledge assistants capable of ingesting, indexing, retrieving, and reasoning over your documents using Google Gemini, LangGraph, FastAPI, Next.js, PostgreSQL, and Qdrant.

<p>










</p>

</div>

📖 Overview

Production RAG Agent is a full-stack, production-oriented Retrieval-Augmented Generation (RAG) system designed to build intelligent AI assistants over private documents.

Instead of relying only on an LLM's internal knowledge, the application retrieves relevant information from uploaded documents using semantic search, injects that context into the prompt, and generates grounded responses with source citations.

The project emphasizes production engineering practices including resilient document ingestion, deterministic chunking, duplicate detection, retry handling, crash recovery, and scalable vector search.

⭐ Highlights

🤖 Enterprise-oriented RAG architecture

📄 Multi-format document ingestion

🧠 Google Gemini integration

🔄 LangGraph-based AI pipeline

⚡ FastAPI backend

🎨 Next.js + TypeScript frontend

🐘 PostgreSQL metadata storage

🔍 Qdrant vector database

✂️ Adaptive semantic chunking

🔁 Duplicate document detection

♻️ Resume-safe indexing

💬 Streaming AI chat

📚 Source citations

🐳 Docker deployment

❤️ Production health monitoring

✨ Features

📂 Document Processing

Supports uploading and indexing:

PDF

DOCX

PPTX

XLSX

CSV

TXT

Markdown

Images through OCR providers where implemented

Each uploaded document can go through:

✅ File validation

✅ Content parsing

✅ Chunking

✅ Embedding generation

✅ Vector indexing

✅ Metadata storage

✅ Duplicate detection

✅ Resume-safe processing

🧠 Adaptive Semantic Chunking

Production-oriented chunking pipeline featuring:

Recursive chunk splitting

Configurable chunk size

Chunk overlap

Deterministic chunk IDs

Duplicate detection

Resume interrupted indexing

🤖 Retrieval-Augmented Generation

Instead of sending the whole document to the LLM:

User asks a question.

The question is converted into an embedding.

Semantic search retrieves relevant chunks.

LangGraph constructs the RAG context.

Google Gemini generates a grounded answer.

Sources are returned alongside the response.

⚡ Resilient Embedding Pipeline

Designed to work reliably with external AI providers.

Features include:

Dynamic batch sizing

Exponential backoff

Retry with jitter

Adaptive batch reduction

Concurrency control

Duplicate-safe processing

Resume-safe processing

Progress tracking

Note: Large documents may require additional processing time when provider rate limits or quota restrictions apply.

💬 AI Chat

Supports:

Conversational RAG

Streaming responses

Markdown rendering

Code blocks

Copy response

Source citations

Conversation context

📁 Document Management

Upload Documents

Delete Documents

Duplicate Detection

Already Indexed Detection

Chunk Statistics

Document Metadata

Collection Management

Indexing Status

📊 Dashboard

Provides monitoring for:

Backend API

Google Gemini

PostgreSQL

Qdrant

Document Count

Chunk Count

Storage Usage

🏗️ Architecture

The system is organized as a full-stack AI application where the Next.js frontend communicates with the FastAPI backend, while the backend coordinates document processing, retrieval, persistence, and Gemini-powered generation.

                              👤 User
                                │
                                ▼
                    ┌──────────────────────┐
                    │   Next.js Frontend  │
                    │   React + TypeScript │
                    └──────────┬───────────┘
                               │
                      REST / Streaming API
                               │
                               ▼
                    ┌──────────────────────┐
                    │   FastAPI Backend   │
                    │   Python + APIs     │
                    └──────────┬───────────┘
                               │
             ┌─────────────────┼─────────────────┐
             │                 │                 │
             ▼                 ▼                 ▼
     ┌──────────────┐  ┌───────────────┐  ┌───────────────┐
     │ Google Gemini│  │  PostgreSQL   │  │    Qdrant     │
     │ LLM + Embed. │  │   Metadata    │  │ Vector Search  │
     └──────┬───────┘  └───────────────┘  └───────┬───────┘
            │                                       │
            └────────────────┬──────────────────────┘
                             ▼
                   ┌──────────────────────┐
                   │  LangGraph RAG Flow  │
                   │                      │
                   │ Retrieve → Context   │
                   │         → Generate   │
                   └──────────────────────┘

🔹 Frontend

Built with Next.js, React, and TypeScript for document uploads, AI chat, source display, dashboard monitoring, and document management.

🔹 Backend

Built with FastAPI to coordinate ingestion, parsing, chunking, embeddings, retrieval, RAG orchestration, conversation management, and health monitoring.

🔹 PostgreSQL

Stores document and application metadata, processing state, and conversation information.

🔹 Qdrant

Stores document embeddings and performs semantic similarity search to retrieve relevant chunks.

🔹 Google Gemini

Used for embedding generation and AI answer generation. The current configured generation model is:

gemini-3.6-flash

🔹 LangGraph

Orchestrates the retrieval and generation workflow:

User Query
    ↓
Retrieve Relevant Chunks
    ↓
Build Context
    ↓
Generate Answer
    ↓
Return Sources

🔄 RAG Pipeline

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

PDF parsing

📘 DOCX

✅

Document parsing

📙 PPTX

✅

Presentation parsing

📗 XLSX

✅

Spreadsheet extraction

📊 CSV

✅

Tabular parsing

📄 TXT

✅

Text processing

📝 Markdown

✅

Markdown parsing

🖼️ Images

⚙️

OCR where available

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

AI

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

📊 Dashboard



📤 Upload Documents



📁 Documents



💬 AI Chat



🚀 Getting Started

Prerequisites

Install:

Git

Docker Desktop

Node.js

npm

Google Gemini API key

1️⃣ Clone Repository

git clone https://github.com/gourav-ai-engineer/RAG.git
cd RAG

2️⃣ Configure Environment

Create the required environment files from the supplied examples.

Frontend:

.env

Backend:

backend/.env

Example backend values:

GOOGLE_API_KEY=your_api_key_here
GEMINI_MODEL=gemini-3.6-flash

🔐 Never commit .env files or API keys to GitHub.

🐳 Start Backend

From the backend directory:

cd backend
docker compose up --build

Or in detached mode:

docker compose up -d --build

Check containers:

docker ps

Follow logs:

docker compose logs -f

🎨 Start Frontend

Open another terminal in the project root:

npm install
npm run dev

Open:

http://localhost:3000

🌐 Application URLs

Service

URL

🎨 Frontend

http://localhost:3000

⚙️ Backend API

http://localhost:8000

📚 Swagger API

http://localhost:8000/docs

❤️ Health Check

http://localhost:8000/health

🔍 Qdrant

http://localhost:6333

🧪 Health Monitoring

Check backend health:

curl http://localhost:8000/health

Expected healthy response:

{
  "status": "ok",
  "gemini": "connected",
  "postgres": "connected",
  "qdrant": "connected"
}

📂 Project Structure

Production-RAG-Agent/
│
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
│   ├── alembic/
│   ├── tests/
│   ├── Dockerfile
│   ├── docker-compose.yml
│   └── requirements.txt
│
├── screenshots/
├── package.json
├── next.config.ts
├── tsconfig.json
└── README.md

🔥 Production Engineering Features

✅ Deterministic Chunk IDs

✅ Duplicate Document Detection

✅ Resume Interrupted Indexing

✅ Adaptive Batch Embedding

✅ Exponential Backoff & Retry

✅ Dynamic Batch Reduction

✅ Similarity Threshold Filtering

✅ Streaming Responses

✅ Source Citations

✅ Health Monitoring

✅ Multi-Format Parsing

✅ OCR Support

✅ Dockerized Services

🧪 Testing

The backend contains tests and validation scripts for document upload, duplicate detection, adaptive chunking, retrieval, conversation quality, deterministic IDs, multi-format parsing, memory behavior, concurrent processing, and file safety.

Example:

cd backend
python test_all.py

🗺️ Roadmap

Future improvements:

Background Workers

Async Upload Queue

Redis Cache

User Authentication

Multi-Tenant Support

Role-Based Access Control

Observability Dashboard

Kubernetes Deployment

CI/CD Pipeline

Automated Evaluation Suite

🎯 Learning Objectives

This project demonstrates practical experience with:

Retrieval-Augmented Generation

AI Engineering

Vector Databases

Semantic Search

LangGraph Workflows

Google Gemini APIs

Production FastAPI Development

Full-Stack AI Applications

Docker Deployment

PostgreSQL

Qdrant

Production AI Architecture

🤝 Contributing

Contributions are welcome.

Fork the repository.

Create a feature branch.

Make your changes.

Run tests.

Commit your changes.

Push the branch.

Open a Pull Request.

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

The repository provides .env.example files as configuration templates.

Before pushing changes, verify:

git status
git ls-files | findstr /i ".env"

📄 License

This project is licensed under the MIT License.

See the LICENSE file for details.

👨‍💻 Author

Gourav

AI Engineer | GenAI Developer | Software Engineer

Areas of Interest

🤖 Artificial Intelligence

🧠 Generative AI

📚 Retrieval-Augmented Generation

🔎 AI Search

🏗️ AI Agents

⚙️ Backend Engineering

💻 Full-Stack Development

🔬 Machine Learning

GitHub

https://github.com/gourav-ai-engineer

<div align="center">

⭐ Production RAG Agent

Retrieval · Reasoning · Generation · Engineering

Built with ❤️ by Gourav

</div>