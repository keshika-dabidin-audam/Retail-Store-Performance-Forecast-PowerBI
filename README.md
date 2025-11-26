# 📊 Retail Store Performance & Forecasting – Power BI Project

## 📌 Project Overview  
This project is an end-to-end **Business Intelligence (BI)** solution built with **Power BI** to analyze and forecast the performance of a network of retail stores.

It integrates:

- **Sales data**
- **Store footfall**
- **Customer satisfaction scores**
- **A calendar table (DateTable)**

…to produce:

- Executive KPIs  
- Store-level deep-dive analysis  
- Product category insights  
- A forecasting page with trendline & uncertainty interval  

The aim is to give business leaders a clear view of store performance and expected revenue evolution.

---

# 🗂 Data Model & Architecture

## ⭐ Star Schema
The model is structured using a clean star schema with one fact table and multiple dimensions.

### 🟦 Fact Table: `sales`
Contains all daily transactions:
- date  
- store_id  
- product  
- category  
- quantity  
- revenue  

### 🟨 Dimension Tables
| Table | Description |
|-------|-------------|
| **stores** | Metadata: store name, city, region, staff_count |
| **footfall** | Daily store visitors |
| **feedback** | Satisfaction score per store/day |
| **DateTable** | Calendar: Date, Year, Month, MonthName, YearMonth |

### 📌 Data Model Screenshot
`/screenshots/data-model.png`

---

# 📈 KPIs (Key Measures)

### **Sales KPIs**
- Total Revenue  
- Total Quantity Sold  
- Total Visitors  
- Conversion Rate (Units)  
- Average Satisfaction  

### **Forecast KPIs**
- Revenue Last 3 Months  
- Projected Next 3 Months  
- Trend 3 Months (%)  

---
---
# 🧮 Core DAX Measures

### Revenue Last 3 Months
```DAX
Revenue Last 3 Months =
CALCULATE(
    [Total Revenue],
    DATESINPERIOD(DateTable[Date], MAX(DateTable[Date]), -3, MONTH)
)
```

### Projected Next 3 Months =
```DAX
VAR LastMonth =
    CALCULATE([Total Revenue], DATEADD(DateTable[Date], -1, MONTH))
VAR PrevMonth =
    CALCULATE([Total Revenue], DATEADD(DateTable[Date], -2, MONTH))
VAR Trend = DIVIDE(LastMonth - PrevMonth, PrevMonth)
RETURN LastMonth * (1 + Trend)
```

### Trend 3 Months (%) =
```DAX
DIVIDE(
    [Projected Next 3 Months] - [Revenue Last 3 Months],
    [Revenue Last 3 Months]
)
```
---

#🖥 Power BI Report Pages

##1️⃣ Global Overview

Screenshot:
'/screenshots/global-overview.png'

Includes:

-Total Revenue

- Total Quantity

- Total Visitors

- Conversion Rate

- Average Satisfaction

- Revenue by Date (line chart)

- Top Stores (bar chart)

- Region slicer

- Date timeline filter

🎯 Purpose : Provide management with a complete performance snapshot.

##2️⃣ Store Analysis

Screenshot:
'/screenshots/store-analysis.png'

Includes:

- Store name slicer

- Revenue by product category

- Satisfaction vs Revenue scatter plot

- Daily performance table

🎯 Purpose : Deep-dive into each store’s strengths, weaknesses, and customer satisfaction effects.

##3️⃣ Forecast Page

Screenshot:
'/screenshots/forecast-page.png'

Includes:

  Revenue line chart

- Trendline

- Power BI forecast (confidence interval)

- Region slicer

- KPI cards:

Revenue Last 3 Months

Projected Next 3 Months

Trend 3 Months (%)

🎯 Purpose : Predict short-term revenue evolution, detect early growth/decline trends.

---

#🔮 Forecast Logic

This project uses two forecasting approaches:

1. **Power BI Built-In Forecast**

Adds a prediction line and shaded confidence interval directly in the visual.

2. **Custom DAX Linear Trend Model**

A transparent, easy-to-interpret approach:

- Measure last month

- Measure previous month

- Compute growth

- Apply it forward

Used for KPI cards.

---

#💡 Key Insights

- Revenue shows a moderate upward trend in the next quarter.

- West region remains the most stable and high-performing area.

- Stores with higher satisfaction tend to generate higher revenue.

- Some high-footfall stores show low conversion → improvement potential.

---

#🛠 Tech Stack
| Tool                 | Purpose                       |
| -------------------- | ----------------------------- |
| **Power BI Desktop** | Main analytics & visuals      |
| **Power Query**      | ETL, cleaning, transformation |
| **DAX**              | Calculations & KPIs           |
| **Python**           | Data generation (optional)    |
| **GitHub**           | Version control & portfolio   |

---

#📁 Repository Structure
Retail-Store-Performance-Forecast-PowerBI/
│
├── data/
│   ├── sales.csv
│   ├── stores.csv
│   ├── footfall.csv
│   ├── feedback.csv
│   └── DateTable.csv
│
├── reports/
│   ├── PowerBI_Retail_Forecast.pbix
│
├── screenshots/
│   ├── Screenshots.pdf
├── src/
│   └── generate_data.py   # optional
│
└── README.md

#🚀 How to Run This Project

1.** Clone the repository**
git clone https://github.com/<your-username>/Retail-Store-Performance-Forecast-PowerBI.git

2. **Open the Power BI file**
reports/PowerBI_Retail_Forecast.pbix


#⭐ Future Enhancements

- Add Year-over-Year (YoY) revenue comparison

- Add Row Level Security (RLS) by region

- Integrate promotion or weather data to improve forecasting

- Build advanced predictive models using Python (Prophet, ARIMA)

- Automate refresh using Power BI Service

#👩‍💻 Author

*Keshika Dabidin Audam*
