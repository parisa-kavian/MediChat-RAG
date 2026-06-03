[README.md](https://github.com/user-attachments/files/28556831/README.md)
<div align="center">

# MediChat-RAG

### A retrieval-augmented medical Q&A assistant grounded in authoritative clinical sources

<a href="https://colab.research.google.com/github/parisa-kavian/MediChat-RAG/blob/main/MedicChat.ipynb"><img src="https://colab.research.google.com/assets/colab-badge.svg" alt="Open In Colab"/></a>
<img src="https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white"/>
<img src="https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white"/>
<img src="https://img.shields.io/badge/FAISS-0467DF?style=flat-square&logo=meta&logoColor=white"/>
<img src="https://img.shields.io/badge/OpenAI%20GPT--4o--mini-412991?style=flat-square&logo=openai&logoColor=white"/>

</div>

> A **Retrieval-Augmented Generation (RAG)** chatbot that answers health questions using content scraped from **authoritative Mayo Clinic articles** — not the model's open-ended memory. It ships in two flavors: a **stateless** bot that answers each question independently, and a **stateful** bot that remembers recent turns for natural follow-ups.



---

## Why RAG here

General LLMs can hallucinate clinical facts. RAG fixes this by **retrieving relevant passages from trusted documents first**, then asking the model to answer *only from that evidence*. This project grounds every answer in a curated set of Mayo Clinic pages covering heart disease, cancer, diabetes, high blood pressure, and healthy diet.

---

## How it works

```
Mayo Clinic URLs
      │  AsyncHtmlLoader
      ▼
[ HTML scrape ] ──► [ BeautifulSoup clean ] ──► [ RecursiveCharacterTextSplitter chunks ]
      │
      ▼
[ OpenAI Embeddings ] ──► [ FAISS vector index ]
      │
      ▼  user question
[ Semantic retrieval (top-k) ] ──► [ Prompt + GPT-4o-mini (LCEL chain) ] ──► grounded answer
```

The pipeline is orchestrated with the **LangChain Expression Language (LCEL)** using `RunnableParallel` / `RunnablePassthrough`, and token usage is tracked with `get_openai_callback` for cost transparency.

---

## Two variants

| Variant | Behavior | Best for |
| --- | --- | --- |
| **Stateless** | Treats each question independently — no history | One-off factual lookups |
| **Stateful** | Keeps the **last 4 messages** as context | Multi-turn conversations, pronoun resolution ("it", "its") in follow-ups |

---

## Features

- **Authoritative sources** — answers grounded in Mayo Clinic articles, not free-form generation.
- **Full ingestion pipeline** — automated scraping, HTML cleaning, and chunking.
- **Semantic search** — `OpenAIEmbeddings` + **FAISS** retrieve the most relevant chunks by meaning.
- **LCEL orchestration** — clean, composable retrieval-and-generation chain.
- **Conversational memory** — the stateful version resolves context across turns.
- **Cost-aware** — built-in token/cost tracking.

---

## Demo

<p align="center">
  <img src="https://raw.githubusercontent.com/parisa-kavian/MediChat-RAG/main/medichat1.png" width="80%"/><br/>
  <img src="https://raw.githubusercontent.com/parisa-kavian/MediChat-RAG/main/medichat2.png" width="80%"/><br/>
  <img src="https://raw.githubusercontent.com/parisa-kavian/MediChat-RAG/main/medichat3.png" width="80%"/>
</p>

---

## Getting started

```bash
git clone https://github.com/parisa-kavian/MediChat-RAG.git
cd MediChat-RAG
pip install -r requirements.txt
```

Set your OpenAI key as an **environment variable** (never hard-code it):

```bash
export OPENAI_API_KEY="your_key_here"
```

Open `MedicChat.ipynb` in Jupyter or [Colab](https://colab.research.google.com/github/parisa-kavian/MediChat-RAG/blob/main/MedicChat.ipynb) and run the cells.

---

## Repository structure

```
.
├── MedicChat.ipynb     # stateless + stateful RAG pipelines
├── requirements.txt    # dependencies
├── medichat1.png       # demo screenshots
├── medichat2.png
├── medichat3.png
└── README.md           # you are here
```

---

## Tech stack

`LangChain` · `OpenAI GPT-4o-mini` · `OpenAIEmbeddings` · `FAISS` · `AsyncHtmlLoader` · `BeautifulSoup` · `RecursiveCharacterTextSplitter` · `pandas`

---

## Author

**Parisa Kavianpour** — Applied ML Researcher
[Website](https://parisa-kavian.github.io/) · [Google Scholar](https://scholar.google.com/citations?user=Y5cXz8QAAAAJ&hl=en) · [LinkedIn](https://www.linkedin.com/in/parisa-kavianpour/) · [GitHub](https://github.com/parisa-kavian)
