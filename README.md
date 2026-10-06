# Macro Regime-Switching Asset Allocation Engine

![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Status](https://img.shields.io/badge/Status-Completed-success.svg)

An econometric quantitative finance pipeline that applies a **2-State Markov-Switching Autoregressive Model** to dynamically allocate assets across Equities (S&P 500), Fixed Income (10-Year Treasuries), and Gold. The framework utilizes macroeconomic factors—specifically the **10Y-2Y Treasury Yield Curve Spread**—to estimate real-time regime transition probabilities and hedge portfolio tail-risk during market contractions.

---

## Key Features

* **Macro Data Integration:** Automated data ingestion from Yahoo Finance and Federal Reserve Economic Data (FRED).
* **Econometric Diagnostics:** Augmented Dickey-Fuller (ADF) stationarity testing to validate time-series inputs.
* **Non-Linear Regime Identification:** Unsupervised separation of market regimes into Low-Volatility (Expansion) and High-Volatility (Contraction) states.
* **Hysteresis-Stabilized Rebalancing:** Dual-threshold probability switching (`0.65` / `0.35`) and rolling-window probability smoothing to eliminate high-frequency whipsawing.
* **Realistic Friction Backtesting:** Incorporates turnover-based transaction cost penalties (15 bps) to deliver true net-of-cost performance metrics.

---

## Strategy & Asset Allocation Model

The dynamic allocation engine shifts between two core asset regimes based on the smoothed probability $P(S_t = \text{High Risk})$:

| Market Regime | State Condition | Equity ($^GSPC) | Bonds (TLT) | Gold (GLD) |
| :--- | :--- | :---: | :---: | :---: |
| **Growth / Expansion** | $P(\text{High Risk}) \le 0.35$ | **70%** | 20% | 10% |
| **Defensive / Contraction** | $P(\text{High Risk}) \ge 0.65$ | **20%** | 50% | 30% |

---

## Repository Structure

```text
macro-regime-allocation/
│
├── data/
│   └── Macro_Regime_Portfolio_Results.xlsx   # Exported performance & allocation tables
├── plots/
│   └── macro_regime_dashboard.png            # Visual dashboard
├── macro_regime_pipeline.ipynb               # Full Jupyter / Colab Notebook
├── requirements.txt                          # Python dependencies
├── LICENSE                                   # MIT License
└── README.md                                 # Documentation
