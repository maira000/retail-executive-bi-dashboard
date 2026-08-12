# ABC Retail Store — Executive Power BI Dashboard

A Data Warehousing & BI project built around a fictional omnichannel retailer, **ABC Retail Store**. Covers the full path from raw relational Excel data to an interactive executive dashboard: dimensional modeling, star schema design, DAX measures, and business decision intelligence.

## Scenario

ABC Retail Store operates across multiple states, selling Electronics, Furniture, and Office Supplies. Executive decision-makers were facing operational visibility bottlenecks due to fragmented data across siloed systems. As the newly appointed Data Engineer / BI Developer, the goal was to ingest raw transactional data, transform it into a dimensional model (star schema), write core analytical DAX measures, and deliver a dynamic, interactive BI dashboard for the CEO and CCO.

## Project Structure

```
abc-retail-powerbi-dashboard/
├── dashboard/
│   └── ABC_Executive_Dashboard_v1.0.pbix   # Power BI dashboard (open in Power BI Desktop)
├── data/
│   └── ABC_Retail_Store_Data.xlsx          # Source data: Sales, Customers, Products
└── docs/
    └── Data_Engineering_Week5_Assignment.pdf  # Full write-up: modeling, DAX, dashboard, insights
```

## Data Model

Three source tables, modeled as a star schema:

| Table | Type | Key |
|---|---|---|
| **Sales** | Fact table | `OrderID` (PK), `CustomerID` / `ProductID` (FK) |
| **Customers** | Dimension table | `CustomerID` (PK) |
| **Products** | Dimension table | `ProductID` (PK) |

`Sales` holds the numeric, additive transaction measures (Quantity, Sales $); `Customers` and `Products` hold the descriptive attributes used to filter and group them. Relationships are modeled 1:* from each dimension into the fact table, with single-direction filter propagation.

## Dashboard Contents

Built in Power BI Desktop, the executive dashboard includes:

- **KPI cards** — Total Sales, Total Orders, Average Order Value, Quantity Sold
- **Clustered bar chart** — Sales by Product Name
- **Pie & donut charts** — Sales by Product Category, Revenue Share by Category
- **Line chart** — Sales trend over time
- **Column chart** — Sales by Customer City
- **Matrix visual** — Category (rows) vs City (columns)
- **Slicers** — Category, City (multi-select), Date range
- **Gauge chart** — Sales target achievement vs. $10,000 goal
- Custom blue corporate theme, page navigation, and report tooltips (bonus UX task)

Explicit DAX measures used include:

```dax
Total Sales = SUM(Sales[Sales])
Total Orders = DISTINCTCOUNT(Sales[OrderID])
Average Order Value = DIVIDE([Total Sales], [Total Orders], 0)
Total Quantity Sold = SUM(Sales[Quantity])
Maximum Sale = MAX(Sales[Sales])
Minimum Sale = MIN(Sales[Sales])
Average Sales = AVERAGE(Sales[Sales])
```

## Key Findings & Recommendations

Dashboard analysis on the provided sample data (Total Sales: $6,200 vs. a $10,000 goal — 62% attainment) surfaced:

- **Lahore** generated the highest total revenue; **Laptop Ultra** was the top-selling product; **Electronics** was the strongest category overall.
- **Electronics concentration risk** — Electronics drove 70% of total sales, led by Laptop Ultra and Smart Monitor. Recommendation: expand the assortment (accessories, complementary SKUs) while diversifying against category-level demand shocks.
- **Underperforming categories** — Office Supplies (3% of sales) and Furniture (27%) may need investigation into product visibility, pricing, or marketing investment.
- **Regional growth gap** — Lahore ($3,600) significantly outpaced Karachi ($750) and Peshawar ($500), suggesting untapped demand outside the current stronghold.
- **Customer concentration** — Two customers accounted for 58% of total revenue, a material dependency risk; loyalty and referral incentive programs were recommended to diversify the customer base.
- **Declining month-over-month trend** — sales fell 23% from January to February, flagged for immediate investigation (seasonality, stock-outs, or reduced spend).

Full reasoning, screenshots, and the complete Task 1–8 write-up (data warehousing fundamentals, OLTP vs. OLAP, ETL process, star schema diagram, relationship modeling, and all dashboard visuals) are in `docs/Data_Engineering_Week5_Assignment.pdf`.

## Tools

Microsoft Power BI Desktop, Power Query, DAX, Microsoft Excel.

## Author

Maira Naveed
