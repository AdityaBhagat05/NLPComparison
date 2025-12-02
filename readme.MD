# POS Tagging – Comparative Study  
Comparative Analysis of Classical and LLM-based NLP Techniques for Part-of-Speech Tagging in Indian Contexts

This repository contains Jupyter notebooks and dataset preparation scripts used to compare different POS-tagging approaches:  
- **Rule-Based model**  
- **Hidden Markov Model (HMM)**  
- **spaCy Neural Tagger (CNN/LSTM)**  
- **BERT Fine-Tuned Model**  
- **GPT-style LLM Prompting**

The project evaluates accuracy, inference speed, and robustness on an English dataset augmented with **Indian names**, **locations**, and **code-mixed sentences (Indian English / Hinglish).**

---

## Repository Structure

```
NLPComparison/
│
├── dataset.ipynb           # Builds augmented dataset (PTB + Indian context)
├── Rule_based (2).ipynb    # Rule-based POS tagger implementation
├── HMM__model.ipynb        # HMM training + Viterbi decoding
├── spaCy_final.ipynb       # spaCy neural model training & evaluation
├── Bert_final.ipynb        # BERT fine-tuning & accuracy evaluation
├── GPTcleaned.ipynb        # GPT-based POS tagging via prompting
│
└── readme.MD               # This README file
```

---

## 🔧 Requirements

Install  Python packages:

```bash
pip install -r requirements.txt
```

Additional steps:

```bash
python -m spacy download en_core_web_sm
```

Downloading Datasets

- https://www.kaggle.com/datasets/zed9941/top-500-indian-cities
- https://www.kaggle.com/datasets/rowhitswami/all-indian-companies-registration-data-1900-2019
- https://www.kaggle.com/datasets/ananysharma/indian-names-dataset



(Optional but recommended):  
A GPU greatly speeds up BERT training and GPT prompting.

---

## ▶️ How to Reproduce the Results

Follow these steps **in order** to regenerate all results and plots used in the report.

---

## 1️⃣ Create the Augmented Dataset

Open **`dataset.ipynb`** and run all cells.

This notebook:  
- Loads the Penn TreeBank 
- Loads Indian augmentation lists (names, places,companies)  
- Creates a final train/dev/test split  
- Saves pkl files for use by other notebooks  



---

## 2️⃣ Run Each Model Notebook

### **A. Rule-Based Model**
Open **`Rule_based (2).ipynb`**  
This notebook:  
- Builds a simple lexicon + suffix rules  
- Tags sample sentences  
- Computes accuracy on test set  

### **B. Hidden Markov Model (HMM)**
Run **`HMM__model.ipynb`**  
This performs:  
- Transition + emission probability calculation  
- Viterbi decoding  
- Accuracy evaluation on augmented dataset

### **C. spaCy Neural Tagger**
Run **`spaCy_final.ipynb`**  
This:  
- Fine-tunes spaCy's CNN/LSTM-based POS tagger  
- Evaluates macro-F1  
- Exports accuracy + confusion matrix  

### **D. BERT Fine-Tuning**
Run **`Bert_final.ipynb`**  
This notebook:  
- Loads HuggingFace BERT  
- Maps tokens → tags  
- Fine-tunes on augmented dataset  
- Records F1 score  
- Measures inference latency per batch  

### **E. GPT Prompting**
Run **`GPTcleaned.ipynb`**  
This tests:  
- Zero-shot prompting  
- Few-shot prompting  
- GPT-based tag quality  
- Latency measurements

> Note: GPT requires access to API keys or a local LLM.

---

## 3️⃣ Generate Figures Used in the Report

Each notebook exports numerical results.  
From these, generate two main plots:

### **Accuracy Plot (F1-Macro)**
Values used:
- HMM — 88.5%
- Rule-Based — 84%
- spaCy — 93.2%
- BERT — 97.2%
- LLM — 64.1%

### **Inference Speed Plot**
(seconds per 100 sentences on CPU):

- HMM — 8  
- Rule-Based — 6  
- spaCy — 25  
- BERT — 120  
- GPT/LLM — 600  




## 📌 Summary of Findings

- **BERT achieves highest F1 score**, especially on culturally-specific tokens.  
- **spaCy** provides the best **accuracy vs speed trade-off**.  
- **HMM + Rule-Based** are extremely fast and good for edge devices.  
- **GPT models are inconsistent**, slower, and prone to hallucination for structured tasks.  

---

## 📬 Contact

For help running any notebook, open an issue or message the repository owner.

---
