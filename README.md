# 🕵️‍♂️ Fraud Detector Analyst – Open WebUI Assistant

A custom AI assistant built with [Open WebUI](https://github.com/open-webui/open-webui) and [Ollama](https://ollama.com/) to help detect anomalies in financial transactions and flag suspicious patterns.

---

## 🔍 Features

- ⚙️ Powered by local open-source LLMs via Ollama (e.g. `llama3`, `gemma`, or `mistral`)
- 📊 Accepts raw transaction logs or summaries
- 💡 Highlights top suspicious activities for financial fraud detection
- 💬 Code interpreter enabled for deeper log analysis (CSV, JSON, etc.)
- 🌐 Runs fully offline – privacy-friendly and secure

---

## 📸 Preview

<img width="945" height="424" alt="image" src="https://github.com/user-attachments/assets/e7b8683b-d8a6-45c7-94c2-16dd901df5a4" />

---

## 🚀 How to Use

> ⚠️ Requires ~6GB+ RAM for LLMs like `llama3:instruct`.

1. Install [Ollama](https://ollama.com/)
2. Install [Open WebUI](https://github.com/open-webui/open-webui)
3. Run the model (e.g.):
  ```bash
   ollama run llama3
  ```
4. Launch Open WebUI and import the assistant_export.json (if available)
5. Start chatting with your Fraud Detector Analyst!

🧠 Why?
Built as a side project to simulate what a financial analyst AI assistant could do for early-stage fraud detection. Inspired by real-world scenarios in fintech and audit.

📢 Notes
Due to system memory constraints, full model execution may not be shown in demos. However, all setup and assistant logic is open and replicable.

🧑‍💻 Created by
Souptik Chakraborty
Feel free to reach out or fork the repo!

⭐️ Star if helpful!


---

### ✅ Step 4: Optional Files

- `assistant_export.json`: You can export the assistant from Open WebUI and include it.
- `screenshots/preview.png`: Use your last screenshot.
- `docker-instructions.md`: Only needed if you want to document AMD GPU setup, etc.

---

### ✅ Step 5: Git Commands

If you want to quickly create and push:

```bash
cd ~/open-webui/
mkdir -p ~/fraud-detector-open-webui/screenshots
cp <your_screenshot>.png ~/fraud-detector-open-webui/screenshots/preview.png
cd ~/fraud-detector-open-webui

git init
git remote add origin https://github.com/YourUsername/fraud-detector-open-webui.git
touch README.md
# (Paste the content above into README.md)
git add .
git commit -m "Initial commit: Fraud Detector Assistant"
git push -u origin main
