# Bank Customer Churn Analysis (Excel & Tableau)

## Overview

This project analyzes **bank customer churn** using the popular *Churn Modelling* dataset.  
Each row represents one customer and the target variable `Exited` indicates whether the customer has left the bank:

- `Exited = 1` → customer churned (left the bank)  
- `Exited = 0` → customer is still active  

The goal of the analysis is to answer:

> Which types of customers are more likely to churn based on gender, age and balance?

I used **Excel** for data exploration and basic aggregation, and **Tableau** to build a simple but clear churn dashboard.

---

## Dataset

- **Source:** [Churn Modelling – Bank Customer Churn](https://www.kaggle.com/datasets/shrutimechlearn/churn-modelling)
- **Grain:** One row per bank customer
- **Key columns:**
  - `CustomerId`
  - `Geography`
  - `Gender`
  - `Age`
  - `Tenure` (years with the bank)
  - `Balance`
  - `NumOfProducts`
  - `IsActiveMember`
  - `EstimatedSalary`
  - `Exited` (1 = churned, 0 = stayed)

---

## Business Questions

1. What is the **overall churn rate** in the customer base?
2. Do **men and women** churn at different rates?
3. How does **age** affect churn risk?
4. How does **account balance level** relate to churn?

---

## Data Preparation (Excel)

I prepared the data in Excel before building the visualisations:

1. **Overall churn rate**
   - Calculated total number of customers and number of churned customers using:
     ```excel
     =COUNTIF(ExitedRange,1) / COUNTA(ExitedRange)
     ```
   - Overall churn rate is approximately **20%**.

2. **Derived grouping fields**
   - Created age bands:
     - `<30`, `30–40`, `41–50`, `>50` (column `AgeGroup`)
   - Created balance bands:
     - `No Balance`, `Low`, `Medium`, `High` (column `BalanceBand`)

3. **Pivot tables for churn analysis**
   - Churn by **Gender** (Gender × Exited)
   - Churn by **AgeGroup** (AgeGroup × Exited)
   - Churn by **BalanceBand** (BalanceBand × Exited)
   - For each pivot, I added a **churn rate** column:
     ```excel
     = Churn_Count / (Churn_Count + NonChurn_Count)
     ```

These pivot tables provided the basis for the Tableau visualisations.

---

## Tableau Dashboard

I then recreated the same logic in Tableau and built a simple churn dashboard.

### Worksheets

- **Overall Churn Rate**  
  - Single KPI card using `AVG(Exited)` formatted as a percentage.

- **Churn Rate by Gender**  
  - Bar chart with `Gender` on the x-axis and `AVG(Exited)` on the y-axis.

- **Churn Rate by Age Group**  
  - Bar chart with `AgeGroup` on the x-axis and `AVG(Exited)` on the y-axis.

- **Churn Rate by Balance Band**  
  - Bar chart with `BalanceBand` on the x-axis and `AVG(Exited)` on the y-axis.

### Dashboard Layout

- Top: **Overall Churn Rate** KPI card.  
- Bottom row: three bar charts side by side:
  - Gender, Age Group, Balance Band.

This layout allows a quick comparison of churn risk across different customer segments.

---

## Key Insights

From the analysis:

- **Overall churn rate** is around **20%** of customers.
- **Gender**
  - Female churn rate ≈ **25%**
  - Male churn rate ≈ **16%**  
  → Female customers are more likely to churn than male customers.
- **Age**
  - `<30`: ~**8%**
  - `30–40`: ~**12%**
  - `41–50`: ~**34%**
  - `>50`: ~**45%**  
  → Churn risk increases strongly with age, especially for customers over 50.
- **BalanceBand**
  - `Low` balance customers have the highest churn rate (~**35%**).
  - `High` balance customers churn at about **25%**.
  - `Medium` balance customers around **20%**.
  - `No Balance` customers have the lowest churn rate (~**14%**).  
  → Customers with **low balances** appear to be the riskiest segment.

These findings suggest that the bank should pay special attention to **older customers** and those with **low balances**, especially female customers, when designing retention strategies.

---

│   └── bank_churn_dashboard.png        # Screenshot of the Tableau dashboard
└── README.md
