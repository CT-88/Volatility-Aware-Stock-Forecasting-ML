# Stock Price Forecasting Under Volatility  
### A Comparative Machine Learning Study Using Python

## ⚙️ Tools & Technologies
- **Programming:** Python
- **Data Analysis:** pandas, numpy
- **Visualization:** matplotlib, seaborn
- **Machine Learning:** scikit-learn, XGBoost
- **Environment Management:** UV
- **Version Control:** Git & GitHub

## 📋 Overview
This project investigates how **stock volatility** and **forecasting horizon** affect the performance of different machine learning models in stock price prediction.

Building on prior academic research, the study compares **tree-based ensemble models** and **regularized linear models** when forecasting stocks with distinct volatility characteristics:

- **Apple (AAPL)** — aggressive, high volatility  
- **Procter & Gamble (PG)** — defensive, low volatility  

Each stock is evaluated over two time horizons:
- **5-year period (2019–2023)**
- **10-year period (2014–2023)**

The goal is to determine **when model complexity improves forecasting accuracy and when it leads to overfitting** in non-stationary financial data.

## 🎯 Research Questions
- How does **market volatility** influence machine learning forecast accuracy?
- Do complex models outperform simpler ones in financial time series?
- How does model performance change across **short vs long horizons**?
- Which models generalize best under **structural market change**?

## 🤖 Models Implemented
- **Random Forest**
- **XGBoost**
- **LASSO Regression**
- **Elastic Net Regression**

## 📊 Data Collection & Volatility Classification
Historical daily closing prices were collected using the **Yahoo Finance API** (via `yfinance`). The S&P 500 index served as a market benchmark.

To objectively classify stock risk profiles, two financial risk measures were calculated:

### Annualized Volatility (σ)
Measures total price dispersion based on daily log returns:
\[
\sigma = \text{sd} \times \sqrt{252}
\]
Where:
- sd = standard deviation of daily log returns
- 252 = approximate trading days per year

### Beta Coefficient (β) — Relative to S&P 500
Measures sensitivity to market movements:
\[
\beta_i = \frac{\text{Cov}(R_i, R_m)}{\text{Var}(R_m)}
\]

### Volatility Summary
| Stock | Annualized Volatility (σ) | Beta (β) | Classification |
|-------|---------------------------|----------|----------------|
| AAPL  | 28.38% | 1.1904 | **Aggressive / Volatile** |
| PG    | 18.23% | 0.5756 | **Defensive / Stable** |

Both absolute (σ) and market-relative (β) risk measures consistently justify the volatility classification.

## 🔧 Feature Engineering
- Lagged prices (1, 2, 3 days)
- Rolling means and rolling standard deviations (5-day, 10-day)
- Percentage price changes
- All features standardized using `StandardScaler`

## 📈 Evaluation Metrics
- **Mean Absolute Error (MAE)**
- **Root Mean Square Error (RMSE)**
- **Mean Absolute Percentage Error (MAPE)**
- **R² Score**

## 📊 Results & Visual Analysis

### 5-Year Forecast (2019–2023)
- **Apple (AAPL)**: LASSO achieved the lowest error and highest R² (~0.97). Elastic Net performed similarly. Tree-based models struggled with volatility spikes.
- **Procter & Gamble (PG)**: All models performed well. Lower volatility reduced forecasting noise. LASSO remained most consistent.

### 10-Year Forecast (2014–2023)
- **Apple (AAPL)**: Random Forest and XGBoost exhibited negative R², showing severe overfitting and poor generalization. Regularized linear models remained stable.
- **Procter & Gamble (PG)**: Similar degradation in tree-based models. LASSO and Elastic Net maintained strong explanatory power.

## 🔑 Key Findings
1. **Forecasting accuracy decreases as volatility increases**
2. **Tree-based models are highly sensitive to time horizon**
3. **Regularization improves robustness in non-stationary data**
4. **Model simplicity outperformed complexity in most scenarios**

## 💡 Practical Implications
- Model selection must align with asset risk profile
- Long-term forecasting requires strong regularization
- Complexity should be justified, not assumed

## 🛠️ Environment & Reproducibility
This project uses **UV** for dependency and environment management.

- Python version defined in `.python-version`
- Dependencies locked via `pyproject.toml` and `uv.lock`

To reproduce the environment:
```bash
uv sync
```

## 🧩 Repository Structure
```text
├── data/
│   ├── raw_data.csv
│   ├── five_year_data.csv
│   └── ten_year_data.csv
│
├── notebook/
│   ├── initial_data_processing.ipynb
│   └── empirical_research_analysis.ipynb
│
├── report/
│   ├── figure/
│   │   ├── aapl_5_year_period.png
│   │   ├── aapl_10_year_period.png
│   │   ├── pg_5_year_period.png
│   │   └── pg_10_year_period.png
│   └── findings.md
│
├── .gitignore
├── .python-version
├── pyproject.toml
├── uv.lock
└── README.md
```