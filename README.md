# Aave V2 Wallet Credit Scoring System

##  Overview

This project aims to assign **credit scores (0–1000)** to wallets interacting with the Aave V2 DeFi protocol based on historical on-chain behavior. The goal is to detect **responsible, risk-averse users** versus **exploitative, bot-like, or risky actors**, using only transaction-level data.

---

##  Methodology

We process transaction-level logs (e.g., `deposit`, `borrow`, `repay`, `redeemUnderlying`, `liquidationCall`) and aggregate behavior by wallet. A machine learning model is trained on these features to predict a normalized credit score between 0 and 1000.

---

## Architecture

        ┌────────────┐
        │ JSON Input │
        └─────┬──────┘
              │
   ┌──────────▼──────────┐
   │ Data Preprocessing  │
   │ - Normalize amounts │
   │ - Parse timestamps  │
   └──────────┬──────────┘
              │
 ┌────────────▼────────────┐
 │ Feature Engineering     │
 │ - Borrow/Repay ratio    │
 │ - Txn counts/types      │
 │ - Liquidation history   │
 └────────────┬────────────┘
              │
      ┌───────▼────────┐
      │ ML Model (RF)  │
      │ - Trained on   │
      │   engineered   │
      │   behavior     │
      └───────┬────────┘
              │
     ┌────────▼─────────┐
     │ Scoring Script   │
     │ - Score wallets  │
     │   0–1000 range   │
     └──────────────────┘

---

##  Features Engineered

- Total transaction count
- Borrow count, total amount borrowed
- Repay count, total amount repaid
- Borrow-to-repay ratio
- Liquidation count
- Average borrow duration
- Time since last activity
- Unique asset interactions
- Redeem vs deposit ratio

---

##  Usage

### 1. Train and Score
Use the one-step scoring script:

```bash
python wallet_score_generator.py --input sample_data.json --output scores.json
```

## Analysis
- See analysis.md for:
- Score distribution
- Behavioral breakdown by score range
- Anomalies and patterns in user interactions
---

## Authors
D Ravi Kiran

---
## License
This project is licensed under the MIT License.
---
