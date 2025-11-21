# 📊 PhonePe Pulse Analytics Dashboard (Power BI)

A clean, interactive Power BI dashboard analyzing India’s digital payment trends (2018–2022) using the official **PhonePe Pulse** dataset. The report highlights how transaction behavior evolves across states, categories, and time.

---

## 🚀 Overview

This project delivers clear, data-driven insights on:

- Total Transaction Amount & Count  
- State-wise performance (Shape Map)  
- Year-wise & Quarter-wise trends  
- Category-wise breakdown  
- Brand-wise usage  
- Top-N state comparison  
- KPI metrics: YoY Growth %, CAGR %, Average Ticket Size  

The design is optimized for **professional use**, **portfolio display**, and **HR-friendly review**.

---

## 🛠 Tech Used

- **Power BI Desktop**  
- **Power Query** (ETL)  
- **DAX Measures**  
- **CSV datasets from PhonePe Pulse**  
- **India TopoJSON** (Shape Map)

---

## 📁 Dataset

Place the following CSV files in a `data/` folder:

aggregated_transaction.csv
aggregated_user.csv
map_transaction.csv
map_user.csv
top_transaction.csv
top_user.csv

diff
Copy code

Dataset includes state-level, category-level, and brand-level payment metrics.

---

## 🧩 Data Model

Structured as a **Star Schema**:

**Facts:**  
- aggregated_transaction  
- aggregated_user  
- map_transaction  
- map_user  
- top_transaction  
- top_user  

**Dimensions:**  
- Dim_Date (Calendar)  
- Dim_Geo (States)  
- Dim_Brand  
- Metric Selector  
- TopN Selector  

Key relationship:  
Dim_Date[Date] → Fact[PeriodStart]

yaml
Copy code

---

## 📈 Core Features

- 📌 **KPI Cards:** Total Amount, Registered Users, Avg Ticket Size, YoY %, CAGR %  
- 🗺 **Map:** State-wise intensity visualization  
- 📊 **Trends:** Year-wise transaction counts  
- 🧩 **Categories:** Treemap for transaction types  
- 🔝 **Top N States:** Dynamic ranking using What-If parameter  
- 🧾 **Brand Table:** Sorted by usage metrics  
- 🎨 **UI/UX:** Clean whitespace, soft shadows, PhonePe theme  

---

## 📊 Key DAX Metrics

### YoY Transactions %
```dax
YoY Transactions % :=
VAR Prev = [Transactions PY (YQ Robust)]
RETURN
IF(ISBLANK(Prev) || Prev = 0, BLANK(), DIVIDE([Total Transactions] - Prev, Prev))
CAGR Amount %
dax
Copy code
CAGR Amount % :=
VAR MinY = MIN('Dim_Date'[Year])
VAR MaxY = MAX('Dim_Date'[Year])
VAR Years = MaxY - MinY
VAR FirstAmt = CALCULATE([Total Amount], ALL('Dim_Date'), 'Dim_Date'[Year] = MinY)
VAR LastAmt  = CALCULATE([Total Amount], ALL('Dim_Date'), 'Dim_Date'[Year] = MaxY)
RETURN IF(Years > 0 && FirstAmt > 0, (LastAmt / FirstAmt) ^ (1/Years) - 1, BLANK())
📝 Insights (High-Level)
Southern states and Maharashtra dominate digital transactions.

Category distribution reveals major usage patterns (e.g., P2P, recharge, merchant payments).

Several states show positive YoY growth even if long-term CAGR dips.

Seasonal trends are visible across quarters.

▶ Usage
Download the .pbix file

Place CSVs into data/ folder

Open in Power BI

Click Refresh

Explore with filters & slicers

👨‍💻 Author
Sibam Sen
Data Visualization & Analytics Enthusiast
