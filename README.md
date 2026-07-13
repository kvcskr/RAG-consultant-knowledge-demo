# n8n — RAG Consultant (Company Knowledge Base via WhatsApp)

An internal AI assistant for sales consultants built with n8n and Retrieval-Augmented Generation (RAG). Consultants ask questions via WhatsApp and receive precise answers sourced directly from company documents — in real time.

---

## The Problem It Solves

Sales consultants constantly need to look up product specs, pricing rules, policies, and procedures. Searching through shared drives or asking colleagues breaks focus and slows down sales calls.

This workflow turns company documents into a searchable AI assistant available via WhatsApp — the tool consultants already have on their phone.

---

## How It Works

The workflow is split into two parts:

### Part 1 — Document Ingestion (run once)

```
PDF document on Google Drive
        ↓
Extract and split text into chunks
        ↓
Generate embeddings (OpenAI text-embedding-ada-002)
        ↓
Store vectors in Pinecone index
```

Run this once to build the knowledge base. Re-run whenever documents are updated.

### Part 2 — Consultant Chat (always active)

```
Consultant sends question via WhatsApp
        ↓
Search Pinecone for relevant document fragments
        ↓
GPT-4o builds answer from retrieved context only
        ↓
Answer sent back via WhatsApp
```

The agent answers **only from company documents** — it does not guess or use external knowledge.

---

## Use Cases

| Document type | Example questions |
|--------------|------------------|
| Product catalog | "What are the specs of product X?" |
| Pricing policy | "What discount applies for orders over 10k?" |
| Internal procedures | "What is the return process for damaged goods?" |
| Company guidelines | "Who approves exceptions to standard terms?" |

---

## Tech Stack

| Component | Technology |
|-----------|-----------|
| Automation | n8n |
| AI Model | GPT-4o (OpenAI) |
| Vector Database | Pinecone |
| Embeddings | OpenAI text-embedding-ada-002 |
| Messaging | WhatsApp Business API |
| Document Source | Google Drive |

---

## Setup

1. Add credentials: OpenAI API, Pinecone API, WhatsApp Business API, Google Drive OAuth
2. Set your Pinecone index name in both Pinecone nodes
3. Set the Google Drive file ID of your source PDF
4. Run **Part 1** manually to ingest documents into Pinecone
5. Activate the workflow — Part 2 triggers automatically on incoming WhatsApp messages

