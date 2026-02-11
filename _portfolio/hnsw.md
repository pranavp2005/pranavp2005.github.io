---
title: "Scalable Retrieval with Project Gutenberg"
order: 6
collection: portfolio
excerpt: "Built an embeddings-based retrieval prototype and a simplified HNSW-style ANN index; instrumented time/peak-memory to study scalability tradeoffs."
teaser: projects/nanogpt-domain.png
header:
  teaser: projects/nanogpt-domain.png
---

Modern AI systems rely on retrieval to fetch the right context before generation. In this project, I built a retrieval indexing prototype over the Project Gutenberg corpus: from dataset validation → text chunking → dense embeddings → hierarchical ANN graph construction (HNSW-style), with profiling to understand runtime and memory bottlenecks.

- GitHub: TODO (paste repo link)
- Demo: TODO (optional)

Notes
=====

What I built
------------

- **Corpus validation + inspection**
  - Loaded and sampled `gutenberg_over_70000_metadata.csv` to verify dataset integrity.
  - Traversed the corpus directory and opened serialized `.pkl` book files to preview contents and confirm expected structure.

- **Text → embeddings pipeline**
  - Implemented overlap-based sliding-window chunking (`chunk_text`) to fit within embedding model input limits.
  - Generated dense embeddings using `sentence-transformers/all-MiniLM-L6-v2` (`embed_book`) to enable nearest-neighbor retrieval in vector space.

- **Simplified HNSW-style ANN index construction**
  - Implemented exponential **level assignment** to create a multi-layer hierarchy with sparse upper layers (hub-like nodes).
  - Built per-layer nearest-neighbor connectivity using vectorized squared-distance computation and NetworkX graphs.

- **Scalability instrumentation**
  - Added a profiling utility to measure **wall-clock time** and **peak memory usage** with `tracemalloc`, enabling data-driven discussion of bottlenecks.

Key takeaways
-------------

- Retrieval quality and speed depend heavily on preprocessing choices (chunk size, overlap, embedding strategy).
- Pairwise distance computation is the dominant bottleneck at scale, motivating hierarchical/approximate methods like HNSW.
- Exponential layer assignment concentrates connectivity in a small number of high-level “hub” nodes, enabling fast navigation during search.
- Measuring both **time and peak memory** is essential for understanding whether an indexing approach will scale.
