### `docker-instructions.md`

````markdown
# 🐳 Docker Instructions for Open WebUI + Ollama (GPU Support)

This guide shows how to run **Open WebUI** with **Ollama** using AMD or NVIDIA GPUs.

---

## 📦 Prerequisites
- Docker & Docker Compose installed
- Ollama installed and working locally → [Install Guide](https://ollama.com/download)
- Open WebUI directory created: `~/open-webui`

---

## 🚀 Steps

### 1️⃣ Clone Open WebUI
```bash
cd ~
git clone https://github.com/open-webui/open-webui.git
cd open-webui
````

---

### 2️⃣ Start Ollama in the background

```bash
ollama serve
```

---

### 3️⃣ Download your model

Example:

```bash
ollama pull llama3:instruct
```

*(Ensure your system has enough RAM — `llama3:instruct` needs \~6GB)*

---

### 4️⃣ Run Open WebUI with GPU support

#### **For NVIDIA GPU**

```bash
docker run -d \
    --gpus all \
    -p 3000:8080 \
    -v ~/.ollama:/root/.ollama \
    -v ./open-webui:/app/data \
    ghcr.io/open-webui/open-webui:main
```

#### **For AMD GPU (ROCm)**

```bash
docker compose -f docker-compose.amdgpu.yaml up -d
```

> Make sure `docker-compose.amdgpu.yaml` exists in your Open WebUI repo.
> If not, copy it from the [Open WebUI GitHub repository](https://github.com/open-webui/open-webui).

---

### 5️⃣ Access Open WebUI

Visit:

```
http://localhost:3000
```

---

## ⚠️ Notes

* Large models may fail on low-RAM systems
* You can delete large models via:

```bash
ollama rm model-name
```

This will also free disk space and prevent others on the same machine from running it.

---

## 🛠 Troubleshooting

* Check logs:

```bash
docker logs <container_id>
```

* Restart containers:

```bash
docker compose down && docker compose up -d
```

---

✅ Done! Your **Fraud Detector Analyst** should now be ready to run on Open WebUI.

```
