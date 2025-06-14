# AI-Chatbot-for-Club-Recommendations-at-NCCU
An AI-powered chatbot that recommends NCCU student clubs based on user interests, using semantic search and natural language processing to enhance student engagement.


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



## File Structure

This project is organized into several key files and directories that work together to build the NCCU Club Recommendation Chatbot. Below is an overview of the structure and the purpose of each file or folder:

```
NCCU_Club_Chatbot/
│
├── club_data/
│   ├── Database_G2.xlsx            # Excel file containing categorized club metadata such as club name and description
│   └── [PDF files]                 # PDFs from each club with detailed introductions used as source documents
│
├── chatbot_system/
│   └── chatbot.ipynb               # Main Google Colab notebook containing the entire implementation pipeline:
│                                  # - Installs dependencies
│                                  # - Loads and splits documents
│                                  # - Embeds content into vector database
│                                  # - Sets up the RAG chain
│                                  # - Launches the Gradio QA interface
│
├── vectorstore/
│   └── MongoDBAtlasVectorSearch   # Vector search index used to store and retrieve embedded club documents
│
├── gradio_interface/
│   └── interface.py                # Code to launch a simple Gradio interface that allows users to input questions
│
├── .env or user config            # (Optional) File for storing API keys securely (e.g., OPENAI_API_KEY)
│
└── README.md                      # Project overview, setup instructions, usage guide, and citations
```

### File & Folder Descriptions

* **club\_data/**: Contains raw input data. The `Database_G2.xlsx` file includes club categories and descriptions used for keyword matching. PDF files hold rich club information sourced directly from the university.
* **chatbot\_system/chatbot.ipynb**: The central file for your project. It reads input files, preprocesses and embeds them, configures the retrieval pipeline, and sets up the user-facing Q\&A experience.
* **vectorstore/**: Manages embedded vectors using MongoDB Atlas Vector Search for efficient and accurate retrieval.
* **gradio\_interface/**: Launches a simple GUI that allows users to type questions and get intelligent responses from the chatbot.
* **README.md**: A documentation file that explains how to install, run, and contribute to the project.



## Analysis

To analyze and improve student access to club information at NCCU, we developed a Retrieval-Augmented Generation (RAG) chatbot system that leverages both structured and unstructured data. Our goal was to answer the question:
**"How can we help students efficiently discover clubs that match their interests using AI?"**

### Methods

We employed the following steps for analysis:

1. **Data Collection**

   * We gathered data from two primary sources:
     a. An Excel spreadsheet (`Database_G2.xlsx`) containing structured information about club names, categories, and descriptions.
     b. PDF documents submitted by individual clubs, containing more detailed and narrative descriptions of their missions, activities, and membership.

2. **Text Processing**

   * All PDF files were converted into plain text using `PyPDFLoader`.
   * Text was split into chunks using `RecursiveCharacterTextSplitter` to maintain semantic coherence while enabling chunk-level vector embeddings.

3. **Embedding and Storage**

   * Using `OpenAIEmbeddings`, we converted each text chunk into a high-dimensional vector.
   * Vectors were stored in **MongoDB Atlas Vector Search** and **ChromaDB** to support similarity-based retrieval.

4. **Question-Answer System (RAG)**

   * A retriever searched for relevant text based on user queries.
   * Retrieved documents were passed to a language model (`gpt-3.5-turbo` or `gpt-4o`) to generate contextual, natural language answers.
   * Questions and answers were evaluated manually to ensure relevance, clarity, and diversity of responses.

### Visualizations & Outputs

Although the system runs in a code-based interface (Gradio), we analyzed and verified our results through sample queries. Below are a few representative outputs:

| **Query**                                  | **Sample Answer**                                                                                     |
| ------------------------------------------ | ----------------------------------------------------------------------------------------------------- |
| I like to dance. Which club should I join? | You might be interested in joining the NCCU Dance Club or Modern Dance Society.                       |
| Are there any volunteering clubs?          | Yes, clubs like the Community Service Club and Red Cross Youth Division focus on volunteering.        |
| How many types of clubs are there at NCCU? | NCCU has a diverse set of clubs including Academic, Art, Fellowship, Fitness, and Service categories. |

> *Note:* We also observed a common misconception during Innofest: some users expected a voice chatbot. We identified this as a limitation and clarified that our system is currently text-only.

### Key Insights

* **Students value specificity**: Instead of broad summaries, students prefer answers that recommend clubs by name, event type, or activity.
* **Searchable documents improve engagement**: Uploading and embedding rich PDFs allowed us to capture detailed club identities beyond Excel entries.
* **RAG > Static Keyword Search**: A RAG system powered by OpenAI models significantly outperformed static filtering methods by providing contextual and dynamic responses.

These findings support our hypothesis that a hybrid system combining traditional databases and generative AI can enhance student engagement and decision-making when exploring extracurricular options.



## Results

Our project set out to solve the problem:
**"How can we help students efficiently discover clubs that match their interests using AI?"**

### Key Findings

1. **Improved Information Accessibility**
   The chatbot successfully answered over 20 types of student-focused questions, including:

   * Club recommendations based on interests (e.g., dancing, photography, volunteering).
   * Number and categories of clubs available.
   * Club-specific event types and benefits of joining.
     This demonstrated that our Retrieval-Augmented Generation (RAG) system could translate dense PDFs and structured spreadsheets into natural language insights for students.

2. **High-Quality Recommendations**
   By using vector search and OpenAI's GPT models, the system consistently returned club suggestions that matched user queries with context, tone, and specificity—something keyword-based searches could not achieve.

3. **Scalable and Adaptable Framework**
   The use of MongoDB Atlas and LangChain allowed for scalable data ingestion and retrieval. The framework is highly adaptable for other universities or organizations seeking to build similar recommendation systems.

4. **Successful Integration with Gradio**
   The deployment of our chatbot via Gradio provided a simple and user-friendly interface, encouraging interaction during live demos and test scenarios.

### Conclusions

* Our RAG-based chatbot solution effectively addressed the initial problem statement: it helps students quickly and easily find NCCU clubs that align with their interests.
* The blend of structured (Excel) and unstructured (PDF) data made our system more robust and inclusive of club diversity.
* The project demonstrates the practical application of generative AI in improving student decision-making and campus engagement.

### Recommendations for Future Research

* **Voice and Multilingual Support**: Implement speech-to-text and translation to support a broader range of users, including international students and those with disabilities.
* **Club Member Reviews or Testimonials**: Integrate student feedback into the database to offer social proof and deeper insights.
* **Automated Club Updates**: Enable clubs to update their information dynamically via a portal to ensure accuracy over time.
* **Integration with Student Portals**: Embedding this chatbot directly into university platforms could boost visibility and usage.



## Contributors

### Chen, Tzu-Jung (Laura) – Project Manager

* Collected and organized data from Excel and PDF sources.
* Oversaw overall project planning and task delegation.
* Wrote and compiled the final project paper, ensuring coherence and alignment with objectives.

### Pawarun Pungton (Penny) – Coder, Project Manager

* Developed the core codebase for the chatbot system.
* Built and implemented the vector embedding pipeline using OpenAI’s API and LangChain.
* Ensured consistency in data formatting and retrieval structure.
* Co-led the project, contributing to both technical direction and coordination.

### Naphat Nateprakan (Title) – Poster Design, Ideation

* Contributed to the conceptual development of the project idea.
* Assisted with the design and layout of the final poster used for presentations and visual communication.

### Phatharasuda Maneekiang (Baiyoke) – Poster Design

* Designed key elements of the project poster, focusing on clarity and visual appeal.
* Helped translate technical elements into an accessible visual format.

### Nawanun Sangguean (Neena) – Poster Design

* Contributed to the overall creation and design of the project poster.
* Collaborated on formatting, aesthetic cohesion, and final poster assembly.



