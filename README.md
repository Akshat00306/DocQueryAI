# DocQuery AI 📄

> **AI-powered document intelligence and natural-language database querying in one application.**

Upload documents, ask questions in natural language, or query structured data without writing SQL.

<p align="center">
  <a href="https://docquery-ai-omega.vercel.app">
    <strong>DocQuery-AI</strong>
  </a>
</p>

---

## ✨ Features

DocQuery AI provides two AI-powered modes for working with documents and structured data.

### 1. Document Chat — RAG

Upload documents and interact with them using natural language.

* PDF, DOCX, TXT, CSV, XLSX, JSON, PPTX and Markdown support
* Automatic text extraction and chunking
* Gemini-powered document embeddings
* Semantic similarity search with ChromaDB
* Top relevant chunks retrieved for every question
* Context-aware answers generated using Groq LLM

### 2. SQL Query — Text-to-SQL

Query structured data using plain English instead of writing SQL manually.

* Upload CSV, XLSX or database files
* Automatically load data into SQLite
* Extract database schema
* Convert natural-language questions into SQL
* Execute generated SQL against SQLite
* Display query results in a structured table

---

## 🏗️ System Design

DocQuery AI uses a modular full-stack architecture connecting the React frontend with a FastAPI backend, two independent AI processing pipelines, external AI services, and data stores.

<p align="center">
  <img src="https://raw.githubusercontent.com/Akshat00306/DocQueryAI/main/DOCQuery1.png" alt="DocQuery AI System Design" width="100%">
</p>

[DocQuery AI System Design](https://akshat00306.github.io/DOCQuery-Systemdesign/)

### Architecture Components

| Component           | Technology             | Purpose                                                    |
| ------------------- | ---------------------- | ---------------------------------------------------------- |
| Frontend            | React.js               | User interface, file upload, chat and result visualization |
| Backend            | FastAPI                | REST API and application orchestration                     |
| Document Processing | Python                 | File extraction and preprocessing                          |
| RAG Pipeline        | Custom Python Pipeline | Chunking, embedding, retrieval and generation              |
| Embeddings          | Gemini API             | Converts documents and queries into vectors                |
| Vector Database     | ChromaDB               | Stores and retrieves document embeddings                   |
| LLM                 | Groq — Llama 3.1-8b    | Answer generation and SQL generation                       |
| Text-to-SQL         | LangChain              | Converts natural language into SQL                         |
| Database            | SQLite                 | Structured data storage and SQL execution                  |
| Backend Hosting     | Render                 | Hosts the FastAPI application                              |
| Frontend Hosting    | Vercel                 | Hosts the React application                                |

---

## 🔄 How It Works

### Document Chat — RAG Pipeline

#### Document Ingestion

```text
User uploads document
        │
        ▼
   Extract text
        │
        ▼
   Split into chunks
        │
        ▼
Generate Gemini embeddings
        │
        ▼
 Store in ChromaDB
```

#### Question Answering

```text
User asks a question
        │
        ▼
Generate question embedding
        │
        ▼
Similarity search in ChromaDB
        │
        ▼
Retrieve top 3 relevant chunks
        │
        ▼
Context + question → Groq
        │
        ▼
Generate AI response
        │
        ▼
Return answer to user
```

The application retrieves only the most relevant document content and provides it as context to the LLM rather than sending the complete document.

---

### SQL Query — Text-to-SQL Pipeline

```text
CSV / XLSX / DB upload
          │
          ▼
      Load into SQLite
          │
          ▼
    Extract database schema
          │
          ▼
     Natural-language query
          │
          ▼
  Schema + question → Groq
          │
          ▼
       Generate SQL
          │
          ▼
     Execute on SQLite
          │
          ▼
      Return results
```

### Example

Instead of manually writing:

```sql
SELECT product, SUM(sales) AS total_sales
FROM sales
GROUP BY product
ORDER BY total_sales DESC
LIMIT 5;
```

A user can simply ask:

> **Show me the top 5 products by sales.**

The system understands the database schema, generates the SQL query, executes it, and displays the result.

---

## 🧰 Tech Stack

| Layer            | Technology              |
| ---------------- | ----------------------- |
| **Frontend**     | React.js                |
| **Backend**      | FastAPI · Python        |
| **LLM**          | Groq API · Llama 3.1-8b |
| **Embeddings**   | Gemini Embeddings API   |
| **Vector Store** | ChromaDB                |
| **Text-to-SQL**  | LangChain               |
| **Database**     | SQLite                  |
| **Deployment**   | Render + Vercel         |

---

## 📁 Project Structure

```text
DocQueryAI/
│
├── backend/
│   ├── main.py                 # FastAPI server
│   ├── utils.py                # File text extraction
│   ├── sql_agent.py            # Text-to-SQL logic
│   ├── requirements.txt
│   │
│   └── rag/
│       ├── chunker.py          # Text splitting
│       ├── embedder.py         # Gemini embeddings
│       ├── vectorstore.py      # ChromaDB operations
│       ├── generator.py        # Groq LLM generation
│       └── pipeline.py         # RAG pipeline
│
├── frontend/
│   └── src/
│       └── App.js              # React application
│
└── DOCQuery1.png               # System design diagram
```

---

## 📄 Supported File Formats

| Mode              | Supported Formats                                |
| ----------------- | ------------------------------------------------ |
| **Document Chat** | PDF · DOCX · TXT · CSV · XLSX · JSON · PPTX · MD |
| **SQL Query**     | CSV · XLSX · DB · SQLite                         |

---

# ⚙️ Setup & Installation

## Prerequisites

Before running the application, install:

* **Python 3.11+**
* **Node.js 18+**
* **npm**
* **Git**
* **Groq API Key**
* **Gemini API Key**

---

## 1. Clone the Repository

```bash
git clone https://github.com/Akshat00306/DocQueryAI.git
cd DocQueryAI
```

---

## 2. Backend Setup

Navigate to the backend:

```bash
cd backend
```

### Windows

Create the virtual environment:

```bash
python -m venv venv
```

Activate it:

```bash
venv\Scripts\activate
```

Install dependencies:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### Linux

For Ubuntu/Debian:

```bash
sudo apt update
sudo apt install python3 python3-pip python3-venv git
```

Create the virtual environment:

```bash
python3 -m venv venv
```

Activate it:

```bash
source venv/bin/activate
```

Install dependencies:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

### macOS

If Homebrew is not installed, install it from:

[brew.sh](https://brew.sh)

Then:

```bash
brew install python git
```

Create the virtual environment:

```bash
python3 -m venv venv
```

Activate it:

```bash
source venv/bin/activate
```

Install dependencies:

```bash
python -m pip install --upgrade pip
python -m pip install -r requirements.txt
```

---

## 3. Configure API Keys

Create a `.env` file inside the `backend/` directory.

Linux/macOS:

```bash
touch .env
```

On Windows, create a file named:

```text
.env
```

Add:

```env
GROQ_API_KEY=your_groq_api_key_here
GEMINI_API_KEY=your_gemini_api_key_here
```

### API Keys

* **Groq:** [console.groq.com](https://console.groq.com)
* **Gemini:** [aistudio.google.com](https://aistudio.google.com)

> **Security:** Never commit your `.env` file or expose API keys in source code.

Add the following to `.gitignore`:

```gitignore
.env
venv/
__pycache__/
*.pyc
```

---

## 4. Start the Backend

From the `backend/` directory:

```bash
uvicorn main:app --reload
```

Or:

```bash
python -m uvicorn main:app --reload
```

The API will be available at:

```text
http://127.0.0.1:8000
```

FastAPI Swagger documentation:

```text
http://127.0.0.1:8000/docs
```

---

## 5. Frontend Setup

Open a new terminal and navigate to:

```bash
cd frontend
```

Install dependencies:

```bash
npm install
```

Start the React application:

```bash
npm start
```

The frontend will be available at:

```text
http://localhost:3000
```

---

## 6. Run the Complete Application

The backend and frontend should run simultaneously.

### Terminal 1 — Backend

Windows:

```bash
cd backend
venv\Scripts\activate
python -m uvicorn main:app --reload
```

Linux/macOS:

```bash
cd backend
source venv/bin/activate
python -m uvicorn main:app --reload
```

### Terminal 2 — Frontend

```bash
cd frontend
npm start
```

Open:

**http://localhost:3000**

---

## 🔌 API Endpoints

| Method | Endpoint      | Description                             |
| ------ | ------------- | --------------------------------------- |
| `POST` | `/upload`     | Upload and process a document for RAG   |
| `POST` | `/query`      | Query a document using natural language |
| `POST` | `/sql/upload` | Upload and load a database file         |
| `POST` | `/sql/query`  | Query a database using natural language |

---

## 🌐 Deployment

### Frontend

**Platform:** Vercel

**Live Application:**
[docquery-ai-omega.vercel.app](https://docquery-ai-omega.vercel.app)

### Backend

**Platform:** Render

**API:**
[docquery-ai-final.onrender.com](https://docquery-ai-final.onrender.com)

### Deployment Architecture

```text
                         Internet
                            │
                            ▼
                   ┌─────────────────┐
                   │     Vercel      │
                   │  React Frontend │
                   └────────┬────────┘
                            │
                         HTTPS
                            │
                            ▼
                   ┌─────────────────┐
                   │     Render      │
                   │ FastAPI Backend │
                   └────────┬────────┘
                            │
                ┌───────────┴───────────┐
                │                       │
                ▼                       ▼
          RAG Pipeline            Text-to-SQL
                │                       │
                ▼                       ▼
            ChromaDB                 SQLite
                │                       │
                └───────────┬───────────┘
                            │
                  ┌─────────┴─────────┐
                  │                   │
                  ▼                   ▼
              Gemini API           Groq API
```

---

## 🔐 Security Considerations

* API keys are stored using environment variables.
* `.env` files are excluded from version control.
* Uploaded files should be validated before processing.
* SQL queries should be validated before execution.
* User input should be handled carefully to reduce prompt-injection risks.
* Production deployments should use HTTPS.
* Database operations should be restricted to the intended data source.

---

## 💡 Key Concepts Demonstrated

This project demonstrates practical implementation of:

* Retrieval-Augmented Generation (RAG)
* Large Language Models
* Semantic Search
* Text Embeddings
* Vector Databases
* Natural Language Processing
* Text-to-SQL
* LangChain
* FastAPI
* REST APIs
* React.js
* SQLite
* ChromaDB
* Prompt Engineering
* API Integration
* Full-Stack Development
* Cloud Deployment

---

## 🚀 Future Improvements

* User authentication and authorization
* Multi-document conversations
* Persistent chat history
* SQL result visualization and automatic charts
* Hybrid search
* Document reranking
* Streaming LLM responses
* Persistent cloud vector storage
* Advanced SQL validation
* Multi-user support
* Improved responsive UI
* Conversation memory

---

## 👨‍💻 Author

### Akshat Sankalpura

**GitHub:** [@Akshat00306](https://github.com/Akshat00306)

**LinkedIn:** [linkedin.com/in/akshat-ads153](https://linkedin.com/in/akshat-ads153/)

---

## ⭐ Support

If you find **DocQuery AI** useful, consider giving the repository a ⭐ on GitHub.

<p align="center">
  <b>Built with React · FastAPI · LangChain · ChromaDB · SQLite · LLMs</b>
</p>

