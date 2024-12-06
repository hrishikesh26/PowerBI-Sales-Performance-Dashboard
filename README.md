# Sales Analytics Dashboard for AtliQ Hardware

This repository contains the Power BI project files and resources for AtliQ Hardware's Sales Analytics Dashboard. AtliQ Hardware, a leading hardware supplier in India, faces challenges in dynamically tracking and analyzing sales data across its widespread operations. This project aims to automate and streamline their sales data analysis, enabling more informed decision-making through advanced analytics.

![!alt text](https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExYTg3aHk0anBjZXprcXd5cHd2NGg0MG9ja202dzI2Nnd5aGRwbXZvOCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/NQj3aNgf8Rw8LijJ2z/giphy.gif)

## Project Background

AtliQ Hardware services a wide range of clients including Surge Stores, Nomad Stores, and Excel Stores. The rapidly expanding market has exacerbated challenges related to data management and insight generation. Previously, regional managers relied on verbal communication, leading to data inconsistencies and delays in decision-making.

## Goals and Objectives

The Sales Analytics Dashboard project for AtliQ Hardware is structured around clear, strategic objectives designed to enhance data-driven decision-making and streamline sales performance analytics. The goals of this project encompass the following areas:

1. **Streamline Data Integration**: 
    - Database Connection: Utilize Power BI’s MySQL database connector to establish a live connection to AtliQ Hardware's sales data, enabling direct and real-time data querying.
    - Data Transformation: Employ Power BI’s Power Query for initial data cleaning (removing nulls, normalizing currencies, converting data types) to ensure clean and consistent data for analysis.
    - Optimizing Load Performance: Implement query optimization techniques and scheduled data refreshes within Power BI to maintain data currency and performance.

2. **Enable Comprehensive Sales Insights**:
    - Revenue and Sales Volume Analysis: Analyze revenue and sales volumes across different markets and segments to identify trends and peak sales periods.
    - Profitability Analysis: Evaluate profitability by product and market segment to determine the most lucrative business areas.
    - Cost Efficiency: Compare sales revenue against operational costs to pinpoint cost reduction opportunities.


3. **Enhance Decision-Making Capabilities**:

    - Actionable Insights: Provide detailed analytics to highlight areas for business improvement, informing resource allocation and operational strategies.
    - Predictive Insights: Integrate predictive analytics models to forecast future sales trends based on historical data.


4. **Improve User Interactivity and Accessibility**:
    - Dynamic Interactivity: Incorporate interactive elements like slicers and dropdowns that allow users to customize their analytical views.
    - Customizable Views: Offer various visual formats for data display, enhancing user experience and understanding of insights.
 




## Data Description
The Sales Analytics Dashboard utilizes a comprehensive dataset from AtliQ Hardware's MySQL database, which includes sales transactions across various regions and customer segments in India.

- Key attributes of the dataset include:
    - _Sales Transactions_: Records each sale with details on customer, product, sales amount, and date.
    - _Customer Information_: Provides customer demographics such as type (e.g., Brick & Mortar, E-commerce) and geographical location.
    - _Product Details_: Includes information about product type and cost price.
    - _Sales Performance Metrics_: Tracks metrics such as revenue, sales quantity, and profit margins.

The dataset consists of 148,395 rows, reflecting the diverse and dynamic nature of AtliQ Hardware's operations. This rich dataset forms the foundation for the analytical insights generated through the dashboard.


![alt text](https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExeTN5aW9zbHc1ZnU0MThmM2l3aGlvbGh2OGhhNmExczYxNmp3b2J0bSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/GkDWg6b1wUqMhDyS2n/giphy.gif)

## Data Analysis Process

### Data Integration and Preparation
1. **Database Connection**:

    - **Connection Setup**: Established a direct query connection to the MySQL database using Power BI’s database connector, enabling real-time data access without importing it into Power BI's in-memory model.
    - **Security and Reliability**: Ensured secure data access by configuring the connection with appropriate credentials and permissions.

2. **Data Transformation using Power Query**:

    - **Cleaning and Preprocessing**: Removed rows with null values in critical columns such as `sales_amount` and `zone` to ensure data quality. Applied conditions in Power Query to exclude such entries.
        - Utilizing Power Query, rows with null values in critical fields like `sales_amount` and `zone` were removed to maintain the integrity of analyses. For example, `Table.SelectRows(sales_markets, each ([zone] <> ""))` ensures that only entries with valid market zones are included.


    - **Normalization and Type Conversion**:
        - **Currency Normalization**: The sales data contained multiple currencies which were normalized to INR using a custom Power Query function. This function multiplied USD amounts by a fixed exchange rate (e.g., 75) and left INR amounts unchanged, ensuring uniformity across financial data: `Table.AddColumn(#"Filtered Rows", "norm_sales_amount", each if [currency] = "USD" or [currency] = "USD#(cr)" then [sales_amount]*75 else [sales_amount])`.


        - **Data Type Conversions**: The `norm_sales_amount` column, initially loaded as a string due to inconsistencies in source data, was converted to a decimal type to support accurate financial calculations and aggregations.


### Advanced Data Modeling and Analytics
1. **Data Modeling in Power BI**:

    - **Schema Design**: Utilized a star schema for efficient data modeling, which involved setting up fact and dimension tables. The `sales_transactions` table served as the central fact table, with dimension tables for products, customers, and markets.
    - **Relationships**: Configured relationships between these tables to enable coherent and aggregated data analysis across different dimensions.

        ![alt text](https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExbmhqenMzamE2cnRpcGVrNWZ4YTU4ZTJzMzBsNWZ3aHRienoxZmxhdiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/OQsV0cSxQaa02i2N15/giphy.gif)

2. **DAX Measures and Calculations:**
Robust DAX measures form the backbone of the dashboard’s analytical capabilities:


    - **Revenue and Profit Calculations**:
        - `Total Revenue`: Summed up `norm_sales_amount` to calculate total revenue. SUM`('sales_transactions'[norm_sales_amount])`
        - `Total Profit Margin`: Aggregated profit margins from sales transactions to assess overall profitability.
    - **Profitability Metrics**:
        - `Profit Margin %`: Created a measure to calculate profit margin as a percentage of revenue, highlighting profitability efficiency. `DIVIDE([Total Profit Margin], [Revenue], 0)`
        - `Profit Margin Contribution %`: This measure provided insights into how much each region contributed to overall profit margins, helping identify high-performance areas despite lower revenue figures.

        ![alt text](https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExcHpjOGY5a3NidGIzejVnNGlodXZ2bGlmMGtxOGp1ODhrNTV1eXR2ayZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/xuLipzMVuLTsR5r41G/giphy.gif)


3. **Dynamic Reporting and Insights**:

    - **Interactive Visualizations**: Developed interactive charts and graphs that allow users to filter and slice data by various dimensions such as time period, market, and customer type.
    - **Performance Benchmarking**: Integrated year-over-year comparisons to track growth and performance trends. `Revenue LY = CALCULATE([Revenue], SAMEPERIODLASTYEAR('sales_date'[date]))`

4. **Predictive Analytics and Forecasting (if implemented)**:

    - Developed models to predict future sales trends based on historical data, using Power BI’s built-in analytics capabilities or external tools like Python or R scripts integrated into Power BI.


### **Performance Optimization**
- **Query Performance**: Optimized data queries to improve dashboard responsiveness and loading times by minimizing data fetch sizes and using efficient DAX formulas.
- **Scheduled Updates**: Configured periodic data refreshes to ensure the dashboard remains updated with the latest data from the MySQL database.



## Key Insights and Analysis
### Overview of Key Measures
The following DAX measures were essential in uncovering insights from the sales data at AtliQ Hardware:

1. Total Revenue: This measure sums up the normalized sales amounts to provide the total revenue generated across all markets.

DAX:
``` 
Total Revenue = SUM('sales_transactions'[norm_sales_amount])
```
2. Profit Margin %: Calculated as the ratio of total profit to total revenue, this measure helps assess the efficiency of sales in generating profit.

DAX

```
Profit Margin % = DIVIDE([Total Profit Margin], [Total Revenue], 0)
```

3. Profit Margin Contribution %: This measure assesses the contribution of each region to the overall profit margin, considering their individual sales revenue contributions.

DAX
```
Profit Margin Contribution % = DIVIDE([Total Profit Margin], CALCULATE([Total Profit Margin], ALL('sales_products'), ALL('sales_customers'), ALL('sales_markets')))
```

4. Revenue Contribution %: Identifies what percentage of the total revenue is contributed by each market, providing insights into market performance relative to size.

DAX

```
Revenue Contribution % = DIVIDE([Revenue], CALCULATE([Revenue], ALL('sales_products'), ALL('sales_customers'), ALL('sales_markets')))
```
5. Revenue LY (Last Year): Compares the current year's revenue against the previous year’s to assess growth or decline.

DAX

```
Revenue LY = CALCULATE([Revenue], SAMEPERIODLASTYEAR('sales_date'[date]))
```

### Key Insights Derived

1. Profitability Variances Across Markets:

    - The analysis highlighted that markets like Bhubaneshwar, despite generating lower revenues, showed significantly higher profit margins compared to markets like Delhi. For instance, Bhubaneshwar had a profit margin of 10.5% compared to Delhi’s 0.6%. This was critical in identifying markets where sales strategies were highly efficient and could be mirrored in other regions.

        ![alt text](https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExdm9zM3lranQ2YXp0aG1ob2N4YnJ1NTFiOHlicWphZ255NzZ0bTV5aiZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/dvj1XtxaZM9R3VtW4P/giphy.gif)

2. Revenue vs. Profit Contribution Analysis:

    - Markets with high revenue did not always correspond to high profit contributions. For example, Mumbai, with comparatively lower revenue figures than Delhi, contributed more significantly to the profit margins. This insight was pivotal for reallocating marketing and sales efforts to optimize profitability.

        ![alt text](https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExcjl5M2Zpdm1kbTBoMnJtMmQ4emkzOG5mMDV0ejV1NnhmMDhwZWkxMyZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/PzCRYYgydnyudnj8cV/giphy.gif)

3. Dynamic Year-on-Year Sales Performance:

    - By comparing current sales data to the previous year's through the Revenue LY measure, significant insights into growth trends and performance metrics over time were obtained. This enabled strategic planning for inventory management, promotions, and sales forecasts.

4. Interactive Dashboard for Dynamic Insights:

    - The dashboard allowed users to dynamically adjust parameters like profit targets and view corresponding regions' performance in real-time. Using dynamic color coding based on performance relative to targets (e.g., regions not meeting profit targets highlighted in red) provided immediate visual feedback to users.

        ![alt text](https://i.giphy.com/media/v1.Y2lkPTc5MGI3NjExNGM4b2NmMnpyeG9qYjNrdWRtN3o3OGlpdGdlanJ2emFlOHFvOGRuNSZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/JLfRQ1gnjRDCtfaWLz/giphy.gif)

5. Strategic Decision-Making Based on Profit Margins:

    - Detailed analysis of profit margins helped in understanding which products or services are more profitable relative to their sales volume, aiding in strategic product placement and promotional efforts.


## Analysis Overview

These insights demonstrate the power of integrated data analysis within Power BI, where advanced DAX measures not only provide a deep dive into the current state of business but also enable predictive and strategic analysis to drive business decisions. The measures created and the insights derived from them help AtliQ Hardware to not only understand their current market dynamics but also to strategically plan for future growth and profitability enhancement




















