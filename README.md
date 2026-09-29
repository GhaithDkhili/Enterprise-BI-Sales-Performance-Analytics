# Enterprise-BI-Sales-Performance-Analytics
An end-to-end Business Intelligence project built with Microsoft Power
BI to transform transactional sales data into an interactive
analytical reporting solution.

Project Overview

The objective is to build a management-oriented BI solution that answers
key business questions:

How much revenue is being generated?

How much gross profit is being generated?

How is profitability changing over time?

Which products and categories contribute most to revenue and profit?

Which countries/territories generate the strongest results?

How do sales volume and profitability differ across products?

Where should management investigate further?

The report combines dimensional modeling, Power Query, DAX, time
intelligence, KPI reporting and interactive dashboard design.

Dataset

The project uses Microsoft's AdventureWorks Sales sample dataset.

Official dataset:
https://github.com/microsoft/powerbi-desktop-samples/raw/refs/heads/main/AdventureWorks%20Sales%20Sample/AdventureWorks%20Sales.xlsx

Microsoft dimensional modeling guidance:
https://learn.microsoft.com/en-us/power-bi/create-reports/desktop-dimensional-model-report

Data Model

The solution follows a star-schema / dimensional modeling approach.

                    DimDate
                       |
DimCustomer ----> FactSales <---- DimTerritory
                       |
                  DimProduct
                       |
              DimSubcategory
                       |
                  DimCategory

FactSales

The central transactional table contains sales-order line information
such as Sales Order Number, Sales Order Line Number, Order Date, Product
Key, Customer Key, Territory Key, Order Quantity, Unit Price, Sales
Amount and Total Product Cost.

Dimensions

Dimension               Purpose

DimDate                 Time and fiscal-year analysis
DimProduct              Product-level analysis
DimProductSubcategory   Subcategory analysis
DimProductCategory      Category analysis
DimCustomer             Customer analysis
DimTerritory            Geographic analysis

Data Preparation

The preparation process was performed in Power BI using Power Query:

Import the AdventureWorks workbook.

Select the relevant analytical tables.

Inspect column names and data types.

Validate date and numeric fields.

Check dimension keys and relationships.

Review blanks and data-quality issues.

Load the prepared tables into the Power BI model.

DAX Measures

Total Sales

TotalSales =
SUM(FactSales[SalesAmount])

Total Costs

TotalCosts =
SUM(FactSales[TotalProductCost])

Gross Profit

GrossProfit =
[TotalSales] - [TotalCosts]

Profit Margin

Profit Margin % =
DIVIDE([GrossProfit], [TotalSales])

Total Orders

Total Orders =
DISTINCTCOUNT(FactSales[SalesOrderNumber])

Units Sold

UnitSold =
SUM(FactSales[OrderQuantity])

Average Order Value

AverageOrderValue =
DIVIDE([TotalSales], [Total Orders])

Sales Previous Year

Sales LY =
CALCULATE(
    [TotalSales],
    SAMEPERIODLASTYEAR(DimDate[Date])
)

Sales YoY Growth

YoY Growth % =
DIVIDE(
    [TotalSales] - [Sales LY],
    [Sales LY]
)

Profit Previous Year

Profit LY =
CALCULATE(
    [GrossProfit],
    SAMEPERIODLASTYEAR(DimDate[Date])
)

Profit YoY Growth

Profit YoY Growth % =
DIVIDE(
    [GrossProfit] - [Profit LY],
    [Profit LY]
)

Time-intelligence note: Profit YoY Growth % requires a meaningful
date context. With a specific fiscal year selected, it compares that
period with the equivalent prior-year period. With all fiscal years
selected, there is no single current period for a one-year comparison,
so the measure may return BLANK.

Report Structure

1. Executive Overview

High-level KPIs and overall sales performance: - Total Sales - Gross
Profit - Profit Margin - Total Orders - Sales Trend - Sales by Product
Category - Sales by Country

2. Sales Performance

Total Sales

Units Sold

Total Orders

Average Order Value

Sales Trend

Sales by Category

Sales by Country

Top 10 Products by Sales

3. Customer & Product Analysis

Sales by Product Category

Sales by Subcategory

Top 10 Products

Geographic performance

Product-level performance matrix

Category → Subcategory → Product drill-down

4. Profitability Analysis

KPIs: - Total Revenue - Gross Profit - Profit Margin % - Profit YoY
Growth %

Visuals: - Revenue & Gross Profit Trend - Gross Profit by Product
Category - Gross Profit by Country - Top 10 Products by Gross Profit -
Sales vs Profitability by Product - Profitability by Category & Product
matrix

Interactivity

Typical slicers include: - Date - Fiscal Year - Product - Country -
Product Category - Product Subcategory

The report uses cross-filtering and drill-down to allow users to move
from management-level KPIs to detailed product and geographic analysis.

Key Business Metrics

Metric                Definition

Total Sales           Sum of sales amount
Total Costs           Sum of product costs
Gross Profit          Total Sales − Total Costs
Profit Margin         Gross Profit ÷ Total Sales
Total Orders          Distinct number of sales orders
Units Sold            Total quantity sold
Average Order Value   Total Sales ÷ Total Orders
Sales YoY Growth      Current-period revenue vs prior-year period
Profit YoY Growth     Current-period gross profit vs prior-year period

Technologies & Skills

Microsoft Power BI

DAX

Power Query

Dimensional / Star Schema Modeling

Data Transformation

Time Intelligence

KPI Development

Business Performance Analysis

Interactive Dashboard Design

Data Visualization

Drill-down Reporting

Top-N Analysis

Profitability Analysis

Project Architecture

Raw Sales Data
      ↓
Power Query
      ↓
Data Cleaning & Validation
      ↓
Dimensional Data Model
      ↓
DAX Measures
      ↓
Power BI Semantic Layer
      ↓
Interactive Report
      ↓
Business Insights

Validation & Testing

The report was tested using different filtering scenarios, including
fiscal-year, country, product and category selections.

Business calculations were validated by checking: - Gross Profit = Total
Sales − Total Costs - Profit Margin = Gross Profit ÷ Total Sales -
Average Order Value = Total Sales ÷ Total Orders - YoY calculations
against the equivalent prior-year period
