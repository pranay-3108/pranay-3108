# Pranay Ugale

**AI/ML Engineer | Computer Vision | Local LLM Research | Applied AI Systems**

I am a B.Tech Data Science student focused on developing practical machine learning systems and investigating their performance under real-world conditions.

My work spans computer vision, medical image segmentation, local language models and experimental evaluation. I am particularly interested in understanding model limitations, improving evaluation reliability and building reproducible engineering workflows.

I approach projects through implementation, experimentation, error analysis and documentation. My focus is not limited to achieving a particular metric, but also understanding the conditions under which a model performs well or fails.

**Research Interests:** Computer Vision, Medical Image Analysis, LLM Evaluation, Long-Context Understanding, Model Reliability and Applied AI Engineering.

**GitHub:** https://github.com/pranay-3108  
**LinkedIn:** https://www.linkedin.com/in/pranayugale/

---

## Selected Projects

### 1. MedPlug: Standardized and Reproducible Medical Image Segmentation Benchmarking

**Domain:** Computer Vision, Medical Imaging, Deep Learning, Research Engineering

**Repository:** [MedPlug](https://github.com/pranay-3108/MedPlug-Standardized-and-Reproducible-Benchmarking-of-Medical-Image-Segmentation)

**Research Paper:** [MedPlug Project Paper (PDF)](https://drive.google.com/file/d/19ztNvJ3WWUTH76GH6a37FAy6qCVXWQn0/view?usp=drive_link)

**Demonstration:** [Watch Project Demo](https://drive.google.com/file/d/1XNMTAUU8XPLFVRQNTnd2orrWQ2o62kZk/view?usp=drive_link)

MedPlug is a modular benchmarking framework designed to improve the consistency and reproducibility of medical image segmentation experiments.

The project addresses an important research problem: reported performance differences between segmentation models can be influenced by dataset splits, preprocessing, checkpoint selection, thresholding policies and metric implementations.

The framework introduces explicit experimental contracts and independent verification mechanisms to make model evaluation more transparent.

**Engineering Components**

- Dataset contracts and preflight validation.
- DICOM image and segmentation mask processing.
- Modular architecture and model registration.
- Configurable training and evaluation pipelines.
- Experiment-specific artifact management.
- Training diagnostics and metric tracking.
- Prediction visualization and reporting.
- Independent metric recomputation from stored outputs.
- Bootstrap-based uncertainty analysis.

**Experimental Architectures**

- Compact U-Net
- Attention U-Net
- TransUNet-style architecture
- SegFormer-style architecture

**Dataset:** [SIIM-ACR Pneumothorax Segmentation](https://www.kaggle.com/c/siim-acr-pneumothorax-segmentation)

**Research Objective**

Investigate how experimental inconsistencies affect segmentation evaluation and how software-level controls can improve the reliability of model comparisons.

**Technologies:** Python, PyTorch, NumPy, DICOM, Medical Image Processing.

---

### 2. Long-Context Retention and Hallucination Evaluation in Lightweight LLMs

**Domain:** Natural Language Processing, LLM Evaluation, Local AI Research

**Repository:** [DeepSeek-R1 Long-Context Evaluation](https://github.com/pranay-3108/DeepSeek-R1-Long-Context-Retention-Hallucination-Evaluation-in-Lightweight-LLMs)

**Demonstration:** [Research Dashboard Demo](https://drive.google.com/file/d/12T9uPdO7QcpBxOo8M_RqbmAy37hZcroG/view?usp=sharing)

This research project investigates how lightweight language models process and retain information from long research documents.

The benchmark evaluates document understanding across multiple input lengths using fixed questions and common reference answers.

**Experimental Design**

- 55 fixed research questions.
- Five document-length stages: 8K, 16K, 24K, 32K and 44K characters.
- Lightweight local model evaluation.
- Question-level answer inspection.
- Reference-based evaluation.
- Missing-information and unsupported-claim analysis.
- Numerical consistency and answer completeness checks.
- Interactive Streamlit research dashboard.

**Models Considered**

- DeepSeek 1.5B
- IBM Granite 3.3 2B
- Granite 7B baseline

The current publicly documented result table reports Granite 3.3 2B results using lexical Answer F1. Additional model results are maintained separately.

**Research Objective**

Understand the relationship between model size, context length, information retention and factual reliability.

The project also investigates whether better document processing and context management can improve the usefulness of smaller models on resource-constrained hardware.

**Technologies:** Python, Ollama, DeepSeek, IBM Granite, Streamlit.

---

### 3. Chess Image to FEN Generator

**Domain:** Computer Vision, Image Classification, Deep Learning

**Repository:** [Chess FEN Generator](https://github.com/pranay-3108/Chess_Fen_GENERATOR)

A computer vision pipeline that converts chessboard photographs into machine-readable Forsyth-Edwards Notation (FEN).

The implementation processes a chessboard image, extracts individual squares, classifies the contents of each square and reconstructs the complete board position.

**Pipeline**

Chessboard Image → Board Cropping → Square Extraction → Piece Classification → Board Reconstruction → FEN Generation

**Technical Components**

- Image preprocessing and board extraction.
- Individual square classification.
- Chess piece recognition.
- Board reconstruction.
- FEN generation and output validation.

**Model Evaluation**

The documented training snapshot reports approximately 98% training accuracy and 96% validation accuracy.

However, testing on unfamiliar images exposed false-positive predictions on empty squares due to blur, reflections, faint outlines and screen artifacts.

The next development direction focuses on hard-negative examples, empty-versus-occupied discrimination and board-level evaluation.

**Technologies:** Python, Computer Vision, Image Processing, Deep Learning.

---

### 4. Granite Sandbox: Lightweight Local LLM Experiments

**Domain:** Local AI, Language Models, Performance Experimentation

**Repository:** [Granite Sandbox](https://github.com/pranay-3108/granite-sandbox)

An experimental environment for exploring local inference and document-processing workflows using lightweight language models.

The project investigates the practical use of IBM Granite models through Ollama and examines the trade-offs involved in local model deployment.

**Technical Areas**

- Local language model inference.
- PDF text extraction.
- Document-processing workflows.
- Prompt experimentation.
- Runtime analysis.
- Resource utilization and hardware constraints.

**Research Objective**

Understand how lightweight models can support practical document-processing applications while operating under limited computing resources.

**Technologies:** Python, Ollama, IBM Granite, PDF Processing.

---

## Research Paper and Technical References

The following research works provide the technical background for my experiments. These are external papers and architectural references, not publications authored by me.

### Language Models and Long-Context Evaluation

**1. BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding**

Authors: Jacob Devlin, Ming-Wei Chang, Kenton Lee and Kristina Toutanova.

[Read Paper on arXiv](https://arxiv.org/abs/1810.04805)

Used as the source research document for the long-context question-answering benchmark.

**2. DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning**

Authors: DeepSeek-AI.

[Read Paper on arXiv](https://arxiv.org/abs/2501.12948)

Relevant background for understanding the reasoning-model family used in local LLM experimentation.

### Medical Image Segmentation

**3. U-Net: Convolutional Networks for Biomedical Image Segmentation**

Authors: Olaf Ronneberger, Philipp Fischer and Thomas Brox.

[Read Paper on arXiv](https://arxiv.org/abs/1505.04597)

Foundational reference for convolutional encoder-decoder segmentation architectures.

**4. Attention U-Net: Learning Where to Look for the Pancreas**

Authors: Ozan Oktay and collaborators.

[Read Paper on arXiv](https://arxiv.org/abs/1804.03999)

Reference for attention-gated segmentation architectures.

**5. TransUNet: Transformers Make Strong Encoders for Medical Image Segmentation**

Authors: Jieneng Chen and collaborators.

[Read Paper on arXiv](https://arxiv.org/abs/2102.04306)

Reference for combining transformer encoders with U-Net-style medical image segmentation.

**6. SegFormer: Simple and Efficient Design for Semantic Segmentation with Transformers**

Authors: Enze Xie and collaborators.

[Read Paper on arXiv](https://arxiv.org/abs/2105.15203)

Reference for transformer-based semantic segmentation architectures.

### Dataset and Research Resources

- [SIIM-ACR Pneumothorax Segmentation Challenge](https://www.kaggle.com/c/siim-acr-pneumothorax-segmentation)
- [Society for Imaging Informatics in Medicine: Pneumothorax Challenge](https://siim.org/research-journal/siim-machine-learning-challenges/pneumothorax-kaggle-challenge/)

---

## Open-Source Contributions

### PyTorch Tutorials

**Pull Request:** [#3796 — Fix invalid escape sequence in Saving and Loading Models tutorial](https://github.com/pytorch/tutorials/pull/3796)

Submitted a documentation correction addressing an invalid Python escape-sequence warning in the PyTorch Saving and Loading Models tutorial.

The contribution is part of my experience with external repositories, code review workflows and collaborative software development.

**Current Status:** Open pull request.

---

## Technical Skills

| Category | Technologies and Concepts |
|---|---|
| Programming | Python, SQL |
| Machine Learning | Machine Learning, Deep Learning, Model Evaluation |
| Deep Learning Frameworks | PyTorch |
| Computer Vision | OpenCV, Image Classification, Segmentation |
| Data Analysis | NumPy, Pandas, Matplotlib |
| Language Models | Ollama, DeepSeek, IBM Granite |
| Application Development | Streamlit |
| Engineering Tools | Git, GitHub |
| Research Practices | Benchmarking, Error Analysis, Experiment Tracking, Reproducibility |

---

## Engineering Approach

My development workflow emphasizes experimental discipline and technical verification.

1. Define the problem and measurable objectives.
2. Validate datasets and experimental inputs.
3. Establish a baseline for comparison.
4. Design controlled experiments.
5. Evaluate models using appropriate metrics.
6. Investigate unexpected behaviour and failure cases.
7. Record configurations, results and limitations.
8. Improve the system based on experimental evidence.

I consider reproducibility, transparent reporting and failure analysis essential parts of machine learning engineering.

---

## Current Research Interests

- Long-context language model evaluation.
- Document understanding and information retention.
- Reliable and reproducible ML benchmarking.
- Medical image segmentation.
- Computer vision model generalization.
- Model diagnostics and explainability.
- Efficient local AI inference.

---

## Professional Interests

I am interested in opportunities involving applied machine learning, computer vision, LLM engineering and AI research.

I welcome opportunities to contribute to research teams, collaborate on open-source projects and work on practical engineering challenges.

**GitHub:** [pranay-3108](https://github.com/pranay-3108)

**LinkedIn:** [Pranay Ugale](https://www.linkedin.com/in/pranayugale/)

