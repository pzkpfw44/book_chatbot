import os
import openai
import pickle
import chromadb
from langchain_openai import OpenAIEmbeddings
from langchain_chroma import Chroma
from langchain.text_splitter import RecursiveCharacterTextSplitter
from langchain_community.document_loaders import PyPDFLoader, Docx2txtLoader
from langchain_community.llms import OpenAI

# Load OpenAI API key (replace with your own key)
os.environ['OPENAI_API_KEY'] = "your_openai_api_key_here"

# Define paths
BOOKS_FOLDER = r"C:\Users\Alex\Desktop\Books"  # Folder containing multiple book files
DB_PATH = "chroma_db"

# Step 1: Load book content
def load_books():
    all_text = ""
    for filename in os.listdir(BOOKS_FOLDER):
        file_path = os.path.join(BOOKS_FOLDER, filename)
        if filename.endswith(".pdf"):
            loader = PyPDFLoader(file_path)
        elif filename.endswith(".docx"):
            loader = Docx2txtLoader(file_path)
        else:
            continue  # Skip unsupported files
        
        documents = loader.load()
        all_text += "\n".join([doc.page_content for doc in documents]) + "\n"
    return all_text

# Step 2: Process text and create vector database
def create_vector_store():
    text = load_books()
    splitter = RecursiveCharacterTextSplitter(chunk_size=500, chunk_overlap=100)
    documents = splitter.create_documents([text])
    
    embeddings = OpenAIEmbeddings(openai_api_key=os.environ['OPENAI_API_KEY'])
    vector_store = Chroma.from_documents(documents, embeddings, persist_directory=DB_PATH)
    # Chroma no longer requires manual persistence as it automatically saves data
    print("Vector store created successfully!")
    print("Vector store created successfully!")

# Step 3: Load vector database for querying
def load_vector_store():
    embeddings = OpenAIEmbeddings()
    return Chroma(persist_directory=DB_PATH, embedding_function=embeddings)

# Step 4: Query the AI
def query_ai(question: str):
    vector_store = load_vector_store()
    docs = vector_store.similarity_search(question, k=3)
    context = "\n".join([doc.page_content for doc in docs])
    
    
    client = openai.Client(api_key=os.environ['OPENAI_API_KEY'])
    response = client.chat.completions.create(
        model="gpt-4",
        messages=[
            {"role": "system", "content": "You are an AI assistant trained to answer questions based on the user's books."},
            {"role": "user", "content": f"""Answer the following question based on these book excerpts:
{context}

Question: {question}"""}
        ],
        temperature=0.7  # Ensure compatibility with OpenAI's latest API
    )
    return response.choices[0].message.content

# Example usage
if __name__ == "__main__":
    create_vector_store()  # Run once to build the index
    while True:
        user_question = input("Ask a question about the books: ")
        answer = query_ai(user_question)
        print("AI Answer:", answer)

