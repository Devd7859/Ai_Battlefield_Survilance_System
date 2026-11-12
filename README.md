# GuardianAI: AI-Powered Battlefield Surveillance System

### A Decoupled Dual-Model YOLO11 Pipeline for Scene and Safety-Object Detection with Human-in-the-Loop Review

GuardianAI is an AI-powered surveillance system designed to support battlefield and security monitoring through object detection and safety-object identification. It uses two independently trained YOLO11 models to process a shared video-frame stream, combining scene understanding with specialized safety-object detection.

The system integrates a Human-in-the-Loop (HITL) review mechanism and a tamper-evident event logging system to support human verification and traceability of critical detections.

---

## Project Overview

Traditional object detection systems often combine different detection tasks into a single model. GuardianAI explores a decoupled approach in which two specialized YOLO11 models operate independently on the same input frames.

The system consists of:

- **Scene Detection Model:** Detects 10 object categories from the VisDrone dataset.
- **Safety-Object Detection Model:** Detects two firearm categories: handgun and rifle.
- **Detection Compositor:** Combines the outputs of both models into a unified detection interface.
- **Human-in-the-Loop Review:** Routes safety detections exceeding a configurable confidence threshold for human verification.
- **Tamper-Evident Event Logging:** Uses SHA-256 hash chaining to maintain a verifiable event history.

## System Architecture

```text
                 Input Video / Frames
                         |
                         v
                  Shared Frame Stream
                         |
              +----------+----------+
              |                     |
              v                     v
       Scene Detection       Safety Detection
        YOLO11n Model          YOLO11n Model
              |                     |
              v                     v
       10 Scene Classes       2 Safety Classes
              |                     |
              +----------+----------+
                         |
                         v
                Detection Compositor
                         |
                         v
              Unified Detection Output
                         |
                         v
             Confidence Threshold Check
                         |
                         v
                Human-in-the-Loop
                    Verification
                         |
                         v
                Event Logging System
                  (SHA-256 Chain)
```

## Models and Datasets

GuardianAI uses two independently trained YOLO11n models.

| Component | Dataset | Classes |
|---|---|---:|
| Scene Detection | VisDrone 2019 DET | 10 |
| Safety-Object Detection | Original `gundataset` | 2 |

### 1. Scene Detection Model

- Architecture: YOLO11n
- Dataset: VisDrone 2019 DET
- Number of classes: 10
- Training duration: 25 epochs
- Batch size: 8

### 2. Safety-Object Detection Model

- Architecture: YOLO11n
- Dataset: `gundataset`
- Classes: Handgun and Rifle
- Training duration: 25 epochs
- Batch size: 32

**Dataset Availability**

The repository includes the original datasets used during development, subject to their respective distribution and licensing conditions.

- VisDrone: https://github.com/VisDrone/VisDrone-Dataset
- Safety-object dataset: https://www.kaggle.com/datasets/yadavdevdayanand/gundataset

Please refer to the original dataset sources for their licensing and usage conditions.

## Model Performance

The following results were obtained during model validation.

### Safety-Object Detection Model

| Metric | Result |
|---|---:|
| mAP@0.5 | 0.912 |
| mAP@0.5:0.95 | 0.719 |
| Precision | 0.887 |
| Recall | 0.852 |

### Scene Detection Model

| Metric | Result |
|---|---:|
| mAP@0.5 | 0.290 |
| mAP@0.5:0.95 | 0.159 |
| Precision | 0.414 |
| Recall | 0.310 |

### Inference Performance

| Parameter | Result |
|---|---|
| GPU | NVIDIA Tesla T4 |
| Input resolution | 640 × 640 |
| Inference mode | Sequential |
| Measured throughput | 52.86 FPS |
| Average inference latency | 18.92 ms/frame |

**Benchmarking note:** The inference measurement was obtained using a synthetic 640 × 640 input frame, with 10 warm-up passes followed by 100 forward passes. It should not be interpreted as an end-to-end real-world video performance measurement.

## Key Features

- **Decoupled Detection Architecture:** Two specialized YOLO11 models handle different detection tasks.
- **Multi-Class Scene Understanding:** Detects 10 scene-object categories using VisDrone.
- **Specialized Safety Detection:** Identifies handgun and rifle categories.
- **Detection Composition:** Combines outputs from independently trained models.
- **Human-in-the-Loop Verification:** Enables human review of qualifying safety detections.
- **Tamper-Evident Logging:** Maintains event integrity through SHA-256 hash chaining.
- **Configurable Confidence Threshold:** Supports threshold-based routing of detections for review.

## Repository Contents

This repository provides the original project resources used to develop and evaluate GuardianAI, including:

- Original datasets used for training and evaluation.
- YOLO11 model training code.
- Trained model weights.
- Model evaluation and experimentation resources.
- System implementation and integration code.
- Project documentation and demonstration materials.

Refer to the repository folders for the corresponding source files and resources.

## Installation

Clone the repository:

```bash
git clone https://github.com/Devd7859/Ai_Battlefield_Survilance_System.git
cd Ai_Battlefield_Survilance_System
```

Create and activate a Python virtual environment:

```bash
python -m venv venv
```

Windows:

```bash
venv\Scripts\activate
```

Linux / macOS:

```bash
source venv/bin/activate
```

Install the required dependencies:

```bash
pip install ultralytics opencv-python numpy pandas matplotlib
```

Additional dependencies may be required depending on the specific training, inference, and interface scripts. Refer to the individual project files for their requirements.

## Running the Project

The repository contains the original training and implementation code.

For model training, evaluation, and inference:

1. Clone the repository.
2. Install the required dependencies.
3. Prepare the datasets using their corresponding annotations and configurations.
4. Load the appropriate YOLO11 model configuration and training script.
5. Run the scene and safety-object detection workflows.
6. Integrate the model outputs through the GuardianAI detection pipeline.
7. Review qualifying safety detections through the human-verification workflow.

Use the relevant scripts and configuration files available in the repository. Exact execution commands depend on the individual script names and dataset paths.

## Demonstration

The repository includes a demonstration of the GuardianAI system, illustrating its detection workflow and output.

See the demonstration video and project resources included in this repository.

## Research Paper

**Title:** GuardianAI: A Decoupled Dual-Model YOLO11 Pipeline for Scene and Safety-Object Detection with Human-in-the-Loop Review.

This project is accompanied by a research paper describing the system architecture, model training methodology, evaluation results, implementation approach, and limitations.

## Current Limitations and Future Work

The current implementation provides a foundation for exploring decoupled object-detection architectures. Further work includes:

- Comparison against a jointly trained 12-class YOLO11 baseline.
- Confidence-threshold calibration and false-alarm analysis.
- Evaluation across multiple random seeds.
- Real-world video benchmarking, including latency percentiles.
- GPU memory and concurrent-inference benchmarking.
- Testing under low-light, occlusion, and motion-blur conditions.
- Evaluation of human-review workload and operational reliability.

The system is a research prototype and has not been validated for operational battlefield deployment.

## Author

**Dev Dayanand Yadav**  
Department of Computer Science and Engineering  
VIT-AP University, Amaravati, Andhra Pradesh, India

GitHub: https://github.com/Devd7859

---

## Acknowledgements

- VisDrone Dataset contributors.
- Ultralytics YOLO11 framework.
- Contributors and maintainers of the original datasets used in this project.

---

*GuardianAI — Combining specialized AI detection with human verification for safety-oriented surveillance research.*
