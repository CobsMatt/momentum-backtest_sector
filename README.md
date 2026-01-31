# Systematic Momentum Strategy (Python) — Backtest + Memo

A rules-based **cross-sectional momentum** strategy tested on the **top 30 S&P 500 constituents by index weight** (as of current list), with **SPY** as benchmark.

## What’s inside
- `notebooks/momentum_backtest.ipynb` — full analysis + backtest
- `reports/strategy_memo.md` — 1–2 page strategy memo (print-friendly)
- `data/results_monthly.csv` — monthly returns + turnover
- `data/weights_monthly.csv` — monthly portfolio weights
- `figures/light/` — charts for PDF/memo
- `figures/dark/` — optional “codey” dark charts for style

## Strategy (Baseline)
- Signal: **12–1 momentum** (past 12-month return, skipping most recent month)
- Selection: top 10 stocks monthly (ranked by momentum)
- Weighting: equal weight
- Rebalance: monthly
- Costs: 10 bps × monthly turnover (turnover from weight changes)

## Results (Net of Costs, 2021-10 to 2026-01)
Baseline (12–1 momentum, top-10, monthly rebalance; costs = 10 bps × turnover):
- Momentum CAGR: **28.12%** vs SPY **13.27%**
- Sharpe (rf=0): **1.24** vs **0.87**
- Max drawdown: **-20.10%** vs **-23.93%**
- Annualized vol: **21.97%** vs **15.73%**
- Avg monthly turnover: **0.169 (~16.9%)**

## Results Sector Strategy
Risk-free adjusted performance: Sharpe ratios are computed on excess returns using the Fama–French monthly risk-free rate (RF). Over 1999–2025, the sector momentum strategy achieved a higher excess-return Sharpe than SPY (0.514 vs 0.477), with the strongest relative performance during 2000–2010.

Controls & validation:
- Equal-weight Top-30 benchmark: **28.1% vs 27.7% CAGR** (momentum vs EW Top-30)
- FF5 attribution (HAC): **α ≈ 1.04%/month** (t=2.62, p=0.0088), market beta ~**1.09**
- Walk-forward OOS (expanding window, net of costs): **Sharpe ≈ 1.92**
- Vol targeting overlay implemented (20% target, de-risk only; scale capped at 1.0)

Robustness (CAGR):
- 3–1 momentum: **35.48%**
- 6–1 momentum: **33.65%**
- 12–1 momentum: **28.37%**

## Notes / Limitations
- Universe defined using current top constituents (composition effects).
- Sample starts when full data coverage + lookback availability begins.
- Future work: point-in-time constituents, volatility targeting, larger universes, regime filters.

## How to run
1. Create venv + install dependencies:
   ```bash
   py -m venv .venv
   .\.venv\Scripts\Activate.ps1
   py -m pip install -r requirements.txt