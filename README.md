# 🧠 Semantic Search on NiniSite Q&A Forum (PerCQA Dataset)

## 📘 Overview
This project builds an intelligent search engine over informal Persian Q&A content from the **NiniSite** forum using **semantic search** powered by multilingual sentence embeddings. The dataset, PerCQA, includes ~1,000 Persian questions and ~21,000 answers.

We aim to enhance the platform's search experience by replacing traditional keyword-based search with **embedding-based semantic retrieval** using the **BAAI/bge-m3 model** and **LanceDB**. The pipeline includes preprocessing, EDA, semantic search, full-text search, and optional reranking.

---

## 📁 Dataset

- `questions.json`: ~1,000 Persian questions (QID, QBody, CDate)
- `answers.json`: ~21,000 community answers (AID, QID, ABody, ADate, CUsername)

---

## 🔧 1. Preprocessing
Persian NLP preprocessing using **hazm**, **regex**, and **manual mapping**:
- Normalize Arabic ↔ Persian characters (`ي` → `ی`, `ك` → `ک`)
- Remove diacritics (ً ِ ُ ّ etc.)
- Clean symbols and irregular spacing
- Tokenization (Hazm/Parsivar)
- Stopword removal (e.g., که، به، از)
- Stemming & Lemmatization (`رفتند` → `رفت`)
- Normalize stretched words (`عااااااالی` → `عالی`)
- Replace slang (e.g., `خخخ` → laughter)
- Bonus: Fix RTL display in Jupyter via `arabic_reshaper` + `python-bidi`

---

## 📊 2. Exploratory Data Analysis
- Display sample Q&A pairs
- Analyze & visualize:
  - Length distribution (characters/words)
  - Most answered questions (engagement)
  - Peak activity times (bar/line charts, heatmaps)
  - Top contributors (by answer count)
  - Word cloud & n-gram frequency (before/after stopword removal)

---

## 🔍 3. Semantic Search System

### 🧬 Embedding
- Model: [`BAAI/bge-m3`](https://huggingface.co/BAAI/bge-m3)
- Sample usage: encode `QBody`, inspect embedding structure

### 💽 LanceDB Setup
- Define custom `TextEmbeddingFunction` to embed questions via bge-m3
- Schema: `qid`, `qbody`, `embedding`
- Table populated directly from question dataset (embedding generated live)

### 🔎 Semantic Search
- Perform top-5 retrievals for 5 queries
- Manual relevance check

### 📚 Full-Text Search
- Index `qbody` field with LanceDB full-text features
- Run same 5 queries and compare with semantic results

### 🔁 Hybrid Search
- Research hybrid methods (e.g., combining keyword + semantic)
- Explain advantages and trade-offs

### 🧪 Evaluation Metrics (Theory Only)
- Explain: `Precision@k`, `Recall@k`, `MAP`, `MRR`, `NDCG`

---

## 💡 4. Bonus: Reranker for Better Answer Ranking
- Use model like `bge-reranker` or `cross-encoder`
- Rerank results for 5 queries
- Report qualitative differences pre/post reranking

---

## 🛠 Libraries Used
- `hazm`, `parsivar`
- `pandas`, `matplotlib`, `seaborn`
- `sentence-transformers`, `transformers`
- `LanceDB`
- `arabic_reshaper`, `python-bidi` (for RTL fix)

---

## 📌 Highlights
- Persian-specific NLP pipeline
- Use of multilingual embeddings
- LanceDB integration for scalable search
- Real-world Q&A domain with informal, noisy text
- Modular design: preprocessing → vector DB → semantic ranking → reranker

---