## Project Overview

The **Sales Performance Dashboard** provides a **comprehensive analysis of sales, profit, orders, and customer trends over different time periods**. It helps business stakeholders **track revenue growth, compare year-over-year performance, and make data-driven decisions**.

---

## Business Problems Addressed

**Comparing Sales Performance Over Time** – Identify whether **sales, profit, and customer engagement are increasing or decreasing**.  
 **Identifying Peak and Low-Performing Periods** – Highlights **best and worst-performing months** to optimize marketing and inventory planning.  
 **Tracking Customer Retention** – Analyze whether the **customer base is growing or declining**.  
 **Detecting Declining Trends** – Flags months where **orders, sales, or profit dropped compared to the previous year**.  
 **Optimizing Business Strategies** – Provides **actionable insights to improve sales performance**.

---

# Dashboard Preview

This project includes interactive dashboards providing insights into sales performance and customer trends. Key features include:

1. **Total Sales Over Time** – A **line chart** comparing **current year (CY) vs. previous year (PY) sales trends**.  
2. **Min/Max Sales Indicator** – Highlights the **best and worst months for revenue**.  
3. **Sales Growth Indicator** – KPI displaying **positive or negative growth compared to last year**.  
4. **Profitability Tracker** – A **bar chart** comparing **CY vs. PY profits** to identify trends.  
5. **Customer Trends** – Tracks **customer retention and drop-offs compared to the previous year**.  
6. **Underperforming Sales Alerts** – Flags **months where CY sales fall below PY sales**.  

## Dashboard Previews  

### Sales Dashboard  
<img src="dashboard1.PNG" alt="Sales Dashboard" width="800" height="450">  

### Customer Dashboard  
<img src="dashboard2.PNG" alt="Customer Dashboard" width="800" height="450">  


---

## Steps Taken in the Analysis

### 1 Data Preparation

- Extracted historical **sales transaction data**.
- Ensured **date formats and sales/profit figures were correctly structured**.
- Cleaned and formatted **customer and order data** to remove inconsistencies.

### 2 Data Transformation

- Created **calculated fields** for CY (Current Year) and PY (Previous Year) metrics.
- Added **filters for year selection** to allow dynamic analysis.
- Applied **window functions to identify min/max sales, orders, and profit** over time.

### 3 Data Modeling

- Established relationships between **Sales Data and Date Table**.
- Optimized calculations for **faster performance** in Tableau.

---

## Step 1: Calculate CY (Current Year) and PY (Previous Year)

### CY and PY Sales Calculation

```DAX
CY Sales = IF(YEAR([Order Date]) = YEAR(TODAY()), SUM([Sales]), 0)
PY Sales = IF(YEAR([Order Date]) = YEAR(TODAY())-1, SUM([Sales]), 0)
```

### CY and PY Orders Calculation

```DAX
CY Orders = IF(YEAR([Order Date]) = YEAR(TODAY()), COUNT([Order ID]), 0)
PY Orders = IF(YEAR([Order Date]) = YEAR(TODAY())-1, COUNT([Order ID]), 0)
```

### CY and PY Profit Calculation

```DAX
CY Profit = IF(YEAR([Order Date]) = YEAR(TODAY()), SUM([Profit]), 0)
PY Profit = IF(YEAR([Order Date]) = YEAR(TODAY())-1, SUM([Profit]), 0)
```

### CY and PY Customers Calculation

```DAX
CY Customers = IF(YEAR([Order Date]) = YEAR(TODAY()), DISTINCTCOUNT([Customer ID]), 0)
PY Customers = IF(YEAR([Order Date]) = YEAR(TODAY())-1, DISTINCTCOUNT([Customer ID]), 0)
```

## Step 4: Calculating YoY Growth Rate

### % Sales Change

```DAX
Sales % Change =
IF(SUM([PY Sales]) = 0, BLANK(),
   (SUM([CY Sales]) - SUM([PY Sales])) / SUM([PY Sales]) * 100)
```

### % Orders Change

```DAX
Orders % Change =
IF(SUM([PY Orders]) = 0, BLANK(),
   (SUM([CY Orders]) - SUM([PY Orders])) / SUM([PY Orders]) * 100)
```

### % Profit Change

```DAX
Profit % Change =
IF(SUM([PY Profit]) = 0, BLANK(),
   (SUM([CY Profit]) - SUM([PY Profit])) / SUM([PY Profit]) * 100)
```

### % Customers Change

```DAX
Customers % Change =
IF(SUM([PY Customers]) = 0, BLANK(),
   (SUM([CY Customers]) - SUM([PY Customers])) / SUM([PY Customers]) * 100)
```

## Summary of Why We Do These Calculations:

| **Metric**     | **CY Formula**                       | **PY Formula**                       | **% Change Formula**   | **Why Important?**                                  |
| -------------- | ------------------------------------ | ------------------------------------ | ---------------------- | --------------------------------------------------- |
| ** Sales**     | CY Sales = SUM([Sales])              | PY Sales = SUM([Sales])              | `(CY - PY) / PY * 100` | Tracks revenue growth and business performance.     |
| ** Orders**    | CY Orders = COUNTD([Order ID])       | PY Orders = COUNTD([Order ID])       | `(CY - PY) / PY * 100` | Measures demand and customer activity.              |
| ** Profit**    | CY Profit = SUM([Profit])            | PY Profit = SUM([Profit])            | `(CY - PY) / PY * 100` | Ensures profitability and cost control.             |
| ** Customers** | CY Customers = COUNTD([Customer ID]) | PY Customers = COUNTD([Customer ID]) | `(CY - PY) / PY * 100` | Monitors customer retention and acquisition trends. |

---

## Min & Max Analysis:

---

| **Metric**               | **Min Calculation**               | **Max Calculation**               | **Purpose**                                        |
| ------------------------ | --------------------------------- | --------------------------------- | -------------------------------------------------- |
| ** Min & Max Sales**     | `WINDOW_MIN(SUM([CY Sales]))`     | `WINDOW_MAX(SUM([CY Sales]))`     | Identifies best and worst-performing sales months. |
| ** Min & Max Orders**    | `WINDOW_MIN(SUM([CY Orders]))`    | `WINDOW_MAX(SUM([CY Orders]))`    | Finds peak and low demand periods.                 |
| ** Min & Max Profit**    | `WINDOW_MIN(SUM([CY Profit]))`    | `WINDOW_MAX(SUM([CY Profit]))`    | Tracks profitability fluctuations.                 |
| ** Min & Max Customers** | `WINDOW_MIN(SUM([CY Customers]))` | `WINDOW_MAX(SUM([CY Customers]))` | Helps analyze customer engagement trends.          |

---

## Future Improvements:

- **AI-Powered Sales Predictions** – Use machine learning to forecast future trends.
- **Real-Time Data Updates** – Automate daily sales tracking for instant insights.
- **Customer Segmentation Analysis** – Identify top customers and their buying behavior.

## Final Impact:

- **A clear view of sales, profit, orders, and customer trends.**
- **Year-over-year comparisons to track business performance.**
- **Min/Max indicators to detect best and worst-performing months.**
- **Actionable insights to optimize revenue, customer retention, and profitability.**
