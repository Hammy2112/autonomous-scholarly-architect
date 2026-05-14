# 🏛️ Autonomous Scholarly Architect

An autonomous, agentic AI pipeline built with **LangGraph**, **Llama 3.1 (8B)**, and **SerpAPI** that acts as a sophisticated research assistant. It observes your drafted text, autonomously scours Google Scholar for recent (2020-2025) open-access papers, seamlessly integrates citations into your writing, and evaluates its own work against strict academic constraints.

---

## 🚀 Key Features

- **Multi-Agent Architecture:** Utilizes specialized LangGraph nodes (Observer, Researcher, Auditor, Drafter, Critic) to manage the complex workflow of academic research.
- **Live Google Scholar Research:** Bypasses hallucinations by directly querying Google Scholar via SerpAPI to find real, traceable academic papers.
- **Strict Constraint Enforcement:** Automatically filters sources to ensure they are:
  - Published within the last 5 years (2020–2025).
  - Open-access (prioritizing available PDFs and HTML texts).
  - From reputable, user-specified publishers (e.g., Elsevier, MDPI, Nature).
- **Self-Correcting Loop:** A built-in "Critic" node rigorously evaluates the drafted text and bibliography. If any constraint is violated, the agent blacklists the invalid sources and automatically restarts the research phase (up to 3 times).
- **Automated Formatting:** Supports automatic, seamless citation formatting in APA, MLA, or IEEE styles.
- **Word Document Integration:** Directly reads your un-cited claims from a local `.docx` file.

---

## 🧠 System Architecture

The pipeline is modeled as a state machine using **LangGraph**:

1. **Observer Node:** Reads the user's Word document, identifies missing citations, and generates 10 targeted search queries. If previous loops failed, it reads the feedback history to adjust its strategy.
2. **Researcher Node:** Executes the generated queries strictly across Google Scholar (via SerpAPI).
3. **Auditor Node (The Bouncer):** Hard-blocks blacklisted URLs and strictly filters the raw results to ensure they contain open-access links.
4. **Drafter Node:** Synthesizes the valid papers, rewrites the user's paragraph with embedded citations, provides a "Strategic Source Mapping" table, and compiles the bibliography.
5. **Critic Node:** An uncompromising evaluator that checks the Drafter's output against 6 strict rules (Relevance, Year Range, Open Source, Citable, Publisher, and Format). 
6. **Router:** Reads the Critic's JSON report. If passed, the script ends. If failed, it routes back to the Observer.

---

## 🛠️ Prerequisites

You will need the following to run this agent:
- **Jupyter Environment:** Google Colab, Jupyter Notebook, or VS Code with Jupyter support.
- **Hugging Face Token:** To access the `meta-llama/Llama-3.1-8B-Instruct` model.
- **SerpAPI Key:** To execute real-time Google Scholar searches.

## 📦 Installation

1. Clone this repository:

```bash
   git clone https://github.com/Hammy2112/autonomous-scholarly-architect.git
   cd autonomous-scholarly-architect
```   
2. Open the notebook `Agentic_AI_Project_Final_Work_File.ipynb` in your preferred Jupyter environment (e.g., upload it to Google Colab or open it in VS Code).

3. Install the required Python packages:
```bash
!pip install -qU langchain-huggingface langgraph google-search-results python-docx

```

## ⚙️ Usage

1. **Set up your environment variables:**
Export your API keys in your terminal or set them in your script:
```python
import os
os.environ["HUGGINGFACEHUB_API_TOKEN"] = "your_hf_token_here"
os.environ["SERPAPI_API_KEY"] = "your_serpapi_key_here"

```


2. **Prepare your document:**
Place a Word document named `document.docx` in the root directory. This document should contain the paragraphs or claims you want the agent to research and cite.
3. **Run the pipeline:**
Execute the main Python script 


## 📊 Sample Output

**Input:** A drafted paragraph about telemedicine barriers without any citations.

**Output:**

* A flawlessly rewritten paragraph with APA citations naturally embedded.
* A **Strategic Source Mapping** table explaining exactly *why* and *how* each source was used (e.g., "Use to balance the narrative by acknowledging accessibility limitations").
* A perfectly formatted APA Bibliography with direct links to the source material.

---

## 📄 License

This project is licensed under the MIT License.
