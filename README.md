# ⚡ Electric Vehicle Sales Analysis — India
### Codebasics Resume Project Challenge #12 | AtliQ Motors India Expansion Study

---

## 📌 Project Overview

AtliQ Motors is a leading US automotive company with a **25% market share** in North America's EV/Hybrid segment. As part of their India expansion strategy, Bruce Haryali (Chief, AtliQ Motors India) commissioned a comprehensive market study. This project delivers a **full data analysis and interactive Power BI dashboard** to support their India launch decision.

---

## 🎯 Problem Statement

> AtliQ Motors currently holds **less than 2% market share** in India. Before launching their bestselling EV models, they need deep insights into India's EV market — who's buying, where, how fast the market is growing, and where to focus first.

---

## 🗂️ Project Structure

```
EV-Sales-Analysis-India/
│
├── 📊 Dashboard/
│   ├── EV_project.pbix              # Power BI dashboard file
│   └── ev_background.png            # Custom dashboard background
│
├── 📁 Data/
│   ├── electric_vehicle_sales_by_state.csv
│   ├── electric_vehicle_sales_by_makers.csv
│   └── dim_date.csv
│
├── 📄 Reports/
│   ├── Primary_Questions_Answers.pdf
│   ├── Secondary_Research_Answers.pdf
│   └── DAX_Measures_Reference.xlsx
│
├── 🎬 Presentation/
│   └── Screen_Recording_Demo.mp4
│
└── README.md
```

---

## 📊 Dashboard Pages

### 🏠 Home Page
- AtliQ Motors branded landing page with dark teal theme
- Navigation buttons to all analysis pages
- Live EV penetration rate scroller

### 📈 Sales by Makers
- Total EVs Sold + Revenue KPIs (2W & 4W)
- Quarterly & Monthly sales trends (Top 5 makers)
- Top 5 makers by Market Share (EVs + Revenue)
- Market Share vs YoY Growth scatter plot
- CAGR for Top 5 EV Makers
- Dynamic Top/Bottom N slicer

### 🗺️ Sales by States
- Total Vehicles, EVs, Revenue, Projected 2030 KPIs
- 2030 Projected EV Sales with CAGR & Penetration combo chart
- Top 5 States by Penetration Rate (treemap)
- Statewise EV Penetration & YoY Decline table
- Comparative Growth Rate Analysis (2W EVs)
- CAGR for Top 5 States (Total Vehicles)
- Delhi vs Karnataka comparison

### 🔄 State Comparison
- Side-by-side state comparison with dropdown selectors
- 6 KPIs per state including Operational PCS (charging stations)
- EVs sold by category (2W + 4W)
- Revenue donut charts per category
- EV Sales vs Charging Stations scatter plot
- Statewise EV Sales + Operational PCS table

---

## 🔢 Key Metrics & Findings

| Metric | Value |
|--------|-------|
| Total EVs Sold (2022–2024) | 2.1 Million |
| Total Vehicles Sold | 57.2 Million |
| Overall EV Penetration Rate | 3.61% |
| EV Sales CAGR (2022–2024) | 93.91% |
| Top State by Volume | Maharashtra (3,96,045 units) |
| Top State by Penetration | Goa (13.75% — FY2024) |
| Top 2W Maker | OLA Electric (373% CAGR) |
| Top 4W Maker | Tata Motors (consistent #1) |
| 2W Market Share | 92.6% of all EV sales |
| Projected Total EV Sales 2030 | 54.2 Million |

---

## ❓ Primary Questions Answered

| # | Question | Key Finding |
|---|----------|-------------|
| Q1 | Top 3 & Bottom 3 2W Makers (FY2023 & FY2024) | OLA Electric dominates; Battre Electric bottom |
| Q2 | Top 5 States by Penetration Rate (FY2024) | Goa 17.99% (2W), Kerala 5.76% (4W) |
| Q3 | States with Negative Penetration Change | Ladakh (2W): -0.41%, Andaman (4W): -1.04% |
| Q4 | Quarterly Trends Top 5 4W Makers (2022–2024) | Tata Motors leads every single quarter |
| Q5 | Delhi vs Karnataka EV Sales & Penetration | Karnataka beats Delhi in both volume & rate |
| Q6 | CAGR Top 5 4W Makers (2022–2024) | BMW India leads at 1141% CAGR |
| Q7 | Top 10 States by CAGR — Total Vehicles | Meghalaya 28.47%, Goa 27.41% top the list |
| Q8 | Peak & Low Season Months | Peak: March (all years); Low: May/June |
| Q9 | Projected EV Sales 2030 — Top 10 States | Maharashtra 15.26M (2W), Karnataka 4.47M (4W) |
| Q10 | Revenue Growth Rate 2W & 4W | 4W grew faster: 131.6% YoY (2023→2024) |

---

## 🔬 Secondary Research Answers

| # | Question | Answer Summary |
|---|----------|----------------|
| S1 | Why customers choose 4W EVs | Cost savings, environment, govt incentives, tech |
| S2 | Govt incentives impact on adoption | FAME II: ₹11,500Cr subsidies. 50% YoY surge in 2023 |
| S3 | Charging station vs EV sales correlation | Strong: 0.91 correlation with EV sales |
| S4 | Ideal brand ambassador | MS Dhoni, Arijit Singh, Manu Bhaker |
| S5 | Best state for manufacturing | Maharashtra — #1 sales + infra + subsidies |
| S6 | Top 3 recommendations | 2W first → Maharashtra plant → Karnataka/Delhi |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|------|---------|
| **Power BI Desktop** | Dashboard development & visualization |
| **Power Query** | Data cleaning & transformation |
| **DAX** | Calculated measures & KPIs |
| **MySQL** | Initial data exploration & SQL analysis |
| **Python (Pandas)** | Data validation & cross-checking |
| **PowerPoint** | Dashboard background design |

---

## 📐 Data Model

```
dim_date ──────────────► EV_sales_by_state
    │                    (date → date, 1:Many)
    │
    └──────────────────► EV_sales_by_makers
                         (date → date, 1:Many)

dim_states ────────────► EV_sales_by_state
dim_makers ────────────► EV_sales_by_makers
dim_category ──────────► EV_sales_by_state + makers
Charging_units ────────► EV_sales_by_state (State)
```

---

## 🔑 Key DAX Measures

```dax
-- EV Penetration Rate
Penetration Rate % =
DIVIDE(
    SUM(EV_sales_by_state[electric_vehicles_sold]),
    SUM(EV_sales_by_state[total_vehicles_sold])
) * 100

-- CAGR
CAGR EV Sales =
VAR end = CALCULATE([Total EV Sales], dim_date[fiscal_year] = 2024)
VAR start = CALCULATE([Total EV Sales], dim_date[fiscal_year] = 2022)
RETURN IF(start > 0, (POWER(DIVIDE(end, start), 0.5) - 1) * 100, BLANK())

-- 2030 Projection
Projected EV Sales 2030 =
VAR cagr = [CAGR EV Sales] / 100
RETURN IF(cagr > 0, [Sales FY2024] * POWER(1 + cagr, 6), BLANK())

-- Revenue
Revenue Total =
SUMX(
    EV_sales_by_makers,
    EV_sales_by_makers[electric_vehicles_sold] *
    LOOKUPVALUE(Revenue[Average Price],
        Revenue[Vehicle_category],
        EV_sales_by_makers[vehicle_category])
)
```

---

## 💡 Strategic Recommendations for AtliQ Motors

### 1️⃣ Enter with 2-Wheeler EVs First
- 92.6% of India's EV market is 2-Wheelers (1.91M units)
- OLA Electric's 373% CAGR proves mass demand exists
- Lower price point = faster adoption and trust building
- Build in-house charging network for competitive advantage

### 2️⃣ Set Up Manufacturing in Maharashtra
- #1 in EV sales (3,96,045 units all-time)
- #1 in charging infrastructure (3,079 stations)
- 60% govt subsidy for slow chargers (up to ₹10K each)
- 50% subsidy for fast chargers (up to ₹5L each)
- 5-year warranty unlocks additional government support

### 3️⃣ Focus Market Penetration on Karnataka & Delhi
- Karnataka: 10.18% penetration rate — highest metro state
- Delhi: 100% road tax waiver + ₹30K subsidy on 2W
- Both states have strong EV policy ecosystems
- High urban awareness = premium segment opportunity

---

## 📁 Data Sources

| Dataset | Source |
|---------|--------|
| EV Sales by State | Vahan Sewa (Parivahan) |
| EV Sales by Makers | Vahan Sewa (Parivahan) |
| Public Charging Stations | Ministry of Heavy Industries / e-AMRIT |
| Date Dimension | Custom built for FY2022–FY2024 |

**Coverage Period:** April 2021 — March 2024 (FY2022 to FY2024)

---

## 🚀 How to Use the Dashboard

1. Open `EV_project.pbix` in Power BI Desktop
2. Verify data model connections in **Model View**
3. Use **fiscal year slicer** (top right) to filter by year
4. Use **vehicle category slicer** to toggle 2W / 4W
5. Use **filter icon** (top right corner) for advanced filters
6. Use **Top/Bottom N slider** to control how many makers/states show
7. Click **navigation buttons** to move between pages
8. Hover over any visual for detailed tooltips

---

## 📬 Connect With Me

Feel free to reach out for questions, feedback or collaboration!

> **Project submitted as part of Codebasics Resume Project Challenge #12**
> *Empowering data analysts with real-world business problems*

---

*⚡ Built with passion for data analytics and India's electric vehicle revolution*
