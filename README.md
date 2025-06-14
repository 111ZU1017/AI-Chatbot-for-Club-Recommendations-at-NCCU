# AI-Chatbot-for-Club-Recommendations-at-NCCU
An AI-powered chatbot that recommends NCCU student clubs based on user interests, using semantic search and natural language processing to enhance student engagement.

## **File Structure**

```
nccu-chatbot/
│
├── app.py
├── chatbot_chain.py
├── club_data/
│   ├── nccu_club_data_expanded.xlsx
│   ├── nccu_club_data.csv
│   └── __init__.py
│
├── vector_store/
│   ├── embedding_utils.py
│   ├── vector_search.py
│   └── __init__.py
│
├── gradio_ui/
│   ├── ui.py
│   └── __init__.py
│
├── config.py
├── requirements.txt
└── README.md
```

### **File and Folder Descriptions**

#### `app.py`

* **Purpose:** Main entry point of the application.
* **Function:** Runs the chatbot by importing components from other modules (embedding, retrieval, and UI).
* **Relationship:** Integrates all functionalities—loads vector store, builds the chatbot chain, and launches the Gradio UI.

#### `chatbot_chain.py`

* **Purpose:** Orchestrates the core logic of the chatbot using LangChain.
* **Function:** Combines retrieval and generation to respond to user queries using the RAG framework and GPT-4o.
* **Relationship:** Uses functions from `vector_store/` to fetch relevant data and passes results to OpenAI for generation.

### `club_data/`

* **Purpose:** Stores the datasets used for embedding and retrieval.
* **Files:**

  * `nccu_club_data_expanded.xlsx`: The original expanded dataset with detailed club descriptions and keywords.
  * `nccu_club_data.csv`: Cleaned and structured version used for loading into MongoDB.
  * `__init__.py`: Makes the folder a package (optional, for Python import structure).

### `vector_store/`

* **Purpose:** Handles embeddings and semantic search.
* **Files:**

  * `embedding_utils.py`: Contains functions to create embeddings from text using OpenAI's embedding model.
  * `vector_search.py`: Builds and queries the vector index using MongoDB Atlas Vector Search.
  * `__init__.py`: For importability.

### `gradio_ui/`

* **Purpose:** Contains code for the web interface.
* **Files:**

  * `ui.py`: Creates and launches a Gradio interface for user interaction with the chatbot.
  * `__init__.py`: For modular access.

### `config.py`

* **Purpose:** Stores configuration variables such as API keys, collection names, and MongoDB credentials.
* **Function:** Centralizes environment-dependent settings, making the system easier to manage and deploy securely.

### `requirements.txt`

* **Purpose:** Lists all Python dependencies and libraries needed to run the project.
* **Function:** Allows easy setup of the Python environment via `pip install -r requirements.txt`.



## Getting Started

To get started with the NCCU Club Recommendation Chatbot, follow these steps to set up your environment and run the system:

### Prerequisites

Ensure you have access to the following tools/services:

* **Google Colab** (for running the notebook)
* **MongoDB Atlas** (used to store and search embedded documents)
* **OpenAI API Key** (used for embeddings and language model interactions)
* **Google Drive** (to store and access club PDFs and Excel files)

### Installation

Install the necessary Python libraries using pip:

```bash
!pip install pymongo pypdf langchain langchain_community langchain_openai langchain_core gradio chromadb
```

### Data Preparation

1. Upload your **club introduction PDFs** to a folder in your Google Drive (e.g., `/AI/Club/`).
2. Upload your **club metadata Excel file** to a folder in Google Drive (e.g., `/AI/club1/Database_G2.xlsx`).

### API & Environment Setup

Set your OpenAI API key securely using:

```python
os.environ["OPENAI_API_KEY"] = "your_openai_api_key_here"
```

Ensure you connect and authenticate your MongoDB Atlas client with the correct credentials and database names.

### Run the System

1. Mount your Google Drive to access club files.
2. Extract and chunk documents using `PyPDFLoader` and `RecursiveCharacterTextSplitter`.
3. Generate embeddings using `OpenAIEmbeddings`.
4. Store data in MongoDB using `MongoDBAtlasVectorSearch`.
5. Deploy the QA system using `LangChain`’s RAG architecture.
6. Launch a Gradio interface with:

   ```python
   iface.launch()
   ```

You can now ask questions like:

* “Which club should I join if I like photography?”
* “Are there any language learning clubs at NCCU?”

