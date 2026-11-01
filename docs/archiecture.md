
# Podcast RAG API — Architecture

## 1. Project Overview

Podcast RAG API is an AI-powered application that allows users
to ask questions about podcast transcripts.

The system uses Retrieval-Augmented Generation (RAG) to retrieve
relevant information from podcast transcripts and generate
context-aware answers using a Large Language Model (LLM).

The API is built with FastAPI and uses a relational database
and a vector database to manage and retrieve information.

## 2. Project Goals

- Upload and process podcast transcripts.
- Extract and clean transcript text.
- Split transcripts into smaller chunks.
- Generate vector embeddings for each chunk.
- Store embeddings in a vector database.
- Retrieve relevant transcript segments using semantic search.
- Generate answers using an LLM.
- Return answers with episode information and timestamps.
- Track background processing jobs.

## 3. System Architecture

The system consists of two main pipelines:

1. Indexing Pipeline
2. Retrieval and Generation Pipeline

### 3.1 Indexing Pipeline

The indexing pipeline processes podcast transcripts
and prepares them for semantic retrieval.

Processing steps:

1. Transcript Upload
2. File Validation
3. Transcript Parsing
4. Text Cleaning
5. Text Chunking
6. Embedding Generation
7. Vector Storage
8. Job Status Update

Each chunk is stored with its corresponding metadata,
including episode ID, timestamp, speaker and source information.

### 3.2 Retrieval and Generation Pipeline

The retrieval pipeline handles user questions.

Processing steps:

1. Receive the user's question.
2. Generate an embedding for the question.
3. Perform semantic search in the vector database.
4. Retrieve the most relevant chunks.
5. Build the context for the LLM.
6. Generate an answer using the retrieved context.
7. Return the answer with its sources.

The system should avoid generating unsupported answers
when relevant information cannot be found.

## 4. Technology Stack

- Python: Main programming language
- FastAPI: REST API framework
- SQLModel: Relational database models and ORM
- SQLite: Relational database
- Qdrant: Vector database
- Embedding Model: Text vectorization
- LLM Provider: Answer generation
- Pytest: Automated testing
- Git and GitHub: Version control

## 5. Database Architecture

### Relational Database

SQLite is responsible for structured application data.

Planned entities:

- Users
- Episodes
- Jobs
- Conversations
- Messages

### Vector Database

Qdrant stores transcript chunk embeddings
and their associated metadata.

Each vector record should include information such as:

- Chunk ID
- Episode ID
- Original text
- Start timestamp
- End timestamp
- Speaker

## 6. API Architecture

The application exposes REST API endpoints.

Planned endpoints:

- POST /api/v1/episodes
- GET /api/v1/episodes
- GET /api/v1/episodes/{episode_id}
- GET /api/v1/jobs/{job_id}
- POST /api/v1/chat

## 7. Background Processing

Transcript ingestion may require time-consuming operations.

The application uses background job processing
to handle transcript parsing, chunking and embedding generation.

Each job has a unique identifier and a processing status.

Possible job statuses:

- pending
- running
- completed
- failed

The initial implementation uses FastAPI BackgroundTasks.
A durable task queue may be introduced for production deployment.

## 8. Error Handling and Observability

The application should provide:

- Input validation
- Centralized error handling
- Structured logging
- Request tracking
- Job status tracking
- Performance monitoring

## 9. Project Limitations and Future Improvements

Planned improvements include:

- Durable background job processing
- PostgreSQL integration
- Advanced retrieval strategies
- Hybrid search
- Reranking
- Evaluation of RAG responses
- Production deployment
- Authentication and authorization

## 10. Project Status

Status: Under Development

This document describes the planned architecture.
It will be updated as new components are implemented.
