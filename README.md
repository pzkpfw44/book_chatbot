Book AI Chatbot

Overview

This project is a Knowledge Mining AI that allows users to query their book collection using AI. It reads multiple PDF and DOCX books, processes the content, and provides relevant AI-generated answers based on the books' content.

Features

Supports multiple PDF and DOCX files from a folder
Uses FAISS for fast text search
Integrates OpenAI’s GPT-4 to answer questions
Automatically extracts text and builds a vector database
Interactive CLI-based chatbot

Installation

1️⃣ Install Dependencies

pip install openai langchain faiss-cpu pypdf python-docx

2️⃣ Set Up API Key

Replace your_openai_api_key_here in the script with your actual OpenAI API key, or set it permanently:

setx OPENAI_API_KEY "your_openai_api_key_here"

3️⃣ Place Your Books in the Folder

Create a books/ folder and add all your PDF and DOCX files inside.

4️⃣ Run the Script

python book_ai_chatbot.py

How It Works

Loads and processes all books in books/

Splits text into chunks and stores embeddings in a FAISS vector database

Allows users to ask questions about the books

Retrieves the most relevant excerpts and generates an AI-powered response

Example Usage

Ask a question about the books: What is the main argument of chapter 3?
AI Answer: The chapter discusses...

Future Enhancements

🔹 Web UI using Streamlit

🔹 Support for more file formats (EPUB, TXT)

🔹 Advanced retrieval logic for better answers

