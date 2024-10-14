# SmartReader - BGSW FIT.Fest GenAI Hackathon

## About

This is the submission of team **Pheonix** for PHASE 1 of the BGSW FIT.Fest GenAI Hackathon.
A RAG Q&A application to chat with PDF files, also containing images and tables.

## KPI's achieved for phase I

- ✅ Ability to retrieve and store entire textual content available in the form of text and tables into Vector DB efficiently.
- ✅ Ability to provide relevant and accurate responses to user queries.
- ✅ Probing questions to get more clarity on user prompts
- ✅ Latency of response to user prompt in less than a minute.
- ✅ Basic UI application to demonstrate Chat- Q&A.

## 📝 - TODO's
- Handle string matching in parsed PDF to handle Images.
- Modify the current LLM model to handle multimodal input like images for better processing.

## 🛠️ - Low Level Design

- Streamlit is used to build the frontend.
- Allowed file type for uploads are PDFs. Uploaded PDFs are parsed with _PyPDF2_ library for textual content and _tabula-py_ library for tables. Few preprocessing is done on the table content to ensure only the relevant tables get stored.
- The extracted text and tables are split into chunks with the help of _Langchain_'s CharacterTextSplitter.
- These chunks are embedded with the help of embeddings from the GoogleGenerativeAIEmbeddings model _"embedding-001"_, and then the vectors are stored in the _Pinecone Vector Database_ with a suitable namespace.
- At this point, the prerequisites are completed and the user can start chatting with the document.
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

4. Create a .env file in the root directory. Obtain the following API keys and add them to the .env file. Follow the syntax of .env.example for reference.

- GOOGLE_API_KEY:
  - https://aistudio.google.com/app/u/1/apikey.

5. Start the streamlit file

  - streamlit run main.py

## 🕹️ - For code analysis

> Go through files for an understanding of the code. I added comments in places to help with this process.
Sample images
## Objectives 
![image](https://github.com/user-attachments/assets/d30c5dab-a899-42e1-8fa1-58b434c483b6)
## Q and A
![image](https://github.com/user-attachments/assets/6d6c9090-8438-4a89-9f80-ec94a629890b)
![image](https://github.com/user-attachments/assets/36532e47-a2d8-4ebf-90aa-9571e8e06431)

![image](https://github.com/user-attachments/assets/a50a6f82-4f52-4777-bc32-a1848b03ecb5)
## Tables and history memorization
![image](https://github.com/user-attachments/assets/5d5d34e1-260f-4f57-b9f3-00a74020391d)
## Image input 

![image](https://github.com/user-attachments/assets/3d685faa-74fb-4b6c-9410-ab06755f866e)
![image](https://github.com/user-attachments/assets/6048a914-7635-4520-b0f5-edaebd41f0a8)
![image](https://github.com/user-attachments/assets/c181a9a6-4fb7-419f-bdd6-d9a424fceb6e)















