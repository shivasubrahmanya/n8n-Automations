# 📚 Amazon Annual Report RAG Chatbot

This repository contains two **n8n** workflows that together implement a **Retrieval-Augmented Generation (RAG)** system for querying Amazon’s Annual Report.  
Using **Pinecone**, **Ollama embeddings**, and **Google Gemini**, you can upload a PDF report, store it as vector embeddings, and interact with it via a chatbot.

---

## 🔍 What is RAG?
**Retrieval-Augmented Generation** combines:
1. **Retrieval** – Fetch relevant document chunks from a vector database.
2. **Augmentation** – Add these chunks to the LLM prompt.
3. **Generation** – Use an LLM to produce a final, context-aware answer.

This project uses:
- **DriveToVector** → Data ingestion & embedding.
- **VectorChat** → Querying & chat interface.

---

## 📂 Workflows

### **1️⃣ DriveToVector** – Data Ingestion Workflow
**Purpose:**  
Takes a PDF (Amazon’s Annual Report) from Google Drive, processes it into vector embeddings, and stores them in Pinecone for later retrieval.

**Main Steps:**
1. **Manual Trigger** – Start workflow manually.
2. **Google Drive Download** – Downloads the PDF from a specified file ID.
3. **Document Loader & Splitter** – Splits text into manageable chunks using recursive character splitting.
4. **Ollama Embeddings** – Uses `nomic-embed-text:latest` to generate embeddings.
5. **Pinecone Vector Store** – Inserts embeddings into the `amazon` index, namespace `AMAZON`.

---

**Requirements:**
- n8n (latest)
- Google Drive API credentials
- Pinecone API credentials
- Ollama running locally (`ollama pull nomic-embed-text:latest`)

<br>

### **2️⃣ VectorChat** – Chatbot Workflow
**Purpose:**  
Enables interactive question-answering over the stored document using RAG.

**Main Steps:**
1. **Chat Trigger** – Listens for incoming user messages.
2. **Amazon Agent** – Orchestrates retrieval and response generation.
3. **Memory Buffer** – Maintains conversation context.
4. **Embedding & Retrieval** – Converts queries into embeddings, fetches relevant vectors from Pinecone.
5. **Google Gemini** – Generates a natural language answer, augmented with retrieved document chunks.

**Requirements:**
- n8n (latest)
- Pinecone API credentials
- Ollama running locally (`ollama pull nomic-embed-text:latest`)
- Google Gemini (PaLM) API credentials

---

## ⚙️ Setup Instructions

1. **Import Workflows**  
   - In n8n: `Workflows → Import from File` → Select `DriveToVector.json` and `VectorChat.json`.

2. **Configure Credentials**  
   - **Google Drive**: Set file ID for your PDF.  
   - **Pinecone**: Add API key & index name (`amazon`).  
   - **Ollama**: Ensure embeddings model is installed.  
   - **Google Gemini**: Add API key.

3. **Run DriveToVector First**  
   - Populates Pinecone with PDF data.

4. **Run VectorChat**  
   - Chat and query the stored document.

---

## 💡 Example

**User:**  
> What was Amazon’s total revenue in 2024?

**Bot:**  
> Amazon’s total revenue in 2024 was X, driven primarily by AWS and e-commerce sales...

---

## 📜 License
MIT License — feel free to use, modify, and distribute.

---

**Author:** Shivasubrahmanya K C  
**Created with:** Using n8n, Pinecone, Ollama, and Google Gemini
