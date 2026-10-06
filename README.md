# 📦 Supply Chain Performance Analysis

> End-to-end supply chain analytics project using Excel and Power BI | Kaggle dataset

![Dashboard Preview](dashboard/Full_Dashboard.png)

---

## 📋 Project Overview

An end-to-end supply chain analytics project analysing **100 products** across **5 suppliers**, **3 carriers**, and **4 Indian cities**. Built using Microsoft Excel (6-sheet workbook) and Power BI Desktop, this project covers the full analyst workflow from raw data cleaning to interactive dashboard.

| | |
|---|---|
| **Dataset** | [Supply Chain Analysis — Kaggle](https://www.kaggle.com/datasets/harshsingh2209/supply-chain-analysis) |
| **Tools** | Microsoft Excel · Power BI Desktop |
| **Author** | Abhishek Biradar |

---

## 🔑 Key Findings

| KPI | Value |
|---|---|
| **Total Revenue** | ₹577.60K |
| **Total Orders** | 100 |
| **Avg Defect Rate** | 2.28% |
| **Avg Shipping Time** | 5.75 days |

### Revenue Insights
- **Skincare** leads revenue generation (~₹241.6K), followed by **Haircare** (~₹174.5K) and **Cosmetics** (~₹161.5K)
- **High-revenue** products dominate the revenue tier distribution
- **Road** and **Rail** transport generate the highest revenue across all product types

### Logistics & Operations
- **Carrier A** has the highest average shipping time (~6.14 days), while **Carrier B** is the fastest (~5.30 days)
- Delivery status analysis reveals both **On Time** and **Late** deliveries across all carriers
- **Sea** and **Air** transport modes handle significant revenue alongside Road and Rail

### Supplier Quality
- **Supplier 1** (Mumbai) has the lowest average defect rate (~1.80%), with a **Reliability Score of 8**
- **Supplier 3** (Mumbai) has the highest defect rate (~2.47%) but the highest **Reliability Score of 9**
- Suppliers are distributed across **Mumbai, Delhi, Kolkata, Bangalore, and Chennai**

---

## 📊 Dashboard Pages

The Power BI dashboard contains visual analyses covering:

| Page | Focus Area | Key Visuals |
|---|---|---|
| **Executive Overview** | KPIs, revenue by product type, defect rate treemap | Card visuals, bar charts, donut chart |
| **Logistics & Operations** | Shipping times, delivery status, transport mode analysis | Bar charts, line chart, stacked bar |
| **Supplier Quality** | Defect rates by supplier, location map, reliability | Treemap, Bing map, bar charts |

### Dashboard Screenshots

| Executive Overview | Full Dashboard |
|---|---|
| ![Page 1](dashboard/Full_Dashboard.png) | ![Full](dashboard/Full_Dashboard.png) |

---

## 🗂️ Project Structure

```
supply-chain-performance-analysis/
│
├── data/
│   └── Supply_Chain_Analysis.xlsx      # 6-sheet Excel workbook (raw → clean → analysis)
│
├── dashboard/
│   └── Full_Dashboard.png              # Power BI dashboard screenshot
│
├── documentation/
│   ├── DAX_Measures.md                 # All DAX measures used in the dashboard
│   └── Data_Cleaning.md               # Data cleaning & transformation steps
│
└── README.md                           # This file
```

---

## 📑 Data Dictionary

The Excel workbook contains **6 sheets**:

### 1. Raw Data (100 rows × 24 columns)
| Column | Description | Example |
|---|---|---|
| Product type | Product category | haircare, skincare, cosmetics |
| SKU | Stock Keeping Unit identifier | SKU0, SKU1, ... SKU99 |
| Price | Unit price (₹) | 69.81 |
| Availability | Product availability score | 55 |
| Number of products sold | Units sold | 802 |
| Revenue generated | Revenue in ₹ | 8,661.99 |
| Customer demographics | Customer segment | Male, Female, Non-binary, Unknown |
| Stock levels | Current stock level | 58 |
| Lead times | Order lead time (days) | 7 |
| Order quantities | Quantity per order | 96 |
| Shipping times | Shipping duration (days) | 4 |
| Shipping carriers | Carrier name | Carrier A, B, C |
| Shipping costs | Cost of shipping (₹) | 2.96 |
| Supplier name | Supplier identifier | Supplier 1–5 |
| Location | Supplier city | Mumbai, Delhi, Kolkata, Bangalore, Chennai |
| Lead time | Supplier lead time (days) | 29 |
| Production volumes | Units produced | 215 |
| Manufacturing lead time | Mfg lead time (days) | 29 |
| Manufacturing costs | Cost per unit (₹) | 46.28 |
| Inspection results | QC status | Pending, Pass, Fail |
| Defect rates | Defect rate (%) | 0.23 |
| Transportation modes | Shipping mode | Road, Air, Rail, Sea |
| Routes | Route identifier | Route A, B, C |
| Costs | Transport cost (₹) | 187.75 |

### 2. Clean Data (100 rows × 28 columns)
All raw data columns plus **4 derived columns**:
- `Lead time category` — Short / Medium / Long
- `Reliability score` — Supplier reliability (1–10)
- `Defect flag` — Cleaned defect rate
- `Defect rate (clean)` — Standardised defect rate

### 3. Lookup Tables (5 rows × 4 columns)
Supplier reference table with location, lead time category, and reliability score.

### 4. Analysis (100+ rows × 30+ columns)
Extended dataset with calculated fields:
- `Delivery status` — On Time / Late
- `Stock status` — OK / Critical
- `Mfg efficiency` — Within lead time / Exceeds lead time
- `Revenue tier` — High / Medium / Low
- Aggregated metrics: Revenue by type, Avg defect by supplier, Orders per carrier

### 5. Pivot Summary
Summary pivot tables for:
- Revenue by product type
- Average shipping times by carrier
- Average defect rates by supplier

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Microsoft Excel** | Data cleaning, transformation, lookup tables, pivot analysis |
| **Power BI Desktop** | Interactive dashboard, DAX measures, data visualisation |
| **Kaggle** | Source dataset |

---

## 🚀 How to Use

1. **Clone the repository**
   ```bash
   git clone https://github.com/ABHI-2802/supply-chain-analytics.git
   ```

2. **Explore the data** — Open `data/Supply_Chain_Analysis.xlsx` in Excel to see the full 6-sheet workflow

3. **View the dashboard** — Open the `.pbix` file in Power BI Desktop (if included), or refer to the screenshots in `dashboard/`

4. **Review documentation** — Check `documentation/` for DAX measures and data cleaning methodology

---

## 📄 License

This project is for educational and portfolio purposes. Dataset sourced from [Kaggle](https://www.kaggle.com/datasets/harshsingh2209/supply-chain-analysis).

---

*Built with 📊 by [Abhishek Biradar](https://github.com/ABHI-2802)*
