# 🤖 RAG Copilot – Hybrid Search & Reranking

A modular, framework-free **Retrieval-Augmented Generation (RAG)** system that combines dense vector search and sparse keyword search with cross-encoder reranking to deliver accurate, context-aware answers from PDF documents.

---

## 📌 Project Overview

Most basic RAG systems rely only on dense vector similarity, which often fails on exact keywords, technical jargon, and short factual queries.  

This project solves that problem with a **two-stage retrieval pipeline**:

**Hybrid Search (Dense + BM25) → Cross-Encoder Reranking → LLM Generation**

The entire pipeline is built directly on core libraries (no LangChain abstraction) for full transparency and control.

---

## 🛠️ Tools & Technologies

- **Python** – Core language
- **ChromaDB** – Dense vector store
- **sentence-transformers** – Embeddings (`all-MiniLM-L6-v2`) & Cross-Encoder reranker
- **rank-bm25** – Sparse keyword search (BM25)
- **PyMuPDF** – PDF text extraction
- **Groq API** – Fast LLM inference (`openai/gpt-oss-20b`)
- **Streamlit** – Interactive web interface
- **python-dotenv** – Environment variable management

---

## ✨ Key Features

- Framework-free architecture (no LangChain)
- Hybrid retrieval (Dense vectors + BM25)
- Two-stage Cross-Encoder reranking for higher precision
- Sliding window text chunking with adjustable overlap
- Real-time source citation highlighting
- Retrieval latency tracking
- Clean Streamlit UI with PDF upload
- Modular and easy-to-extend codebase

---

## 🧠 Why Hybrid Search + Reranking?

- Dense-only retrieval often misses exact keyword matches
- BM25 catches precise terms and jargon
- Combining both increases **recall**
- Cross-encoder reranking improves **precision** by jointly scoring query + chunk
- Final top chunks are much more relevant before being sent to the LLM

---

## 📁 Project Structure

```
rag-copilot/
├── src/
│   ├── ingester.py          # PDF → text extraction
│   ├── chunker.py           # Sliding window chunking
│   ├── vector_store.py      # ChromaDB dense store
│   ├── sparse_search.py     # BM25 sparse retriever
│   ├── hybrid_retriever.py  # Hybrid + Reranking logic
│   ├── reranker.py          # Cross-encoder
│   ├── generator.py         # Groq LLM
│   ├── evaluator.py         # Optional RAGAS evaluation
│   └── logger.py            # Observability
├── streamlit_app.py         # Main interactive UI
├── app.py                   # CLI version
├── requirements.txt
├── .gitignore
└── README.md
```

---

## 🚀 How to Run the Project

### 1. Clone the repository
```bash
git clone https://github.com/YOUR_USERNAME/rag-copilot.git
cd rag-copilot
```

### 2. Create virtual environment
```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Mac/Linux
source venv/bin/activate
```

### 3. Install dependencies
```bash
pip install -r requirements.txt
```

### 4. Add your Groq API Key
Create a `.env` file in the root folder:
```
GROQ_API_KEY=your_groq_api_key_here
```

### 5. Run the Streamlit App
```bash
streamlit run streamlit_app.py
```

- Upload any PDF from the sidebar  
- Ask questions about the document  
- View answers + source chunks with latency

---

## 📊 Architecture

```
[PDF Document]
      │
      ▼
[PyMuPDF Text Extraction]
      │
      ▼
[Sliding Window Chunker]
      │
      ├──► [Dense Vector Index (ChromaDB)]  ──┐
      │                                        ├──► [Candidate Pool]
      └──► [Sparse Keyword Index (BM25)]     ──┘
                                                  │
                                                  ▼
                                   [Cross-Encoder Reranker]
                                                  │
                                                  ▼
                                   [Top-K Reranked Contexts]
                                                  │
                                                  ▼
                                   [Groq LLM (openai/gpt-oss-20b)]
                                                  │
                                                  ▼
                                   [Answer + Citations UI]
```

---

## 🖼️ Screenshots

*(Add your screenshots here later)*

- Streamlit UI with PDF upload  
- Answer + Source Citations  
- Retrieval latency display  

---

## 👤 Author

**Mubeen Salman**  
Aspiring Data Analyst 

- LinkedIn: [https://www.linkedin.com/in/mubeen-salman-459776364/]  
- GitHub: [https://github.com/MuhammadMubeen04]  

---

## 📄 License

This project is for educational and portfolio purposes.
