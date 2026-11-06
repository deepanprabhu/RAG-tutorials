# 🔬 Advanced RAG Experiments

A modular sandbox for implementing, evaluating, and comparing advanced Retrieval-Augmented Generation (RAG) techniques to improve context relevance and answer accuracy.

## 📌 Active Experiments

| # | Technique | Description | Status |
|---|---|---|---|
| 01 | **Hybrid Retrieval** | Sparse (BM25) + Dense (Embeddings) search with Reciprocal Rank Fusion (RRF) | 🛠️ In Progress |
| 02 | Multi-Query Expansion | Generating query variants using LLMs to widen retrieval scope | ⏳ Planned |
| 03 | Context Recanking | Cross-encoder re-ranking (e.g., Cohere, BGE) post-retrieval | ⏳ Planned |
| 04 | Parent-Child Chunking | Storing large parent contexts while indexing small child vectors | ⏳ Planned |

---

## 🧪 Technique 01: Hybrid Retrieval

### Overview
Standard dense vector search often struggles with domain-specific jargon, exact key terms, or short alphanumeric queries (e.g., product IDs). **Hybrid Retrieval** combines the keyword precision of sparse search (BM25) with the semantic understanding of dense vector embeddings.

Inspired by [Atlan's Advanced RAG Techniques](https://atlan.com/know/advanced-rag-techniques/#technique-1-hybrid-retrieval).

### Architecture & Pipeline

```text
               ┌────────────────┐
               │   User Query   │
               └───────┬────────┘
                       │
          ┌────────────┴────────────┐
          ▼                         ▼
   ┌─────────────┐           ┌─────────────┐
   │ BM25 Search │           │ Dense Search│
   │  (Keyword)  │           │ (Embedding) │
   └──────┬──────┘           └──────┬──────┘
          │
