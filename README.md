# langchain-js-practice

Step-by-step LangChain JS practice roadmap with free resources, weekly exercises, RAG, agents, memory, and deployment.

# 🌟 Overview

This repo is a 4-week hands-on learning path for LangChain JS.
You’ll build real LLM-powered apps using free/local models (Ollama), plus optional integrations (OpenAI, Anthropic, HuggingFace).

# ✅ What you’ll learn

Prompt engineering & model chaining

Retrieval-Augmented Generation (RAG) with FAISS

Tools & Agents (including LangGraph workflows)

Memory for conversations

Deployment with Express

📂 Repo Structure

    langchain-js-practice/
    │── README.md                # This file
    │── .env.example             # Env template
    │── package.json             # npm setup
    │── utils/
    │   ├── env.js               # Env variable validation
    │   └── logger.js            # (optional) Debugging helper
    │
    ├── week1-foundations/
    │   ├── 01-models.js
    │   ├── 02-prompts.js
    │   ├── 03-chain.js
    │   ├── 04-output-parsing.js
    │   └── data/
    │
    ├── week2-rag/
    │   ├── 05-load-docs.js
    │   ├── 06-split-chunks.js
    │   ├── 07-embeddings.js
    │   ├── 08-vectorstore.js
    │   └── 09-rag-pipeline.js
    │
    ├── week3-agents/
    │   ├── 10-custom-tool.js
    │   ├── 11-basic-agent.js
    │   ├── 12-function-calling.js
    │   ├── 13-langgraph.js
    │   └── 14-multi-agent.js
    │
    └── week4-memory-deploy/
        ├── 15-memory-buffer.js
        ├── 16-express-rag-api.js
        ├── 17-conversation-summary.js
        └── 18-deployment-tips.md

# ⚡ Setup

1. Clone & Install
   git clone https://github.com/yourusername/langchain-js-practice.git
   cd langchain-js-practice
   npm init -y
   npm install langchain @langchain/ollama @langchain/community faiss dotenv express

# 2. Setup Environment

    cp .env.example .env
    If using Ollama locally:

    Install Ollama → https://ollama.com

    Pull a model:

      ollama pull llama2
      No API key required 🎉

Optional APIs (OpenAI, Anthropic, HuggingFace) can be added later in .env.

# 📅 Learning Roadmap

# Week 1 – Foundations

    LangChain Models (ChatOllama, OpenAI)
    PromptTemplate & ChatPromptTemplate
    Runnable pipelines (RunnableSequence)
    Output parsers (string, JSON)

    📖 Free Resources:
            LangChain JS: Getting Started
            PromptTemplates
    🛠 Exercises:
            Build a chain that takes {topic} and outputs a JSON with "summary" and "keywords".

# Week 2 – RAG (Retrieval-Augmented Generation)

    Load documents
    Split into chunks
    Embeddings (OllamaEmbeddings)
    Vector stores (FAISS)
    RAG pipeline

    📖 Free Resources:
            LangChain: Document Loaders
            FAISS VectorStore
    🛠 Exercises:
            Index sample.txt into FAISS and query: “What is this text about?”

# Week 3 – Agents & Tools

    Chains vs Agents
    Custom tools
    Function calling (OpenAI style)
    LangGraph basics
    Micro-agents & mixture of agents

    📖 Free Resources:
            LangChain: Tools
            LangGraph Docs
    🛠 Exercises:
            Build a custom get_weather(city) tool and use it in an agent.

# Week 4 – Memory & Deployment

    BufferMemory & ConversationSummaryMemory
    Long conversation management
    RAG API with Express
    Deployment tips (Render, Vercel, Railway)

    📖 Free Resources:
            LangChain: Memory
            Express Docs
    🛠 Exercises:
            Deploy a RAG chatbot API (/chat) with memory.
