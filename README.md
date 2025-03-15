# BigData_Assignment04.1

## **PDF & Markdown Chatbot with LLM**

Vemana Anil Kumar

Ashwin Badamikar

Madhura Sunil Adadande

**LIVE LINKS**

fastapi: http://0.0.0.0:8000

streamlit: http://0.0.0.0:8501
 
 redis: port 6379
 
application URL: http://34.46.62.44:8502

Codelabs Link : https://codelabs-preview.appspot.com/?file_id=1onzZthH2AI72qgMpsv3t4V8WDCT_bsVicoxIT6cvyBg#0
 
## **INTRODUCTION**

In this project, we aim to enhance our existing document analysis pipeline by integrating Large Language Models (LLMs) to enable intelligent summarization and Q&A functionalities. The enhanced system builds on our previous assignment by incorporating a user-friendly Streamlit frontend, a robust FastAPI backend, and seamless communication with LLMs via LiteLLM. Users can upload or select parsed PDF documents, ask questions, and receive context-aware answers or document summaries. All components are containerized using Docker and deployed to the cloud using DigitalOcean, ensuring a scalable and production-ready architecture. This solution empowers users to extract insights from documents interactively, leveraging the power of modern LLMs in a real-time application.

## **Technologies:**

Frontend Application: Streamlit

Backend: FastAPI

LLM API Management: LiteLLM

LLM Models: OpenAI GPT-4o, Google Gemini Flash, Claude, DeepSeek, Grok

Document Processing: PyMuPDF, Markdown conversion

Data Transfer and Communication: Redis Streams

Containerization: Docker, Docker Compose

Deployment: DigitalOcean

Logging & Monitoring: Standard Python logging (with extensible support for error handling and performance tracking)

## **PROBLEM STATEMENT**

With the rapid growth of digital documents, especially in PDF formats, accessing relevant information from lengthy and unstructured files has become increasingly time-consuming. The challenge is to create an intelligent system that can automatically extract, summarize, and answer questions based on the content of uploaded documents. Traditional methods lack the ability to provide contextual responses or interactive summaries. This project addresses the need for a scalable, automated solution by integrating advanced LLMs through a seamless frontend-backend architecture. The key challenge lies in orchestrating components for real-time processing, maintaining low latency, ensuring accuracy, and supporting multiple LLM providers with minimal setup effort.



## **ARCHITECTURE DIAGRAM:**

![Assignment4_Part1](https://github.com/user-attachments/assets/8141654a-bff3-4cf1-91b3-c49dc01e4d2b)





## **PROOF OF CONCEPT**

Our application is a full-stack platform that allows users to upload or select previously processed PDF files and interactively query them using state-of-the-art Large Language Models (LLMs). The architecture is modular and can be broken down into three core layers:

1. Document Upload & Processing:
 Users can either upload new PDF documents or select from already parsed ones stored in markdown format. PyMuPDF is used to extract content from uploaded PDFs, and a markdown converter translates this content into a structured format suitable for downstream tasks. This setup ensures that documents are pre-processed and standardized before interaction.

2. LLM Interaction Layer (Summarization & Q&A):
 The core intelligence lies in our use of LiteLLM, which routes requests to multiple LLM providers such as OpenAI GPT-4o, Google Gemini Flash, Claude, Grok, and DeepSeek. The FastAPI backend exposes RESTful endpoints that communicate with LiteLLM and return model responses in real-time. Redis Streams facilitate efficient asynchronous communication and queuing between services.

3. Frontend, Integration, and Deployment:
 The Streamlit frontend offers an intuitive interface where users can select the model of choice, view parsed content, ask contextual questions, and receive summaries. Docker Compose manages and deploys all services in isolated containers. The entire application stack is deployed on a DigitalOcean droplet, ensuring scalability and ease of access from any device.
Challenges and Optimizations:
 Handling large PDF files posed a latency challenge during markdown conversion and LLM processing. We optimized this by caching markdown results and integrating error-handling and retry logic in the LiteLLM calls. Token pricing and usage details are transparently shown to the user after each query, aiding cost visibility and user awareness. Communication bottlenecks between the frontend and backend were resolved by tuning Redis Streams and applying response compression techniques in FastAPI.








## **WALKTHROUGH OF THE APPLICATION**

Open this link: http://34.46.62.44:8502/ to access the deployed application.

On the left sidebar of the Streamlit UI:

Select a parsed PDF from the dropdown or upload a new PDF file.

Choose your preferred LLM model from the list (e.g., GPT-4o, Gemini, Claude).

The LLM response will be shown below with a token usage and cost breakdown for each request.

For backend testing and debugging:

Access the FastAPI interactive API documentation here: http://0.0.0.0:8000/docs

## **APPLICATION WORKFLOW**

The application workflow is designed to provide an interactive user experience for document analysis using LLMs, orchestrated through a modular backend and real-time processing. Here's a step-by-step breakdown of the workflow:

User Interaction (Streamlit Frontend):

The user begins by uploading a new PDF or selecting from previously parsed markdown files.

The user then chooses a preferred LLM model (e.g., GPT-4o, Gemini, Claude, etc.).

The interface provides two main options:

Summarize the content of the document

Chat based on the content


Request Routing (FastAPI Backend):

The frontend sends the request to the appropriate REST API endpoint on FastAPI

FastAPI parses the request, validates it, and prepares the data payload for LLM processing.


Redis Stream Messaging:

The backend pushes the LLM query into a Redis Stream for asynchronous processing.
Redis enables reliable message queuing and scalable handling of multiple user requests.


LLM Processing (LiteLLM Integration):

The message is picked up and routed through LiteLLM, which acts as a unified interface for accessing multiple LLMs.
Based on user selection, LiteLLM routes the query to the appropriate provider (e.g., OpenAI, Google, Anthropic).


LLM Response Handling:

The output from the model is returned back to the backend.
FastAPI formats the response (including token usage and pricing), and sends it back to the frontend.


Frontend Display & Cost Transparency:

The Streamlit app displays the LLM output (summary or answer) along with token count, cost breakdown, and response time.


Deployment & Scalability:

All components (Streamlit, FastAPI, Redis, LiteLLM) run inside Docker containers.
The entire stack is deployed on a Google Cloud droplet for production accessibility.

## **DIRECTORY STRUCTURE**
```
BigData_Assignment04.1/
│
├── backend/
│   ├── __init__.py
│   ├── .env
│   ├── Dockerfile
│   ├── main.py                     
│   ├── llm_chat.py                
│   ├── pdf_extractor.py           
│   ├── pdf_markdown_convertor.py  
│   ├── requirements.txt          
│
├── frontend/
│   ├── .env
│   ├── app.py                     
│   ├── config.toml
│   ├── Diagram_Application_Deployment.png
│   ├── Diagram_Data_Pipeline.png
│   ├── Dockerfile
│   ├── requirements.txt           
│
├── shared/
│   ├── redis_conn.py              
│   ├── constants.py               
│
├── data/
│   ├── parsed_markdowns/          
│
├── .gitignore
├── docker-compose.yaml           
├── README.md
```
## **REFERENCES**

Streamlit

 Official Documentation: https://docs.streamlit.io/

FastAPI

 Official Documentation: https://fastapi.tiangolo.com/
 
 Request Handling & Pydantic Models: https://fastapi.tiangolo.com/tutorial/body/

LiteLLM

 LiteLLM GitHub: https://github.com/BerriAI/litellm
 
 Documentation: https://docs.litellm.ai/

Redis Streams

 Redis Stream Docs: https://redis.io/docs/data-types/streams/
 
 Redis-Py (Python Client): https://redis-py.readthedocs.io/en/stable/

LLM Providers

OpenAI GPT-4o: https://platform.openai.com/docs/guides/gpt

Gemini (Google): https://docs.aimlapi.com/api-references/text-models-llm/google/gemini-2.0-flash-exp

Claude (Anthropic): https://docs.anthropic.com/en/docs


Docker & Deployment

Docker Documentation: https://docs.docker.com/

Docker Compose: https://docs.docker.com/compose/

PyMuPDF (fitz)

 PDF Text Extraction: https://pymupdf.readthedocs.io/en/latest/

## **DISCLOSURES**

WE ATTEST THAT WE HAVEN’T USED ANY OTHER STUDENTS’ WORK IN OUR ASSIGNMENT AND ABIDE BY THE POLICIES LISTED IN THE STUDENT HANDBOOK

AI USAGE DISCLOSURE

For this project, we used AI tools like ChatGPT, DeepSeek, and Claude to enhance various aspects of development debugging code, optimizing SQL queries, and generating explanations for complex concepts. These tools were leveraged to improve clarity, efficiency, and accuracy in our work, but all final decisions, implementations, and analyses were conducted by us.



 






