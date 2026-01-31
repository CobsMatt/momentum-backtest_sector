# Sector Momentum Rotation (GICS Sector ETF Strategy)

This project implements and evaluates a rules-based **sector rotation** strategy using long-lived **Select Sector SPDR ETFs**. The goal is to test momentum as a **macro allocation tool** (asset allocation across sectors) rather than stock picking.

## Universe (Point-in-Time Investable)
To avoid survivorship and look-ahead bias from selecting “today’s winners,” the universe is a fixed set of highly liquid sector ETFs with long histories:

- XLB (Materials), XLE (Energy), XLF (Financials), XLI (Industrials), XLK (Technology),
  XLP (Consumer Staples), XLU (Utilities), XLV (Health Care), XLY (Consumer Discretionary)
- Benchmark: SPY

## Strategy Overview
At each month-end:
1. Convert daily prices to **month-end prices**.
2. Compute **12–1 momentum** for each sector ETF (12-month total return, skipping the most recent month to reduce short-term reversal effects).
3. Rank sectors by momentum and hold the **top 3 sectors**, equally weighted.
4. Rebalance monthly.

### Transaction Costs
Strategy performance is reported **net of costs**, modeled as:
- **cost = turnover × 10 bps**, where turnover is the one-way change in portfolio weights.

### Risk Management (Volatility Targeting)
A volatility targeting overlay is applied to maintain a stable risk budget:
- Target volatility: **20% annualized**
- Vol estimate: **12-month rolling volatility of monthly returns**
- **Lagged scaling** (scale used for month *t* is estimated from data available through month *t–1*) to avoid lookahead.
- **De-risk only** (scaling capped at 1.0; no leverage).

## Evaluation Framework
The strategy is evaluated across multiple market regimes to reduce “cherry-picking”:

- **Full Period:** 1999–2026  
- **Sub-Period 1:** 2000–2010 (“Lost Decade”)  
- **Sub-Period 2:** 2011–2026 (“Post-GFC Bull”)

Metrics reported include CAGR, volatility, max drawdown, turnover, and Sharpe ratios.
Sharpe is also computed on an **excess-return basis** using the **Fama–French monthly risk-free rate (RF)**.

## Key Results (High Level)
- Over the **full sample**, the strategy is comparable to SPY with improved drawdown behavior.
- The strategy’s **strongest relative performance occurs during 2000–2010**, consistent with sector rotation helping in choppy/sideways equity regimes.
- During the **post-2011 bull market**, SPY tends to lead, consistent with broad equity beta dominating in extended bull trends.

See saved figures for regime equity curves and the “Lost Decade” comparison.

## Factor Attribution (FF5 + MOM)
To understand what drives returns (and avoid mistaking unintended exposures for “alpha”), monthly excess returns are regressed on:
- Fama–French 5 factors (Mkt-RF, SMB, HML, RMW, CMA)
- **Momentum (MOM)** factor
- HAC (Newey–West) standard errors

Results indicate the strategy has meaningful exposure to **market beta** and a statistically significant loading on **momentum**, consistent with its construction. The intercept (alpha) is not statistically significant after controlling for these factors, which supports an interpretation of the strategy as systematic factor-driven sector rotation rather than unexplained alpha.

## Outputs
- Figures (light/dark): `figures/`
- Saved charts include regime equity curves and a “Lost Decade” comparison chart.

## Notes / Limitations
- Sector definitions evolve over time; this implementation uses the long-lived Select Sector SPDR ETF baskets for consistency across 1999–2026.
- Results are sensitive to universe, rebalance frequency, and transaction cost assumptions.
