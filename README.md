# 🧬 ChEMBL Molecule Protein Classification Using Gradient Boosting Trees


## 📌 Project Overview

This project builds a machine learning pipeline to predict which **disease-related protein** a molecule is most likely to bind to, based on its physicochemical properties. It is a **multi-class classification problem** in the field of **drug discovery and cheminformatics**.

By automating protein target prediction, this model could help pharmaceutical researchers quickly screen thousands of drug candidates without running expensive laboratory experiments.

---

## 🎯 Objective

> Given the physicochemical properties of a molecule, predict whether it binds to **DRD2**, **EGFR**, **HDAC1**, or **BACE1**.

| Protein | Disease Link |
|---------|-------------|
| DRD2 | Parkinson's Disease, Schizophrenia |
| EGFR | Lung Cancer, Breast Cancer |
| HDAC1 | Cancer (Epigenetic Target) |
| BACE1 | Alzheimer's Disease |

---

## 📂 Dataset

- **Source:** [ChEMBL Database](https://www.ebi.ac.uk/chembl/)
- **Samples:** 1,422 molecules
- **Features:** 5 numeric physicochemical properties
- **Target:** Protein class (4 categories)

### Features

| Feature | Description | Drug-like Threshold |
|---------|-------------|-------------------|
| Molecular Weight | Mass/size of molecule | ≤ 500 g/mol |
| LogP | Fat vs water solubility | ≤ 5 |
| HBA | Hydrogen Bond Acceptors | ≤ 10 |
| HBD | Hydrogen Bond Donors | ≤ 5 |
| TPSA | Topological Polar Surface Area | ≤ 140 Ų |

### Class Distribution

```
DRD2     1271  →  89.4%
EGFR       91  →   6.4%
HDAC1      58  →   4.1%
BACE1       2  →   0.1%
```
> ⚠️ Severely imbalanced dataset — addressed using RandomOverSampler

---

## 🛠️ Tech Stack

- **Python 3.8+**
- **Pandas & NumPy** — data manipulation
- **Matplotlib & Seaborn** — data visualization
- **Scikit-Learn** — modelling and evaluation
- **XGBoost / GradientBoostingClassifier** — classification model
- **Imbalanced-Learn** — handling class imbalance

---

## ⚙️ Project Pipeline

```
1. Data Loading & Cleaning       → wrangle() function
2. Exploratory Data Analysis     → distributions, correlations, pairplots
3. Preprocessing                 → LabelEncoder, train/test split (stratified)
4. Handling Class Imbalance      → RandomOverSampler (training data only)
5. Baseline Accuracy             → majority class benchmark (~89%)
6. Model Building                → Pipeline (SimpleImputer + GradientBoosting)
7. Hyperparameter Tuning         → GridSearchCV (cv=5, scoring='f1_weighted')
8. Evaluation                    → Accuracy, Precision, Recall, F1, Confusion Matrix
9. Feature Importance            → Gini importance scores
```

---

## 📊 Results

| Metric | Score |
|--------|-------|
| Baseline Accuracy | 0.8940 |
| Training Accuracy |  |
| Test Accuracy | 0.9400 |
| Weighted F1 Score | 0.9500 |
| Macro F1 Score | 0.6400 |

### Per Class Performance

| Protein | Precision | Recall | F1 Score | Support |
|---------|-----------|--------|----------|---------|
| BACE1 | 0.00 | 0.00 | 0.00 | 1 |
| DRD2 | 0.97 | 0.97 | 0.97 | 249 |
| EGFR | 0.70 | 0.74 | 0.72 | 19 |
| HDAC1 | 0.81 | 0.81 | 0.87 | 16 |

> The model performs excellently on DRD2 and HDAC1, fairly on EGFR, and fails on
> BACE1 due to only 2 training samples being available in the entire dataset.

---


## 🔮 Future Improvements

- Generate **Morgan Fingerprints** from SMILES strings using RDKit for richer molecular features
- Collect more **BACE1 samples** to make that class learnable
- Try **Random Forest** and **LightGBM** as alternative models
- Deploy model as a simple **web app** for researchers to input molecule properties and get predictions

---

## 👤 Author

**Timi Ojumoola**
- GitHub: [@ojumoolatimi](https://github.com/ojumoolatimi)

---


This project is open source and available under the [MIT License](LICENSE).
