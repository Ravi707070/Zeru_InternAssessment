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
        └────────────┘

        ┌────────────────────┐
        │ Clean & Prepare    │
        │ - Normalize data   │
        │ - Format time      │
        └────────────────────┘

        ┌────────────────────┐
        │ Create Features    │
        │ - Ratios, counts   │
        │ - History flags    │
        └────────────────────┘

        ┌────────────────────┐
        │ Train ML Model     │
        │ - Random Forest    │
        └────────────────────┘

        ┌────────────────────┐
        │ Score Wallets      │
        │ - Range: 0–1000    │
        └────────────────────┘


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
python avee-credit.ipynb --input user-wallet-transcations.json --output wallet_scores.csv
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
