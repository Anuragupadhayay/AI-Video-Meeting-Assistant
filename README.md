# AI Video Meeting Assistant 🚀

An automated, production-ready AI pipeline that downloads meeting recordings or video URLs, transcribes them using local/API audio intelligence, structures data into a vector store, and extracts deep actionable insights (summaries, action items, key decisions, and open questions) using Large Language Models.


---

## 🚀 Features

- **Automated Audio Extraction:** Seamlessly downloads high-quality audio from YouTube/meeting URLs using `yt-dlp`.
- **Hybrid Intelligent Transcription:**
  - *English:* Processes locally via OpenAI's Whisper model (`base`), optimizing memory footprint.
  - *Hinglish:* Interacts with external voice APIs (Sarvam AI) to handle complex mixed-language contexts.
- **Smart Audio Processing:** Slices large media files into manageable semantic chunks using `pydub` to prevent container memory overloads.
- **Semantic RAG Engine:** Constructs a local vector database using ChromaDB and HuggingFace Embeddings (`all-MiniLM-L6-v2`) to allow interactive context querying over transcript segments.
- **LLM-Powered Insights:** Uses LangChain and Mistral AI to automatically generate structured summaries, cross-reference questions, and extract strict task-oriented action items.

---

## 🛠️ Tech Stack

| Category | Tools |
|---|---|
| UI Framework | Streamlit |
| AI & LLM Orchestration | LangChain (LCEL), MistralAI API, Sarvam AI API |
| Speech-to-Text Engine | Local OpenAI-Whisper |
| Vector Store & Embeddings | ChromaDB, HuggingFace Transformers, Sentence-Transformers |
| Audio Engineering | `pydub`, `yt-dlp`, FFmpeg |
| Environment / Tooling | `uv` package manager, `python-dotenv` |

---

## ⚙️ Prerequisites (Local Development)

Before running the app locally, you must have **FFmpeg** installed on your system for audio rendering and slicing.

**Windows** (via winget):
```bash
winget install Gyan.FFmpeg
```

**macOS** (via Homebrew):
```bash
brew install ffmpeg
```

> **Note:** Please restart your terminal or IDE after installing FFmpeg to ensure it updates your system's PATH variables.

---

## 📦 Installation & Setup

**1. Clone the repository:**
```bash
git clone https://github.com/Anuragupadhayay/AI-Video-Meeting-Assistant.git
cd AI-Video-Meeting-Assistant
```

**2. Initialize the environment using `uv`:**
```bash
uv venv --python 3.12
source .venv/bin/activate  # On Windows use: .venv\Scripts\activate
```

**3. Install dependencies:**
```bash
uv pip install -r requirements.txt
```

**4. Environment Configuration (`.env`):**

Create a `.env` file in the root workspace (this file is ignored by Git for security):
```env
WHISPER_MODEL=base
MISTRAL_API_KEY=your_mistral_api_key
SARVAM_API_KEY=your_sarvam_api_key
```

---

## ☁️ Production Deployment Notes

To deploy this pipeline to cloud infrastructures like Streamlit Community Cloud, the following system accommodations were engineered:

- **Python 3.13/3.14 Compatibility:** Integrated the `audioop-lts` shim module to backport deprecated audio operations required by core file-slicing packages.
- **Cloud Database Fix:** Implemented a runtime hot-swap of the host environment's outdated SQLite binary using `pysqlite3-binary` to meet strict vector processing version requirements for ChromaDB.

---

## 📂 Project Structure

```text
AI-Video-Meeting-Assistant/
├── core/
│   ├── vector_store.py    # ChromaDB vector database initialization
│   ├── transcriber.py     # Local Whisper & Sarvam AI processing engines
│   ├── summarizer.py      # LLM logic for titles and summaries
│   ├── extractor.py       # Structuring logic for action items, decisions, and questions
│   └── rag_engine.py      # Prompt templates and RAG retrieval chains
├── utils/
│   └── audio_processor.py # yt-dlp media downloader and file utilities
├── app.py                 # Streamlit web application interface wrapper
├── main.py                # Command-line execution pipeline
├── requirements.txt       # Production cloud deployment dependencies
└── README.md              # Project documentation

```
## 👨‍💻 Author

**Anurag Upadhyaya**
* GitHub: [@Anuragupadhayay](https://github.com/Anuragupadhayay)
