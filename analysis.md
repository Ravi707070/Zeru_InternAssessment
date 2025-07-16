# Analysis of Wallet Credit Scores

This document provides insights into the wallet scores computed from historical Aave V2 transaction behavior.

---

##  Score Distribution

The wallet credit scores were bucketed into 10 equal ranges between 0 and 1000:

| Score Range | Wallet Count |
|-------------|---------------|
| 0–100       | 12 wallets    |
| 101–200     | 8 wallets     |
| 201–300     | 21 wallets    |
| 301–400     | 31 wallets    |
| 401–500     | 694 wallets   |
| 501–600     | 92 wallets    |
| 601–700     | 12 wallets    |
| 701–800     | 78 wallets    |
| 801–900     | 2406 wallets  |
| 901–1000    | 0 wallets     |



---

##  Observations

###  Low-Scoring Wallets (0–300):
- Tend to borrow large amounts but repay little to none.
- High liquidation call history.
- Exhibit bot-like or high-risk behavior (e.g., rapid transactions, large borrow spikes without repayment).
- Poor repayment ratio (< 0.5).

###  Mid-Scoring Wallets (400–600):
- Perform both deposits and borrows but inconsistent repayments.
- May have had 1 or 2 liquidations.
- Moderate to decent repayment ratios (0.5 – 0.75).

###  High-Scoring Wallets (700–1000):
- Strong repayment history (repay ratio > 0.9).
- Never got liquidated.
- Regular deposits and stable behavior.
- Indicate healthy participation and responsible usage of the protocol.

---

## Conclusion
The model successfully distinguishes risky from responsible DeFi users based on their Aave V2 behavior. While the majority of users fall into the safe zone, the system highlights critical outliers that could represent financial risks. Future improvements can include incorporating time-series behavior, integrating more DeFi protocols, or combining off-chain indicators (if ever allowed in cross-layer analysis).


---

