---
title: "RAG Retrieval over the SciPy Codebase"
order: 4
collection: portfolio
excerpt: "Built a scalable retrieval pipeline (chunk → embed → FAISS) to answer natural-language questions over SciPy’s docs and source code."
teaser: projects/nanogpt-domain.png
header:
  teaser: projects/nanogpt-domain.png
---

Built the retrieval core of a Retrieval-Augmented Generation (RAG) system for a large real-world codebase (SciPy). The system ingests documentation and source files, chunks them with overlap, embeds chunks using domain-specific sentence embedding models, and indexes everything in FAISS for fast top-k similarity search. I added query tooling to inspect retrieved chunks and trace results back to the original file paths—enabling qualitative analysis and setting up the foundation for quantitative evaluation (Precision@k/Recall@k) and grounded Q&A.

- GitHub: TODO (paste repo link)
- Demo: TODO (optional)

Notes
=====

What I built
------------
- **Code/doc ingestion:** Recursive file loader to crawl the SciPy repository and collect `.py` (code) and `.rst` (docs) text while safely skipping unreadable files.
- **Chunking with overlap:** Word-based chunking with overlap to preserve context across boundaries; tuned chunk sizes differently for code vs. documentation.
- **Embedding pipeline (GPU):** Batch embedding generation with SentenceTransformers and normalized vectors for retrieval.
  - Used separate embedding models for **code** and **docs** to improve relevance by domain.
- **Vector database (FAISS):** Built and persisted a FAISS `IndexFlatL2` index plus JSONL-style metadata so retrieval can run without recomputing embeddings.
- **Retrieval + inspection:** Query function that embeds the query, retrieves top-k chunk IDs, and prints matched chunks with file paths for debugging and evaluation.

Key takeaways
-------------
- Retrieval quality depends heavily on **chunking strategy** (size + overlap) and **domain-appropriate embeddings** (code vs. docs).
- Persisting the index + metadata makes the system practical: embedding is the expensive step; retrieval becomes fast and repeatable.
- Stress-testing with diverse query styles (API names, conceptual questions, misspellings) is essential before moving to quantitative metrics and LLM-grounded answer generation.
