# University Policy Assistant — RAG-Powered LLM System

A Retrieval-Augmented Generation (RAG) system built with FLAN-T5-base and FAISS that answers university policy questions by retrieving relevant passages from a curated knowledge base.

## Deliverable for CIS142-6 NLP & Generative AI — Part B

## Setup & Installation

### Option 1: Run in Google Colab (Recommended)

1. Open `University_Policy_Assistant.ipynb` in [Google Colab](https://colab.research.google.com/)
2. Run all cells sequentially
3. Use either file upload or Google Drive mount for the KnowledgeBase

### Option 2: Run Locally

```bash
pip install -r requirements.txt
jupyter notebook University_Policy_Assistant.ipynb
```

### Option 3: Streamlit Web App

```bash
pip install -r requirements.txt
streamlit run app.py
```

## Architecture

```
User Query → Input Filter → Embedding (all-MiniLM-L6-v2) → FAISS Search (k=3) →
    Context + Prompt → FLAN-T5-base → Answer + Source Citations
```

## Knowledge Base

11 policy documents covering:
- Academic Integrity, Assessment & Grading, Attendance Policy, Code of Conduct, Extenuating Circumstances (.txt)
- Student Appeals, Data Protection & Privacy, Library Resources, IT Acceptable Use, Disability Support, Tuition & Fees (.pdf)

## Model

| Component | Model | Params |
|-----------|-------|--------|
| Embeddings | all-MiniLM-L6-v2 | 80MB |
| LLM | google/flan-t5-base | 250M |
| Vector DB | FAISS IndexFlatL2 | In-memory |

## Safeguard

Two-layer protection:
1. **Input keyword filter** — blocks unsafe queries (cheating, hacking, forgery)
2. **Prompt-level guardrails** — LLM instructed to refuse off-topic questions

## Evaluation

| Metric | Method |
|--------|--------|
| Latency | Time per query (measured on CPU) |
| Retrieval quality | Manual inspection of top-3 chunks |
| Hallucination risk | Comparison with/without RAG |

## Limitations

- Small knowledge base (11 documents)
- FLAN-T5-base has limited reasoning capability vs larger models
- Keyword safeguard can be bypassed with synonyms
- No caching — every query re-computes embeddings

## References

Course material: W5-L2 (Prompt Engineering & RAG), W5-lab2 (Advanced RAG), W4-L1 (LLM Foundations), W6-L2 (Deployment & Ethics)
