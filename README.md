# Customer Shopping Sales Dashboard

## Project Overview

An interactive Power BI dashboard analysing 99,458 retail transactions across ten shopping malls in Istanbul, Turkey. The dashboard breaks down revenue by product category, shopping mall, payment method and gender, so a retail stakeholder can see where sales come from and how customers pay in a single view.

![Customer Shopping Sales Dashboard](dashboard-preview.png)

## Business Objective

The dashboard was built to answer:

- What is total sales revenue, and how many orders and units does it represent?
- What is the average value of an order?
- Which product categories generate the most revenue?
- Which shopping malls perform best?
- Which payment methods do customers use most?
- How do purchasing patterns differ between female and male customers?

## Dashboard KPIs

| KPI | Result |
|---|---:|
| Total Sales | ₺68.55M |
| Total Quantity | 299K units |
| Total Invoices | 99,458 |
| Average Order Value | ₺689.25 |

## Dataset

**Source:** [Customer Shopping Dataset — Retail Sales Data](https://www.kaggle.com/datasets/mehmettahiraslan/customer-shopping-dataset) (Kaggle)

| Column | Description |
|---|---|
| invoice_no | Unique invoice identifier |
| customer_id | Unique customer identifier |
| gender | Customer gender |
| age | Customer age |
| category | Product category |
| quantity | Units purchased on the line |
| price | Line revenue (Turkish lira) |
| payment_method | Cash, Credit Card, or Debit Card |
| invoice_date | Date of transaction |
| shopping_mall | Mall where the purchase was made |

Currency is Turkish lira (₺) throughout and is not converted.

## Data Model and DAX Measures

The report runs on a single fact table (`customer_shopping_data`) with four core measures:

```DAX
Total Sales =
SUM(customer_shopping_data[price])
```

```DAX
Total Quantity =
SUM(customer_shopping_data[quantity])
```

```DAX
Total Invoices =
COUNT(customer_shopping_data[invoice_no])
```

```DAX
Average Order Value =
DIVIDE([Total Sales], [Total Invoices])
```


## Dashboard Visuals

- KPI cards — Total Sales, Total Quantity, Total Invoices, Average Order Value
- Revenue by category (ranked horizontal bar)
- Revenue by shopping mall (ranked horizontal bar, all ten malls)
- Revenue by payment method (donut)
- Revenue by category and gender (clustered column)
- Gender and Category slicers

## Key Insights

- Clothing is the leading category at roughly ₺31M, well ahead of Shoes (₺18M) and Technology (₺16M); Cosmetics, Toys, Food & Beverage, Books and Souvenir together make up a small long tail.
- Mall of Istanbul (₺13.9M) and Kanyon (₺13.7M) are the two strongest malls, with Metrocity third at ₺10.2M.
- Cash is the most common payment method at 44.8% of revenue, ahead of Credit Card (35.1%) and Debit Card (20.1%).
- Female customers generate more revenue than male customers in every category, most visibly in Clothing, Shoes and Technology.

## Known Limitations

- `Total Invoices` counts rows, not distinct invoice numbers — see the DAX note above.
- The dataset has no cost or margin field, so profitability and markup are out of scope; every revenue figure here is gross sales.
- `customer_id` is not guaranteed stable across invoices, so it should be read as distinct IDs seen rather than a strict unique-customer count.
- Prices are nominal Turkish lira and are not inflation-adjusted across the dataset's 2021–2023 window.

## Future Improvements

- Switch `Total Invoices` to `DISTINCTCOUNT` for correctness beyond this dataset's current 1-row-per-invoice shape.
- Add a date table and a monthly revenue trend line with MoM/YoY comparisons.
- Add a second page for customer demographics (age bands, average order value by age group).
- Add a "Clear filters" button and bookmark-driven reset state.

## Tools Used

- Microsoft Power BI
- Power Query
- DAX
- CSV dataset

## Files

```text
customer-shopping-sales-dashboard/
├── README.md
├── customer-shopping-sales-dashboard.pbix
├── customer_shopping_data.csv
└── dashboard-preview.png
```

## How to Run the Project

1. Clone or download this repository.
2. Open `customer-shopping-sales-dashboard.pbix` in Power BI Desktop (June 2024 or later).
3. If prompted, point the data source to `customer_shopping_data.csv` in this repository, then refresh.

## Author

**Akshat Arya**

Data analytics learner developing skills in Power BI, DAX, Power Query and business analysis.
