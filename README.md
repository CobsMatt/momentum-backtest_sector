# Macro-Aware Sector Rotation Strategy (2001–2026)

### **Executive Summary**
This project implements a systematic **US Sector Rotation Strategy** designed to outperform the S&P 500 on a risk-adjusted basis. By combining **Cross-Sectional Momentum** with a **Macro-Economic Risk Overlay**, the strategy captures upside trends while mechanically reducing exposure during recessionary regimes.

**Key Performance Highlights (Feb 2001 – Jan 2026):**
* **Superior Efficiency:** Achieved a **Sharpe Ratio of 0.63**, outperforming the S&P 500 (0.61).
* **Capital Preservation:** Reduced the Max Drawdown to **-33.4%**, providing a significant safety buffer compared to the S&P 500's **-50.8%** crash.
* **Crisis Alpha:** Successfully identified and defended against the 2001 Dot-Com crash and the 2008 Great Financial Crisis.

---

### **Strategy Performance**

| Metric | Base Strategy (Momentum) | **Macro Overlay (Risk-Managed)** | S&P 500 (SPY) |
| :--- | :--- | :--- | :--- |
| **Ann. Return (CAGR)** | 8.96% | 8.13% | 9.10% |
| **Ann. Volatility** | 14.48% | **12.92%** | 14.92% |
| **Sharpe Ratio** | 0.619 | **0.630** | 0.610 |
| **Max Drawdown** | -39.06% | **-33.43%** | -50.78% |

> *Note: Benchmarked against SPY (S&P 500 Total Return) to account for dividend reinvestment.*

---

### **Methodology**

#### **1. The Core Engine: Sector Momentum**
* **Universe:** The 9 Select Sector SPDR ETFs (XLB, XLE, XLF, XLI, XLK, XLP, XLU, XLV, XLY).
* **Signal:** 12-Month Momentum (lagged 1 month to prevent look-ahead bias).
* **Selection:** Long the **Top 3** sectors, Equal-Weighted.
* **Rebalancing:** Monthly.
* **Friction:** Transaction costs modeled at **10 bps** per turn.

#### **2. The Risk Engine: Macro Overlay**
To solve the "drawdown problem" of pure momentum, I engineered a dynamic risk overlay:
* **Regime Detection:** Uses Leading Economic Indicators (LEI) to classify the market state.
* **Dynamic Volatility Targeting:**
    * **Growth Regime:** Target **15% Volatility** (Aggressive).
    * **Stress Regime:** Target **10% Volatility** (Defensive).
* **Execution:** Mechanically scales exposure down (shifting to Cash/Treasuries) when realized volatility exceeds the target.

---

### **Why It Matters**
While the S&P 500 delivered a higher raw total return (+777% vs +748%) driven largely by the hyper-concentration of Mega-Cap Tech in the 2020s, the Macro Overlay strategy proved superior in **capital preservation**. 

By trading "junk volatility" for stability, the strategy offers a smoother equity curve, making it a viable alternative for risk-averse investors or a candidate for institutional leverage.

---

### **Tech Stack**
* **Python:** Core logic and backtesting engine.
* **Pandas/NumPy:** Vectorized data manipulation and signal generation.
* **Statsmodels:** Used for Factor Regression (Fama-French 3-Factor analysis).
* **Matplotlib:** Visualization of equity curves and underwater plots.

---

### **Files in this Repository**
* `sector_momentum_main.ipynb`: The complete backtesting code.
* `figures_sector/`: Generated charts (Equity Curves, Drawdown Profiles).
* `reports_sector/`: Raw CSV outputs of monthly returns and statistics.





