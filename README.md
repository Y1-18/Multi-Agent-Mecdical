Multi-Agent Medical Assistant

A research-focused, multi-agent medical AI system that combines medical image analysis, retrieval-augmented generation (RAG), and real-time medical web search into a single, extensible assistant.

The system is designed with a modular, agent-based architecture, making it suitable for experimentation, academic research, and portfolio demonstration.

Overview

The Multi-Agent Medical Assistant intelligently routes user inputs (text or medical images) to specialized agents:

Image Analysis Agent – Medical image inference
(Skin lesions, Chest X-rays, Brain tumors)

RAG Agent – Evidence-based answers retrieved from indexed medical documents

Web Search Agent – Real-time medical information retrieval
(PubMed, Tavily, etc.)

A central Decision Agent determines the most appropriate processing path based on user intent and input modality.

System Architecture
┌────────────────────┐
│   Streamlit UI     │  ← app.py (User Interface)
└─────────┬──────────┘
          │
          ▼
┌────────────────────┐
│  Decision Agent    │  ← agents/agent.py
│ (Routing Logic)    │
└───────┬─────┬──────┘
        │     │
        │     │
        ▼     ▼
┌──────────────┐   ┌──────────────────┐
│ Image Agent  │   │   RAG Agent      │
│ (Vision AI)  │   │ (Medical Docs)  │
└──────┬───────┘   └─────────┬────────┘
       │                     │
       ▼                     ▼
┌──────────────┐   ┌──────────────────┐
│ HF / PyTorch │   │ Qdrant Vector DB │
└──────────────┘   └──────────────────┘
          │
          ▼
┌──────────────────┐
│ Web Search Agent │
│ (PubMed/Tavily) │
└──────────────────┘

Decision Agent Logic

The Decision Agent analyzes each request and routes it as follows:

Medical image uploaded → Image Analysis Agent

Clinical or knowledge-based question → RAG Agent

Latest research or guidelines → Web Search Agent

Hybrid queries → Combined RAG + Web Search

This design improves accuracy, scalability, and explainability.

Project Structure
.
├── app.py                      # Streamlit main entry point
├── config.py                   # Central configuration (LLMs, RAG, CV, Search)
├── requirements.txt            # Python dependencies
│
├── agents/
│   ├── agent.py                # Decision / Orchestrator Agent
│   ├── image_analysis_agent.py # Vision-based medical inference
│   └── rag_agent.py            # Retrieval-Augmented Generation logic
│
├── image_analysis_agent/
│   ├── skin_lesion.py          # Swin Transformer (Dermatology)
│   ├── chest_xray.py           # Chest X-ray classification
│   └── brain_tumor.py          # Brain tumor detection
│
├── rag_agent/
│   ├── vectorstore_qdrant.py   # Qdrant integration
│   ├── doc_parser.py           # Medical document parsing
│   └── embeddings.py           # Azure / HF embeddings
│
├── web_search_processor/
│   ├── pubmed.py               # PubMed API integration
│   └── tavily.py               # Tavily search integration
│
└── Docker              # Optional containerization

Medical Image Analysis

Supported image-based medical tasks include:

Skin Lesion Classification (Swin Transformer)

Chest X-ray Disease Detection (Swin Transformer)

Brain Tumor Classification (MRI) (Vision Transformer)

All models are loaded using Hugging Face Transformers and executed with PyTorch.

Retrieval-Augmented Generation (RAG)

Vector Database: Qdrant

Embeddings: Azure OpenAI (text-embedding-3-large, 3072-dim)

Sources:

Clinical notes

Medical PDFs

Guidelines

Textbooks

RAG ensures responses are grounded in verified medical content, significantly reducing hallucinations.

Web Search (Live Medical Data)

For up-to-date or research-oriented queries:

PubMed – Peer-reviewed biomedical literature

Tavily – Real-time web medical search

Search results can be merged with RAG context for hybrid responses.

Technical Stack

Language: Python 3.10+

Frontend: Streamlit

Agents / Orchestration: LangChain, LangGraph, LangSmith

Deep Learning: PyTorch

NLP & Vision Models: Hugging Face Transformers

Vector Database: Qdrant

Web Search: PubMed API, Tavily

LLMs: Azure OpenAI

Containerization: Docker (optional)

Installation & Setup
1️. Clone the Repository
git clone https://github.com/your-username/multi-agent-medical-assistant.git
cd multi-agent-medical-assistant

2️. Create Virtual Environment
python -m venv venv
source venv/bin/activate   # Linux / macOS
venv\Scripts\activate      # Windows

3️. Install Dependencies
pip install -r requirements.txt

4️. Configure Environment Variables

Create a .env file in the project root:

AZURE_OPENAI_API_KEY=your_key
azure_endpoint=https://your-resource.openai.azure.com/
deployment_name=your_chat_deployment
openai_api_version=2024-02-15-preview

QDRANT_URL=your_qdrant_url
QDRANT_API_KEY=your_qdrant_key

TAVILY_API_KEY=your_tavily_key
HUGGINGFACE_TOKEN=your_hf_token

5️. Run the Application
streamlit run app.py

Disclaimer

This project is for research and educational purposes only.

It is NOT a medical device and MUST NOT be used for clinical diagnosis, treatment, or patient care decisions.

Always consult qualified healthcare professionals for medical advice.

Target Audience

AI / ML Engineers

Medical AI Researchers

Healthcare Data Scientists

Recruiters evaluating applied AI system design

Notes for Recruiters

This project demonstrates:

Multi-agent system design

Medical AI pipelines (Vision + NLP)

Azure OpenAI integration

RAG with vector databases

Production-ready configuration management

Responsible AI practices

Built with care for research, learning, and innovation.