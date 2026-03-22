# Challenge 3 Submission Copy/Paste

Use the sections below directly in the submission portal.

---

## GitHub Repository URL
Paste your public URL here after you push:

`https://github.com/<org-or-username>/<repo>`

Quick publish checklist (Windows / PowerShell):
1. Create a new empty repo on GitHub (public).
2. From this project folder:
   - `git init`
   - `git add .`
   - `git commit -m "Initial hackathon submission"`
   - `git branch -M main`
   - `git remote add origin https://github.com/<org-or-username>/<repo>.git`
   - `git push -u origin main`

Note: `.env`, local databases, and build artifacts are ignored via `.gitignore`.

---

## Project Description (>= 100 characters)
AI Legislative Analyzer is a web app that helps citizens understand Indian laws from uploaded PDF Acts/Bills. It extracts and chunks the text, compresses context to reduce tokens, retrieves the most relevant clauses using hybrid search (semantic + BM25), and generates simple, citation-aware explanations with multilingual output for better accessibility.

---

## Tech Stack (tags)
Suggested tags to enter in the portal (press Enter after each):
- FastAPI
- Python
- React
- Vite
- ChromaDB
- sentence-transformers
- BM25
- Gemini API (Google)
- OpenAI (optional)
- deep-translator

---

## Measurable Results
Token compression results captured by the pipeline (example document: “IT Act 2000 Updated”):
- Original tokens: 25,926
- Compressed tokens: 2,394
- Tokens saved: 23,532
- Compression: 90.77% (≈ 10.83× smaller prompt footprint)

Latency / reliability:
- The API is instrumented and exposes `GET /metrics/latency`.
- If the LLM fails/times out, the system still returns the most relevant clauses as a fallback so the user gets a response.

---

## Failure Narrative (>= 200 characters)
Our first implementation failed in two ways: (1) the backend sometimes didn’t answer because strict citation gating blocked responses when the model missed a citation, and (2) verification could stall on first run due to large model downloads. We learned that reliability matters as much as quality: we added timeouts, better prompting, and safe fallbacks so the system always returns useful output. If we did it again, we would design guardrails and measurable metrics from day one and pre-warm models during startup.

---

## Concept Quiz (quick study notes)
If you get questions related to the rubric, these are the core concepts used:
- Token compression: reduce prompt size while preserving key facts.
- Hybrid retrieval: combine vector similarity + BM25 keyword matching.
- RRF (Reciprocal Rank Fusion): merges ranked lists robustly.
- Citation coverage: ensures factual sentences point back to source clauses.
- Guardrails: timeouts + fallbacks to keep the app responsive.
