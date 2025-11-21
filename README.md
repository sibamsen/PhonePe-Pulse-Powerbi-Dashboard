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

📊 Key DAX (examples)

YoY Transactions %

YoY Txn % :=

VAR Prev = [Transactions PY]

RETURN IF(ISBLANK(Prev) || Prev = 0, BLANK(), DIVIDE([Total Transactions] - Prev, Prev))


CAGR Amount %

CAGR Amount % = 

VAR MinDate = CALCULATE(MIN('Dim_Date'[Date]), ALLSELECTED('Dim_Date')) 

VAR MaxDate = CALCULATE(MAX('Dim_Date'[Date]), ALLSELECTED('Dim_Date'))

VAR Years = DATEDIFF(MinDate, MaxDate, YEAR)

VAR FirstAmt =
    CALCULATE([Total Amount], ALL('Dim_Date'), 'Dim_Date'[Date] = MinDate)
    
VAR LastAmt =
    CALCULATE([Total Amount], ALL('Dim_Date'), 'Dim_Date'[Date] = MaxDate)
RETURN

IF(Years > 0 && FirstAmt > 0,
    (LastAmt / FirstAmt) ^ (1 / Years) - 1
)

---

📝 Key Insights (concise)

A few large states (e.g., Maharashtra, Karnataka) dominate transaction volume.

Category mix shows dominant payment types (P2P / merchant / recharges).

YoY highlights recent growth/decline; CAGR indicates long-term trend (can be negative if ending < starting).

Top-N slicer quickly surfaces highest contributing states.

▶ How to use

Download/open the .pbix file.

Put CSVs in data/ folder.

Refresh the model.

Use slicers (Year, Quarter, State, Metric, Top-N) to explore.

👨‍💻 Author

Sibam Sen
Data Visualization & Analytics Enthusiast
