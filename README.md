# 🕵️ Fraud Detection Case Study – Accredian Internship

Welcome to my fraud detection case study, submitted as part of the **Accredian Data Science Content Specialist Internship**.

This project tackles a real-world scenario where a financial company must detect fraudulent transactions from over 6 million data points. The focus was not only on building a high-performance ML model, but also on communicating insights through storytelling and visuals,
Internship Project — Accredian (via Internshala)

Dataset Size: ~6.3 Million Records | 10 Features
Tools Used: Python, Pandas, Seaborn, Scikit-learn, XGBoost


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

# 📊 Exploratory Data Analysis
## 🧾 Transaction Type vs Fraud Rate
- Fraud occurs predominantly in TRANSFER and CASH_OUT transactions. Other transaction types had zero fraudulent cases.
  ![Screenshot 2025-04-09 165759](https://github.com/user-attachments/assets/1cc91f19-cf4c-4901-b676-e4a4b3687b09)
  
  Insight: Over 0.75% of TRANSFER transactions were fraudulent, followed by around 0.18% in CASH_OUT.

## 💰 Transaction Amount vs Fraud Status
- Fraudulent transactions tend to involve higher median amounts, and have less variance compared to non-fraud ones.
![Screenshot 2025-04-09 165804](https://github.com/user-attachments/assets/8f1a1cda-d486-4233-949c-c9eb83d4e9d5)

Insight: Fraudulent transactions are skewed toward larger amounts, indicating attackers aim for high-value targets.




## ✅ Results

| Metric            | Score     |
|-------------------|-----------|
| AUC-ROC           | **0.9998** |
| Precision (fraud) | **1.00**   |
| Recall (fraud)    | **0.75**   |
| Accuracy          | 1.00      |

---
## Confusion Matrix
  📉 Confusion Matrix Analysis
  To further evaluate model performance, I analyzed the confusion matrix of the final classifier:
  
  Predicted: Not Fraud (0)	Predicted: Fraud (1)
  
  ![Screenshot 2025-04-09 165822](https://github.com/user-attachments/assets/a37fb989-4555-483c-b881-3ba472bb865d)

  
  🎯 Interpretation:
  The model perfectly avoided false positives, meaning no legitimate user was wrongly flagged.
  
  However, 2 fraudulent transactions slipped through, which highlights a need for fine-tuning recall if the objective is minimizing undetected fraud.
  
  Given the class imbalance, this performance is strong for a baseline, especially with zero cost to customer experience via false alarms.



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

📧 [Email](mailto:karthikmuralim68@gmail.com)  
🔗 [LinkedIn](https://linkedin.com/in/m-karthik-murali-3007a6293)  
💻 [GitHub](https://github.com/Krasper707)

---

> *"A great model is not just one that performs well, but one that earns trust through transparency and actionability."*


