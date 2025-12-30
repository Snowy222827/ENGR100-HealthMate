# ENGR100 Project: Prompt-Tuned Health Expert using Qwen3-8B

## Overview

This repository documents our ENGR100 course project at Zhejiang University International Campus (ZJUI), where we transform the **Qwen3-8B** large language model into a specialized **healthcare expert** through prompt engineering. The model is deployed locally using **Open WebUI**, providing an interactive and privacy-preserving interface for health-related queries.

Instead of modifying model weights, we leverage **prompt design**, **system instructions**, and **contextual framing** to guide the model’s behavior—ensuring reliable, empathetic, and fact-based responses aligned with general health knowledge, while clearly disclaiming that it is **not a substitute for professional medical advice**.

---

## Features

- **Specialized Persona**: Prompt-tuned to act as a knowledgeable, cautious, and user-friendly health information assistant.
- **Local Deployment**: Runs entirely on local infrastructure using Open WebUI + Ollama (or compatible backend), ensuring data privacy.
- **Safety-Aware Responses**: Includes built-in disclaimers, avoids diagnostic claims, and encourages consultation with qualified healthcare providers.

## Model & Tools

- **Base Model**: [`Qwen3-8B`](https://huggingface.co/Qwen/Qwen3-8B) (used via GGUF quantized version for local inference)
- **Inference Backend**: Ollama (or LM Studio / llama.cpp-compatible runner)
- **Frontend Interface**: [Open WebUI](https://github.com/open-webui/open-webui)
- **Prompt Engineering**: Custom system prompt + response guidelines (see `prompts/health_expert_prompt.txt`)

## Setup Instructions

### 1. Pull the Model (via Ollama)

Make sure [Ollama](https://ollama.com/) is installed on your macOS/Linux/Windows system.

```bash
ollama pull qwen3:8b
```

> 💡 If a native `qwen3:8b` tag is unavailable, use a community-converted GGUF version from Hugging Face (e.g., from TheBloke) and load it via `llama.cpp` or Ollama-compatible wrappers.

### 2. Launch Open WebUI (via Docker)

```bash
docker run -d -p 3000:8080 \
  -v open-webui:/app/backend/data \
  --name open-webui \
  --restart always \
  ghcr.io/open-webui/open-webui:main
```

### 3. Configure the Health Expert Prompt

1. Open Open WebUI in your browser (`http://localhost:3000`)
2. Create a new **Preset** or **Model Configuration**
3. Set the **System Prompt** to the content in [`prompts/health_expert_prompt.txt`](./prompts/health_expert_prompt.txt)
4. Select `qwen3:8b` as the model

> Example system prompt includes:
> - Role definition (“You are a health information assistant…”)
> - Behavioral guidelines (empathy, clarity, non-diagnostic stance)
> - Safety disclaimers
> - Response formatting rules

### 4. Test & Interact

Ask questions like:
- _“What are common symptoms of vitamin D deficiency?”_
- _“How can I improve my sleep hygiene?”_
- _“Explain the difference between HDL and LDL cholesterol.”_

The model should respond with accurate, referenced, and cautious information—never claiming to diagnose or treat.

## Team Members

- **Name**: Cao yuming
- **Name**: Ding Zhengyang
- **Name**: Feng He
- **Name**: Gao lexuan
- **Name**: Samval Harutyunyan
- **Name**: Xu zhaokun
- **Name**: Zheng Hao

## Acknowledgements

- [Qwen Team](https://qwenlm.github.io/) for the Qwen3 series
- [Open WebUI](https://openwebui.com/) for the open-source chat interface
- ENGR100 Instructors and TAs at ZJUI for guidance and support
