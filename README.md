Advanced RAG Q&A with Multi-Vector Retrieval

This project implements an advanced Retrieval-Augmented Generation (RAG) pipeline designed for question-answering over PDF documents. 
It utilizes Multi-Vector Retrieval by indexing document summaries while retrieving original full-page context to enhance search accuracy.


Key Features

Multi-Vector Retrieval: Instead of embedding raw chunks, this system generates and embeds concise summaries of each page. This improves the "findability" of relevant content by focusing on high-level semantics during the search phase.

High-Performance LLM: Powered by Llama-3.3-70B via Groq for both rapid summary generation and detailed final answer synthesis.

GPU-Accelerated Search: Uses FAISS-GPU for ultra-fast similarity searches.

Interactive UI: A clean, user-friendly interface built with Gradio for document uploading and real-time streaming of answers.

Contextual Integrity: Uses PyMuPDF for high-quality text extraction that maintains page-level metadata.

System Architecture

The pipeline operates in three distinct phases:

Ingestion:
PDF is loaded and split by page using fitz.
Each page is processed through a Summary Chain to create a 2-3 sentence overview.
Summaries are stored in a FAISS vector store, while original pages are mapped to an In-Memory Docstore using unique IDs.

Retrieval:
User questions are embedded and compared against the page summaries.
The MultiVectorRetriever identifies the best summary and fetches the corresponding full page content.

Generation:
The retrieved context and original question are formatted into a structured prompt.
Llama-3.3 generates a bulleted, accurate response based solely on the provided document.

Installation:
Ensure you have a Python 3.10+ environment. You can install the required dependencies using the following command:

Bash

pip install -qU numpy==1.26.4 PyMuPDF langchain langchain-community langchain-groq gradio sentence-transformers faiss-gpu torch torchvision torchaudio

Getting Started

Obtain an API Key: Sign up at Groq Cloud to get your API key.
Set Environment Variable: Replace "API_KEY" in the script with your actual key:

Python

os.environ["GROQ_API_KEY"] = "your_groq_api_key_here"
Run the Application: Execute the cells in the notebook.

Access the UI: Open the local URL (http://0.0.0.0:7860).

Requirements & Technologies

Orchestration: LangChain
LLM Provider: Groq (Llama-3.3-70B)
Vector Database: FAISS

Embeddings: sentence-transformers/all-MiniLM-L6-v2

Frontend: Gradio
