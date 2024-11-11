## Conversational RAG with PDF Uploads and Chat History

### Overview
This project presents an end to end Generative AI application: a conversational Question & Answer (Q&A) chatbot that allows users to interact with the content of uploaded PDF files. 
Using RAG (Retrieval Augmented Generation), the chatbot combines the power of LLMs with document retrieval techniques to provide accurate and relevant responses. It maintains conversation history to ensure continuity in interactions, enhancing the user experience.

### Features
- PDF Uploads: Users can upload one or multiple PDF files. The content is processed and stored for querying.
- Conversational Interface: The chatbot maintains a history of interactions, allowing for contextual and follow up questions.
- RAG: Combines LLM capabilities with a retriever that searches through the uploaded documents to find relevant information.
- Session Management: Each user interaction is associated with a unique session ID, ensuring personalized and continuous conversations.
- Streamlit Web Application: A user friendly web interface built with Streamlit.

### User Interface

#### Input Fields:
- Groq API Key: Users must provide their Groq API key to authenticate and use the LLM services.
- Session ID: Users can enter a session ID to maintain their conversation history.
- PDF Uploader: Users can upload PDF files, which the chatbot will use as the knowledge base.
- Question Input: Users can type in their questions to interact with the chatbot.

### Document Processing
- PDF Loading: Uploaded PDFs are read and loaded into the application using a PDF loader.
- Text Splitting: The text content is split into small chunks using a text splitter to ensure efficient processing and retrieval.
- Embeddings Generation: Each text chunk is converted into numerical embeddings using Hugging Face's embedding models.
- Vector Store Creation: The embeddings are stored in a vector store (Chroma) which allows for fast similarity searches.

### RetrievalAugmented Generation (RAG)
- Retriever Setup: A retriever is created from the vector store to fetch relevant documents based on the user's query.
- History Aware Retriever: The retriever is enhanced to be aware of the conversation history, allowing it to consider previous interactions when fetching documents.
- Prompt Engineering: A system prompt is designed to reformulate user questions considering the chat history, ensuring that the LLM understands the question in context. Another system prompt instructs the LLM on how to generate concise and accurate answers using the retrieved context.
- Chain Creation: Question Answering Chain combines the LLM and the answer generation prompt to produce the final answer. Retrieval Chain links the history aware retriever with the question answering chain, forming the core RAG mechanism.

### Conversation Management
- Session State: Streamlit's session state is used to manage conversation history across user interactions.
- Message History: Custom functions are implemented to retrieve and update the chat history associated with each session ID.
- User Feedback: The chatbot's responses and the chat history are displayed back to the user, providing a conversational experience.

### Technologies Used
- Large Language Model (LLM): Groq's Gemma2-9b-It model is used for generating responses. This requires a Groq API key.
- Embeddings Model: Hugging Face's all-MiniLM-L6-v2 model generates embeddings for text chunks.
- Vector Store: Chroma is utilized to store embeddings and perform similarity searches.
- Document Loaders: Used to read and extract text from PDF files.
- Text Splitters: Recursive character text splitter divides large text into smaller chunks suitable for processing.
- Prompt Templates: Custom system prompts are crafted for both question contextualization and answer generation.
- Streamlit: Provides an interactive web interface for users to interact with the chatbot.


### Session and Conversation History
- Session ID: Acts as a unique identifier for each user's conversation, allowing multiple users or sessions to be managed simultaneously.
- Chat History Storage: The chat history is stored in Streamlit's session state as a dictionary, with the session ID as the key.
- Message History Management: Custom functions ensure that the chat history is correctly retrieved and updated for each session.

### Prompts and Chains
- Contextualization Prompt: Ensures that the user's question is understood in context by reformulating it if necessary.
- Answer Generation Prompt: Guides the LLM to produce concise and relevant answers using the retrieved documents.
- Chains: The application uses LangChain's chain mechanisms to sequence the retrieval and generation steps effectively.
