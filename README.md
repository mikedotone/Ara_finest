Ara_finest : Chronos Core:
Chronos Core is a self-hosted, evolving AI companion for single-machine deployment (Linux Mint 22, Python 3.10, GTX 1070 8GB VRAM). It uses Ollama for local Mistral 7B inference, ChromaDB for hybrid RAG memory, and Unsloth QLoRA for periodic fine-tuning. Features: temporal awareness, 24/7 daemon (reflections every 15-30 min, training every 60 min), file processing (upload/chunk/embed/summarize), WebSocket chat UI with voice toggle and sleep/wake.
Prerequisites

Python 3.10
CUDA 11.8 (for Torch/Unsloth)
Ollama installed with mistral:7b-instruct-q5_K_M pulled (fallback: q4_K_M)
Embeddings: all-MiniLM-L6-v2 (CUDA if available)

Installation

Clone the repo: git clone <repo-url> && cd Ara_finest
Create/activate venv: python3.10 -m venv venv && source venv/bin/activate
Install deps: pip install -r requirements.txt
Configure config.yaml (e.g., intervals, paths) if needed.

Running

Start Ollama: ollama serve
Launch app: python app.py
Access UI: http://127.0.0.1:8000


Daemon auto-starts; toggle sleep via UI button (edits config.yaml).
Upload files via attach button; processes into RAG.

Key Components

Backend: FastAPI + WebSockets for chat; Ollama for generation.
Memory: SQLite for convos + ChromaDB for vector RAG.
Evolution: Daemon schedules reflections (add to RAG) and QLoRA (4-bit, batch=1, gradient checkpointing; hot-swaps adapters).
UI: Tailwind-styled (glassmorphism, gradients); JS for WebSocket, typing indicator, controls.
Resource Monitoring: Pauses on high CPU/mem via psutil.

Development Notes

Edit in VS Code: Open folder, select Python interpreter, debug via Run menu.
No extras: Strict stack (no LangChain/OpenAI); local-only after setup.
Troubleshooting: Check console logs; ensure CUDA for embeddings/LoRA.
License: MIT

Contributions: Fork, PR with features like full voice (speechrecognition/pyttsx3) or dynamic sidebar.
