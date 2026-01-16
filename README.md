# 🧠 EEG Seizure Detection with Deep Learning & Explainable AI

---

## 📌 Table of Contents
1. [Project Overview](#project-overview)
2. [Business & Clinical Value](#business--clinical-value)
3. [Dataset](#dataset)
4. [Tasks Studied](#tasks-studied)
5. [End-to-End Project Pipeline](#end-to-end-project-pipeline)
6. [Signal Processing](#signal-processing)
7. [Deep Learning Models](#deep-learning-models)
8. [Model Comparison](#model-comparison)
9. [Feature Extraction & Comparison](#feature-extraction--comparison)
10. [Explainable AI (XAI)](#explainable-ai-xai)
11. [XAI Method Comparison](#xai-method-comparison)
12. [Outputs](#outputs)
13. [Key Takeaways](#key-takeaways)
14. [Future Work](#future-work)

---

## Project Overview

Epilepsy is a chronic neurological disorder affecting over 50 million people worldwide. EEG (Electroencephalogram) analysis is the gold standard for seizure detection, but manual inspection is time-consuming and difficult to scale.

This project presents an **end-to-end EEG seizure detection pipeline** using **deep learning and Explainable AI (XAI)**.  
Unlike accuracy-only approaches, this work emphasizes:

- Robust signal processing
- Deep feature extraction and comparison
- Model selection based on representation quality
- Faithfulness-based explainable AI
- Clear clinical and business value

---

## Business & Clinical Value

### 🏥 Clinical Impact
- Automatic seizure detection assists neurologists
- Reduces EEG review time
- Improves response speed during seizures

### ⌚ Remote & Wearable Monitoring
- Suitable for ICU/EMU systems
- Can be deployed in wearable EEG devices
- Enables continuous patient monitoring

### 🧠 Trustworthy Medical AI
- Incorporates explainable AI techniques
- Builds clinician trust
- Supports regulatory and ethical requirements

### 💼 Business Impact
- Reduces operational healthcare costs
- Enables scalable AI-driven medical solutions
- Improves adoption through interpretability

---

## Dataset

This project uses the **University of Bonn EEG Dataset**.

### 📥 Download Link
You can download the dataset from the official source:

🔗 https://physionet.org/content/eegmat/1.0.0/

*(Alternatively available via multiple academic mirrors as “Bonn EEG Dataset”)*

### Dataset Structure

| Set | Description |
|---|---|
| A | Healthy subjects (eyes open, scalp EEG) |
| B | Healthy subjects (eyes closed, scalp EEG) |
| C | Interictal EEG from epileptic patients |
| D | Interictal EEG from epileptic patients (different region) |
| E | Ictal EEG (seizure activity) |

**Sampling rate:** 173.61 Hz  
**Segment length:** 4096 samples (~23.6 seconds)  
**Channels:** Single-channel EEG  

---

## Tasks Studied

Two complementary binary classification tasks are evaluated:

### Task 1 — AB vs E (Healthy vs Seizure)
- Non-seizure: A + B
- Seizure: E
- Clean baseline for benchmarking

### Task 2 — CD vs E (Interictal vs Ictal)
- Non-seizure: C + D
- Seizure: E
- Clinically more realistic patient-specific detection

---

## End-to-End Project Pipeline

```
Raw EEG Files
   ↓
Signal Processing
   ↓
Leakage-Safe Train / Val / Test Split
   ↓
Train Deep Learning Models
   ↓
Model Comparison
   ↓
Feature Extraction & Comparison
   ↓
Best Model Selection
   ↓
Explainable AI (2 methods)
   ↓
XAI Faithfulness Comparison
   ↓
Reports & Business Insights
```

---

## Signal Processing

EEG signals are noisy and non-stationary.

### Steps
- **Bandpass filtering (0.5–40 Hz)** to retain seizure-relevant frequencies
- **Z-score normalization per segment**
- Optional windowing for real-time extensions

---

## Deep Learning Models

Three architectures are implemented:

1. **CNN1D** – learns local waveform patterns
2. **CNN + BiLSTM** – combines spatial and temporal modeling
3. **Transformer1D** – captures long-range dependencies via self-attention

---

## Model Comparison

Models are evaluated using Accuracy, F1-score, and ROC-AUC.

| Task | Best Model | Accuracy | F1 | AUC |
|---|---|---:|---:|---:|
| AB vs E | Transformer1D | 0.983 | 0.974 | 1.000 |
| CD vs E | CNN1D | 0.967 | 0.947 | 0.982 |

**Insight:**  
The optimal architecture depends on the clinical scenario.

---

## Feature Extraction & Comparison

To understand *why* models perform well, we extract **128-dimensional embeddings** from each model.

### Feature Evaluation Methods
- **Silhouette Score** – cluster separability
- **Linear Probe** – linear separability of embeddings
- **t-SNE** – visual cluster inspection

### Key Result (AB vs E)
Transformer1D embeddings show the highest separability and perfect linear probe performance.

---

## Explainable AI (XAI)

Two model-compatible XAI methods are applied to the best model per task:

1. **Integrated Gradients**
2. **Occlusion Attribution**

Grad-CAM is not used due to incompatibility with pure Transformer architectures.

---

## XAI Method Comparison

XAI faithfulness is evaluated using:

- **Deletion Test** (lower is better)
- **Insertion Test** (higher is better)

### AB vs E (Best Model: Transformer1D)
Occlusion outperforms Integrated Gradients on both tests.

### CD vs E (Best Model: CNN1D)
Results are task-dependent, showing mixed faithfulness behavior.

---

## Outputs

Each task generates:
- `summary.txt` – model metrics
- `feature_report.txt` – embedding analysis
- `tsne_*.png` – feature visualization
- `xai_report.txt` – explanation faithfulness
- Model checkpoints
- Final comparison CSV

---

## Key Takeaways

- Feature quality explains model superiority
- Best model varies by clinical task
- Occlusion is the most faithful XAI for Transformer-based EEG models
- Explainability is essential for real-world adoption

---

## Future Work

- Multi-channel EEG analysis
- Continuous seizure onset detection
- Attention-based explanations
- Cross-dataset validation
- Real-time deployment

---

## Final Statement

> High-performing EEG seizure detection systems must integrate strong signal processing, discriminative feature learning, and faithful explainable AI to deliver real clinical and business value.
