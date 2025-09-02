# 🕵️ Fraud Detection System (Rule-Based + Machine Learning)

## 📌 Project Overview
This project explores fraud detection using a **hybrid approach** that combines:
- **Rule-based detection** (domain-driven rules)
- **Machine Learning** (Isolation Forest for anomaly detection)

The goal is to flag suspicious transactions by analyzing transaction behavior and identifying anomalies in financial data.

---

## 📂 Dataset
The dataset is synthetic and contains banking transaction records with features such as:

- `TransactionAmount` – transaction value  
- `LoginAttempts` – number of login attempts before a transaction  
- `AmountToBalanceRatio` – ratio of transaction amount to account balance  
- `AccountsPerDevice` – accounts linked to the same device  
- `AccountsPerIP` – accounts linked to the same IP  
- `TransactionHour` – hour of transaction  
- `TimeSinceLastTransaction` – time between transactions  
- `AccountBalance` – balance of the account  

---

## ⚙️ Workflow
### 1. Data Preprocessing
- Filled missing values  
- Scaled features using **StandardScaler**  
- Created engineered features like `AmountToBalanceRatio`, `SuspiciousFlags`, and `SuspiciousScore`

### 2. Rule-Based Detection
Custom rules were applied to detect suspicious activity, e.g.:
- Large transaction relative to account balance  
- High number of login attempts  
- Multiple accounts per device/IP  
- Transactions during unusual hours (before 6 AM or after 10 PM)  
- Very short gaps between transactions  

### 3. Machine Learning (Isolation Forest)
- Trained an **Isolation Forest** model with contamination rate `0.02`  
- Predicted anomalies as fraud candidates  

### 4. Hybrid Approach
Final fraud prediction was derived by combining rules and ML output:

```python
df['FinalFraudPrediction'] = (
    (df['SuspiciousScore'] > 0) | (df['IsFraudPredicted'] == 1)
).astype(int)
Results
