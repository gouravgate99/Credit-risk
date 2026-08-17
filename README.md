# Credit Loss Analytics: From Default Risk to Portfolio ECL

## Overview
This project implements an **end-to-end credit risk analytics pipeline** using the **Lending Club loan dataset** to estimate **Expected Credit Loss (ECL)** through the **PD–LGD–EAD framework**.

The project closely mirrors **real-world banking and NBFC credit risk workflows**, emphasizing **interpretability, stability, and portfolio monitoring** rather than black-box modeling.

---

## Dataset Description (Lending Club)

### Source
**Lending Club** is a peer-to-peer lending platform that provides publicly available, loan-level data covering borrower characteristics, loan attributes, repayment behavior, and default outcomes.

### Dataset Characteristics
- **Loan Type:** Unsecured personal loans
- **Granularity:** Loan-level observations
- **Time Horizon:** Multi-year origination and performance data
- **Target Variable:** Loan default indicator

### Key Feature Categories
- **Borrower Profile:**  
  Annual income, employment length, home ownership
- **Loan Characteristics:**  
  Loan amount, interest rate, term, installment
- **Credit History:**  
  Delinquencies, credit utilization, credit age
- **Behavioral Variables:**  
  Payment history, outstanding principal, recoveries

The dataset is widely used in **credit risk research and industry benchmarking**, making it suitable for PD, LGD, and EAD modeling.

---

## Business Objective
- Estimate borrower **default risk**
- Quantify **expected credit losses**
- Enable **portfolio-level loss forecasting**
- Demonstrate **industry-aligned credit risk modeling practices**
- Monitor model stability and data drift over time

---

## End-to-End Project Flow
1. Raw Lending Club data ingestion  
2. Data cleaning and missing value treatment  
3. Feature binning and transformation  
4. Weight of Evidence (WoE) & Information Value (IV) analysis  
5. Probability of Default (PD) model development  
6. Loss Given Default (LGD) modeling  
7. Exposure at Default (EAD) estimation  
8. Expected Credit Loss (ECL) calculation  
9. Model validation and performance evaluation  
10. Portfolio monitoring and drift detection  

---

## Feature Engineering

### Weight of Evidence (WoE)
Categorical variables and binned numerical variables are encoded using WoE to ensure interpretability and monotonic risk behavior.

$$WoE = \ln\left(\frac{\% \text{Good Loans}}{\% \text{Bad Loans}}\right)$$


**Why WoE?**
- Linear relationship with log-odds
- Interpretable coefficients
- Widely accepted in regulated credit risk modeling

---

### Information Value (IV)
Used to assess predictive power and guide feature selection.

$$IV = \sum (\%Good - \%Bad) \times WoE$$

| IV Range | Predictive Strength |
|--------|---------------------|
| < 0.02 | Weak |
| 0.02 – 0.10 | Medium |
| 0.10 – 0.30 | Strong |
| > 0.30 | Very Strong |

---

## Probability of Default (PD) Model
- **Model:** Logistic Regression
- **Input:** WoE-transformed features
- **Output:** Probability of loan default

$$PD = \frac{1}{1 + e^{-(\beta_0 + \beta_1x_1 + \dots + \beta_nx_n)}}$$

### Evaluation Metrics
- ROC-AUC
- KS Statistic
- Gini Coefficient
- Confusion Matrix
- Calibration assessment

---

## Loss Given Default (LGD)
LGD represents the proportion of exposure that is not recovered after a borrower defaults.

$$LGD = 1 - \frac{\text{Total Recoveries}}{\text{Exposure at Default}}$$

Modeled using post-default recovery information available in the Lending Club dataset.

---

## Exposure at Default (EAD)
EAD represents the outstanding exposure at the time of default and is derived from:
- Outstanding principal
- Loan repayment status
- Credit exposure assumptions

---

## Expected Credit Loss (ECL)

$$\boxed{ECL = PD \times LGD \times EAD}$$

- Calculated at **loan level**
- Aggregated to produce **portfolio-level expected loss**
- Enables forward-looking credit loss estimation

---

## Model Monitoring & Stability

### Population Stability Index (PSI)
Used to detect shifts between training and monitoring datasets.

$$PSI = \sum (A - E) \times \ln\left(\frac{A}{E}\right)$$

| PSI Value | Interpretation |
|---------|----------------|
| < 0.10 | Stable |
| 0.10 – 0.25 | Moderate shift |
| > 0.25 | Significant drift |

### Monitoring Coverage
- Feature distribution drift
- IV stability over time
- PD score distribution shifts

---

## Tools & Technologies
- Python
- Pandas, NumPy
- Scikit-learn
- Jupyter Notebook
- Statistical & risk modeling techniques

---

## Key Takeaways
- Built a **full credit risk lifecycle pipeline**
- Applied **bank-grade interpretability techniques**
- Modeled **PD, LGD, EAD, and ECL from scratch**
- Implemented **portfolio monitoring and drift detection**
- Used a **real-world, industry-standard dataset**

---

## Future Enhancements
- Tree-based PD models with explainability
- SHAP-based risk driver analysis
- Stress testing and macroeconomic scenarios
- Interactive monitoring dashboards

---

## Author
**Sandipan Mondal**  
Data Science | Credit Risk | Machine Learning | Optimization
