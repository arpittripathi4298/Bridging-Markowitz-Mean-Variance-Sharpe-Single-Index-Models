# Portfolio Optimization & Single Index Model (SIM)

This project implements **Markowitz Mean-Variance Portfolio Optimization** and **Sharpe’s Single Index Model (SIM)** in Microsoft Excel using 6 years of daily historical price data (1,487 trading observations from November 2020 to November 2026) across five Indian market assets—**HUL, TCS, HDFC, AIRTEL, and GOLD**—benchmarked against the **NIFTY-500** index.

---

## Workbook Structure
 **`Raw Data`**  Daily closing prices and log returns for HUL, TCS, HDFC, AIRTEL, and GOLD (1,487 observations).
 
 **`Optimal Portfolio`**  Mean-variance optimization (Solver), annualized return/volatility, covariance matrix, Capital Allocation Line (CAL), and allocation chart. 

 **`Single Index Model`**  Excess returns vs. NIFTY-500, asset alphas/betas, systematic vs. unsystematic risk decomposition, Security Market Line (SML), and SIM portfolio metrics. 

 **`Regression Model`**  OLS regression outputs (ANOVA, $R^2$, $t$-stats, $p$-values, and residuals) for AIRTEL and GOLD against NIFTY-500. |

---

## 1. Asset Summary & Optimal Portfolio (Markowitz)

Using a **Risk-Free Rate ($R_f$) of 5.934%** (annual), Excel Solver maximizes the Sharpe Ratio under long-only constraints ($0 \le w_i \le 1, \sum w_i = 1$). The optimizer allocates capital exclusively to **AIRTEL** and **GOLD**, eliminating underperforming equities.

| Security | Annual Return | Annual Std. Dev. | Optimum Weight |
| :--- | :---: | :---: | :---: |
| **HUL** | -1.57% | 20.47% | 0.00% |
| **TCS** | -1.74% | 22.58% | 0.00% |
| **HDFC** | 2.76% | 21.91% | 0.00% |
| **AIRTEL** | 28.82% | 22.67% | **49.69%** |
| **GOLD** | 20.26% | 17.81% | **50.31%** |

### Optimal Portfolio Metrics
* **Expected Annual Return:** `24.51%`
* **Annualized Standard Deviation:** `14.42%`
* **Risk-Free Rate:** `5.93%`
* **Sharpe Ratio:** `1.29`

### Capital Allocation Line (CAL)

| Risky Portfolio Weight | Expected Return | Standard Deviation |
| :---: | :---: | :---: |
| 0.0 | 5.93% | 0.00% |
| 0.5 | 15.22% | 7.21% |
| 1.0 | 24.51% | 14.42% |
| 2.0 | 43.09% | 28.83% |

---

## 2. Single Index Model (SIM) Output

The two-asset optimal portfolio (**AIRTEL** & **GOLD**) is evaluated against the **NIFTY-500** market index using excess returns:

$$R_i - R_f = \alpha_i + \beta_i (R_M - R_f) + e_i$$

### Asset & Portfolio Parameters

| Metric | AIRTEL | GOLD | SIM Portfolio |
| :--- | :---: | :---: | :---: |
| **Portfolio Weight ($W$)** | 48.82% | 51.18% | 100.00% |
| **Daily Alpha ($\alpha$)** | 0.000623 | 0.000627 | — |
| **Beta ($\beta$)** | 0.7456 | 0.0136 | **0.3710** |
| **Expected Annual Return** | 27.91% | 20.03% | **23.88%** |
| **Residual Variance ($\sigma_e^2$, Daily)** | 0.000158 | 0.000125 | — |

### SIM Portfolio Summary
* **Market Annualized Risk Premium (NIFTY-500):** `10.89%`
* **Market Daily Variance ($\sigma_M^2$):** `0.000084` (Annual Variance: `2.12%`)
* **Portfolio Daily Variance ($\sigma_P^2$):** `0.000082`
* **Portfolio Annualized Std. Dev. ($\sigma_P$):** `14.37%`
* **Portfolio Sharpe Ratio:** `1.25`

---

## 3. OLS Regression Summary (vs. NIFTY-500)

| Regression Statistic | AIRTEL | GOLD |
| :--- | :---: | :---: |
| **Observations ($N$)** | 1,487 | 1,487 |
| **Multiple $R$** | 0.4774 | 0.0111 |
| **$R^2$** | 0.2279 | 0.0001 |
| **Adjusted $R^2$** | 0.2274 | -0.0005 |
| **Standard Error** | 0.0126 | 0.0112 |
| **Beta (NIFTY-500 Coefficient)** | 0.7456 ($t = 20.94, p < 0.001$) | 0.0136 ($t = 0.43, p = 0.668$) |
| **F-Statistic** | 438.35 ($p < 0.001$) | 0.18 ($p = 0.668$) |

---

## Key Insights
* **Strong Diversification Benefit:** GOLD exhibits a near-zero beta ($\beta = 0.0136, R^2 = 0.0001$) relative to the NIFTY-500, acting as an effective hedge against equity market movements.
* **Risk-Adjusted Performance:** Combining AIRTEL (high growth, $\beta = 0.75$) with GOLD (uncorrelated defensive asset) reduces portfolio volatility to **14.37%–14.42%**, lower than either asset individually, while delivering a **Sharpe Ratio of 1.25–1.29**.
* **Model Consistency:** The Markowitz full-covariance model (`24.51%` return, `14.42%` risk) and the Single Index Model (`23.88%` return, `14.37%` risk) produce closely aligned risk-return profiles.

---

## Tools Used
* **Microsoft Excel** (Solver, Analysis ToolPak for OLS Regression, Dynamic Formulas & Charts)
