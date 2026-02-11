# Healthcare Management Decision Support System (HMDSS)

HMDSS is an advanced decision support system designed for healthcare management. It leverages a multi-agent architecture powered by CrewAI and integrates Retrieval-Augmented Generation (RAG) strategies to provide comprehensive answers to complex healthcare queries. The system also includes predictive analytics capabilities using an Artificial Neural Network (ANN) to forecast patient volume.

## Key Features

- **Multi-Agent Architecture**: Utilizes specialized AI agents (Analyst, Scholar, Fact-Checker, Investigator) to handle different aspects of query processing.
- **Advanced RAG Strategies**: Implements Branching, Iterative, and Self-Reflective RAG to ensure high-quality information retrieval.
- **Predictive Analytics**: Includes a custom ANN model (`PatientVolumePredictor`) to forecast patient volume based on historical data.
- **Mock Data Generation**: Capable of generating synthetic healthcare data, including surgical policies (PDF), resource logs (CSV), and EHR metadata (JSON).
- **Result Fusion**: Employs Reciprocal Rank Fusion to combine and rank results from multiple agents effectively.

## System Architecture

The system operates through a collaborative workflow:

1.  **Input**: Users provide a natural language query (e.g., "Optimize surgical scheduling for next Monday").
2.  **Agent Execution**: Four agents work in parallel:
    - **Analyst**: Decomposes complex queries into sub-queries using *Branching RAG*.
    - **Scholar**: Performs deep research through *Iterative RAG*.
    - **Fact-Checker**: Validates information using *Self-Reflective RAG*.
    - **Investigator**: Uses predictive models and search tools to provide data-driven insights.
3.  **Fusion**: The results from all agents are combined using Reciprocal Rank Fusion.
4.  **Synthesis**: An LLM synthesizes the fused information to provide a final, comprehensive recommendation.

## Prerequisites

- **Python 3.8+**
- **Ollama**: For local LLM inference. Ensure Ollama is installed and running.

## Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/hmdss.git
    cd hmdss
    ```

2.  **Create a virtual environment (optional but recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows: venv\Scripts\activate
    ```

3.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

4.  **Set up Ollama:**
    Ensure Ollama is running and pull the default model (or the one you intend to use):
    ```bash
    ollama pull gemma:2b
    ```

## Usage

To run the system, execute the `hmdss.main` module from the root directory. The system will automatically generate necessary mock data and train the analytics model on the first run.

```bash
python -m hmdss.main --query "Your healthcare query here"
```

### Command Line Arguments

- `--query`: The healthcare query to process (default: "Optimize surgical scheduling for next Monday").
- `--model`: The LLM model to use (default: "ollama/gemma:2b").
- `--api_base`: The API base URL for the LLM (default: "http://localhost:11434").

### Example

```bash
python -m hmdss.main --query "How does patient volume impact surgical staffing requirements?" --model ollama/llama3
```

## Project Structure

```
hmdss/
├── agents/             # Agent definitions (Analyst, Scholar, etc.)
├── analytics/          # Machine Learning models for prediction
├── core/               # Core workflow and fusion logic
├── data/               # Generated mock data (Policies, Logs, EHR)
├── scripts/            # Data generation scripts
├── tools/              # Custom tools (RAG, ANN, Search)
└── main.py             # Entry point of the application
```
