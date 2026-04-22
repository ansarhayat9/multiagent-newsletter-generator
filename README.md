# 📰 Multi-Agent Newsletter Generator

A fully autonomous AI-powered newsletter generator built with **CrewAI**, **Groq LLaMA**, and **Serper** — using a team of specialized AI agents that research, write, and proofread a professional newsletter on any topic.

---

## 🚀 What It Does

Given a **topic** (e.g., *"Artificial Intelligence in Finance"*), three AI agents collaborate in sequence to produce a polished, publication-ready newsletter article saved as a Markdown file.

```
Researcher → Writer → Proofreader → newsletter.md
```

---

## 🤖 The Agents

| Agent | Role | Responsibility |
|-------|------|----------------|
| **Researcher** | Technology Intelligence Specialist | Searches the web, finds the latest trends, pros/cons, and market insights on the topic |
| **Writer** | Technology Storyteller | Transforms research into an engaging, readable 4-paragraph article |
| **Proofreader** | Principal Proofreader | Polishes the article, fixes errors, adds citations and 3 further reading sources |

---

## 🛠️ Tech Stack

- **[CrewAI](https://github.com/joaomdmoura/crewAI)** — Multi-agent orchestration framework
- **[Groq](https://console.groq.com/)** — Ultra-fast LLM inference (LLaMA 3)
- **[Serper](https://serper.dev/)** — Google Search API for real-time web research
- **[LiteLLM](https://github.com/BerriAI/litellm)** — LLM provider abstraction layer
- **Python 3.10+**

---

## 📁 Project Structure

```
multiagent-newsletter-generator/
│
├── agents.py        # Defines the 3 AI agents (Researcher, Writer, Proofreader)
├── tasks.py         # Defines the tasks assigned to each agent
├── tools.py         # Google Search tool via Serper API
├── crew.py          # Assembles and runs the CrewAI crew
├── newsletter.md    # ✅ Output file (generated after running)
├── .env             # API keys (not committed to git)
├── Pipfile          # Pipenv dependency file
└── README.md
```

---

## ⚙️ Setup & Installation

### 1. Clone the repository
```bash
git clone https://github.com/ansarhayat9/multiagent-newsletter-generator.git
cd multiagent-newsletter-generator
```

### 2. Create a virtual environment
```bash
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # macOS/Linux
```

### 3. Install dependencies
```bash
pip install crewai crewai-tools langchain-groq litellm python-dotenv
```

### 4. Configure API Keys

Create a `.env` file in the root directory:
```env
GROQ_API_KEY=your_groq_api_key_here
SERPER_API_KEY=your_serper_api_key_here
```

Get your keys here:
- 🔑 **Groq API Key** → [console.groq.com](https://console.groq.com)
- 🔑 **Serper API Key** → [serper.dev](https://serper.dev)

---

## ▶️ Running the Project

```bash
python crew.py
```

The agents will start working sequentially. The final newsletter is saved to **`newsletter.md`**.

---

## 📝 Changing the Topic

Open `crew.py` and update line 11:

```python
topic = "Artificial Intelligence in Finance"  # ← Change this
```

Examples:
- `"Quantum Computing in Healthcare"`
- `"Blockchain and Supply Chain Management"`
- `"Future of Electric Vehicles"`

---

## 📤 Example Output

After running, `newsletter.md` will contain a structured article like:

```
# The Rise of AI in Finance

## Introduction
...

## Key Trends
...

## Risks & Opportunities
...

## Conclusion
...

### Sources
1. ...
2. ...
3. ...
```

---

## ⚠️ Known Limitations

| Issue | Details |
|-------|---------|
| **Groq Free Tier Rate Limits** | Free tier allows ~6,000 tokens/min. Complex topics may hit this limit. Wait 60 seconds and retry. |
| **Serper API Limit** | Free plan includes 2,500 searches/month. |
| **Output Quality** | Depends on the LLM model used. `llama3-8b-8192` is fast but less detailed than larger models. |

---

## 🧠 How It Works (Flow)

```
┌─────────────────────────────────────────────────────┐
│                    crew.py                          │
│                                                     │
│  topic = "AI in Finance"                            │
│  crew.kickoff(inputs={"topic": topic})              │
└──────────────────────┬──────────────────────────────┘
                       │
          ┌────────────▼────────────┐
          │    RESEARCHER AGENT     │
          │  Searches web, finds    │
          │  trends & insights      │
          └────────────┬────────────┘
                       │
          ┌────────────▼────────────┐
          │     WRITER AGENT        │
          │  Writes engaging 4-para │
          │  article from research  │
          └────────────┬────────────┘
                       │
          ┌────────────▼────────────┐
          │   PROOFREADER AGENT     │
          │  Polishes, cites sources│
          │  Saves → newsletter.md  │
          └─────────────────────────┘
```

---

## 📄 License

 feel free to use, modify, and distribute.

---

## 🙌 Acknowledgements

- [CrewAI](https://github.com/joaomdmoura/crewAI) by João Moura
- [Groq](https://groq.com/) for blazing-fast LLM inference
- [Serper](https://serper.dev/) for real-time Google search API
