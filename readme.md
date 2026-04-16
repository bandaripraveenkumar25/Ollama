# Ollama on Linux Server

This guide explains how to install, configure, and use Ollama to run local large language models (LLMs) on a Linux server.

---

## 📦 Prerequisites

* Linux (Ubuntu, Debian, CentOS, or similar)
* `curl` installed
* Root or sudo access
* (Optional) NVIDIA GPU with CUDA for better performance

---

## 🚀 Installation

Install Ollama using the official script:

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

Verify installation:

```bash
ollama --version
```

---

## ▶️ Start the Service

Run Ollama manually:

```bash
ollama serve
```

Run in the background:

```bash
nohup ollama serve > ollama.log 2>&1 &
```

---

## 🤖 Running Models

Pull and run a model:

```bash
ollama run llama3
```

Other available models:

* mistral
* phi
* codellama

---

## 📡 API Usage

Ollama exposes a local API at:

```
http://localhost:11434
```

Example request:

```bash
curl http://localhost:11434/api/generate -d '{
  "model": "llama3",
  "prompt": "Explain how a Linux kernel works."
}'
```

---

## ⚙️ Systemd Service Setup (Optional)

Create a systemd service file:

```bash
sudo nano /etc/systemd/system/ollama.service
```

Add the following:

```ini
[Unit]
Description=Ollama Service
After=network.target

[Service]
ExecStart=/usr/local/bin/ollama serve
Restart=always
User=root

[Install]
WantedBy=multi-user.target
```

Enable and start the service:

```bash
sudo systemctl daemon-reexec
sudo systemctl enable ollama
sudo systemctl start ollama
```

Check status:

```bash
sudo systemctl status ollama
```

---

## 🧠 Tips

* Use smaller models for low-RAM systems (e.g., phi)
* Ensure sufficient disk space (models can be several GB)
* For GPU acceleration, install NVIDIA drivers and CUDA
* Secure the API if exposing it externally

---

## 🛠 Troubleshooting

**Port already in use**

```bash
lsof -i :11434
```

**Service not starting**

```bash
journalctl -u ollama -f
```

**Reinstall**

```bash
curl -fsSL https://ollama.com/install.sh | sh
```

---

## 📄 License

Refer to the official Ollama documentation for licensing and usage terms.

---
