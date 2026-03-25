# alterEGO 🤖

> *An agentic AI personal assistant that represents me on the web — so I can be in two places at once.*

**alterEGO** is an AI-powered portfolio agent built to represent **Alan Muchiri** on his personal website. It answers questions about his career, skills, and background — and actively works to connect interested visitors with him via email. It's not just a chatbot; it's a digital twin with agency.

---

## ✨ Features

- **Conversational AI** — Engages visitors in natural, professional dialogue about Alan's background, skills, and experience
- **Grounded in real context** — Reads Alan's CV (PDF) and a personal summary at startup to stay accurate and on-brand
- **Tool-calling (Agentic)** — Autonomously decides when to invoke tools based on conversation context:
  - 📬 `record_user_details` — Captures name, email, and conversation notes from interested visitors
  - ❓ `record_unknown_question` — Logs any question it couldn't answer for later review
- **Push notifications** — Sends real-time alerts via Pushover whenever a lead is captured or an unknown question is logged
- **Gradio UI** — Clean, chat-based interface deployable on HuggingFace Spaces with zero frontend code

---

## 🧠 How It Works
```
User visits portfolio website
        ↓
Sends a message to alterEGO
        ↓
Agent loads system prompt (CV + summary context)
        ↓
LLM decides: answer directly OR call a tool
        ↓
Tool results fed back → final response streamed to user
        ↓
Alan gets a Pushover ping if a lead or unknown question is recorded
```

alterEGO uses an **agentic loop** — it keeps processing tool calls until the model signals it's done, only then returning a response to the user.

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| LLM | DeepSeek (`deepseek-chat`) via OpenAI-compatible SDK |
| Framework | Gradio (`gr.ChatInterface`) |
| Notifications | Pushover API |
| PDF Parsing | `pypdf` |
| Deployment | HuggingFace Spaces |
| Config | `python-dotenv` |

---

## 📁 Project Structure
```
alterEGO/
├── app.py              # Main application — agent logic, tool handling, Gradio UI
├── me/
│   ├── myCV.pdf        # Source of truth for career history
│   └── summary.txt     # Personal bio / narrative summary
├── .env                # API keys (not committed)
└── requirements.txt    # Python dependencies
```

---

## ⚙️ Setup & Running Locally

### 1. Clone the repo
```bash
git clone https://github.com/alanmuchiri/alterEGO.git
cd alterEGO
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Configure environment variables

Create a `.env` file in the root:
```env
DEEPSEEK_API_KEY=your_deepseek_api_key
PUSHOVER_TOKEN=your_pushover_app_token
PUSHOVER_USER=your_pushover_user_key
```

### 4. Add your personal context

Place your CV at `me/myCV.pdf` and your written summary at `me/summary.txt`.

### 5. Run the app
```bash
python app.py
```

Gradio will launch a local interface at `http://127.0.0.1:7860`.

---

## 🚀 Deploying to HuggingFace Spaces

1. Create a new Space on [HuggingFace](https://huggingface.co/spaces) with the **Gradio** SDK
2. Push this repo to the Space
3. Add your environment variables under **Settings → Repository Secrets**
4. The Space will auto-build and serve the app

---

## 🔐 Environment Variables

| Variable | Description |
|---|---|
| `DEEPSEEK_API_KEY` | API key for DeepSeek (used via OpenAI-compatible client) |
| `PUSHOVER_TOKEN` | Pushover application token for notifications |
| `PUSHOVER_USER` | Pushover user key to receive notifications |

---

## 🗺️ Roadmap

- [ ] Add voice interface (speech-to-text + TTS)
- [ ] Integrate LinkedIn / GitHub APIs for live profile data
- [ ] RAG over project portfolio (not just CV)
- [ ] LangGraph-based multi-agent orchestration
- [ ] Analytics dashboard for visitor questions

---

## 👤 Author

**Alan Muchiri** — Data & AI Engineer | Nairobi, Kenya

🌐 [alanmuchiri.com](https://alanmuchiri.com) · 💼 [LinkedIn](https://www.linkedin.com/in/alan-muchiri-5534631a4?utm_source=share_via&utm_content=profile&utm_medium=member_android) · 🤗 [HuggingFace](https://huggingface.co/muchiri-254)

---

## 📄 License

MIT License — feel free to fork and build your own digital twin.