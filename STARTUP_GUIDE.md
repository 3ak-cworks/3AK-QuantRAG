# 3AK-QuantRAG: Quick Startup Guide

Welcome to **3AK-QuantRAG**! This guide is designed to help you go from a fresh `git clone` to a fully operational multi-agent intelligence layer querying your quantitative data.

## Step 1: Environment Setup

1. **Clone the repository:**
   ```bash
   git clone https://github.com/Ak-coder1/3AK-QuantRAG.git
   cd 3AK-QuantRAG
   ```

2. **Create and activate a virtual environment:**
   ```bash
   python3 -m venv venv
   source venv/bin/activate
   ```

3. **Install standard dependencies:**
   While this repository relies on your specific quantitative ecosystem, you will need the core agentic dependencies at a minimum:
   ```bash
   pip install flask flask-cors duckdb pyyaml
   ```

## Step 2: Configuration & Credentials

1. **Configure `config.yaml`:**
   Open `config.yaml` in the root directory. This acts as the brain for your LLM setup.
   - Choose your default LLM provider under `provider:`.
   - Update `models:` if you wish to override the default routing, SQL, and synthesis models.
   
2. **Set API Keys:**
   **DO NOT commit real API keys to the repository.** Replace the placeholder values under `llm.keys` with your actual API keys (e.g. NVIDIA, Groq, Anthropic, Gemini).

## Step 3: Integrating Your Data

By default, the SQL engine (Data Engine) looks for your Parquet data stores.
1. Place your Parquet files in `data/parquet/` (or update the `paths.data_dir` in `config.yaml`).
2. Define the schema in `context/catalog/` so the semantic parser can inject your precise tabular definitions into the LLM logic layer.

## Step 4: Running the Server

Start the API Gateway to expose the multi-agent Orchestrator:
```bash
export PYTHONPATH=.
python3 finchat/api/server.py
```
*(The server defaults to port 5000 and is accessible via `http://localhost:5000/api/finchat/ask`)*

## Step 5: Testing the Orchestrator

You can test the system locally via a `curl` command:
```bash
curl -X POST http://localhost:5000/api/finchat/ask \
     -H "Content-Type: application/json" \
     -d '{"query": "What is the market stance as of today based on Nifty500 and market breadth?", "provider": "nim"}'
```

## Next Steps
- Review the `README.md` for architectural concepts (Intent Router, Data Engine, Synthesizer).
- Read the documentation in `docs/` to expand your Hybrid RAG capabilities.
