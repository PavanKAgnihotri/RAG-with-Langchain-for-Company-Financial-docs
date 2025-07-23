# RAG-with-Langchain-for-Company-Financial-docs

This project is a Retrieval Augmented Generation (RAG) chatbot designed to answer questions based on information found within a collection of PDF financial documents.

Here's a breakdown of what it does:

Ingests Documents: It takes PDF files from a specified directory.

Processes Text: It extracts the text from the PDFs and splits it into smaller, manageable chunks.

Creates a Searchable Index: It converts these text chunks into numerical representations called embeddings and stores them in a searchable database (FAISS index). This index allows for quick retrieval of relevant text based on a query.

Answers Questions: When the user ask a question, it uses the FAISS index to find the most relevant chunks of text from the financial documents. It then provides these retrieved text chunks as context to a language model (a Hugging Face model) along with the user's question, allowing the model to generate an informed answer based only on the provided document context.

LangChain is a framework designed to help one to develop applications powered by language models. Think of it as a toolkit that makes it easier to connect language models (like the Hugging Face) with other sources of data (like financial documents) and create more complex applications like chatbots.

Here are some important LangChain topics and how they are used in my project:

Document Loaders (PyMuPDFLoader): LangChain provides tools to load data from various sources. Here, PyMuPDFLoader is used to specifically load content from the PDF files. It reads the text and metadata from each page, turning the documents into a format LangChain can work with.

Text Splitters (RecursiveCharacterTextSplitter): Large documents are hard for language models to process all at once. Text splitters break down the documents into smaller, manageable chunks. RecursiveCharacterTextSplitter is used here to split the PDF text while trying to keep related text together, which is important for maintaining context.

Embeddings (HuggingFaceEmbeddings): Embeddings are numerical representations of text. Models like BAAI/bge-small-en-v1.5 convert the text chunks into these numerical vectors. LangChain provides an interface (HuggingFaceEmbeddings) to easily use these models. These embeddings capture the semantic meaning of the text, allowing the computer to understand the relationships between different pieces of text.

Vector Stores (FAISS): A vector store is a database designed to store and search these text embeddings efficiently. FAISS (Facebook AI Similarity Search) is a popular library for this. LangChain provides an integration with FAISS (FAISS.from_documents, FAISS.load_local) to create and load a searchable index of the document chunks based on their embeddings. This is what allows the chatbot to quickly find relevant document pieces when user ask a question.

Chains/Pipelines (LLMChain, HuggingFacePipeline): LangChain allows one to combine different components into sequences called chains or pipelines.
   1. HuggingFacePipeline is used to easily integrate a Hugging Face language model (google/flan-t5-base) into this LangChain flow.
   2. LLMChain is a specific type of chain that takes a language model (llm) and a prompt template (prompt) and runs them together. It formats         the input using the template and sends it to the language model.

Prompt Templates (PromptTemplate): A prompt template is a predefined structure for the input the user give to a language model. In this chatbot, the PromptTemplate defines how the retrieved document context and questions from the user are combined into a single input string that the language model will process to generate the answer. It helps guide the language model on how to use the provided context to answer the user's question.

  In summary, LangChain helps by providing pre-built components (DocumentLoaders, TextSplitters, HuggingFaceEmbeddings, FAISS, HuggingFacePipeline, LLMChain, PromptTemplate) that one can easily connect to build the entire RAG workflow, from loading documents to getting an answer from the language model based on those documents.
