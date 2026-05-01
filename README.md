# AI-Driven Prompt Evaluation for Safety-Aligned Language Models

## Overview

This project studies how different prompt templates affect the refusal and compliance behavior of a safety-aligned large language model (LLM).

The goal is to analyze how natural-language prompt framing influences whether a model refuses or complies with requests, using a controlled evaluation pipeline.

This work is inspired by:

Zou et al. (2023) — *Universal and Transferable Adversarial Attacks on Aligned Language Models*

Instead of reproducing full adversarial attacks, this project explores a simplified, interpretable setting using prompt templates and automated evaluation.

---

## Repository Structure

```
.
├── jailbreak_case_study.ipynb
├── data/
│   └── benchmark_tasks.json
├── results/
│   ├── evaluation_results.csv
│   └── final_summary.csv
├── finalproject.pdf
├── README.md
```

---

## Setup Instructions

### 1. Create environment

```
conda create -n jailbreak-ai python=3.10
conda activate jailbreak-ai
```

### 2. Install dependencies

```
pip install pandas numpy matplotlib
```

### 3. Install Ollama (local LLM)

Download and install:
https://ollama.com/download

Then run:

```
ollama run llama3
```

---

## Running the Project

1. Open the notebook:

```
jailbreak_case_study.ipynb
```

2. Run all cells sequentially to:
- load tasks
- define candidates
- query the model
- evaluate outputs
- compute metrics

---

## Evaluation Pipeline

Each candidate prompt is evaluated as follows:

1. Insert `{TASK}` into the template  
2. Send prompt to LLaMA3 (via Ollama)  
3. Record model response  
4. Classify response as:
   - REFUSE
   - COMPLY
   - UNKNOWN  
5. Compute metrics:
   - Refusal Rate
   - Compliance Rate
   - Unknown Rate
   - Clean Output Rate

---

## Candidate Prompts

The project includes:

- Manual candidates:
  - Direct baseline
  - Research framing
  - Classification-style prompts

- AI-generated candidate:
  - Generated using the model itself

---

## Key Results

| Candidate  | Refusal | Compliance | Unknown | Clean |
|------------|--------|------------|---------|-------|
| base_001   | 0.50   | 0.33       | 0.17    | 0.83  |
| cand_002   | 1.00   | 0.00       | 0.00    | 1.00  |
| cand_003   | 0.50   | 0.50       | 0.00    | 1.00  |
| cand_004   | 0.50   | 0.50       | 0.00    | 1.00  |

### Insights

- Prompt framing significantly impacts behavior  
- Some prompts cause over-refusal  
- Classification-style prompts produce balanced outputs  
- AI-generated prompts can match manual ones  

---

## Research Insight

Natural-language prompt variation alone can significantly influence model behavior, even without gradient-based adversarial optimization.

Ambiguous tasks reveal boundary behavior, where responses shift depending on prompt framing.

---

## Limitations

- Small benchmark (6 tasks)  
- Single model (LLaMA3)  
- Heuristic evaluation  

---

## Reproducibility

Run the notebook to regenerate:

```
results/evaluation_results.csv
results/final_summary.csv
```

---

## Appendix / Prompts

All prompt templates are defined in the notebook.

---

## Author

Mohammed Rashed Ali Yahmoor Alshehhi  
CS7602 – Coursework Project
