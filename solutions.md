# ✅ LangChain JS – Solutions

Reference answers for the Progressive Challenges.
👉 Attempt the challenges first before checking here!

# 📅 Week 1 – Foundations (Prompts, Models, Runnables, Output Parsing)

Q1. What is a Runnable?

    A Runnable is a composable building block in LangChain.
    Instead of directly calling a model, you wrap steps like prompts → model → output parsers into a pipeline.
    This makes workflows reusable, testable, and modular.

Q2. Minimal code: Ollama + Prompt + Parser
import "dotenv/config";
import { ChatOllama } from "@langchain/ollama";
import { ChatPromptTemplate } from "@langchain/core/prompts";
import { StringOutputParser } from "@langchain/core/output_parsers";

    const model = new ChatOllama({ model: "llama2" });

    const prompt = ChatPromptTemplate.fromTemplate("Q: {question}\nA:");
    const parser = new StringOutputParser();

    const chain = prompt.pipe(model).pipe(parser);

    const res = await chain.invoke({ question: "What is LangChain?" });
    console.log(res);

Q3. Difference: PromptTemplate vs ChatPromptTemplate

    PromptTemplate → For plain text prompts (single-shot).

    ChatPromptTemplate → For structured chat messages (multi-turn).

    👉 Example: Use PromptTemplate for summarization.
    👉 Use ChatPromptTemplate for chatbots.

Q4. Why few-shot examples are useful?

    Demonstrate output format → reduces invalid answers.

    Guide reasoning style → improves alignment with task.

Q5. Enforcing JSON output
import { JsonOutputParser } from "@langchain/core/output_parsers";

    const parser = new JsonOutputParser();

    try {
      const res = await chain.invoke({ question: "Return a JSON object with keys: summary, keywords" });
      console.log(await parser.parse(res));
    } catch (err) {
      console.error("Parsing failed, retrying...");
    }

📅 Week 2 – RAG (Retrieval-Augmented Generation)
Q6. Flow of RAG pipeline

Load documents.

Split into chunks.

Embed chunks into vectors.

Store vectors in Vector DB.

Query → retrieve top k chunks.

Pass retrieved docs into LLM context.

Generate grounded answer.

Q7. Code: End-to-end RAG
import "dotenv/config";
import fs from "fs";
import { RecursiveCharacterTextSplitter } from "langchain/text_splitter";
import { OllamaEmbeddings, ChatOllama } from "@langchain/ollama";
import { FaissStore } from "@langchain/community/vectorstores/faiss";

const raw = fs.readFileSync("./data/sample.txt", "utf8");
const splitter = new RecursiveCharacterTextSplitter({ chunkSize: 500, chunkOverlap: 50 });
const docs = await splitter.createDocuments([raw]);

const embeddings = new OllamaEmbeddings({ model: "nomic-embed-text" });
const store = await FaissStore.fromDocuments(docs, embeddings);

const retriever = store.asRetriever(3);
const results = await retriever.getRelevantDocuments("What is this text about?");
console.log(results.map(r => r.pageContent));

Q8. Retriever vs VectorStore

VectorStore: persistent storage of embeddings.

Retriever: query interface that fetches top-k similar docs.

Q9. Two knobs to tune

Chunk size / overlap → tradeoff between completeness and noise.

k (retrieval size) → controls recall vs precision.

Q10. Two failure modes & fixes

Hallucination → ask for citations, return chunks alongside answer.

Irrelevant retrievals → improve chunking or embeddings model.

📅 Week 3 – Agents & Tools
Q11. Chain vs Agent

Chain: fixed pipeline of steps.

Agent: dynamic planner that decides which tool/model to call at runtime.

Q12. Custom Tool Example
import { DynamicTool } from "@langchain/core/tools";

const getWeather = new DynamicTool({
name: "get_weather",
description: "Get weather for a city",
func: async (city) => `Weather in ${city}: Sunny, 25°C`,
});

Q13. Manual vs Automatic Tool Use

Manual → developer explicitly calls tool.

Automatic → model chooses when/how to call tool (e.g., function calling).

Q14. Mini LangGraph Example
import { StateGraph } from "@langchain/langgraph";

const graph = new StateGraph()
.addNode("input", async (state) => state.input)
.addNode("weather", async (city) => `Weather in ${city}: Cloudy`)
.addNode("summarize", async (weather) => `Summary: ${weather}`);

graph.addEdge("input", "weather");
graph.addEdge("weather", "summarize");

Q15. Advantage of Micro-Agents

Each agent is specialized.

Easier debugging.

Parallelizable.

Q16. Mixture-of-Agents Example

Multiple agents answer the same question.

Aggregator agent compares and fact-checks.

Reduces hallucination risk.

📅 Week 4 – Memory & Deployment
Q17. BufferMemory Example
import { ChatOllama } from "@langchain/ollama";
import { BufferMemory } from "langchain/memory";

const model = new ChatOllama({ model: "llama2" });
const memory = new BufferMemory();

await memory.saveContext({ input: "Hi" }, { output: "Hello!" });
const past = await memory.loadMemoryVariables({});
console.log(past.history);

Q18. BufferMemory vs ConversationSummaryMemory

BufferMemory → stores all turns (can get large).

ConversationSummaryMemory → compresses into a running summary (better for long chats).

👉 For very long convos, use ConversationSummaryMemory.

Q19. Deploying RAG Agent with Express

Steps:

Setup Express API.

Build chain with retriever + model.

Wrap in POST /chat endpoint.

Return JSON responses.

Deploy to Render/Vercel/Railway.

Q20. Fix Hallucinated Citations

Return retrieved chunks directly in response.

Use map-reduce RAG with strict grounding in retrieved docs.

Q21. Free Stack Choice

Model → Ollama (llama2)

Embeddings → Ollama (nomic-embed-text)

VectorStore → FAISS (free & local)

Orchestration → LangChain JS + Express
