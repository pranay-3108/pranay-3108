# DeepSeek-R1: Long-Context Retention & Hallucination Evaluation in Lightweight LLMs

**Python · Ollama · Prompt Engineering · LLM Evaluation · Statistical Testing**

[Research Demo](https://drive.google.com/file/d/12T9uPdO7QcpBxOo8M_RqbmAy37hZCroG/view?usp=sharing) · [Research Report](https://lnkd.in/dc4wGCit)

## Overview

This project studies how lightweight language models answer questions about long research documents, how answer quality changes as more context is supplied, and when models produce unsupported answers instead of abstaining.

The benchmark uses the BERT research paper and a fixed set of questions evaluated at five document lengths. The same question set and reference key are used across comparable runs so that results can be inspected at both aggregate and question level.

## Research Questions

- How does answer quality change as document length increases?
- Can a lightweight model retain key details across longer contexts?
- Does the model abstain when a question cannot be answered from the supplied document?
- Do structure-aware document chunks preserve section boundaries better than fixed-size slicing?

## Benchmark Design

| Component | Setup |
|---|---|
| Source document | *BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding* |
| Question set | 55 fixed questions across 9 categories |
| Hallucination checks | 5 unanswerable questions, evaluated at each of the 5 context lengths (25 response checks) |
| Context lengths | 8K, 16K, 24K, 32K, and 44K characters |
| Models | DeepSeek-R1 1.5B, Granite 3.3 2B, and a Granite 7B comparison baseline |
| Reference | Claude-written reference answer key, used consistently across model comparisons |

Question categories cover factual understanding, reasoning, methodology, numerical evidence, experimental details, synthesis, and unanswerable-question checks.

## Evaluation Method

The primary answer-quality metric is **lexical Answer F1**, calculated against the common reference answer key. Precision and recall are also recorded. The analysis includes question-level comparisons, missing and added information, numerical inconsistencies, unsupported claims, negation changes, answer length, and generation time.

Statistical analysis uses bootstrap confidence intervals and paired tests with Holm correction for multiple comparisons. Agreement with a reference answer is treated as an evaluation signal, not proof of factual correctness; the reference key and benchmark scope are limitations to keep in mind.

## Main Findings

### DeepSeek-R1 1.5B

- Answer F1 remained within **24.1%–25.7%** across the five tested document lengths.
- At 44K characters, the comparison with the 7B baseline found no statistically significant difference; the reported DeepSeek-R1 1.5B Answer F1 was **24.1%**.

### Granite 3.3 2B

| Context length | Average Answer F1 |
|---:|---:|
| 8K | 23.78% |
| 16K | 26.49% |
| 24K | 27.61% |
| 32K | 26.96% |
| 44K | 30.73% |

Granite 3.3 2B improved from **23.78% to 30.73% Answer F1** over the tested context range (**p < 0.001** in the reported paired analysis). It also abstained correctly on all **25 unanswerable-question checks** across the five context lengths.

### Structure-Aware Chunking

In the tested chunk-boundary comparison, the structure-aware chunker produced **16/16 clean chunk boundaries**, compared with **0/16** for fixed 7K-character slicing. This improvement came from document-aware preprocessing and required **no additional model call**.

## What the Dashboard Supports

The Streamlit dashboard is designed to make the benchmark inspectable rather than reducing it to a leaderboard. It supports:

- selecting models and context lengths for comparison;
- comparing model answers against the common reference key;
- inspecting individual questions and responses;
- reviewing answer metrics and detected differences;
- examining performance trends and diagnostic signals;
- recording human research judgments and exporting results.

## Project Structure

```text
.
├── app.py
├── benchmark/
├── bert/
├── scripts/
├── results/
├── tests/
└── requirements.txt
```

The repository contains the evaluation dashboard, benchmark components, stored results, and supporting scripts. See the source files for the current implementation details.

## Running the Dashboard

```bash
git clone https://github.com/pranay-3108/DeepSeek-R1-Long-Context-Retention-Hallucination-Evaluation-in-Lightweight-LLMs.git
cd DeepSeek-R1-Long-Context-Retention-Hallucination-Evaluation-in-Lightweight-LLMs
pip install -r requirements.txt
streamlit run app.py
```

Model inference requires Ollama and the model tags used by the experiment. The repository's requirements file covers the Python dependencies; install and pull the required Ollama models separately before reproducing inference runs.

## Interpretation and Limitations

- Results describe this BERT-paper benchmark and should not be generalized to all documents or tasks.
- Answer F1 is a lexical metric; it does not independently establish semantic correctness or factual grounding.
- The Claude-written reference key is a comparison reference, not an independently verified gold standard.
- The Granite 7B output is a model comparator, not ground truth.
- The 25 abstention checks correspond to 5 unanswerable questions evaluated at 5 context lengths.
- The chunk-boundary result is based on the tested 16-boundary comparison; broader document coverage is needed before making a general claim about all chunking workloads.

## Research Status

This is an ongoing experimental project. Further work includes evaluating additional research papers and model families, repeating runs, expanding semantic evaluation, and testing the chunking approach across a broader range of document structures.

## Author

**Pranay Ugale**  
B.Tech, Computer Science and Engineering (Data Science)  
[GitHub](https://github.com/pranay-3108) · [LinkedIn](https://linkedin.com/in/pranayugale) · [Email](mailto:pranayugale31@gmail.com)
