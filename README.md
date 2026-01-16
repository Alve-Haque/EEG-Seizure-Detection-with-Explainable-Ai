# 🧠 EEG Seizure Detection using Deep Learning & Explainable AI  

📊 Accurate · 🔍 Interpretable · 💼 Business-Ready · 🏥 Clinically Relevant

---

## 📌 Table of Contents
1. Project Overview  
2. Business & Clinical Value  
3. Dataset  
4. Problem Formulation  
5. End-to-End Project Pipeline  
6. Signal Processing (In Detail)  
7. Deep Learning Models  
8. Model Comparison  
9. Feature Extraction & Comparison  
10. Explainable AI (XAI)  
11. XAI Method Comparison  
12. Project Outputs  
13. Key Takeaways  
14. Future Work  

---

## 🔹 Project Overview

Epilepsy is a chronic neurological disorder affecting **50+ million people worldwide**. EEG (Electroencephalogram) analysis is the gold standard for seizure detection, yet manual inspection is time-consuming, expert-dependent, and not scalable.

This project presents a **complete, end-to-end EEG seizure detection system** using **deep learning and Explainable AI (XAI)**, focusing not only on accuracy but also on **feature learning, interpretability, and business value**.

---

## 💼 Business & Clinical Value

### 🏥 Clinical Value
- Automated seizure detection to assist neurologists  
- Reduced EEG review workload  
- Faster medical intervention  
- Transparent explanations for clinical trust  

### ⌚ Remote & Wearable Monitoring
- ICU and Epilepsy Monitoring Units (EMU)  
- Wearable EEG devices  
- Long-term home monitoring  

### 💼 Business Value
- Reduced operational healthcare costs  
- Scalable AI-driven medical solutions  
- Regulatory-friendly explainable AI  
- Higher adoption through transparency  

---

## 📂 Dataset

This project uses the **University of Bonn EEG Dataset**.

### 📥 Dataset Download
Official source:  
https://physionet.org/content/eegmat/1.0.0/

### 📁 Dataset Structure
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
| A | Healthy EEG (eyes open) |
| B | Healthy EEG (eyes closed) |
| C | Interictal EEG (epileptic patients) |
| D | Interictal EEG (different region) |
| E | Ictal EEG (seizure) |

Sampling rate: 173.61 Hz  
Segment length: 4096 samples  

---

## 🧪 Problem Formulation

Two complementary classification tasks are studied:

### Task 1 — AB vs E
- Non-seizure: A + B  
- Seizure: E  
- Clean baseline task  

### Task 2 — CD vs E
- Non-seizure: C + D  
- Seizure: E  
- Clinically realistic patient-specific detection  

---

## 🔄 End-to-End Project Pipeline

Raw EEG → Signal Processing → Train/Val/Test Split →  
Model Training → Model Comparison → Feature Extraction →  
Explainable AI → XAI Comparison → Reports

---

## ⚙️ Signal Processing (In Detail)

- **Bandpass filtering (0.5–40 Hz)**  
  Removes noise while preserving seizure-relevant rhythms  

- **Z-score normalization per segment**  
  Stabilizes training and removes amplitude bias  

- **Optional windowing**  
  Enables future real-time deployment  

---

## 🧠 Deep Learning Models

### CNN1D
- Learns local temporal patterns  
- Efficient and robust  

### CNN + BiLSTM
- Captures temporal dependencies  
- Higher complexity  

### Transformer1D
- Self-attention based  
- Learns long-range EEG context  

---

## 📊 Model Comparison

| Task | Best Model | Accuracy | F1 | AUC |
|---|---|---|---|---|
| AB vs E | Transformer1D | 0.983 | 0.974 | 1.000 |
| CD vs E | CNN1D | 0.967 | 0.947 | 0.982 |

---

## 🧩 Feature Extraction & Comparison

- 128-dimensional embeddings  
- Silhouette score  
- Linear probe (logistic regression)  
- t-SNE visualization  

Transformer1D learned the most discriminative features in AB vs E.

---

## 🧠 Explainable AI (XAI)

### Methods
- Integrated Gradients  
- Occlusion Attribution  

Grad-CAM is not used due to Transformer incompatibility.

---

## 📉 XAI Method Comparison

### AB vs E (Transformer1D)
- Occlusion outperformed Integrated Gradients on deletion & insertion tests  

---

## 📦 Project Outputs

- Model checkpoints  
- Feature reports  
- t-SNE plots  
- XAI reports  
- Final comparison CSV  

---

## ✅ Key Takeaways

- Signal processing is critical  
- Best model depends on task  
- Feature quality explains performance  
- Faithful XAI enables trust  

---

## 🚀 Future Work
- Multi-channel EEG  
- Continuous seizure onset detection  
- Attention-based explanations  
- Real-time deployment  

---

## 🏁 Final Remark

Reliable EEG seizure detection requires **robust signal processing, strong feature learning, and faithful explainable AI** to deliver real clinical and business value.
