# 🏆 LangChain JS – Progressive Challenge Set

# 📅 Week 1: Foundations (Prompts, Models, Runnables, Output Parsing)

Level 1 – Basics

        What is a Runnable in LangChain JS, and how does it differ from just calling the model directly?
        Show minimal code:
                Load an Ollama chat model.
                Create a ChatPromptTemplate.
                Pipe it into a StringOutputParser.
                Invoke it with {question: "What is LangChain?"}.

        What’s the difference between PromptTemplate and ChatPromptTemplate? Give an example of when you’d use each.
        Why are few-shot examples useful? Name two concrete benefits.
        How can you enforce JSON output reliably? Write a short snippet showing how to retry if parsing fails.

# 📅 Week 2: Data & Retrieval (RAG)

Level 2 – Retrieval

        Explain the flow of a basic RAG pipeline in JS (end-to-end).
        Show code:
                Load a .txt file.
                Split into chunks with RecursiveCharacterTextSplitter.
                Embed using OllamaEmbeddings.
                Store in FAISS.
                Run a similarity search with k=3.

        What’s the role of a Retriever vs a VectorStore?
        Name two knobs you’d tune in RAG to improve answer quality. Explain why.
        What are two failure modes of RAG (e.g., hallucination, irrelevant chunks) and one fix for each?

# 📅 Week 3: Agents & Tools (LangGraph basics, Architectures)

Level 3 – Agents

        In your own words: what’s the difference between a Chain and an Agent?
        Build a custom tool get_weather(city) and wrap it with LangChain’s Tool interface. Show how an agent might call it.
        Explain the difference between manual tool invocation and automatic tool calling (e.g., OpenAI function calling).
        Show code for a LangGraph with three nodes:
        User input → Weather tool → Summarizer model.
        What’s the main advantage of the micro-agents architecture compared to a single large agent?
        Describe how a mixture-of-agents setup can be used to fact-check answers.

# 📅 Week 4: Memory, Deployment, Advanced Topics

Level 4 – Memory & Production

        Show code: add a BufferMemory to a conversational chain so it remembers previous turns.
        What’s the difference between BufferMemory and ConversationSummaryMemory? Which would you use for very long conversations and why?
        How would you deploy a LangChain JS RAG agent behind an Express API endpoint? Outline the steps.
        Your deployed agent sometimes hallucinates sources in its citations. Give two concrete fixes you could apply.
        You need a free stack (no paid APIs). Which models, embeddings, vector store, and orchestration framework would you pick?
