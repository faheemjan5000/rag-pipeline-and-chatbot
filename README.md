# rag-pipeline-and-chatbot

This repository contains an automated n8n workflow designed to monitor a specific Google Drive folder for new files (Java tutorial documents), process and embed their contents using Google Gemini, store them in a Pinecone vector database, and make them queryable via a LangChain-powered chat agent.

🔁 Workflow Overview
This n8n workflow automates the following steps:

Trigger when a file is created in a specific Google Drive folder.

Download the file from Google Drive.

Preprocess & Embed its content using Google Gemini embeddings.

Store the embedded data into a Pinecone vector database under the Java_tutorial namespace.

Enable querying the vector store via a chat interface powered by a LangChain AI agent and Google Gemini chat model.

🔧 Nodes Description
📂 Google Drive Trigger
Node: Google Drive Trigger

Function: Monitors a specified folder (13Zf4OpYTGAnv642XKn3yN_fOxj_T1xTJ) for new file creation.

Polling: Every minute.

Event: fileCreated

⬇️ Download
Node: Download

Function: Downloads the newly created file using its ID.

🧹 Preprocessing & Embedding
📄 Default Data Loader
Node: Default Data Loader

Function: Loads binary documents for further processing.

🔤 Recursive Character Text Splitter
Node: Recursive Character Text Splitter

Function: Splits large documents into manageable chunks.

🧠 Embeddings Google Gemini
Node: Embeddings Google Gemini

Function: Converts the text into embeddings using the text-embedding-004 model.

🧠 Pinecone Vector Store (Insert)
Node: Pinecone Vector Store

Function: Stores embeddings in the Pinecone vector database.

Index: demo-index

Namespace: Java_tutorial

💬 AI Chat Interface
This setup allows querying the Pinecone-stored documents through a chatbot interface.

📨 Chat Trigger
Node: When chat message received

Function: Initiates workflow on chat message.

🤖 AI Agent
Node: AI Agent

Function: Main LangChain agent handling user input and calling tools.

💬 Google Gemini Chat Model
Node: Google Gemini Chat Model

Model: gemini-1.5-flash

Function: Handles natural language processing and reasoning.

🧠 Pinecone Vector Store (Query Tool)
Node: Pinecone Vector Store1

Function: Retrieves relevant vectors/documents from the Pinecone DB.

Mode: retrieve-as-tool

Tool Name: randomName

Description: call this tool to access the java_tutorial database

🧠 Embeddings Google Gemini (for querying)
Node: Embeddings Google Gemini1

Function: Converts user queries into embedding vectors for comparison.

🧠 Technologies Used
n8n – Workflow automation platform.

Google Drive API – File monitoring and downloading.

Google Gemini (PaLM API) – Embedding & language models.

Pinecone – Vector database for fast similarity search.

LangChain – Framework to build language model-powered agents and tools.

📦 Folder Watched
Google Drive Folder: Link

Folder ID: 13Zf4OpYTGAnv642XKn3yN_fOxj_T1xTJ

✅ Prerequisites
Before activating this workflow, ensure the following:

Your n8n instance is authenticated with:

Google Drive API (OAuth2)

Google Gemini (PaLM API)

Pinecone API

Pinecone Index demo-index exists with namespace Java_tutorial.

🚀 Deployment
Clone this repository or import the workflow JSON into your n8n instance.

Set up your credentials in n8n (Google Drive, Gemini API, Pinecone).

Activate the workflow in n8n.

Start uploading Java tutorials into the specified Google Drive folder.

🙋‍♂️ Use Case
This automation can be used for:

Creating searchable documentation knowledge bases.

Integrating vector search into learning platforms.

Powering AI chatbots with domain-specific knowledge.

📌 Future Improvements
Add file type filtering (e.g., only PDF/DOCX).

Include logging or error-handling steps.

Implement rate limits and batching for large files.
