# 📊 Exchange Rate Forecasting on a Napkin

> **Official repository for the exchange rate analysis developed for the Macroeconomic Outlook report by the IbMacro student-led league**

[![R](https://img.shields.io/badge/Made_with-R-blue?style=for-the-badge&logo=R)](https://www.r-project.org/)
[![Status](https://img.shields.io/badge/Status-Educational-yellow?style=for-the-badge)]()

This repository contains the R implementation of a forecasting model for the Brazilian nominal exchange rate (BRL/USD), based on the **"Exchange Rate Forecasting on a Napkin"** methodology by Ca' Zorzi and Rubaszek (2020).

# 🎯 Objective

The main objective is to project the **Nominal Exchange Rate (NER)** assuming that the Real Exchange Rate tends to return to its historical mean (Purchasing Power Parity - PPP) over time. The model utilizes a **half-life** approach to estimate the speed of this adjustment.

# 🧠 Methodology

The code implements the following theoretical and empirical steps:

### 1. Data Collection
Automatic data extraction from the **Central Bank of Brazil (BCB)** via the `rbcb` package:
* **Series 11752:** Real Effective Exchange Rate (IPCA).
* **Series 3698:** Nominal Exchange Rate (BRL/USD).

### 2. Deviation Calculation
Definition of equilibrium via a **3-year (36-month) moving average** of the real rate.

### 3. Adaptive Half-Life Model
Unlike the pure static model, this code adjusts the parameter $\rho$ (convergence speed) depending on the forecast horizon ($h$):
* $h \le 3$ months: $\rho = 0.95$ (Faster reversion).
* $3 < h \le 6$ months: $\rho = 0.97$.
* $h > 6$ months: $\rho = 0.981$ (Literature standard, 3-year half-life).

### 4. Benchmarking & Validation
* **Comparison:** Model performance vs. a **Random Walk**.
* **Metrics:** RMSE (Root Mean Square Error).
* **Significance:** **Diebold-Mariano Test (DM Test)** to verify the statistical significance of the difference between forecasts.

## 🛠️ Technologies & Packages

The project was developed in **R**. Key libraries include:

* **Data Collection:** `rbcb`, `quantmod`, `OECD` (via GitHub).
* **Data Manipulation:** `dplyr`, `lubridate`, `zoo`, `timetk`.
* **Modeling & Time Series:** `forecast`, `tseries`, `tvReg`, `dlm`.
* **Visualization:** `ggplot2`, `scales` (with custom color palette).
* **Evaluation:** `Metrics`.

# ✍️ Authors
* **Gabriela Colen**
* **Lauro Aguiar**

# 📄 Reference
Based on the paper:
> Ca' Zorzi, M., & Rubaszek, M. (2020). *Exchange rate forecasting on a napkin*. Journal of International Money and Finance.

---
*This is an academic and educational project developed under IbMacro.*
