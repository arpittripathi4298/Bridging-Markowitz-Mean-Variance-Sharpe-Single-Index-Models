Most portfolios do not fail because of poor asset selection; they fail because of hidden correlation risk. During macro drawdowns, assets assumed to be diversified often move in lockstep, eroding downside protection.

This repository presents a two-stage institutional portfolio optimization study conducted across **1,487 trading days ($\approx 6$ years)** of Indian market data. By sequentially combining **Markowitz Mean-Variance Optimization (MVO)** with the **Sharpe Single Index Model (SIM)**, this project demonstrates how to screen out underperforming assets and re-engineer portfolio weights to maximize risk-adjusted efficiency.

**Headline Result:** Transitioning from pure Markowitz optimization to a combined Markowitz + Single Index Model framework reduced portfolio volatility by **541 bps ($\approx 27\%$)**, capped systematic market exposure at a defensive **$\beta_P = 0.37$**, and boosted the **Sharpe Ratio from 1.03 to 1.25**.

---

## Dataset & Parameters

* **Observation Window:** 1,487 trading days ($\approx 6$ years)
* **Asset Universe:** Hindustan Unilever (HUL), Tata Consultancy Services (TCS), HDFC Bank, Bharti Airtel, and Gold
* **Market Benchmark:** NIFTY-500
* **Risk-Free Rate ($R_f$):** $5.93\%$

---

## Methodology: A Two-Stage Framework

### Stage 1: Markowitz Mean-Variance Optimization (The Asset Screener)
Assets are evaluated based on historical returns, standalone volatility, and the full pairwise variance-covariance matrix to construct the Efficient Frontier. The objective is to maximize the portfolio Sharpe Ratio:

$$\text{Maximize } S_P = \frac{E(R_P) - R_f}{\sigma_P}$$

Subject to full investment and no short-selling constraints:

$$\sum_{i=1}^{n} w_i = 1, \quad w_i \ge 0$$

### Stage 2: Sharpe Single Index Model (The Risk Architect)
Winning assets from Stage 1 are regressed against the NIFTY-500 benchmark to decompose total risk into **systematic (market) risk** and **unsystematic (asset-specific) risk**:

$$R_i = \alpha_i + \beta_i R_m + e_i$$

Where:
* $R_i$ = Return of asset $i$
* $R_m$ = Return of the market index (NIFTY-500)
* $\alpha_i$ = Asset-specific excess return (intercept)
* $\beta_i$ = Sensitivity of asset $i$ to market movements
* $e_i$ = Residual (idiosyncratic) error term

---

## Empirical Results

### 1. Standalone Asset Screening
Prior to optimization, individual asset risk-return profiles revealed clear divergence across the universe:

| Asset | Annualized Return | Annualized Volatility ($\sigma$) | Markowitz Weight |
| :--- | :---: | :---: | :---: |
| **HUL** | $-1.57\%$ | $20.47\%$ | $0.00\%$ |
| **TCS** | $-1.74\%$ | $22.59\%$ | $0.00\%$ |
| **HDFC Bank** | $+2.76\%$ | $21.91\%$ | $0.00\%$ |
| **Bharti Airtel** | $+28.82\%$ | $22.67\%$ | $70.91\%$ |
| **Gold** | $+20.26\%$ | $17.81\%$ | $29.09\%$ |

*Markowitz optimization ruthlessly eliminated legacy underperformers (HUL, TCS, and HDFC Bank) and allocated $100\%$ of capital to Bharti Airtel and Gold.*

### 2. Single Index Regression Diagnostics (vs. NIFTY-500)
Regressing the two surviving assets against the NIFTY-500 exposed the mathematical driver behind their diversification synergy:

| Asset | Expected Return | Market Beta ($\beta$) | $R^2$ | $p$-value | Interpretation |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Bharti Airtel** | $27.91\%$ | $0.75$ | $22.80\%$ | $< 0.001$ | Statistically significant equity growth driver with sub-1.0 market beta. |
| **Gold** | $20.03\%$ | $0.01$ | $0.01\%$ | $0.67$ | Mathematically uncorrelated to the NIFTY-500; true macro hedge. |

### 3. Model Comparison: Markowitz vs. Single Index Model

| Metric | Markowitz MVO | Sharpe Single Index Model | Impact / Delta |
| :--- | :---: | :---: | :---: |
| **Bharti Airtel Weight** | $70.91\%$ | $48.82\%$ | $-22.09\%$ |
| **Gold Weight** | $29.09\%$ | $51.18\%$ | $+22.09\%$ |
| **Expected Annual Return** | $26.33\%$ | $23.88\%$ | $-245\text{ bps}$ |
| **Portfolio Volatility ($\sigma_P$)** | $19.78\%$ | $14.37\%$ | **$-541\text{ bps}$ ($\approx 27\%$ reduction)** |
| **Portfolio Beta ($\beta_P$)** | — | $0.37$ | Defensive systematic exposure |
| **Sharpe Ratio** | $1.03$ | **$1.25$** | **$+0.22$ ($\approx 21\%$ efficiency gain)** |

---

## Key Insights & Strategic Interpretation

1. **Markowitz Chases Return; SIM Engineers Resilience:** Markowitz heavily weighted Bharti Airtel ($70.91\%$) to capture raw upside ($26.33\%$), accepting nearly $20\%$ volatility. The Single Index Model rebalanced to a near $50/50$ split—sacrificing just $2.45\%$ in expected return to cut portfolio volatility by more than a quarter.
2. **The $\beta = 0.01$ Advantage:** With an $R^2$ of $0.01\%$ and $p = 0.67$, Gold is not merely a defensive asset—it is statistically decoupled from Indian equity market movements. Pairing it with a high-alpha, moderate-beta compounder like Airtel creates an asymmetric risk profile.
3. **Alpha Above the Security Market Line (SML):** Both Bharti Airtel and Gold plotted well above the SML, generating substantial positive alpha while keeping systematic market exposure anchored at $\beta_P = 0.37$.
4. **Institutional Takeaway:** Combining both models sequentially solves the classic pitfalls of each. Use **Markowitz** to strip away emotional bias and filter the investable universe, then apply the **Single Index Model** to size positions against macro risk budgets.


*This project is for educational, quantitative research, and portfolio modeling purposes only. Historical performance and statistical parameters do not guarantee future results. Nothing in this repository constitutes financial or investment advice.*
