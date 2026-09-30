# ⚖️ Judicial Intelligence & Knowledge Graph

An AI-powered judicial intelligence platform that transforms legal documents into a connected knowledge graph and helps users discover relevant judicial cases through AI-assisted keyword extraction, legal case search, and interactive graph visualization.

The system combines **Generative AI, Knowledge Graphs, Neo4j, FastAPI, React, and legal document processing** to provide an interactive environment for exploring relationships between uploaded cases, legal keywords, external cases, courts, parties, and orders.

---

## 🚀 Overview

Legal documents contain large amounts of interconnected information such as:

- Cases
- Courts
- Petitioners
- Respondents
- Orders
- Legal keywords
- Related judicial cases
- Source documents

Traditional keyword-based searching can make it difficult to discover meaningful relationships between these entities.

This project addresses that problem by converting judicial information into a **graph-based representation**.

The platform allows users to:

1. Upload a legal document.
2. Extract text from the document.
3. Generate relevant legal search keywords using AI.
4. Search external judicial case sources.
5. Identify cases related to the extracted keywords.
6. Store relationships in Neo4j.
7. Generate an interactive knowledge graph.
8. Explore cases, courts, parties, orders, and related documents through a web dashboard.

---

## ✨ Key Features

### 📄 1. Legal Document Upload

Users can upload:

- PDF documents
- TXT documents

The backend validates the uploaded file, calculates its SHA-256 hash, and extracts readable text.

Maximum supported file size is **10 MB**.

---

### 🤖 2. AI-Assisted Keyword Extraction

The system extracts legal concepts from uploaded documents.

A hybrid keyword pipeline is implemented:

- Local keyword extraction
- Legal stop-word filtering
- Legal terminology normalization
- Keyword generalization
- Groq-based AI keyword refinement

The system generates up to **6 legal search keywords** for the uploaded document.

If the Groq API is unavailable, the system can fall back to a local heuristic keyword extraction mechanism.

---

### 🔎 3. Judicial Case Search

The generated keywords are used to search external judicial case information.

The project contains an `IndianKanoonService` for retrieving judicial search results.

For each keyword, the system can retrieve multiple candidate results and combine them into a unified candidate pool.

---

### 🧠 4. AI-Based Case Matching

After collecting candidate cases, the system performs cross-keyword matching.

The Groq-powered matching process evaluates whether candidate cases are relevant to the complete set of generated legal keywords.

The implementation uses a configurable relevance threshold, with the current pipeline using:

```text
Minimum relevance score: 0.80
Maximum selected cases: 30
