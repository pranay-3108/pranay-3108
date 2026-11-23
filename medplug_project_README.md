# MedPlug

**Standardized and Reproducible Benchmarking of Medical Image Segmentation**

[Research Paper](https://drive.google.com/file/d/19ztNvJ3WWUTH76GH6a37FAy6qCVXWQn0/view?usp=drive_link) · [Demo Video](https://drive.google.com/file/d/1XNMTAUU8XPLFVRQNTnd2orrWQ2o62kZk/view?usp=drive_link)

**Research status:** Accepted for oral presentation at **IC-AIDSA-2026**, an AICTE-sponsored conference.

## Overview

Medical image segmentation results are difficult to compare fairly when experiments use different data splits, preprocessing pipelines, checkpoint-selection rules, thresholds, metric implementations, or empty-mask conventions. When several of these factors change together, a reported performance difference cannot be attributed to the model alone.

MedPlug is a modular, plugin-based PyTorch framework that makes the experimental protocol explicit. It provides common interfaces for datasets, preprocessing, and models, records each run separately, and independently checks reported metrics against stored per-image outputs.

MedPlug does not introduce a new segmentation architecture. Its contribution is an auditable benchmarking workflow for running and comparing segmentation experiments under clearly stated protocols.

## What the Framework Provides

| Area | Implementation |
|---|---|
| Model interface | Common tensor contract: `N × C × H × W` input to `N × 1 × H × W` output |
| Dataset checks | Preflight validation of schema, split sizes, class counts, DICOM mapping, and RLE decoding |
| Plugin design | Dataset, preprocessing, and model components are registered through explicit interfaces |
| Checkpoint selection | Best checkpoint selected using positive-case validation Dice |
| Run isolation | Each experiment receives a unique run ID and its own configuration, logs, checkpoints, metrics, predictions, and reports |
| Independent audit | Metrics are recomputed from stored per-image outputs and checked against the run report |

## Data Pipeline

The SIIM-ACR pneumothorax data pipeline was built around DICOM images and run-length-encoded (RLE) masks.

- Worked with **10,000+ DICOM images** (approximately **3 GB** of image data).
- Implemented DICOM loading, RLE mask parsing, image-to-label mapping, and handling of negative samples.
- Prepared **3,000+ image-mask pairs**; the pipeline checks completed without detected data corruption.
- Added dataset preflight checks to catch schema, split, mapping, and mask-decoding problems before training.

The dataset itself is external to this repository and is not redistributed here.

## Audit Findings

The audit workflow is intended to detect protocol and artifact problems that can be hidden by a single aggregate metric. During development it exposed:

- validation–test identifier overlap (42 of 174 test identifiers also appeared in validation);
- degenerate image-level metrics caused by an unsuitable decision rule;
- disagreement between a run's reported status and independent verification;
- channel-count inconsistencies between configuration and archived checkpoints;
- incomplete training logs and missing artifacts in earlier runs.

These findings are documented as limitations and follow-up work, not presented as evidence of a completed, leakage-free benchmark.

## Experimental Demonstration

Four model families were exercised in two deliberately separate protocols. The protocols differ in data composition, input channels, and early-stopping policy, so the results below **must not be ranked against one another**.

### Protocol A — Full contract split containing negative cases

- Model: Compact U-Net
- Positive-case validation Dice: approximately **0.617**
- All-case test Dice: **0.132**

The model predicted foreground on nearly every healthy image. This illustrates why aggregate scores and positive-case metrics need to be inspected together.

### Protocol B — Positive-only diagnostic split

| Model | Test Dice | 95% bootstrap interval |
|---|---:|---:|
| Attention U-Net | 0.670 | [0.637, 0.702] |
| TransUNet-style | 0.666 | [0.633, 0.700] |
| SegFormer-style | 0.455 | [0.432, 0.477] |

A paired bootstrap comparison between Attention U-Net and the TransUNet-style model gave a mean difference of **0.004**, with interval **[-0.005, 0.012]**. Since the interval contains zero, this experiment does not demonstrate a difference between those two models.

All three Protocol-B models under-segmented, with recall between **0.33 and 0.41**. Their mean predicted mask area was smaller than the mean ground-truth mask area.

## Metrics and Evaluation

Primary pixel-level metrics include Dice, IoU, Precision, Recall, Specificity, MCC, FPR, FNR, Pixel Accuracy, and HD95. Positive-case Dice and IoU are also computed explicitly.

Uncertainty is estimated using 95% percentile bootstrap intervals from 5,000 resamples of test cases. Paired model comparisons use the same bootstrap procedure on identical images.

Empty-prediction conventions are explicit: both-empty images receive Dice/IoU of 1; a non-empty target with an empty prediction receives an HD95 penalty equal to the image diagonal.

Image-level metrics are currently flagged as uninterpretable under the positive-only diagnostic protocol. A redesigned decision rule is required before these metrics can be used for model comparison.

## Installation

```bash
git clone https://github.com/pranay-3108/MedPlug-Standardized-and-Reproducible-Benchmarking-of-Medical-Image-Segmentation.git
cd MedPlug-Standardized-and-Reproducible-Benchmarking-of-Medical-Image-Segmentation
pip install -r requirements.txt
pytest
```

## Dataset Setup

The dataset remains external. Configure one dataset root with the following layout:

```text
dataset_root/
├── data/
│   ├── train-rle.csv
│   ├── val-rle.csv
│   └── test-rle.csv
├── images/
│   ├── dicom-images-train/
│   └── dicom-images-test/
└── aligned_dataset/          # optional
    ├── images/
    └── masks/
```

Example configuration:

```yaml
dataset:
  plugin: siim_acr
  root: "path/to/dataset_root"
```

In `source_mode: auto`, the framework prefers pre-aligned image/mask pairs when available and otherwise uses DICOM images with RLE labels.

## Run the Application

```bash
python app.py
```

Use the control panel to configure the model, hyperparameters, and metrics. Run **Verify & Prepare Run** to execute preflight checks and generate the training command. Execute that command in a separate terminal; `run_pipeline.py` handles preflight, training, evaluation, audit, and report generation.

Command-line workflow:

```bash
python preflight.py --config configs/your_config.yaml
python run_pipeline.py --config configs/your_config.yaml
```

Resume an interrupted run:

```bash
python train.py --config configs/your_config.yaml --resume
```

## Current Limitations

- Experiments to date use a single random seed; seed-level variance has not yet been quantified.
- Protocol A and Protocol B are not interchangeable, so no architecture ranking across the four model families is claimed.
- The positive-only diagnostic split cannot measure false-positive behaviour on healthy radiographs.
- Image-level metrics under the current decision rule are not interpretable on the positive-only test set.
- Validation–test identifier overlap found during auditing must be resolved in future runs.
- Full paper artifacts, including checkpoints and per-image result tables, are not yet publicly released.

A multi-seed comparison under one shared protocol is planned after leakage checks, image-level rule redesign, and shared-split infrastructure are addressed.

## Research Paper

Pranay Ugale, Manindra Dharani, Gaurav Paradhe, Mahamuni Kotangale, and Ashwini Pise. **“MedPlug: Standardized and Reproducible Benchmarking of Medical Image Segmentation.”** Accepted for oral presentation at IC-AIDSA-2026, an AICTE-sponsored conference.

## Contact

**Pranay Ugale**  
Department of CSE – Data Science  
Tulsiramji Gaikwad-Patil College of Engineering & Technology, Nagpur, India  
[Email](mailto:pranayugale31@gmail.com) · [LinkedIn](https://linkedin.com/in/pranayugale)
