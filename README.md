# 🕵️ Fraud Detection Case Study – Accredian Internship

Welcome to my fraud detection case study, submitted as part of the **Accredian Data Science Content Specialist Internship**.

This project tackles a real-world scenario where a financial company must detect fraudulent transactions from over 6 million data points. The focus was not only on building a high-performance ML model, but also on communicating insights through storytelling and visuals,

---

## 📌 Problem Statement

A financial services firm is facing frequent fraudulent transactions where agents gain control of user accounts and attempt to empty them through transfers and cashouts. The task is to:

- Predict whether a given transaction is fraudulent
- Interpret the model’s decisions
- Translate results into business-focused insights

---

## 🧠 Objectives

- Build a fraud detection model using machine learning
- Handle extreme class imbalance (fraud < 0.1%)
- Improve recall without compromising precision
- Communicate actionable business recommendations

---

## 📊 Dataset Overview

- 📦 6,362,620 rows | 10 columns
- ⏱️ Each `step` = 1 hour (30 days total)
- 🏷️ Key columns: `type`, `amount`, `oldbalanceOrg`, `newbalanceOrig`, `nameDest`, `isFraud`
- 🔍 Fraud is **only present** in `TRANSFER` and `CASH_OUT` transactions

---

## 🧪 Process Overview

### 1. 📖 Data Exploration
- Uncovered fraud only happens in 2 types: `TRANSFER` and `CASH_OUT`
- Fraudsters often leave no change in destination balance
- Many transactions had balance inconsistencies → engineered `errorOrig`, `errorDest`

### 2. 🛠 Feature Engineering
- `errorOrig`, `errorDest` to capture mismatch in balances
- `sender_txn_count`, `receiver_txn_count` to detect mule behavior
- `step_gap` to capture bot-like rapid fire transactions
- Flags like `isToMerchant`, `isLargeAmount`

### 3. ⚖️ Imbalance Handling
- Applied **SMOTE** to oversample fraud cases during training
- Trained a **Random Forest Classifier** with class balancing

### 4. 🔍 Threshold Tuning
- Default threshold (0.5) → recall: 0.50
- Tuned threshold to 0.3 → recall: **0.75**, precision: **1.00**

---

## ✅ Results

| Metric            | Score     |
|-------------------|-----------|
| AUC-ROC           | **0.9998** |
| Precision (fraud) | **1.00**   |
| Recall (fraud)    | **0.75**   |
| Accuracy          | 1.00      |

---

## 📌 Business Recommendations

- Flag transactions where:
  - `TRANSFER` or `CASH_OUT` occurs
  - Amount > ₹200,000
  - Origin balance drops to zero but no destination balance change
- Implement a **real-time fraud probability score** in your system
- Route high-risk transactions for **manual review** before processing
- Build a dashboard with SHAP explainability for internal auditors

---

## 🧠 Learnings

- Deepened my understanding of how **class imbalance** affects model performance
- Learned how to **tune probability thresholds** for real-world cost-sensitive applications
- Practiced communicating technical ML results to **non-technical stakeholders**
---

## 🔗 Connect With Me

📧 [karthikmuralim68@gmail.com](mailto:karthikmuralim68@gmail.com)  
🔗 [LinkedIn](https://linkedin.com/in/m-karthik-murali-3007a6293)  
💻 [GitHub](https://github.com/Krasper707)

---

> *"A great model is not just one that performs well, but one that earns trust through transparency and actionability."*


