# Customer Shopping Behavior Analysis

## Project Overview

This project focuses on analyzing customer shopping behavior data using **Python, SQL, and Power BI** to uncover meaningful business insights. The workflow includes loading raw data, performing exploratory data analysis (EDA), cleaning and transforming data, running SQL-based business queries, building an interactive dashboard in Power BI, generating a business report, and creating a presentation using Gamma.

The main objective of this project is to understand customer purchasing behavior, identify trends, and present insights in a business-friendly format.

---

## Business Problem

Retail businesses generate large amounts of customer transaction data, but raw data alone does not provide actionable insights.

This project aims to answer business questions such as:

- Which products generate the highest sales?
- How do discounts affect customer purchases?
- What are the purchasing patterns of repeat customers?
- Which shipping type performs better?
- How do ratings relate to customer spending?
- What categories perform best?

---

## Dataset Information

The dataset contains customer shopping behavior records with information such as:

| Column | Description |
|--------|-------------|
| customer_id | Unique customer identifier |
| age | Customer age |
| gender | Gender of customer |
| item_purchased | Product purchased |
| category | Product category |
| purchase_amount | Amount spent |
| location | Customer location |
| size | Product size |
| color | Product color |
| season | Season of purchase |
| review_rating | Customer review rating |
| subscription_status | Subscription status |
| shipping_type | Shipping method |
| discount_applied | Discount usage |
| promo_code_used | Promo code usage |
| previous_purchases | Number of past purchases |
| payment_method | Payment method |
| frequency_of_purchases | Purchase frequency |

---

## Tools & Technologies Used

### Programming & Analysis
- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn

### Database & Querying
- PostgreSQL
- MySQL
- SQL Server
- SQLAlchemy
- psycopg2

### Visualization & Reporting
- Power BI
- Gamma

### Development Environment
- Jupyter Notebook

---

## Project Workflow

---

### 1. Data Loading

Loaded dataset into Python using Pandas.

Tasks performed:

- Imported CSV dataset
- Inspected rows and columns
- Checked data types
- Verified null values
- Understood dataset structure

Example:

```python
import pandas as pd

df = pd.read_csv("shopping_data.csv")
df.head()
df.info()
```

---

### 2. Exploratory Data Analysis (EDA)

Performed EDA to understand customer behavior and data patterns.

Analysis included:

- Age distribution
- Gender analysis
- Category-wise sales
- Purchase amount trends
- Shipping preferences
- Discount usage
- Payment methods
- Review rating patterns
- Purchase frequency analysis

Visualizations created using:

- Bar charts
- Histograms
- Pie charts
- Count plots
- Correlation analysis

---

### 3. Data Cleaning & Transformation

Cleaned and transformed data before loading into SQL and Power BI.

Tasks performed:

- Renamed columns
- Removed duplicate columns
- Removed unnecessary columns
- Checked for duplicates
- Standardized column names
- Converted data types
- Validated consistency across columns
- Handled missing values
- Prepared SQL-compatible schema

Example:

```python
df.rename(columns={'purchase_amount(usd)': 'purchase_amount'}, inplace=True)

df.drop(columns=['promo_code_used'], inplace=True)
```

---

### 4. SQL Database Loading

Loaded cleaned data into SQL databases using SQLAlchemy.

Databases used:

- PostgreSQL
- MySQL
- SQL Server

Example:

```python
from sqlalchemy import create_engine

engine = create_engine("postgresql+psycopg2://username:password@localhost:5432/customer_behavior")

df.to_sql("customer", engine, if_exists="replace", index=False)
```

---

### 5. SQL Business Analysis

Performed SQL analysis to answer business questions.

Queries included:

#### Customer Analysis
- New vs returning vs loyal customers
- Purchase frequency segmentation
- Repeat customer behavior

#### Product Analysis
- Top-selling items
- Category performance
- Discount purchase rates

#### Financial Analysis
- Average purchase amount
- High-value customer analysis
- Purchase amount comparisons

#### Shipping Analysis
- Standard vs express shipping comparison
- Shipping behavior impact

#### Review Analysis
- Average ratings
- Spending vs ratings relationship

#### Discount Analysis
- Discount impact on purchases
- Discount usage by product
- Discount percentage analysis

---

## Sample SQL Queries

### Average Purchase Comparison

```sql
SELECT
AVG(CASE WHEN shipping_type = 'Standard' THEN purchase_amount END) -
AVG(CASE WHEN shipping_type = 'Express' THEN purchase_amount END)
AS avg_difference
FROM customer;
```

---

### Discount Rate by Product

```sql
SELECT item_purchased,
ROUND(
100.0 * SUM(CASE WHEN discount_applied = 'Yes' THEN 1 ELSE 0 END)/COUNT(*),
2
) AS discount_rate
FROM customer
GROUP BY item_purchased
ORDER BY discount_rate DESC
LIMIT 5;
```

---

### Customer Segmentation using CTE

```sql
WITH customer_type AS (
SELECT customer_id,
CASE
WHEN previous_purchases = 1 THEN 'New'
WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
ELSE 'Loyal'
END AS customer_segment
FROM customer
)

SELECT customer_segment,
COUNT(*) AS total_customers
FROM customer_type
GROUP BY customer_segment;
```

---

## Power BI Dashboard

Created an interactive Power BI dashboard to visualize business insights.

Dashboard includes:

### KPI Cards
- Total Sales
- Average Purchase Amount
- Total Customers
- Average Review Rating

### Charts
- Category-wise sales
- Product sales distribution
- Discount analysis
- Payment method usage
- Shipping type comparison
- Purchase frequency analysis
- Customer segmentation

### Interactive Features
- Filters / slicers
- Drill-down analysis
- Cross-filtering visuals

---

## Dashboard Preview

(Add screenshots here after uploading)

Example:

```text
/dashboard/dashboard_preview.png
```

---

## Report Creation

Created a business summary report based on dashboard insights.

Report includes:

- Executive summary
- Key findings
- KPI analysis
- Product insights
- Customer behavior insights
- Business recommendations

---

## Presentation (Gamma)

Created presentation slides using Gamma.

Presentation covers:

- Project objective
- Dataset overview
- Analysis process
- Key insights
- Dashboard highlights
- Business recommendations

---

## Key Insights / Results

Some major insights discovered:

- Top-performing products identified
- Best-selling categories analyzed
- Discount impact measured
- Repeat customer patterns identified
- Shipping preferences compared
- Payment method trends discovered
- Ratings and spending relationship analyzed

---

## Project Structure

```text
Customer-Shopping-Behavior-Analysis/
│
├── data/
│   └── shopping_data.csv
│
├── notebooks/
│   └── Customer_Shopping_Behavior.ipynb
│
├── sql/
│   └── queries.sql
│
├── dashboard/
│   └── customer_dashboard.pbix
│
├── report/
│   └── business_report.pdf
│
├── presentation/
│   └── project_presentation.ppt
│
└── README.md
```

---

## How to Run This Project

### Step 1: Clone Repository

```bash
git clone https://github.com/your-username/customer-shopping-behavior-analysis.git
```

---

### Step 2: Install Dependencies

```bash
pip install pandas numpy matplotlib seaborn sqlalchemy psycopg2-binary
```

---

### Step 3: Launch Jupyter Notebook

```bash
jupyter notebook
```

Open:

```text
Customer_Shopping_Behavior.ipynb
```

---

### Step 4: Configure Database

Update connection details:

```python
username = "postgres"
password = "your_password"
host = "localhost"
port = "5432"
database = "customer_behavior"
```

---

### Step 5: Load Data into SQL

Run notebook SQL loading section.

---

### Step 6: Open Power BI Dashboard

Open:

```text
customer_dashboard.pbix
```

in Power BI Desktop.

---

### Step 7: View Reports & Presentation

Open:

- PDF report
- PPT presentation

---

## Deliverables

This project includes:

- Python Notebook
- SQL Query File
- Power BI Dashboard
- Business Report
- Presentation
- README Documentation

---

## Skills Demonstrated

- Python Data Analysis
- Data Cleaning
- Exploratory Data Analysis
- SQL Query Writing
- PostgreSQL / MySQL / SQL Server
- Power BI Dashboarding
- Business Reporting
- Data Storytelling

---

## Author

**Naveenkumar**

Data Analytics Project Portfolio

---

## Future Improvements

Possible future enhancements:

- Add predictive analytics
- Customer churn prediction
- Recommendation system
- Advanced dashboard KPIs
- Deployment to cloud
