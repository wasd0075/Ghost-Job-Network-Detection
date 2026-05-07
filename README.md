# Ghost Job Network Detection System

> **AI-powered fraud detection for online recruitment platforms using semantic clustering and structured anomaly detection.**

---

## Overview

This project presents a hybrid fraud detection framework designed to identify fake job postings and uncover coordinated ghost employer networks on freelancing platforms such as Upwork. Unlike traditional approaches that classify individual job posts in isolation, this system detects coordinated scam patterns across multiple listings — without requiring any labeled training data.

The system combines **NLP-based semantic analysis** (MiniLM / DistilBERT embeddings) with **tabular anomaly detection** (TabNet Classifier) to flag both near-duplicate scam posts and suspicious employer behavior at scale.

---

## Key Features

- **Unsupervised / Semi-supervised Learning** — No labeled dataset required; the model learns fraud patterns from raw job posting data
- **Dual-Model Architecture** — Combines textual embeddings and structured metadata for complementary fraud signal detection
- **Ghost Network Detection** — Identifies clusters of coordinated fake job rings, not just isolated fraudulent posts
- **Class Imbalance Handling** — Uses class weights to manage skewed fraud/legitimate ratios
- **GDPR-Aware Design** — No PII exposure; anonymized data handling with human oversight mechanisms

---

## Tech Stack

| Component | Technology |
|---|---|
| Language | Python |
| Textual Embeddings | `sentence-transformers` (MiniLM-L6-v2 / DistilBERT) |
| Structured Modeling | TabNet Classifier (`pytorch-tabnet`) |
| Similarity & Clustering | Cosine Similarity, Silhouette Score |
| Anomaly Detection | Autoencoder (reconstruction error) |
| Data Processing | `pandas`, `numpy`, `scikit-learn` |
| Visualisation | `matplotlib`, `seaborn` |
| Environment | Google Colab / Jupyter Notebook |

---

## Project Architecture

```
Input Dataset (Upwork Job Postings)
        │
        ├── Textual Pipeline
        │     ├── Text cleaning & normalisation
        │     ├── MiniLM-L6-v2 embeddings
        │     ├── Cosine similarity clustering
        │     └── Silhouette Score evaluation
        │
        ├── Structured Pipeline
        │     ├── Feature imputation & encoding
        │     ├── Autoencoder anomaly detection
        │     ├── Reconstruction error labelling
        │     └── TabNet Classifier (train/test split)
        │
        └── Fusion Layer
              ├── Merge flagged jobs from both models
              ├── Ghost employer network graph
              └── Cluster visualisation & reporting
```

---

## Model Performance

### TabNet Classifier (Structured Features)

| Metric | Legitimate Jobs (0) | Fake Jobs (1) |
|---|---|---|
| Precision | 0.96 | 0.48 |
| Recall | 0.85 | 0.80 |
| F1-Score | 0.90 | 0.60 |
| **Overall Accuracy** | | **0.84** |

### MiniLM Semantic Clustering

| Metric | Score |
|---|---|
| Silhouette Score | 0.5663 |

### Ghost Job Detection Overlap (Venn Analysis)

| Detection Method | Jobs Flagged |
|---|---|
| DistilBERT Clustering only | 464 |
| TabNet only | 1,716 |
| Both models | 16 |

The low overlap confirms that each method captures distinct, complementary fraud signals — reinforcing the value of the hybrid approach.

---

## Dataset

- **Source:** Real-world Upwork job postings (loaded via Google Drive)
- **Key Features Used:**
  - `Job Title`, `Description` — textual inputs for semantic embeddings
  - `Payment_type`, `Client_Country`, `EX_level_demand` — structured metadata
  - `Budget`, `Duration`, `Post Frequency`, `Client History` — behavioural signals

> **Note:** The dataset is not included in this repository. You will need to supply your own Upwork job postings CSV. Update the Google Drive path in the notebook accordingly.

---

## Getting Started

### Prerequisites

```bash
pip install sentence-transformers pytorch-tabnet scikit-learn pandas numpy matplotlib seaborn
```

### Running the Notebook

1. Clone this repository
2. Upload your Upwork job postings CSV to Google Drive
3. Open `Ghost_Job_Network_Detection_Project.ipynb` in Google Colab
4. Update the dataset path in the data loading cell
5. Run all cells sequentially

---

## Results & Visualisations

The notebook produces the following outputs:

- **Payment Type Distribution** — Baseline pattern analysis for anomaly flagging
- **Geographic Distribution** — Top 10 countries by job volume; identifies suspicious regional clusters
- **Experience Level vs Payment Type** — Red flags from ambiguous or entry-level postings
- **Precision-Recall vs Threshold Curve** — Threshold tuning for platform-specific risk tolerance
- **Confusion Matrix** — Classification breakdown for legitimate vs fake jobs
- **Venn Diagram** — Overlap between clustering and TabNet detections
- **Ghost Job Cluster Plot** — Visualisation of confirmed coordinated fake job networks

---

## Ethical Considerations

- No personally identifiable information (PII) is stored or exposed
- Human oversight is recommended before actioning any fraud flag
- Unlabelled data is used to reduce geographic and demographic bias
- The system is designed to balance fraud prevention with fairness to legitimate users, particularly freelancers in developing regions

---

## References

1. Taneja et al., *Fraud-BERT: transformer based context aware online recruitment fraud detection*, Discover Computing, 2025
2. Mahbub & Pardede, *Using Contextual Features for Online Recruitment Fraud Detection*, ISD, 2018
3. Thanh Vo et al., *Dealing with the Class Imbalance Problem in the Detection of Fake Job Descriptions*, CMC, 2021
4. Lal et al., *ORFDetector: Ensemble Learning Based Online Recruitment Fraud Detection*, IC3, 2019
5. Naudé et al., *A machine learning approach to detecting fraudulent job types*, AI & Society, 2022
6. *Detecting Fake Job Postings Using Bidirectional LSTM*, IRJMETS, 2023
7. Fekade, *Detection of Competency Certification Fraud Using Deep Learning*, 2025

---
