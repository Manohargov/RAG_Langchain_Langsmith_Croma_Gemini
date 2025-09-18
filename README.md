# 📘 Google Gemini RAG Chatbot with LangChain

This project demonstrates how to build a **Retrieval-Augmented Generation (RAG) Chatbot** using **Google Gemini (via LangChain)**.  
It integrates **document loading, text splitting, embeddings, vector storage, and conversational retrieval** with persistent chat history using SQLite.  

---

## 🚀 Features

- **LLM Integration**  
  - Uses `ChatGoogleGenerativeAI` (Gemini-2.5-Flash).  
  - Supports structured outputs with Pydantic models.  
  - Provides jokes, Q&A, and custom prompt templates.  

- **Document Handling**  
  - Load `.pdf` and `.docx` files with `PyPDFLoader` and `Docx2txtLoader`.  
  - Split large documents into manageable chunks with `RecursiveCharacterTextSplitter`.  

- **Embeddings & Vector Store**  
  - Supports Google Generative AI embeddings.  
  - Supports SentenceTransformer embeddings (`all-MiniLM-L6-v2`).  
  - Uses `Chroma` for vector storage and similarity search.  

- **RAG Pipeline**  
  - Retrieval-augmented question answering.  
  - History-aware retriever with context reformulation.  
  - Contextual prompt chaining using `ChatPromptTemplate`.  

- **Database Logging**  
  - SQLite-based logging of user queries and LLM responses.  
  - Persistent **chat history** retrieval per session.  

---

## 📦 Installation

Make sure you have Python **3.9+** installed.  

```bash
git clone https://github.com/yourusername/gemini-rag-chatbot.git
cd gemini-rag-chatbot

# Install dependencies
pip install -r requirements.txt
```

### Dependencies

Key Python libraries:
- `langchain`
- `langchain-google-genai`
- `langchain-core`
- `langchain-community`
- `langchain-chroma`
- `sentence-transformers`
- `pydantic`
- `sqlite3`
- `pdfminer.six`
- `docx2txt`

Install manually if needed:
```bash
pip install langchain langchain-google-genai langchain-community langchain-core langchain-chroma sentence-transformers pydantic pdfminer.six docx2txt
```

---

## 🔑 Environment Setup

Set your **Google API Key** before running:

```bash
export GOOGLE_API_KEY="your_google_api_key"
```

Optional: Enable LangSmith tracing for debugging:
```bash
export LANGCHAIN_TRACING_V2="true"
export LANGCHAIN_ENDPOINT="https://api.smith.langchain.com"
export LANGCHAIN_API_KEY="your_langsmith_api_key"
export LANGCHAIN_PROJECT="GoogleChatBot"
```

---

## ▶️ Usage

### 1. Run LLM for simple queries
```python
llm.invoke("tell me a joke")
```

### 2. Structured output example
```python
output = structured_llm.invoke(review_text)
print(output.dict())
```

### 3. Load and Split Documents
```python
documents = load_documents("./data")
splits = text_splitter.split_documents(documents)
```

### 4. Create Embeddings & Vector Store
```python
vectorstore = Chroma.from_documents(
    documents=splits,
    embedding=embedding_function,
    collection_name="my_collection"
)
```

### 5. Perform Retrieval-Augmented QA
```python
rag_chain.invoke("What are LLMs?")
```

### 6. Store Chat History in Database
```python
insert_application_logs(session_id, "what is prompt?", "LLM explanation...", "gemini-2.5-flash")
```

---

## 🗂 Project Structure

```
├── data/                     # Store your .pdf/.docx documents here
├── rag_app.db                # SQLite database for chat logs
├── chatbot.py                # Main chatbot implementation
├── requirements.txt          # Dependencies
└── README.md                 # Documentation
```

---

## 📝 Example Interaction

```bash
human: what is prompt?
AI: A prompt is the input instruction or query given to an LLM to generate a response.

human: what is counting token?
AI: Token counting refers to how many pieces of text (subwords/words) an LLM processes in a request.
```

---

## 📌 Notes

- Replace file paths (`//Users/manog/...`) with paths relevant to your machine.  
- Ensure your documents are inside the `data/` directory.  
- SQLite database auto-creates on first run.  

---

## 🤝 Contributing

Pull requests are welcome! For major changes, please open an issue first to discuss.  

---

## 📄 License

MIT License © 2025  
