# RAG-with-Langchain-for-Company-Financial-docs

This project is a Retrieval Augmented Generation (RAG) chatbot designed to answer questions based on information found within a collection of PDF financial documents.

Here's a breakdown of what it does:

Ingests Documents: It takes PDF files from a specified directory.

Processes Text: It extracts the text from the PDFs and splits it into smaller, manageable chunks.

Creates a Searchable Index: It converts these text chunks into numerical representations called embeddings and stores them in a searchable database (FAISS index). This index allows for quick retrieval of relevant text based on a query.

Answers Questions: When you ask a question, it uses the FAISS index to find the most relevant chunks of text from your financial documents. It then provides these retrieved text chunks as context to a language model (a Hugging Face model) along with your question, allowing the model to generate an informed answer based only on the provided document context.
