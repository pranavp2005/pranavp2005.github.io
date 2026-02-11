---
title: "Rule-Based Toolformer (Tool-Using Chatbot)"
collection: portfolio
excerpt: "Built a simplified Toolformer-style assistant that routes queries to tools (math, maps, file search) and uses a lightweight local LLM to format tool outputs into user-friendly answers."
teaser: projects/nanogpt-domain.png
header:
  teaser: projects/nanogpt-domain.png
---

A mini “tool-using” chatbot implemented with **rule-based routing**. The system decides when to call external tools, extracts structured tool inputs from natural language, and then formats raw tool outputs into concise responses using a small open-source LLM.

- GitHub: TODO (paste repo link)
- Demo: TODO (optional)

Notes
=====

What I built
------------
- **Safe Math Tool (AST evaluator):** Parses expressions with Python `ast` and evaluates only whitelisted numeric operations to avoid `eval`-style security risks.
- **Maps / Geocoding Tool:** Calls **OpenStreetMap Nominatim** to convert place names into latitude/longitude, with graceful handling of missing results and API errors.
- **File Search Tool:** Searches a local repo (e.g., SciPy) for filenames matching a query using `os.walk`, returning top-k results efficiently.
- **Tool Registry:** A small registry abstraction to register and retrieve tools by name (extensible design).
- **Dispatcher + Argument Extraction:** Keyword routing plus regex parsing to pass clean arguments (e.g., extracting `"Paris"` from “Find the coordinates of Paris”).
- **Toolformer Wrapper:** A single `toolformer_answer()` function that (1) dispatches to tools and (2) uses a mini LLM to rewrite tool outputs into a clear, user-facing response.

Key takeaways
-------------
- Tool-using assistants require more than “calling an API”: **accurate routing + clean argument extraction** matter as much as the tools themselves.
- Security and robustness are first-class concerns (e.g., **AST-based evaluation** instead of unsafe execution).
- Even small LLMs can be useful for **formatting and response polish**, and practical optimizations like **pipeline caching** significantly improve usability.

Tech stack
----------
Python, AST, Regex, requests, OpenStreetMap (Nominatim), HuggingFace Transformers (`google/flan-t5-small`)
