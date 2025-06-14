# AI-Chatbot-for-Club-Recommendations-at-NCCU
An AI-powered chatbot that recommends NCCU student clubs based on user interests, using semantic search and natural language processing to enhance student engagement.

### **Project File Structure Overview**

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


