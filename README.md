# 🔬 Advanced RAG Experiments

A modular sandbox for implementing, evaluating, and comparing advanced Retrieval-Augmented Generation (RAG) techniques to improve context relevance and answer accuracy.

Inspired by [Atlan's Advanced RAG Techniques](https://atlan.com/know/advanced-rag-techniques/).

---

## 📌 Active & Planned Experiments

| # | Technique | Description | Status |
|---|---|---|---|
| 01 | **Hybrid Retrieval** | Sparse (BM25) + Dense (Embeddings) search merged via Reciprocal Rank Fusion (RRF) | ✅ Completed |
| 02 | **Context Re-ranking** | Post-retrieval relevance scoring using Cross-Encoders | ✅ Completed |
| 03 | **Multi-Query Expansion** | Generating query variants using LLMs to widen retrieval scope | ⏳ Planned |
| 04 | **Parent-Child Chunking** | Storing large parent contexts while indexing small child vectors | ⏳ Planned |

---

## 🧪 Experiments 01 & 02: Hybrid Retrieval vs. Cross-Encoder Re-ranking

### Experiment Overview
* **Hybrid Retrieval (BM25 + Dense):** Combines keyword precision with semantic embeddings, merged using Reciprocal Rank Fusion (RRF).
* **Cross-Encoder Re-ranking:** Jointly scores $(\text{Query}, \text{Document})$ pairs post-retrieval to compute deep contextual relevance.

### 📊 Comparative Results (Top Candidate Scores)

| Document Title | Hybrid (RRF Score) | Re-ranker (Cross-Encoder) | Key Insight & Behavior |
|---|:---:|:---:|---|
| **Physiologic changes induced by theophylline...** | `0.9715` | `0.9846` | **Top Match:** Both methods identified this as the highest-relevance context with strong confidence. |
| **Efficacy of caffeine in treatment of apnea...** | `0.9170` | `0.9233` | **High Precision:** Maintains Top-2 status across both pipelines due to exact clinical relevance. |
| **Sudden infant death syndrome (crib death)...** | `0.8215` | `0.8056` | **Stable Ranking:** Consistently captured as a relevant secondary context across both methods. |

---

## 💡 Key Findings & Learnings

1. **Alignment at the Top:** Both Hybrid Retrieval and Cross-Encoder Re-ranking successfully surfaced the exact same top-3 documents in identical order for this query, validating candidate recall.
2. **Precision Scoring:** While Hybrid RRF provides relative ordering based on rank fusion ($0.0 - 1.0$), Cross-Encoder scoring provides absolute semantic probability, making it easier to set confidence thresholds for pruning irrelevant context 
3. **Pipeline Synergy:** Hybrid Retrieval excels at quickly narrowing millions of documents down to candidate pools, while Cross-Encoder Re-ranking acts as an ideal final layer to ensure maximum prompt precision before generation.
