# 🧹 Data Cleaning & Transformation — Supply Chain Analysis

> Step-by-step documentation of the data cleaning process applied to the raw Kaggle dataset.

---

## 📥 Source Data

| Property | Details |
|---|---|
| **Source** | [Kaggle — Supply Chain Analysis](https://www.kaggle.com/datasets/harshsingh2209/supply-chain-analysis) |
| **Format** | CSV → imported into Excel |
| **Raw Records** | 100 rows × 24 columns |
| **Tool Used** | Microsoft Excel |

---

## 🔄 Cleaning Workflow

```
Raw Data (24 cols)
    │
    ├── Step 1: Data Inspection
    ├── Step 2: Missing Value Handling
    ├── Step 3: Data Type Standardisation
    ├── Step 4: Derived Columns (4 new)
    │
    ▼
Clean Data (28 cols)
    │
    ├── Step 5: Lookup Table Creation
    ├── Step 6: Analysis Sheet (Calculated Fields)
    ├── Step 7: Pivot Summaries
    │
    ▼
Analysis Ready (30+ cols)
```

---

## 📋 Step-by-Step Process

### Step 1 — Data Inspection

**Objective:** Understand the raw dataset structure and identify quality issues.

**Actions:**
- Imported CSV into Excel as the `raw data` sheet
- Verified **100 rows** and **24 columns** loaded correctly
- Reviewed all column headers for naming consistency
- Checked for obvious anomalies in numeric ranges

**Findings:**
| Check | Status |
|---|---|
| Row count | ✅ 100 rows — matches source |
| Column count | ✅ 24 columns — matches source |
| Header formatting | ✅ Consistent title case |
| Duplicate SKUs | ✅ All unique (SKU0–SKU99) |

---

### Step 2 — Missing Value & Outlier Handling

**Objective:** Identify and handle null/blank values and outliers.

**Actions:**
- Scanned all columns for blank cells using `COUNTBLANK()`
- Checked numeric columns for negative values or extreme outliers
- Verified categorical columns have valid entries

**Key Decisions:**
| Column | Issue | Resolution |
|---|---|---|
| Defect rates | Some extreme values | Retained — reflect real-world variance |
| Customer demographics | "Unknown" category present | Retained as valid category |
| Inspection results | All showing "Pending" in sample | Kept as-is — reflects QC pipeline status |
| Revenue generated | Wide range (low to ~₹99K) | Retained — categorised into Revenue tiers |

---

### Step 3 — Data Type Standardisation

**Objective:** Ensure proper data types for analysis.

**Actions:**
| Column(s) | Original Type | Cleaned Type |
|---|---|---|
| Price, Revenue, Shipping costs, Manufacturing costs, Costs | Decimal (many d.p.) | Number (2 d.p.) |
| Availability, Stock levels, Lead times, Order quantities | Integer | Number (0 d.p.) |
| Shipping times, Production volumes, Mfg lead time | Integer | Number (0 d.p.) |
| Defect rates | Decimal (many d.p.) | Percentage (2 d.p.) |
| Product type, Supplier name, Location | Text | Text (trimmed) |
| SKU | Text (SKU0–SKU99) | Text |

---

### Step 4 — Derived Columns (Clean Data Sheet)

**Objective:** Enrich the dataset with calculated fields for analysis.

Created **4 new columns** in the `clean data` sheet (columns Y–AB):

#### 4a. Lead Time Category
```excel
=IF(P2<=15, "Short", IF(P2<=25, "Medium", "Long"))
```
| Category | Criteria | Purpose |
|---|---|---|
| Short | Lead time ≤ 15 days | Fast suppliers |
| Medium | 16–25 days | Average performance |
| Long | > 25 days | Slow / needs improvement |

#### 4b. Reliability Score
```excel
=VLOOKUP(N2, 'lookup tables'!A:D, 4, FALSE)
```
Pulled from the lookup tables sheet. Score ranges **1–10** based on supplier historical performance.

#### 4c. Defect Flag
```excel
=IF(U2>0, U2, 0)
```
Cleaned defect rate — ensures non-negative values.

#### 4d. Defect Rate (Clean)
```excel
=VLOOKUP(N2, 'lookup tables'!A:D, 3, FALSE)
```
Standardised defect rate lookup to ensure consistency across the same supplier.

---

### Step 5 — Lookup Table Creation

**Objective:** Create a reference table for supplier attributes.

Built the `lookup tables` sheet with **5 suppliers**:

| Supplier Name | Location | Lead Time Category | Reliability Score |
|---|---|---|---|
| Supplier 1 | Mumbai | Short | 8 |
| Supplier 2 | Kolkata | Medium | 6 |
| Supplier 3 | Mumbai | Short | 9 |
| Supplier 4 | Delhi | Medium | 7 |
| Supplier 5 | Bangalore | Long | 5 |

**Usage:** `VLOOKUP` joins from the clean data sheet to enrich records with supplier metadata.

---

### Step 6 — Analysis Sheet (Calculated Fields)

**Objective:** Build analysis-ready dataset with business logic columns.

Extended the clean data with **6+ calculated columns**:

#### 6a. Delivery Status
```excel
=IF(K2<=I2, "On Time", "Late")
```
Compares `Shipping times` vs `Lead times`.

#### 6b. Stock Status
```excel
=IF(H2>10, "OK", "Critical")
```
Flags products with dangerously low inventory (≤10 units).

#### 6c. Manufacturing Efficiency
```excel
=IF(R2<=P2, "Within lead time", "Exceeds lead time")
```
Compares `Manufacturing lead time` vs supplier `Lead time`.

#### 6d. Revenue Tier
```excel
=IF(F2>=7000, "High", IF(F2>=3000, "Medium", "Low"))
```
Segments products into revenue performance tiers.

#### 6e. Revenue by Type (Aggregated)
```excel
=SUMIFS(F:F, A:A, A2)
```
Total revenue for each product category.

#### 6f. Average Defect by Supplier (Aggregated)
```excel
=AVERAGEIFS(U:U, N:N, N2)
```
Mean defect rate per supplier for benchmarking.

#### 6g. Orders per Carrier (Aggregated)
```excel
=COUNTIFS(L:L, L2)
```
Count of orders handled by each carrier.

---

### Step 7 — Pivot Summaries

**Objective:** Create summary tables for quick reference and dashboard validation.

Built **3 pivot tables** in the `pivot summary` sheet:

#### Pivot 1: Revenue by Product Type
| Product Type | Revenue (₹) |
|---|---|
| Cosmetics | 161,521.27 |
| Haircare | 174,455.39 |
| Skincare | 241,628.16 |

#### Pivot 2: Average Shipping Time by Carrier
| Carrier | Avg Shipping Time (days) |
|---|---|
| Carrier A | 6.14 |
| Carrier B | 5.30 |
| Carrier C | 6.03 |

#### Pivot 3: Average Defect Rate by Supplier
| Supplier | Avg Defect Rate (%) |
|---|---|
| Supplier 1 | 1.80 |
| Supplier 2 | 2.36 |
| Supplier 3 | 2.47 |

---

## ✅ Data Quality Summary

| Metric | Before Cleaning | After Cleaning |
|---|---|---|
| **Columns** | 24 | 28 (clean) / 30+ (analysis) |
| **Rows** | 100 | 100 (no records dropped) |
| **Null values** | None detected | N/A |
| **Duplicates** | None (unique SKUs) | N/A |
| **Derived fields** | 0 | 10+ calculated columns |
| **Lookup tables** | 0 | 1 supplier reference table |
| **Pivot summaries** | 0 | 3 summary tables |

---

## 🔗 Sheet Flow Diagram

```
┌─────────────┐     ┌──────────────────┐     ┌───────────────┐
│  raw data   │────▶│   clean data     │────▶│   analysis    │
│  (24 cols)  │     │   (28 cols)      │     │   (30+ cols)  │
└─────────────┘     └──────────────────┘     └───────────────┘
                           │                        │
                    ┌──────▼──────┐          ┌──────▼──────┐
                    │   lookup    │          │   pivot     │
                    │   tables    │          │   summary   │
                    └─────────────┘          └─────────────┘
                                                    │
                                             ┌──────▼──────┐
                                             │  Power BI   │
                                             │  Dashboard  │
                                             └─────────────┘
```

---

*Documentation by Abhishek Biradar*
