# CSV FAQ Agent

A Streamlit-powered web app that lets you upload a CSV file and ask questions about your data in plain English. It uses LangChain's CSV agent with OpenAI to analyze the data using pandas and return natural language answers.

## Architecture

See [docs/architecture.md](docs/architecture.md) for detailed Mermaid diagrams covering the system overview, request flow, and component details.

```
Browser  -->  Streamlit UI  -->  LangChain CSV Agent  -->  OpenAI GPT-4o-mini
                  |                      |
             File Upload            pandas DataFrame
```

## Prerequisites

- Python 3.10+
- An [OpenAI API key](https://platform.openai.com/api-keys)

## Installation

1. **Clone the repository**

   ```bash
   git clone https://github.com/SashyCashy/CSV-FAQ-Agent.git
   cd CSV-FAQ-Agent
   ```

2. **Create and activate a virtual environment**

   ```bash
   python -m venv .venv
   source .venv/bin/activate        # macOS / Linux
   .venv\Scripts\activate           # Windows
   ```

3. **Install dependencies**

   ```bash
   pip install -r requirements.txt
   ```

4. **Set up your API key**

   Create a `.env` file in the project root:

   ```bash
   echo "OPENAI_API_KEY=sk-your-key-here" > .env
   ```

   The app reads this file on startup. You can also override the key in the sidebar at runtime.

## Usage

1. **Start the app**

   ```bash
   streamlit run app.py
   ```

   The app opens at `http://localhost:8501` by default.

2. **Upload a CSV** using the file uploader. A preview of the first few rows is shown automatically.

3. **Ask a question** in the text input, for example:
   - "What is the average percentage?"
   - "Show me all students with grade A"
   - "What is the total of the sales column?"

4. The agent runs pandas operations on your data and returns a plain-English answer.

## Project Structure

```
CSV-FAQ-Agent/
├── app.py                    # Main Streamlit application
├── requirements.txt          # Python dependencies
├── .env                      # OpenAI API key (not committed)
├── .gitignore
├── .streamlit/
│   └── config.toml           # Streamlit server configuration
└── docs/
    └── architecture.md       # Mermaid architecture diagrams
```

## Configuration

| Setting | Location | Description |
|---|---|---|
| `OPENAI_API_KEY` | `.env` | Your OpenAI API key |
| `runOnSave` | `.streamlit/config.toml` | Auto-reload on file changes |
| `fileWatcherType` | `.streamlit/config.toml` | File watching backend |

### Agent Settings

The LangChain CSV agent is configured with these defaults in `app.py`:

| Parameter | Value | Purpose |
|---|---|---|
| `agent_type` | `openai-tools` | Uses OpenAI's native tool-calling for efficient iterations |
| `model` | `gpt-4o-mini` | Cost-effective model for data queries |
| `temperature` | `0` | Deterministic answers |
| `max_iterations` | `25` | Maximum reasoning steps per query |
| `max_execution_time` | `120s` | Timeout for long-running queries |
| `early_stopping_method` | `generate` | Returns best-effort answer if iterations run out |

## Dependencies

| Package | Purpose |
|---|---|
| `streamlit` | Web UI framework |
| `pandas` | CSV reading and data manipulation |
| `python-dotenv` | Load API key from `.env` |
| `langchain-openai` | OpenAI LLM integration |
| `langchain-experimental` | CSV agent toolkit |
| `tabulate` | Table formatting for display |

## License

This is a personal project for learning and experimentation.
