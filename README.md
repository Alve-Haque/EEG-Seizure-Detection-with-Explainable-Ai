# 🧠 EEG Seizure Detection using Deep Learning & Explainable AI  

📊 **Accurate** · 🔍 **Interpretable** · 💼 **Business-Ready** · 🏥 **Clinically Relevant**

---

## Table of Contents
1. [Project Overview](#project-overview)
2. [Business & Clinical Value](#business--clinical-value)
3. [Dataset](#dataset)
4. [Problem Formulation](#problem-formulation)
5. [End-to-End Project Pipeline](#end-to-end-project-pipeline)
6. [Signal Processing (In Detail)](#signal-processing-in-detail)
7. [Deep Learning Models](#deep-learning-models)
8. [Model Comparison](#model-comparison)
9. [Feature Extraction & Comparison](#feature-extraction--comparison)
10. [Explainable AI (XAI)](#explainable-ai-xai)
11. [XAI Method Comparison](#xai-method-comparison)
12. [Project Outputs](#project-outputs)
13. [Key Takeaways](#key-takeaways)
14. [Future Work](#future-work)

---

## Project Overview

Epilepsy is a chronic neurological disorder affecting **50+ million people worldwide**.  
EEG (Electroencephalogram) analysis is the gold standard for seizure detection, but **manual inspection** is:

- ⏱️ Time-consuming  
- 🧠 Expert-dependent  
- 📉 Not scalable for continuous monitoring  

### 🎯 Goal of This Project
To build a **complete, explainable EEG seizure detection system** using **deep learning**, while answering:

- ❓ Which model performs best?  
- ❓ Why does it perform best?  
- ❓ Can we trust its decisions?  

---

## Business & Clinical Value

### 🏥 Clinical Value
- ✅ Automated seizure detection assists neurologists  
- ✅ Reduces EEG review workload  
- ✅ Enables faster medical intervention  
- ✅ Provides interpretable explanations for trust  

### ⌚ Remote & Wearable Monitoring
- 📡 ICU & Epilepsy Monitoring Units (EMU)  
- ⌚ Wearable EEG devices  
- 🏠 Home-based long-term monitoring  

### 💼 Business Value
- 💰 Reduces healthcare operational cost  
- 🚀 Enables scalable AI-driven medical products  
- ⚖️ Supports regulatory compliance via Explainable AI  
- 🤝 Improves adoption through transparency  

---

## Dataset

This project uses the **University of Bonn EEG Dataset**.

### Dataset Download
🔗(https://www.kaggle.com/datasets/quands/eeg-dataset)

### Dataset Structure
```
Dataset/
├── A/
├── B/
├── C/
├── D/
└── E/
```

| Set | Description |
|----|------------|
| A | Healthy scalp EEG (eyes open) |
| B | Healthy scalp EEG (eyes closed) |
| C | Interictal EEG (epileptic patients) |
| D | Interictal EEG (different region) |
| E | Ictal EEG (seizure activity) |

- 🧠 Sampling Rate: **173.61 Hz**  
- ⏱️ Segment Length: **4096 samples (~23.6 s)**  
- 📡 Channels: **Single-channel EEG**

---

## Problem Formulation

### Task 1 — AB vs E (Healthy vs Seizure)
- 🟢 Non-seizure: A + B  
- 🔴 Seizure: E  
- ✔️ Clean baseline task  
- ✔️ Ideal for feature learning analysis  

### Task 2 — CD vs E (Interictal vs Ictal)
- 🟢 Non-seizure: C + D  
- 🔴 Seizure: E  
- ✔️ Clinically realistic  
- ✔️ Patient-specific seizure detection  

---

## End-to-End Project Pipeline

```
Raw EEG Files
   ↓
Signal Processing
   ↓
Leakage-Safe Train / Validation / Test Split
   ↓
Train Deep Learning Models
   ↓
Model Performance Comparison
   ↓
Feature Extraction & Representation Analysis
   ↓
Best Model Selection
   ↓
Explainable AI (IG + Occlusion)
   ↓
XAI Faithfulness Comparison
   ↓
Final Reports, Plots & Business Insights
```

---

## Signal Processing (In Detail)

EEG signals are **noisy, non-stationary**, and sensitive to artifacts.

### Bandpass Filtering
- 🎛️ Butterworth filter  
- 📉 Frequency range: **0.5 – 40 Hz**  
- Removes DC drift, muscle artifacts, and high-frequency noise  
- Preserves seizure-relevant EEG rhythms  

### Standardization
- 📏 Z-score normalization per segment  
- Removes amplitude scaling issues  
- Improves model convergence  

### Windowing (Optional)
- Default: full 4096-sample segments  
- Supports overlapping windows  
- Enables future real-time deployment  

---

## Deep Learning Models

### CNN1D
- 🧩 Learns local temporal patterns  
- ⚡ Computationally efficient  
- ✔️ Strong at waveform morphology detection  

### CNN + BiLSTM
- 🧩 CNN extracts spatial features  
- 🔁 BiLSTM models temporal dependencies  
- ⚠️ Higher complexity, not always superior  

### Transformer1D
- 🧠 Patch-based EEG embedding  
- 🔍 Self-attention captures long-range context  
- ✔️ Excellent global representation learning  

---

## Model Comparison

| Task | Best Model | Accuracy | F1 | AUC |
|----|-----------|---------|----|----|
| **AB vs E** | **Transformer1D** | 0.983 | 0.974 | 1.000 |
| **CD vs E** | **CNN1D** | 0.967 | 0.947 | 0.982 |

📌 **Insight:**  
The best architecture depends on the clinical scenario.

---

## Feature Extraction & Comparison

### Feature Extraction
- Extract **128-dimensional embeddings**  
- Taken from penultimate layer of each model  

### Feature Evaluation Metrics
- 📊 Silhouette Score – cluster separability  
- 🧪 Linear Probe – linear separability of embeddings  
- 🎨 t-SNE – visual inspection  

### Feature Comparison (AB vs E)

| Model | Silhouette ↑ | Linear Probe Acc ↑ | Linear Probe F1 ↑ |
|----|--------------|-------------------|------------------|
| CNN1D | 0.799 | 0.989 | 0.983 |
| CNN + BiLSTM | 0.780 | 0.933 | 0.893 |
| **Transformer1D** | **0.877** | **1.000** | **1.000** |

---

## Explainable AI (XAI)

### XAI Methods Used
- Integrated Gradients (IG)  
- Occlusion Attribution  

Grad-CAM is not used because it is incompatible with pure Transformer models.

---

## XAI Method Comparison

### AB vs E (Transformer1D)

| Method | Deletion ↓ | Insertion ↑ |
|------|------------|-------------|
| Integrated Gradients | 19.36 | 9.34 |
| **Occlusion** | **18.91** | **18.96** |

### CD vs E (CNN1D)

| Method | Deletion ↓ | Insertion ↑ |
|------|------------|-------------|
| Integrated Gradients | 7.48 | 14.43 |
| Occlusion | 1.49 | 2.52 |

**Interpretation:**  
For the CD vs E task, the faithfulness results are **mixed**, indicating that explanation quality can be task- and model-dependent.

---

## Project Outputs

- 📄 Model checkpoints  
- 📄 Feature reports  
- 🖼️ t-SNE plots  
- 📄 XAI reports  
- 📊 Final comparison CSV  

---

## Key Takeaways

- ⚙️ Signal processing is critical  
- 🧠 Best model depends on task  
- 🧩 Feature quality explains performance  
- 🔍 Faithful XAI enables trust and adoption  

---

## Future Work

- Multi-channel EEG  
- Continuous seizure onset detection  
- Attention-based explanations  
- Real-time deployment  

---

Reliable EEG seizure detection requires **robust signal processing, strong feature learning, and faithful explainable AI** to deliver real clinical and business value.
