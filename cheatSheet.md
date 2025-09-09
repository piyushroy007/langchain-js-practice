📄 LangChain JS Cheatsheet

        Quick reference for LangChain JS essentials.
        Covers prompts, models, chains, RAG, tools, agents, memory, and deployment.

# ⚡ Setup

        npm install langchain @langchain/ollama @langchain/core @langchain/community

# 📝 Prompts

        import { PromptTemplate, ChatPromptTemplate } from "@langchain/core/prompts";

        // Text prompt
        const textPrompt = PromptTemplate.fromTemplate("Summarize: {text}");

        // Chat prompt
        const chatPrompt = ChatPromptTemplate.fromMessages([
        ["system", "You are a helpful assistant."],
        ["user", "{question}"],
        ]);

# 🤖 Models

        import { ChatOllama } from "@langchain/ollama";

        const model = new ChatOllama({ model: "llama2" });

        // Call
        const res = await model.invoke("Hello!");
        console.log(res);

# 🔗 Runnables (pipe syntax)

        import { StringOutputParser } from "@langchain/core/output_parsers";

        const chain = chatPrompt.pipe(model).pipe(new StringOutputParser());

        const output = await chain.invoke({ question: "What is LangChain?" });

# 🗂️ Output Parsers

        import { JsonOutputParser, StringOutputParser } from "@langchain/core/output_parsers";

        const strParser = new StringOutputParser();
        const jsonParser = new JsonOutputParser();

# 📚 Document Loaders & Splitters

        import fs from "fs";
        import { RecursiveCharacterTextSplitter } from "langchain/text_splitter";

        const raw = fs.readFileSync("./data.txt", "utf8");
        const splitter = new RecursiveCharacterTextSplitter({ chunkSize: 500, chunkOverlap: 50 });
        const docs = await splitter.createDocuments([raw]);

# 🔍 Embeddings + VectorStores

        import { OllamaEmbeddings } from "@langchain/ollama";
        import { FaissStore } from "@langchain/community/vectorstores/faiss";

        const embeddings = new OllamaEmbeddings({ model: "nomic-embed-text" });
        const store = await FaissStore.fromDocuments(docs, embeddings);

        const retriever = store.asRetriever(3);
        const results = await retriever.getRelevantDocuments("query");

# 🛠️ Tools

        import { DynamicTool } from "@langchain/core/tools";

        const getWeather = new DynamicTool({
        name: "get_weather",
        description: "Get weather for a city",
        func: async (city) => `Sunny in ${city}`,
        });

# 🤖 Agents

        Chain → fixed pipeline.

        Agent → dynamic decision-maker, calls tools as needed.

        // Pseudo: agent picks tool dynamically
        agent.invoke("What’s the weather in Paris?");

# 🧠 Memory

    import { BufferMemory, ConversationSummaryMemory } from "langchain/memory";

    // BufferMemory → stores full convo
    const bufferMemory = new BufferMemory();

    // SummaryMemory → compresses into summary
    const summaryMemory = new ConversationSummaryMemory({ llm: model });

    🌐 Express API (Deployment)
    import express from "express";

    const app = express();
    app.use(express.json());

    app.post("/chat", async (req, res) => {
      const { query } = req.body;
      const answer = await chain.invoke({ question: query });
      res.json({ answer });
    });

    app.listen(3000, () => console.log("Server running on port 3000"));
