# Executive Sales Performance Dashboard

## Tableau Dashboard and Data Storytelling Project

This repository contains the complete Tableau Executive Dashboard developed for a retail business analytics scenario. The project demonstrates the use of Tableau to transform transactional retail data into meaningful business insights through interactive dashboards, calculated fields, executive KPIs, and visual storytelling.

The dashboard enables business leaders to monitor overall organizational performance, evaluate profitability, identify operational risks, and explore business opportunities using interactive filters and dashboard actions. The project follows Tableau visualization best practices and presents complex business information in a clear, concise, and decision-oriented format.

---

# Table of Contents

* Business Problem Summary
* Dataset Description
* Data Inspection and Assumptions
* Calculated Fields Created
* Tableau Workbook Description
* Dashboard Components
* Dashboard Filters and Interactions
* Key Business Insights
* Dashboard Story Summary
* Assumptions and Limitations
* Repository Structure
* Screenshots Included
* Conclusion

---

# Business Problem Summary

## Project Objective

A retail organization's leadership team requires an executive dashboard that provides a comprehensive overview of business performance while allowing deeper exploration into specific operational areas.

Traditional reports often present large amounts of data without highlighting relationships or supporting interactive analysis. The objective of this project was to design an Executive Sales Performance Dashboard in Tableau that combines sales, profitability, customer behaviour, shipping performance, discounts, and product returns into a single interactive interface.

The dashboard enables executives to:

* Monitor overall business performance through executive KPIs.
* Identify profitable and underperforming regions.
* Compare product categories and customer segments.
* Evaluate shipping efficiency.
* Analyse the relationship between discounts and profitability.
* Monitor product return behaviour.
* Perform interactive drill-down analysis using filters and dashboard actions.

The completed dashboard supports evidence-based decision-making by transforming raw transactional data into actionable business intelligence.

---

# Dataset Description

## Dataset Overview

The dataset contains retail sales transaction records representing customer purchases, product information, shipping details, geographic information, profitability measures, customer ratings, and marketing campaign information.

Each row represents an individual retail order and includes the information required to analyse business performance from multiple perspectives.

The dataset combines sales, customer, product, geographic, shipping, and marketing information, making it suitable for multidimensional business analysis and executive reporting.

### Dataset Fields

| Category               | Fields                                         |
| ---------------------- | ---------------------------------------------- |
| Order Information      | Order ID, Order Date, Ship Date                |
| Customer Information   | Customer ID, Customer Segment, Customer Rating |
| Geographic Information | Region, State, City                            |
| Product Information    | Category, Sub-Category, Product Name           |
| Shipping Information   | Ship Mode, Delivery Days                       |
| Sales Measures         | Sales, Quantity, Discount, Profit              |
| Return Information     | Return Flag                                    |
| Marketing Information  | Campaign Channel                               |

The dataset was imported into Tableau using the Excel file:

`dashboard_sales_data.xlsx`

---

# Data Inspection and Assumptions

## Data Inspection

The dataset was inspected after being imported into Tableau to verify field types and overall data quality. 

The data types assigned by Tableau were verified to ensure that date fields were recognised as dates, geographic fields were available for location-based analysis, categorical fields were treated as dimensions, numerical fields were recognised as measures, and the binary return flag was correctly interpreted for return rate calculations.

### Date Fields

* Order Date
* Ship Date

These fields were recognised as Date data types and used for time-series analysis and delivery performance calculations.

### Geographic Fields

* Region
* State
* City

These dimensions support regional performance analysis and location-based comparisons.

### Categorical Fields

* Customer Segment
* Region
* State
* City
* Category
* Sub-Category
* Product Name
* Ship Mode
* Campaign Channel

These fields are used for grouping, filtering, and comparative analysis.

### Numerical Measures

* Sales
* Quantity
* Discount
* Profit
* Delivery Days
* Customer Rating

These measures support KPI calculations and quantitative analysis.

### Binary Field

* Return Flag

A value of **1** indicates a returned order, while **0** indicates a completed order.

### Data Quality Observations

The dataset was generally clean and suitable for analysis.

Minor missing values were identified in:

* Customer Rating
* Campaign Channel

No transaction records were removed.

Missing customer ratings were retained because not every customer submits feedback.

Missing campaign channels were handled using a calculated field that replaces null values with **"Unknown"**, ensuring clean filtering and reporting.

---

# Calculated Fields Created

Several calculated fields were created in Tableau to extend the original dataset and provide additional business metrics for analysis. These fields were used throughout the dashboard to improve reporting quality and support executive decision-making.

---

## 1. Profit Margin

### Formula

```text
Profit / Sales
```

### Description

The **Profit Margin** field calculates the proportion of profit earned from every unit of sales. Instead of looking only at total profit, this metric shows how efficiently revenue is converted into profit.

It was used to compare profitability across different regions, customer segments, and product categories, making it easier to identify areas with stronger financial performance.

---

## 2. Cost

### Formula

```text
Sales - Profit
```

### Description

The **Cost** field estimates the total cost associated with each sale by subtracting profit from sales revenue.

Although the dataset does not directly provide cost values, this calculated field enables a basic cost analysis and supports comparisons between revenue, cost, and profit during business evaluation.

---

## 3. Average Order Value (AOV)

### Formula

```text
SUM(Sales) / COUNTD(Order ID)
```

### Description

The **Average Order Value (AOV)** measures the average revenue generated from each customer order.

This KPI helps assess customer purchasing behaviour and indicates whether customers are placing larger or smaller orders on average. It is useful for evaluating sales performance and identifying opportunities to increase basket size.

---

## 4. Return Rate

### Formula

```text
SUM(Return Flag) / COUNT(Order ID)
```

### Description

The **Return Rate** calculates the percentage of orders that were returned by customers.

This metric provides insight into customer satisfaction and product performance. A higher return rate may indicate issues related to product quality, customer expectations, shipping damage, or order fulfilment.

---

## 5. Shipping Delay Bucket

### Formula Logic

```text
IF [Delivery Days] <= 2 THEN "1–2 Days"

ELSEIF [Delivery Days] <= 4 THEN "3–4 Days"

ELSEIF [Delivery Days] <= 7 THEN "5–7 Days"

ELSE "8+ Days"

END
```

### Description

The **Shipping Delay Bucket** groups delivery times into meaningful ranges rather than displaying individual delivery-day values.

This improves dashboard readability and allows users to quickly compare shipping performance across different delivery time categories. The field was primarily used in the Shipping Performance visualization.

---

## 6. Campaign Channel Clean

### Formula

```text
IF ISNULL([Campaign Channel]) THEN
    "Unknown"
ELSE
    [Campaign Channel]
END
```

### Description

Some records contained missing values for the campaign channel. This calculated field replaces null values with **"Unknown"**, ensuring that all records are included during filtering and reporting.

It also improves dashboard consistency by preventing blank values from appearing in filter selections and visualizations.

---

# Summary

The calculated fields enhanced the original dataset by introducing additional analytical measures related to profitability, operational efficiency, customer purchasing behaviour, shipping performance, returns, and data quality. Combined with the dashboard's interactive visualizations, these calculations provide management with meaningful business intelligence that supports informed, data-driven decision-making.

---

# Tableau Workbook Description

The Tableau workbook (`executive_dashboard.twbx`) contains multiple worksheets integrated into a single executive dashboard.

The workbook was designed to present information progressively, allowing executives to begin with overall organizational performance before exploring detailed operational metrics.

The workbook contains the following worksheets:

* Executive KPI Cards
* Monthly Sales Trend
* Regional Profit Performance
* Category Profitability
* Customer Segment Performance
* Shipping Performance
* Discount vs Profit Analysis
* Return Rate Analysis

All worksheets are connected using dashboard filters and action filters to support interactive business exploration.

---

# Dashboard Components

The executive dashboard consists of the following components.

## Executive KPI Cards

Three KPI cards summarise the overall business performance.

* **Total Sales:** 217.02M
* **Total Profit:** 33.31M
* **Total Orders:** 4,200

These metrics provide an immediate overview of organizational performance.

## Monthly Sales Trend

Displays monthly sales performance using a line chart to identify business trends and seasonal fluctuations.

## Regional Profit Performance

Compares profit generated across different regions using a horizontal bar chart.

## Category Profitability

Shows profitability across product categories and sub-categories to identify the strongest and weakest product groups.

## Shipping Performance

Analyses shipping efficiency by comparing ship modes against delivery delay buckets.

## Discount vs Profit Analysis

Examines the relationship between discount levels and profitability using a scatter plot with trend lines.

## Return Rate Analysis

Compares customer return percentages across customer segments to identify potential quality or satisfaction issues.

---

# Dashboard Filters and Interactions

The dashboard includes several interactive filters that enable dynamic exploration of business performance.

### Filters

* Region
* Category
* Customer Segment
* Ship Mode

These filters allow executives to customise dashboard views without modifying the underlying data.

### Dashboard Action Filter

An Action Filter has been implemented using the Regional Profit Performance chart.

Selecting any region automatically filters:

* KPI Cards
* Monthly Sales Trend
* Category Profitability
* Shipping Performance
* Discount vs Profit Analysis
* Return Rate Analysis

This provides an intuitive drill-down experience for regional analysis.

---

# Key Business Insights

Analysis of the dashboard revealed several important findings.

* The business generated **217.02M** in total sales and **33.31M** in total profit from **4,200 completed orders**.
* The **South** region achieved the highest overall profitability.
* **Technology** was the most profitable product category, led by Copiers, Accessories, and Phones.
* Most customer deliveries occurred within the **5–7 day** shipping bucket.
* Higher discount levels generally corresponded with lower profitability.
* The **Home Office** customer segment experienced the highest product return rate.
* Monthly sales varied throughout the year, with stronger performance during February and renewed growth in October and November.
* Interactive filtering enables rapid comparison across regions, customer segments, product categories, and shipping methods.

---

# Dashboard Story Summary

The dashboard was intentionally designed to communicate a complete business story rather than present isolated visualizations.

Executives begin by reviewing overall business performance through the KPI cards before analysing monthly sales trends.

Regional and category visualizations identify where profits are being generated, while customer, shipping, discount, and return analyses explain the operational drivers behind overall performance.

This logical progression enables leadership to move naturally from organizational performance to detailed operational analysis, supporting strategic planning and evidence-based decision-making.

Rather than presenting isolated charts, the dashboard connects financial, operational, and customer-related metrics into a single narrative that enables faster and more informed executive decisions.

---

# Assumptions and Limitations

## Assumptions

* Return Flag = 1 represents a returned order.
* Return Flag = 0 represents a completed order.
* Delivery Days correctly represents the time between order placement and shipment.
* Missing Customer Ratings represent unavailable customer feedback.
* Missing Campaign Channels represent unknown acquisition sources.
* The dataset was analysed exactly as provided.

## Limitations

* Missing values exist in Customer Rating and Campaign Channel.
* External business factors such as competitor behaviour, economic conditions, seasonal events, and marketing budgets were not included.
* The dashboard identifies business relationships but does not establish causation.
* Results should be interpreted alongside operational expertise and additional business information.

---

# Repository Structure

```text
part4_tableau_dashboard/
├── data/
│   └── dashboard_sales_data.xlsx
├── tableau/
│   └── executive_dashboard.twbx
├── outputs/
│   ├── business_insights.md
│   ├── dashboard_story.md
│   └── chart_selection_justification.md
├── screenshots/
│   ├── full_dashboard.png
│   ├── sales_trend_view.png
│   ├── regional_performance_view.png
│   ├── category_profitability_view.png
│   └── filter_interaction_view.png
└── README.md
```

---

# Screenshots Included

The repository includes the following screenshots as evidence of dashboard completion.

| Screenshot                      | Description                             |
| ------------------------------- | --------------------------------------- |
| full_dashboard.png              | Complete Executive Dashboard            |
| sales_trend_view.png            | Monthly Sales Trend                     |
| regional_performance_view.png   | Regional Profit Analysis                |
| category_profitability_view.png | Category and Sub-category Profitability |
| filter_interaction_view.png     | Dashboard Filter Interaction            |

These screenshots demonstrate the completed dashboard, individual analytical views, and interactive filtering functionality.

---

# Conclusion

This project demonstrates the end-to-end development of an Executive Sales Performance Dashboard using Tableau. By combining calculated fields, executive KPI cards, interactive filters, dashboard actions, and carefully selected visualizations, the dashboard transforms raw retail transaction data into meaningful business intelligence.

The completed dashboard enables executives to monitor organizational performance, evaluate sales and profitability trends, identify regional and product-level strengths and weaknesses, assess operational efficiency, investigate the impact of discounts and product returns, and support evidence-based strategic decision-making through an intuitive and interactive analytical interface.

Overall, the project demonstrates how Tableau can be used to convert complex business data into clear, actionable insights that help leadership monitor performance, identify opportunities, and make informed business decisions with confidence.
