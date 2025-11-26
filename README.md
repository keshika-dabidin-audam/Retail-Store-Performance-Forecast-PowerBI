📊 Retail Store Performance & Forecasting – Power BI Project
📌 Project Overview

This project is an end-to-end Business Intelligence (BI) solution built with Power BI to analyze and forecast the performance of a network of retail stores.

It combines:

Sales data

Customer footfall

Satisfaction feedback

Calendar intelligence

…and transforms them into:

Executive-level KPIs

Store-level insights

Product category analysis

Revenue forecasting with uncertainty bands

The goal is to provide business leaders with a clear, interactive view of store performance and short-term revenue evolution.

🗂 Data Model & Architecture
⭐ Star Schema

The model follows a clean star-schema to optimize DAX and filtering logic.

Fact Table
Table	Description
sales	Contains all daily sales transactions: date, store, product, category, quantity, revenue
Dimension Tables
Table	Description
stores	Metadata: store name, city, region, staff count
footfall	Daily store visitors
feedback	Satisfaction score (1–5) per store and date
DateTable	Calendar table: Date, Year, Month, MonthName, YearMonth
📌 Data Model Screenshot

screenshots/data-model.png
(Replace with your real path)

📈 Key Metrics (KPIs)
Sales KPIs

Total Revenue

Total Quantity Sold

Total Visitors (Footfall)

Conversion Rate (%)

Quantity / Visitors

Average Satisfaction

Forecast KPIs

Revenue Last 3 Months

Projected Revenue Next 3 Months

Trend 3 Months (%)

Forecasted evolution based on DAX linear trend model

🧮 DAX Measures (Core)
Revenue Last 3 Months
Revenue Last 3 Months =
CALCULATE(
    [Total Revenue],
    DATESINPERIOD(DateTable[Date], MAX(DateTable[Date]), -3, MONTH)
)

Projected Next 3 Months
Projected Next 3 Months =
VAR LastMonth =
    CALCULATE([Total Revenue], DATEADD(DateTable[Date], -1, MONTH))
VAR PrevMonth =
    CALCULATE([Total Revenue], DATEADD(DateTable[Date], -2, MONTH))
VAR Trend = DIVIDE(LastMonth - PrevMonth, PrevMonth)
RETURN LastMonth * (1 + Trend)

Trend 3 Months (%)
Trend 3 Months (%) =
DIVIDE(
    [Projected Next 3 Months] - [Revenue Last 3 Months],
    [Revenue Last 3 Months]
)

🖥 Power BI Report Pages
1️⃣ Global Overview

Screenshot: screenshots/global-overview.png

Includes:

Total Revenue

Total Quantity

Total Visitors

Conversion Rate (%)

Average Satisfaction

Revenue by Date (Line Chart)

Top Stores by Revenue (Bar Chart)

Region slicer

Date range timeline

🎯 Purpose

Provide an executive snapshot for management.

2️⃣ Store Analysis

Screenshot: screenshots/store-analysis.png

Includes:

Store Name slicer

Revenue by Category

Satisfaction vs Revenue (Correlation scatter)

Daily performance table

🎯 Purpose

Deep-dive into each store’s performance.

3️⃣ Forecast Page

Screenshot: screenshots/forecast-page.png

Includes:

Revenue line chart with trendline

Power BI forecast model + confidence band

Region slicer

KPIs:

Revenue Last 3 Months

Projected Next 3 Months

Trend 3 Months (%)

🎯 Purpose

Predict short-term evolution for decision-making.

🔮 Forecast Logic

This project uses two forecasting approaches:

1. Power BI Built-In Forecast

Automatically detects seasonality

Generates a prediction curve + confidence interval

Applied directly on the line chart

2. Custom DAX Forecast Model

A simple linear trend based on the difference between the last 2 months:

If LastMonth > PrevMonth → upward trend

Else → downward trend

This allows:

Cleaner KPI comparison

Transparent logic

Region-based forecasting

💡 Insights Extracted

Revenue trend indicates moderate growth (~2–4% depending on region).

There is a positive correlation between satisfaction and revenue.

The West region consistently outperforms others.

Some stores with high footfall still underperform → optimization potential.

Product categories differ strongly in revenue contribution.

🛠 Tech Stack
Tool	Usage
Power BI Desktop	Dashboard & KPIs
Power Query	Data preparation
DAX	Measures and time intelligence
Python	Data generation (optional)
GitHub	Version control & portfolio
📁 Repository Structure
Retail-Store-Performance-Forecast-PowerBI/
│
├── data/
├── reports/
├── src/
│   └── generate_data.py (optional)
│
└── README.md

🚀 How to Run This Project

Clone the repo:

git clone https://github.com/<your-username>/Retail-Store-Performance-Forecast-PowerBI.git


Open:

reports/PowerBI_Retail_Forecast.pbix


Ensure data paths are correct

Refresh the report

⭐ Future Improvements

Add Year-over-Year (YoY) metrics

Add RLS (Row Level Security) per region

Include external data (weather, promotions)

Use Python Prophet for advanced forecasting

Automate data refresh with a pipeline

👩‍💻 Author

Keshika Dabidin Audam
Data Analyst / Data Scientist – Mauritius 🇲🇺
