# SmartReader - BGSW FIT.Fest GenAI Hackathon

## About

This is the submission of team **Pheonix** for PHASE 1 of the BGSW FIT.Fest GenAI Hackathon.
A RAG Q&A application to chat with PDF files, also containing images and tables.

## KPI's acheived for phase I

- ✅ Ability to retrieve and store entire textual content available in the form of text and tables into Vector DB efficiently.
- ✅ Ability to provide relevant and accurate response to user queries.
- ✅ Probing questions to get more clarity on user prompts
- ✅ Latency of response to user prompt in less than a minute.
- ✅ Basic UI application to demonstrate Chat- Q&A.

## 📝 - TODO's

- Convert the current pipeline to use Agents.
- Handle string matching in parsed pdf to handle Images.
- Modify current LLM model to handle multimodal input like image for better processing.

## 🛠️ - Low Level Design

- Streamlit is used to build the frontend.
- Allowed file type for uploads are PDFs. Uploaded PDFs are parsed with _PyPDF2_ library for textual content and _tabula-py_ library for tables. Few preprocessing is done on the table content to ensure only the relevant tables get stored.
- The extracted text and tables are split into chunks with the help of _Langchain_'s CharacterTextSplitter.
- These chunks are embedded with the help of embeddings from GoogleGenerativeAIEmbeddings model _"embedding-001"_, and then the vectors are stored in the _Pinecone Vector Database_ with suitable namespace.
- At this point the prerequisites are completed and the user can start chatting with the document.
- When a user asks a question, the question is also vectorized and a similarity search is run on the Vector database for both the Textual chunks and the Tabular chunks to get the most relevant documents for the question.
- This is passed to the LLM model along with the question as the Textual context and Tabular context in chat history.
- This is referred to as the _context_ of the question. The LLM model _gemini-1.5-flash-latest_ is then called to find the answer for the given question.
- The prompt segregates the answer as two types: Information present and Information absent. If the information is absent, the prompt is written in such a way, that the LLM model asks follow up questions, until it is able to comprehend the question fully.
- Based on the requirement of the user, either a textual or tabular response is given in stylized HTML.

## 🕹️ - Installation Instructions

> Prerequisites: Python, pip

1. Navigate to the folder "code_smartReader"

2. Create a virtual environment with either _conda_ or _python_
  
  - With python:
    
    - pip install virtualenv
    - virtualenv -p python3.11 <venv name>
    
    -> for linux:    
      - source ./<venv name>/bin/activate
    -> for windows:
      - source ./<venv name>/Scripts/activate.bat

   - With conda:
    - conda init
    - conda create -n <venv name> python=3.11.9
    - conda activate <venv name>

3. Install the required libraries

  - pip install --no-deps -r requirements.txt

4. Create a .env file in the root directory. Obtain the following API keys and add them in the .env file. Follow syntax of .env.example for reference.

- GOOGLE_API_KEY:
  - https://aistudio.google.com/app/u/1/apikey.
- PINECONE_API_KEY:
  - sign up at https://www.pinecone.io
  - create an index with any name. Eg: "bosch"
  - obtain API KEY from the sidebar of the daashboard.
- PINECONE_INDEX_NAME:
  - Paste the name of the above created Index

5. Start the streamlit file

  - streamlit run main.py

## 🕹️ - For code analysis

> Go through files for understanding of code. Comments added at places to aid in this process.

## 👥 - TEAM DETAILS

Institution - KLE Technological University

- Ravishankar B - 6363663113 - 01fe21bcs177@kletech.ac.in
- Pranav S Bhat - 8861668850 - 01fe21bcs230@kletech.ac.in
- Kushalgouda S Patil - 8105784976 - kspatil.ksp@gmail.com
