# 📊 Customer Churn Analysis & Intelligence

## 📌 Project Overview

This project focuses on **Customer Churn Analysis for an OTT subscription platform**, with the objective of identifying customers who are at risk of churn, understanding the factors associated with customer attrition, and quantifying the potential revenue impact.

The project follows an end-to-end data analytics workflow by integrating customer, subscription, and support data stored across relational database tables. SQL queries were used through Python and SQLite to extract the data, followed by data cleaning, feature engineering, exploratory data analysis, KPI calculation, churn-risk segmentation, and visualization.

The analysis converts raw customer and subscription data into actionable business insights that can support **customer retention, pricing, subscription-plan optimization, and revenue protection strategies**.

---

## 🎯 Business Objective

Customer churn is a major challenge for subscription-based businesses because losing customers directly affects recurring revenue and customer lifetime value.

The primary objectives of this project are:

* Identify the overall customer churn rate.
* Measure customer retention.
* Analyze churn across subscription plans.
* Compare churn behavior across contract types.
* Identify high-risk customers using churn scores.
* Analyze customer tenure and subscription behavior.
* Measure revenue at risk due to churn.
* Analyze customer support complaints and escalations.
* Identify geographical patterns in churn.
* Analyze monthly churn trends.
* Generate actionable recommendations for improving customer retention.

---

## 🛠️ Tech Stack

* **Python**
* **SQLite**
* **SQL**
* **Pandas**
* **NumPy**
* **Matplotlib**
* **Seaborn**
* **Jupyter Notebook**

---

## 🗄️ Database Structure

The project uses a SQLite database named:

```text
customer_churn.db
```

The database contains three primary tables:

### 1. `db_customer`

Contains customer demographic information:

* `customerid`
* `name`
* `country`
* `state`
* `gender`
* `dob`
* `interests`
* `pincode`

### 2. `db_subscription`

Contains subscription and revenue information:

* `customerid`
* `subscription_start_date`
* `subscription_type`
* `renewal_date`
* `plan_type`
* `contract_type`
* `cancellation_date`
* `cancellation_reason`
* `monthly_charges`
* `cltv`
* `churn_score`

### 3. `db_support`

Contains customer-support information:

* `customerid`
* `complaint_date`
* `escalations`
* `csat_score`
* `comment`

These tables are connected using `customerid` and combined to create an analytical dataset.

---

# 🔄 Project Workflow

```text
SQLite Database
       ↓
SQL Data Extraction
       ↓
Data Import using Pandas
       ↓
Data Cleaning
       ↓
Feature Engineering
       ↓
Data Integration
       ↓
Exploratory Data Analysis
       ↓
KPI Calculation
       ↓
Churn Risk Segmentation
       ↓
Data Visualization
       ↓
Business Insights
       ↓
Retention Recommendations
```

---

# 🧹 Data Cleaning

The following data-cleaning operations were performed:

* Inspected customer, subscription, and support tables.
* Checked data types and dataset structure.
* Renamed columns for better readability.
* Removed unnecessary columns.
* Converted date fields into appropriate datetime formats.
* Standardized gender values.
* Handled missing country values using state-country mapping.
* Removed unnecessary support-table columns.
* Checked duplicate customer/support records.
* Created a consolidated analytical dataset.

Examples of transformations included:

```python
df_db_customer.rename(
    columns={'name': 'customer_name'},
    inplace=True
)
```

```python
df_db_customer.drop(
    columns=['interests', 'pincode'],
    inplace=True
)
```

```python
df_db_customer['dob'] = pd.to_datetime(
    df_db_customer['dob']
)
```

---

# ⚙️ Feature Engineering

A number of analytical features were created from the existing data.

### Churn Flag

A `churn_flag` was created based on whether a customer had a cancellation date:

```python
df_db_subscription['churn_flag'] = np.where(
    df_db_subscription['cancellation_date'].notna(),
    1,
    0
)
```

Where:

```text
1 = Churned
0 = Active
```

### Customer Tenure

Customer tenure was calculated using the subscription start date and either the cancellation date or the current date.

### Complaint Count

The number of complaints associated with each customer was calculated.

### Churn Risk

Customers were segmented into three risk categories based on their churn score:

```text
Low Risk     → Churn Score < 50
Medium Risk  → Churn Score 50–69
High Risk    → Churn Score ≥ 70
```

---

# 📈 Key KPIs

The project calculates several important customer and business KPIs.

| KPI                | Description                                         |
| ------------------ | --------------------------------------------------- |
| Churn Rate         | Percentage of customers who churned                 |
| Retention Rate     | Percentage of customers retained                    |
| Churn by Plan      | Churn rate across Basic, Standard and Premium plans |
| ARPU               | Average Revenue Per User                            |
| Average Tenure     | Average number of days customers remain subscribed  |
| Revenue at Risk    | Monthly revenue associated with churned customers   |
| Escalation Rate    | Percentage of customers with support escalations    |
| Average Complaints | Average complaints per customer                     |
| Churn Risk         | Customer segmentation based on churn score          |

The project report defines these KPIs using business-oriented formulas such as churn rate, retention rate, ARPU, average tenure, revenue at risk, escalation rate, and complaint frequency.

---

# 📊 Key Results

The analysis produced the following results:

### Overall Churn

**Churn Rate: 28.57%**

**Retention Rate: 71.43%**

This indicates that approximately 28.6% of the analyzed customer base had churned while approximately 71.4% remained retained.

### Churn by Subscription Plan

| Plan     | Churn Rate |
| -------- | ---------: |
| Basic    |     60.00% |
| Standard |     22.22% |
| Premium  |     14.29% |

The Basic plan shows the highest churn rate, making it an important segment for retention analysis.

### Revenue Metrics

**ARPU: ₹18.85**

**Revenue at Risk: ₹74K**

The analysis therefore highlights a measurable recurring-revenue exposure associated with churned customers.

### Customer Tenure

**Average Customer Tenure: ~1,516 days**

### Support Metrics

**Escalation Rate: 19.05%**

**Average Complaints per User: 0.43**

The report also identifies support escalations as an important area for further investigation when studying churn behavior.

---

# 📉 Data Visualization

The project uses **Matplotlib and Seaborn** to visualize customer behavior and churn patterns.

### Visualizations Created

* Monthly Churn Trend
* Churn by Subscription Plan
* Churn by State
* Correlation Heatmap
* Pair Plot
* Multi-dimensional Category Plot
* Plan-level Pivot Analysis

### Monthly Churn Trend

A time-series visualization was created to identify changes in customer churn across cancellation months.

### Churn by Plan

A bar chart was used to compare churn rates across:

```text
Basic
Standard
Premium
```

### Churn by State

State-level analysis was performed to identify geographical differences in customer churn.

### Correlation Analysis

A correlation matrix was explored using numerical representations of selected customer and churn-related variables.

---

# 📊 Data Visualizations

## Churn by Subscription Plan

![Churn by Plan](https://github.com/Ayush-Gautam11122/Customer-Churn-Analysis-Intelligence/blob/main/churn_by_plan.jpeg)

## Monthly Churn Trend

![Monthly Churn](images/monthly_churn.png)

## Churn by State

![Churn by State](https://github.com/Ayush-Gautam11122/Customer-Churn-Analysis-Intelligence/blob/main/churn_by_states.jpeg)

## Correlation Analysis

![Correlation Heatmap](images/correlation_heatmap.png)

# 🔍 Business Insights

## 1. Basic Plan Has the Highest Churn

The Basic plan recorded a **60% churn rate**, considerably higher than Standard and Premium plans.

This suggests that the Basic-plan customer segment requires deeper investigation into pricing, perceived value, engagement, and customer experience.

---

## 2. Contract Type Is an Important Churn Indicator

The project report highlights a substantial difference between monthly and annual contract customers.

Reported churn:

```text
Monthly Contract → 55.6%
Annual Contract  → 8.3%
```

Monthly subscribers therefore represent a significantly higher-risk customer segment.

---

## 3. Revenue Exposure From Churn

The analysis identified approximately **₹74K in revenue at risk** from churned customers.

This demonstrates that churn analysis is not only a customer-behavior problem but also a revenue-protection problem.

---

## 4. Geographical Churn Pattern

The project report identifies **Karnataka** as the most affected state and **September 2024** as the month with the highest observed churn.

Potential reasons recommended for investigation include pricing changes, customer complaints, technical issues, and competitor activity.

---

## 5. Customer Risk Segmentation

Customers were categorized into:

```text
Low Risk
Medium Risk
High Risk
```

using their churn scores.

This segmentation can help businesses prioritize retention campaigns toward customers with higher churn probability.

---

# 💡 Recommended Business Actions

Based on the analysis, the following actions can be considered:

### 1. Investigate Basic Plan Churn

Analyze whether pricing, features, content availability, or customer experience is contributing to the high churn rate among Basic-plan subscribers.

### 2. Promote Annual Contracts

Since monthly subscribers demonstrate substantially higher churn than annual subscribers, targeted incentives could be evaluated to encourage suitable customers to migrate toward annual plans.

### 3. Prioritize High-Risk Customers

Use churn-risk categories together with customer lifetime value to prioritize retention activities.

### 4. Investigate Karnataka

Perform a deeper investigation into customer complaints, pricing changes, technical issues, and competitor activity in Karnataka.

### 5. Monitor Customer Support

Analyze complaints, escalations, and CSAT scores to identify potential customer-experience issues associated with churn.

### 6. Protect High-Value Customers

Retention efforts should consider both churn probability and customer lifetime value so that resources are directed toward customers with the highest potential revenue impact.

The report specifically recommends prioritizing customers with **High and Medium churn risk** and considering their LTV and support history when creating a retention priority list.

---

# 🧪 SQL + Python Integration

An important part of this project is the integration of SQL and Python.

SQLite was connected to Python using:

```python
import sqlite3

conn = sqlite3.connect('customer_churn.db')
```

SQL was then used to inspect database tables and retrieve data into Pandas DataFrames.

Example:

```python
sql_query = """
SELECT name
FROM sqlite_master
WHERE type='table'
"""

tables = pd.read_sql(sql_query, conn)
```

The project also demonstrates creating and querying SQLite tables directly from Python.

This demonstrates practical experience with:

* SQL database connectivity
* SQL querying
* SQLite
* Pandas `read_sql()`
* Relational data analysis
* Data integration

---

# 📂 Project Files

```text
Customer-Churn-Analysis/
│
├── Churn_analysis.ipynb
│
├── customer_churn.db
│
├── expected_churn_data.csv
│
├── README.md
│
└── requirements.txt
```

---

# ▶️ How to Run the Project

### 1. Clone the repository

```bash
git clone YOUR_GITHUB_REPOSITORY_URL
```

### 2. Navigate to the project directory

```bash
cd Customer-Churn-Analysis
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Launch Jupyter Notebook

```bash
jupyter notebook
```

### 5. Open

```text
Churn_analysis.ipynb
```

### 6. Run all cells

Make sure the SQLite database file is located in the same working directory expected by the notebook:

```text
customer_churn.db
```

---

# 📦 Python Libraries

```text
numpy
pandas
matplotlib
seaborn
sqlite3
jupyter
```

---

# 🧠 Skills Demonstrated

### Technical Skills

* Python
* SQL
* SQLite
* Pandas
* NumPy
* Matplotlib
* Seaborn
* Jupyter Notebook
* Data Cleaning
* Data Transformation
* Feature Engineering
* Exploratory Data Analysis
* Data Visualization
* KPI Development
* Pivot Tables
* Correlation Analysis
* Customer Segmentation

### Business Skills

* Customer Churn Analysis
* Customer Retention Analysis
* Revenue-at-Risk Analysis
* Subscription Analytics
* Customer Risk Segmentation
* Customer Lifetime Value Analysis
* Support Analytics
* Business Insight Generation
* Data-driven Decision Making

---

# 📌 Project Outcome

This project demonstrates an end-to-end approach to solving a real-world customer-retention problem using data analytics.

The analysis combines **SQL, Python, data cleaning, feature engineering, exploratory analysis, visualization, KPI development, and business interpretation** to identify churn patterns and quantify their potential impact on recurring revenue.

The resulting insights can be used to design targeted retention strategies, prioritize high-risk customers, investigate geographical and subscription-level churn patterns, and reduce potential revenue leakage.

---

# 🚀 Future Improvements

The project can be further enhanced by:

* Building an interactive Power BI churn dashboard.
* Developing a predictive machine-learning churn model.
* Implementing customer lifetime value segmentation.
* Creating automated churn monitoring.
* Developing customer-level retention recommendations.
* Performing deeper support-ticket sentiment analysis.
* Building monthly churn forecasting.
* Creating an automated executive reporting dashboard.

---

## 👨‍💻 Author

**Ayush Gautam**

Aspiring Data Analyst

**Skills:** Python | SQL | Power BI | Excel | Pandas | NumPy | Data Visualization

---

⭐ If you found this project useful, feel free to explore the notebook and analysis.
