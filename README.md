# LLM Benchmarking Project

[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)



---

## 🧰 Tech Stack & Dependencies

The project relies on the following core libraries:
* **LLM Orchestration:** `openai`, `python-dotenv`
* **Data Science:** `pandas`, `numpy`, `pyreadr`
* **Document Parsing:** `pymupdf` (fitz), `python-docx`
* **Infrastructure:** `docker`
* **Testing:** `pytest`, `pytest-cov`

---
 

## ⚙️ Installation
1. Clone repository:
   ```bash
   cd llm-benchmarking
   ```

2. Environment Setup
The project uses a ```Makefile``` to streamline set up and execute different components of our framework. Make sure you have Python 3.9+ and Docker installed
   ```bash
   # Install all required dependencies
   make install-deps
   
   # Verify your environment and dependencies
   make check-deps
   make check-docker
   ```

3. API Configuration
Create a `.env` file in the root directory:
```
OPENAI_API_KEY=your_api_key_here
```

---

## 🚀 Running the Pipeline
You can run the full end-to-end pipeline or individual using `make`.

### End-to-End Execution
To run the full flow (**Extract → Design → Execute → Interpret**) for a specific study:
```bash
make pipeline-easy STUDY=./data/original/1 MODEL=gpt-4o
```

### Individual Module Commands
| Module / Stage | Command | Description |
| :--- | :--- | :--- |
| **Info Extraction** | `make extract-stage1` | Extracts structured metadata from the original study into `post_registration.json`. |
| **Web Search** | `make web-search` | Performs an open-ended web search to identify data resources needed to replicate a claim given the original paper. |
| **Research Design** | `make design-easy` | Generates the replication design and analysis plan based on extracted info into `replication_info.json`. |
| **Execution** | `make execute-easy` | Runs the generated Python analysis script inside a secure Docker container. |
| **Interpretation** | `make interpret-easy` | Analyzes execution results to produce a final scientific interpretation report. |
| **Validation: Extract** | `make evaluate-extract` | Benchmarks the extraction stage against human-annotated ground truth. |
| **Validation: Design** | `make evaluate-design` | Evaluates the quality and validity of the LLM-generated research design. |
| **Validation: Execute**| `make evaluate-execute` | Compares the statistical output of the executed code against expected results. |
| **Validation: Summary**| `make evaluate-summary` | Generates a comprehensive evaluation report across all pipeline stages. |

---

## 📊 Evaluation (LLM-as-Judge)

The validator compares agent outputs against human-annotated ground truths using specific research rubrics.

* **Evaluate All Stages:**
    ```bash
    make evaluate-pipeline-easy STUDY=./data/original/1
    ```
* **Specific Evaluations:**
    * `make evaluate-extract`: Validates JSON metadata accuracy.
    * `make evaluate-design`: Checks research plan validity.
    * `make evaluate-execute`: Validates statistical outputs.
    * `make evaluate-summary`: Generates an overall performance report.

---

## 📂 Project Structure
```
llm-benchmarking/
├── core/               # Central logic containing autonomous agent, tools, prompts, and actions.
├── info_extractor/     # PDF parsing and metadata extraction
├── generator/          # Research design and code generation
├── interpreter/        # Result analysis and report generation
├── validator/          # CLI tools for LLM-based evaluation
├── templates/          # JSON schemas and prompt templates
├── data/               # Benchmark datasets and ground truth
├── Makefile            # Project automation
└── requirements-dev.txt
```

--- 

## 📄 License

All content in this repository is shared under the [Apache License 2.0](LICENSE)

---
