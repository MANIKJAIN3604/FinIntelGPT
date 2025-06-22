🚀 FinancialAdvisorGPT – AI-Powered Financial Analysis Assistant
FinancialAdvisorGPT is a boilerplate RAG (Retrieval-Augmented Generation) + LLM (Large Language Model) based project designed for intelligent financial analysis. It combines unstructured data from PDFs, news, and APIs to generate insightful financial reports using powerful language models like Mistral-Tiny, Mistral-Small, and OpenAI.

Built with FastAPI, MongoDB, ChromaDB, LangChain, and React (submodule), this system demonstrates the fusion of GenAI, NLP, and full-stack software engineering.

✨ Key Features
📊 AI-generated financial insights from:

SEC filings (e.g., 10-K reports)

Stock market APIs

Financial news

Custom user-uploaded PDFs

🔍 RAG pipeline ensures grounded responses (no hallucinations)

⚙️ Parallelized pipelines for fast multi-source data ingestion

🧠 LLM decision-routing: Model decides whether to pull from stock, news, or existing conversation history

🧾 Source-citation & traceable outputs

🧮 Optimized prompt handling, summarization, and long-document support

🧱 Tech Stack
Layer Technology Purpose
Frontend React (submodule) UI to upload PDFs and ask questions
Backend Python, FastAPI Core logic & API handling
LLM Mistral-Tiny, Mistral-Small, OpenAI Language modeling
RAG LangChain Retrieval-Augmented Generation framework
Vector DB ChromaDB (📦) + MongoDB (planned) Store embeddings & documents
Cache Redis (planned) Speed up conversations & pipeline access
Storage MongoDB Store chat history and pipeline states
Misc Docker, Poetry Deployment & dependency management

📦 Installation & Setup
Clone the repository and fetch all submodules:

bash
Copy
Edit
git clone --recursive https://github.com/mburaksayici/finsean.git
cd finsean
Update environment variables:

bash
Copy
Edit
cp .env.example .env

# Edit API keys, LLM model name, and DB settings

Add Sample Documents:

bash
Copy
Edit
mkdir -p uploaded_files
wget -P uploaded_files https://digitalassets.tesla.com/tesla-contents/image/upload/IR/TSLA-Q4-2023-Update.pdf
wget -P uploaded_files https://ir.tesla.com/_flysystem/s3/sec/000162828024002390/tsla-20231231-gen.pdf
Run the full stack (API + React frontend):

bash
Copy
Edit
docker-compose up -d
Visit: http://localhost:5173

🧠 RAG Pipeline Overview
Modular Pipelines:
PDFPipeline → Parses local SEC PDFs, chunks, embeds, stores in ChromaDB.

NewsPipeline → Summarizes and embeds current financial news articles.

StockDataPipeline → Uses APIs to fetch structured financial metrics.

Optimizations:
Each data retrieval pipeline is parallelized for performance.

LLM acts as a router to decide if a query needs:

PDFs (historical reports)

News (real-time insights)

Stock data (numeric trends)

🔄 Conversation Flow
plaintext
Copy
Edit
User Prompt → LLM decides → Fetch from sources → Embed → Summarize (if needed) → Respond
Subsequent chat rounds use stored memory unless new data is required.

Context is reused for relevant questions; expensive RAG pipelines are skipped if unnecessary.

⚠️ Known Limitations & Improvements
Area Issue Status
LangChain Overengineered and poorly documented Under review
Vector DB Chroma (SQLite-backed) used temporarily Switching to Mongo Vector
Caching Redis planned for faster inference & memory caching Not implemented yet
Streaming Partial streaming; needs improvement WIP
RAG Decisioning LLM-based dynamic routing works, but can be refined In progress
Summarizer LLM Used to shrink large context documents ✔️ Done

🧪 Performance
20 PDFs (~30 pages each) + 2 stock sources + 10 news articles:

With parallelism: ~45 seconds

Without: 3–4 minutes

Local inference + summarization → low cost and fast

🧠 LLM Engineering Learnings
LLMs are non-deterministic – retries may be needed

Use structured prompts and summarizers to reduce context size

Don’t expect “newer models” to always perform better

Streamlined UX (like Devin AI) improves user patience

🔮 Future Work
Migrate vector DB to MongoDB Vector Store

Redis caching for chat & pipeline layers

Full chat decision map (e.g., via NetworkX)

Prompt versioning + optimization

Cost analytics dashboard

Resume streaming with status updates

🧾 Sample Prompt Examples
"What are the risks mentioned in Tesla’s 2023 Q4 report?"
"Why are Snowflake stocks declining recently?"
"Summarize Ford’s AI investments over the past year."

📌 Project Goals
Make financial analysis accessible using AI

Build an LLM+RAG framework that's production-grade

Help students and researchers understand how to blend NLP, APIs, and full-stack engineering

📜 License
MIT License
