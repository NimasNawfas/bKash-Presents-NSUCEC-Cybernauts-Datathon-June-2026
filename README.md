<div align="center">

# 🏦 FictiPay Customer Churn Prediction
### **bKash Presents NSUCEC Cybernauts Datathon 2026**

[![Python](https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![LightGBM](https://img.shields.io/badge/Model-LightGBM-green?style=for-the-badge)](https://lightgbm.readthedocs.io/)
[![AUC-ROC](https://img.shields.io/badge/AUC--ROC-0.98408-brightgreen?style=for-the-badge)](https://kaggle.com)
[![Rank](https://img.shields.io/badge/Rank-165%2F207-orange?style=for-the-badge)](https://kaggle.com)
[![Platform](https://img.shields.io/badge/Platform-Kaggle-20BEFF?style=for-the-badge&logo=kaggle&logoColor=white)](https://kaggle.com)

</div>

---

## 🏆 Performance Overview

| Metric | Value |
| :--- | :--- |
| **AUC-ROC Score** | `0.98408` |
| **Competition Rank** | **165 / 207** teams |
| **Event** | bKash Presents NSUCEC Cybernauts Datathon 2026 |
| **Host** | NSU Computer and Engineering Club (NSUCEC) |
| **Platform** | Kaggle |

---

## 📌 Problem Statement

Tasked with building an end-to-end customer churn prediction pipeline for **FictiPay**, a synthetic mobile wallet provider operating in Emergingland. The objective is a binary classification task to determine whether a customer will churn (`1`) or remain active (`0`).

---

## 📂 Dataset Overview

| Table | Description | Scale |
| :--- | :--- | :--- |
| `transactions/` | Payment history (P2P, BillPay, CashIn, etc.) | 200M+ rows |
| `kyc.parquet` | Customer profiles (region, gender, account type) | ~1M rows |
| `dayend_balance/` | Daily balance snapshots per customer | ~360M rows |
| `train_labels.csv` | Labeled churn training data (~12.7% churn rate) | 595,000 rows |
| `test.csv` | Unlabeled target accounts for prediction | 255,000 rows |

---

## 🧠 Feature Engineering

Engineered **15+ behavioral and temporal features** across sliding windows (7, 30, and 90 days):

* **Transaction Metrics:** Frequency counts (`trx_count`), total volumes (`trx_sum`), mean sizes (`trx_std`), recency days, and transaction-type ratios (BillPay, CashIn, P2P).
* **Balance Metrics:** Mean balance, volatility (`bal_std`), extremes (`min`/`max`), zero-balance ratios, and 30-day trend shifts.
* **Demographic & Profile:** Account age in days, one-hot encoded regions, and gender segmentation.

---

## 🏗️ Pipeline Architecture

```mermaid
graph TD
    A[Raw Data: 200M+ Rows] -->|Dask Filtering| B[Account Subset Extraction]
    B --> C[Feature Engineering]
    C -->|Sliding Windows| D[Feature Matrix: 595K Train / 255K Test]
    D --> E[LightGBM Classifier]
    E -->|Optimized via Optuna| F[Churn Probability Scores]
    F --> G[Final Submission: predictions.csv]
