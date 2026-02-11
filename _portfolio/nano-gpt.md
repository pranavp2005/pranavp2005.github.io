---
title: "Domain-Specialized NanoGPT"
order: 5
collection: portfolio
excerpt: "Trained and analyzed small NanoGPT models across Shakespeare/Wikipedia/Math with zero-shot + few-shot transfer, softmax confidence tracking, and Grad-CAM–style token attribution."
teaser: projects/nanogpt-domain.png
header:
  teaser: projects/nanogpt-domain.png
---

A hands-on project training **NanoGPT (character-level GPT)** models on three tiny corpora (Shakespeare, Wikipedia, and a Math textbook) to study how **domain-specific data** reshapes generation. I built an evaluation and interpretability workflow covering **zero-shot vs few-shot transfer**, **softmax confidence dynamics**, and **gradient-based token attribution (Grad-CAM style)**.

- GitHub: TODO (paste repo link)
- Demo: TODO (optional)

Notes
=====

What I built
------------
- **Domain training (3 models):** Implemented a reusable dataset/vocabulary pipeline and trained NanoGPT checkpoints (`iter_*.pt`, `final.pt`) for Shakespeare/Wikipedia/Math.
- **Zero-shot cross-domain evaluation:** Evaluated each trained model on all other corpora (loss + controlled prompt generations) to quantify distribution shift effects.
- **Few-shot transfer:** Fine-tuned from early/mid/late checkpoints on a target corpus and tracked loss to compare adaptation speed vs pretraining maturity.
- **Softmax inspection:** Tracked top token probabilities and **entropy** over checkpoints to analyze confidence sharpening and overconfidence trends.
- **Grad-CAM-style interpretability:** Used embedding-gradient norms to estimate per-input-token importance for next-token predictions; exported results to CSV and generated plots across prompts/checkpoints.

Key takeaways
-------------
- Domain data strongly changes next-token “classification” behavior (both loss and generations).
- Few-shot adaptation is sensitive to how far training has progressed before transfer.
- Softmax entropy provides a practical signal for confidence/saturation over training.
- Gradient-based attribution can reveal how token importance shifts across domains and checkpoints.
