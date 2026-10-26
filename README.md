# Power BI Sales Report (PBIP)

A sales analytics report built in Power BI.

The report tracks sales, orders, customers, and shipping performance, and compares each metric with the previous month and the previous year.

## Features

- **KPI cards** for Total Sales, Number of Orders, and Number of Customers, each showing MoM %, YoY %, and the difference from the previous year (Δ), with conditional colors and labels.
- **Trend line chart** that shows the current year against the previous year, with markers where the current year is above or below.
- **Field parameters** that let the user change which measure appears in the line chart and in the orders-by-country chart.
- **Bookmarks** that switch between views such as *YoY (%)*, *PY (Δ)*, *Purchase Frequency*, and *Average Days Between Orders*.
- **Shipping metrics**: shipped orders, on-time vs. late shipments, on-time shipment rate, average order-to-ship days, and average days late.
- **Customer and order metrics**: Average Order Value (AOV), Average Selling Price (ASP), and sales by country/territory.
- **Calculation groups** for reusable time intelligence: MTD, QTD, YTD, PY, PY MTD/QTD/YTD, MoM, MoM %, YoY, and YoY %.

## Data model

A star schema:

| Table | Type | Description |
| --- | --- | --- |
| `fact_salesorderdetails` | Fact | Order lines: quantity, unit price, line total, tax, freight, and order/due/ship dates |
| `dim_salesorderheader` | Dimension | Order header: online flag, status |
| `dim_customer` | Dimension | Customer, store, territory, and country |
| `Order Date`, `Due Date`, `Shipped Date` | Date | Role-playing date tables, one for each date column in the fact table |
| `Measure` | Measures | All report measures, grouped into display folders |
| `Time Intelligence`, `CG Time intelligence` | Calculation groups | Time intelligence calculations |
| `Parameter …` | Field parameters | Measure switchers for the visuals |

```
dim_customer ──────────┐                           ┌── Order Date
                       ├── fact_salesorderdetails ─┼── Due Date
dim_salesorderheader ──┘                           └── Shipped Date
```

