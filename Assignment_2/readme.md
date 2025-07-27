# Wallet Scoring – Round 2 Assignment

This project evaluates the risk profile of 100 Ethereum wallets based on their activity with the Compound V2/V3 lending protocol.

---

## Project Structure
├── Wallet id.xlsx # Input wallet list
├── wallet_risk_scores.csv # Final output with risk scores
├── wallet_scoring.ipynb # Main implementation notebook
├── .venv/ # Python virtual environment
└── README.md # This file

---

##  Problem Statement

Given a list of Ethereum wallet addresses, the goal is to:
1. Fetch on-chain transaction history from the Compound protocol.
2. Engineer features that capture risk behavior.
3. Generate a risk score between **0 and 1000** for each wallet.

---

##  How I Executed

1. **Set up a virtual environment**:
    ```bash
    python -m venv .venv
    source .venv/bin/activate  # or .venv\\Scripts\\activate (on Windows)
    pip install -r requirements.txt
    ```

2. **Launch the Jupyter Notebook**:
    ```bash
    jupyter notebook
    ```

3. **Run the notebook (`wallet_scoring.ipynb`)** to:
    - Load wallet data from Excel
    - Simulate or fetch on-chain data
    - Engineer features
    - Normalize features
    - Calculate risk score using a weighted formula
    - Export `wallet_risk_scores.csv`

---

##  Explanation of Risk Scoring Methodology

### 1. **Data Collection Method**
We simulated wallet activity based on realistic lending protocol behavior. This included total borrows, supplies, liquidation history, health factor, and activity recency. In production, this would be replaced by real data via:
- **Covalent**, **Alchemy**, **Flipside**, or **Dune**

### 2. **Feature Selection Rationale**
| Feature | Why It's Useful |
|--------|-----------------|
| `total_borrows` | Indicates leverage exposure |
| `total_supplies` | More collateral = more safety |
| `liquidation_count` | Direct risk signal |
| `health_factor_avg` | Proximity to liquidation |
| `recent_activity_days` | Dormancy = less oversight |
| `collateral_ratio` | Higher = safer |

### 3. **Scoring Method**
Features are normalized (MinMaxScaler), then combined:

```python
score = (
    0.2 × (1 - liquidation_count) +
    0.25 × health_factor_avg +
    0.15 × (1 - recent_activity_days) +
    0.2 × collateral_ratio +
    0.1 × total_supplies +
    0.1 × (1 - total_borrows)
) × 1000
```
Higher = safer wallet, Lower = risky behavior.

4. Justification of Risk Indicators
Chosen to be DeFi-native, interpretable, and scalable

Align with risk criteria used by Aave/Compound in liquidation logic

Output Sample
wallet_id	    score
0xabc...123	   732
0xdef...456	   598

