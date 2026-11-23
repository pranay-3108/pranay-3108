# Pranay Ugale

**Machine Learning | LLM Evaluation | Computer Vision | Data Science**

B.Tech Computer Science and Engineering (Data Science) student at Gaikwad Patil College of Engineering. I work on applied machine learning and research-oriented engineering, with a focus on evaluating model behaviour, building reproducible experiments, and understanding failure cases rather than relying only on headline metrics.

My current work spans lightweight language-model evaluation, medical image segmentation, AI-agent workflows, and edge-AI research for X-ray imaging.

[LinkedIn](https://linkedin.com/in/pranayugale) · [GitHub](https://github.com/pranay-3108) · [Email](mailto:pranayugale31@gmail.com)

---

## Research and engineering interests

- **Large language models:** long-context understanding, information retention, hallucination checks, answer evaluation, and local inference.
- **Computer vision:** image preprocessing, classification, segmentation, and evaluation under difficult real-world conditions.
- **Medical AI:** DICOM workflows, image-to-tensor pipelines, medical-image segmentation, and edge deployment constraints.
- **Reliable experimentation:** controlled comparisons, metric verification, statistical testing, error analysis, and transparent reporting.
- **Applied AI systems:** tool-using agents, model integration, and lightweight systems that can run with limited compute.

## Featured work

### 1. DeepSeek-R1: Long-Context Retention and Hallucination Evaluation in Lightweight LLMs

**2026 · Python · Ollama · Prompt Engineering · LLM Evaluation · Statistical Testing**

[Repository](https://github.com/pranay-3108/DeepSeek-R1-Long-Context-Retention-Hallucination-Evaluation-in-Lightweight-LLMs) · [Demo](https://drive.google.com/file/d/12T9uPdO7QcpBxOo8M_RqbmAy37hZcroG/view?usp=sharing)

An experimental benchmark for studying how lightweight language models answer questions about a research paper as the available document context grows.

**Benchmark design**

- Built a set of **55 fixed questions** based on the BERT research paper, grouped into **9 categories** covering factual understanding, reasoning, methodology, numerical evidence, experiments, synthesis, and unanswerable checks.
- Included **5 unanswerable questions** for testing whether a model appropriately abstains instead of inventing an answer.
- Evaluated at five document lengths: **8K, 16K, 24K, 32K, and 44K characters**.
- Compared DeepSeek-R1 1.5B and Granite 3.3 2B, with a Granite 7B answer set used as a model comparator.
- Scored answers using lexical Answer F1 against a common Claude-written reference key. Used bootstrap confidence intervals and Holm-corrected paired statistical tests for comparisons.

**Selected findings**

| Experiment | Observed result |
|---|---|
| DeepSeek-R1 1.5B across context lengths | Answer F1 remained within **24.1–25.7%** across the five document lengths. |
| DeepSeek-R1 1.5B vs. 7B comparator at 44K | DeepSeek-R1 1.5B scored **24.1% F1**; the paired analysis found no statistically significant difference from the 7B reference model in this benchmark setting. |
| Granite 3.3 2B across context lengths | Answer F1 increased from **23.8% at 8K** to **30.7% at 44K** (**p < 0.001** in the reported comparison). |
| Unanswerable-question checks | Granite 3.3 2B abstained correctly on **25/25 checks** across the five context lengths. |
| Structure-aware chunking | Produced **16/16 clean chunk boundaries**, compared with **0/16** for fixed 7K-character slicing, without adding model calls. |

**Evaluation notes and limitations**

- Answer F1 is a lexical overlap metric against a written reference. It is useful for consistent comparison, but it does not by itself establish semantic equivalence or factual correctness.
- Agreement with a model-generated reference is not the same as agreement with ground truth. The 7B output is treated as a comparator, not as a gold-standard answer key.
- These results describe this benchmark, paper, question set, prompts, and inference setup. They should not be generalized to all documents or all model tasks.

The project also includes a Streamlit dashboard for model and context selection, question-level inspection, answer comparison, result visualization, and export of evaluation data.

### 2. MedPlug: Standardized and Reproducible Benchmarking of Medical Image Segmentation

**2026 · Python · PyTorch · Computer Vision · DICOM · Experiment Tracking**

[Repository](https://github.com/pranay-3108/MedPlug-Standardized-and-Reproducible-Benchmarking-of-Medical-Image-Segmentation) · [Research paper](https://drive.google.com/file/d/19ztNvJ3WWUTH76GH6a37FAy6qCVXWQn0/view?usp=drive_link) · [Demo video](https://drive.google.com/file/d/1XNMTAUU8XPLFVRQNTnd2orrWQ2o62kZk/view?usp=drive_link)

MedPlug is a plugin-based benchmarking framework intended to make medical-image segmentation experiments easier to configure, inspect, and audit. Its focus is the experimental protocol around a model: dataset handling, preprocessing, training configuration, checkpoint selection, metrics, run artifacts, and verification.

**Engineering work**

- Built a DICOM data pipeline for **10,000+ images** (approximately **3 GB**), including image identification, mask parsing, and handling of negative samples.
- Processed **3,000+ image-mask pairs** with no observed data corruption in the documented processing workflow.
- Designed a common model interface and plugin-oriented structure so models can be configured within a shared experiment workflow.
- Added dataset preflight checks, run-level artifact tracking, per-image metric outputs, and an audit step that independently recomputes reported metrics from stored predictions.
- Evaluated Compact U-Net, Attention U-Net, TransUNet-style, and SegFormer-style approaches for SIIM-ACR pneumothorax segmentation.

**Evaluation and reproducibility**

The framework tracks segmentation metrics including Dice, IoU, precision, recall, specificity, MCC, false-positive and false-negative rates, pixel accuracy, and HD95. It also supports bootstrap confidence intervals and paired comparisons when models are evaluated on the same cases under a shared protocol.

An important part of the work is identifying when comparisons are not valid. The repository documents separate experimental protocols and does not rank models across protocols that differ in data composition or evaluation conditions.

**Current research status**

The MedPlug research paper has been **accepted for oral presentation at IC-AIDSA-2026**, an AICTE-sponsored conference.

**Limitations documented in the project**

- The experiments described in the repository use a single random seed; seed-level variability is not yet established.
- A validation/test identifier overlap was identified during an audit in an earlier experiment and is documented for correction before confirmatory comparisons.
- A positive-only diagnostic test split cannot measure false-positive behaviour on healthy images.
- Results from different experimental protocols should not be interpreted as a direct architecture ranking.

These limitations are kept visible so readers can distinguish framework capabilities, diagnostic experiments, and conclusions that still need stronger validation.

### 3. Granite Sandbox: Local PDF Processing with IBM Granite

**2026 · Python · IBM Granite · Ollama · Local Inference**

[Repository](https://github.com/pranay-3108/granite-sandbox)

A small local-inference experiment that uses IBM Granite through Ollama to extract technical information from PDF documents.

- Built a local pipeline for PDF text extraction and skill extraction.
- Compared baseline and iterated pipeline execution times.
- Reduced the documented end-to-end runtime from **133.69 seconds to 10.65 seconds** through prompt and pipeline changes.
- Used the experiment to study cold-start and warm-run behaviour, processing overhead, and practical execution on local hardware.

The runtime figures belong to the documented experiment and hardware/setup; they are not a universal performance guarantee.

### 4. Chess Photo to FEN Generator

**Python · TensorFlow · OpenCV · Computer Vision**

[Repository](https://github.com/pranay-3108/Chess_Fen_GENERATOR)

A computer-vision pipeline that converts a chessboard image into a machine-readable Forsyth–Edwards Notation (FEN) position.

- Detects and crops a chessboard, then divides it into 64 square images.
- Classifies each square and reconstructs the board state.
- Generates a FEN string from the predicted board.
- Investigated generalization failures involving reflections, blur, low-contrast piece outlines, and false-positive piece predictions on empty squares.

The project documents why strong validation accuracy alone did not guarantee reliable predictions on unfamiliar real-world board images.

### 5. Chest X-Ray Pneumothorax Segmentation Data Pipeline

**Python · PyTorch · pydicom · NumPy · Pandas · Image Processing**

[Repository](https://github.com/pranay-3108/Chest-X-Ray-Pneumothorax-Segmentation)

A data-preparation project focused on converting SIIM-ACR DICOM images and run-length-encoded annotations into aligned image-mask pairs for segmentation experiments.

- Loads DICOM images and maps them to annotation records using image identifiers.
- Decodes run-length-encoded pneumothorax masks.
- Handles positive and negative samples and checks image-mask alignment.
- Includes utilities for dataset inspection and visualization of images, masks, and overlays.

The public repository primarily demonstrates preprocessing and data validation; it should not be interpreted as a completed end-to-end model benchmark.

### 6. Agent Neha: Android Security Research Application

**Kotlin · Android · Security Monitoring · Evidence Integrity**

[Repository](https://github.com/pranay-3108/Agent-Neha)

An Android security research application exploring user-authorized monitoring and explainable evidence collection.

- Collects security-relevant signals exposed through Android's supported APIs and user-granted capabilities.
- Uses an evidence-oriented design that separates observed platform data from model-generated interpretations.
- Explores integrity checks for stored evidence and user-authorized VPN-based network isolation.
- Keeps security actions behind explicit user authorization and deterministic policy boundaries.

The project documentation also describes Android platform limitations. It does not claim that an ordinary Android application can silently grant permissions, inspect another app's private sandbox, or universally force-stop other applications.

---

## Experience

### AI Agent Developer Intern — NeuralSeek

**October 2026 – Present**

- Build and test AI-agent workflows that use tools and connect to large language models.
- Work with an international engineering team to evaluate how these workflows behave in practical use.

### Research Intern — Edge AI Medical Device, Vessel Vision

**June 2026 – Present**

- Researching a system for converting an analog X-ray workflow into a digital imaging pipeline using a scintillator-CMOS sensor and NVIDIA Jetson Nano for on-device AI.
- Reviewing research literature and assessing DenseNet-121 as a candidate model for identifying pathologies in X-ray images.
- Investigating image preprocessing, DICOM-to-tensor conversion, and model inference for edge deployment.

---

## Open-source contribution

- **[PyTorch Tutorials #3796](https://github.com/pytorch/tutorials/pull/3796):** submitted a fix for an invalid escape-sequence warning in the `saving_loading_models.py` tutorial. The change removes an unnecessary escape character from a documentation string and does not alter tutorial functionality.

---

## Technical skills

| Area | Tools and concepts |
|---|---|
| Programming | Python, SQL, Kotlin |
| Data analysis | Pandas, NumPy, Matplotlib, data cleaning, data visualization |
| Machine learning | Machine learning, deep learning, model evaluation, benchmarking |
| Frameworks | PyTorch, TensorFlow, scikit-learn |
| Computer vision | OpenCV, image preprocessing, classification, segmentation |
| Language models | LLMs, prompt engineering, Ollama, local inference, answer evaluation |
| Engineering tools | Git, GitHub, Docker, Streamlit |
| Medical imaging | DICOM, image-mask processing, DICOM-to-tensor workflows |

## Education

**B.Tech — Computer Science and Engineering (Data Science)**  
Gaikwad Patil College of Engineering  
Expected graduation: **2027**

- CGPA: **8.72/10**
- Highest semester CGPA: **9.10/10**

## Certifications and programs

- IBM SkillsBuild — Program Participant
- Machine Learning in Production — DeepLearning.AI
- Data Analysis Using Python — IBM
- Advanced Data Analytics — Google

## How I approach technical work

1. Start with a clear question and a working baseline.
2. Keep data, prompts, model settings, and evaluation conditions explicit.
3. Measure outcomes at both aggregate and individual-example levels.
4. Investigate failure cases instead of relying only on a single score.
5. Document what worked, what did not, and what still needs validation.

## Contact

- **Email:** [pranayugale31@gmail.com](mailto:pranayugale31@gmail.com)
- **LinkedIn:** [linkedin.com/in/pranayugale](https://linkedin.com/in/pranayugale)
- **GitHub:** [github.com/pranay-3108](https://github.com/pranay-3108)

---

*This README summarizes selected academic, research, and engineering work. Reported metrics are tied to the specific datasets, benchmarks, configurations, and evaluation protocols described in the linked repositories.*
