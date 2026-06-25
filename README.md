# 📦 Sales Pulse — End-to-End Sales Analytics & Profitability Prediction

> From raw data to interactive dashboard to machine learning — a full data analytics pipeline built on a real-world wholesale sales dataset.

---

## 🗂️ Project Overview

This project covers the complete data analytics workflow:

1. **Data Cleaning** — raw CSV files cleaned and standardized with Python (Pandas)
2. **Machine Learning** — Linear Regression model that predicts whether a sale will be High or Low profit
3. **Interactive Dashboard** — Power BI dashboard visualizing sales performance across 4 analytical pages

---

## 🧾 Project Structure

```
├── cleandata.ipynb          # Data cleaning pipeline (Python / Pandas)
├── LR_model.ipynb           # Profitability prediction model (Scikit-learn)
├── Final_Dashboard.pbix     # Interactive Power BI dashboard
├── data/
│   ├── FactSale.csv
│   ├── DimCustomer.csv
│   ├── DimCity.csv
│   ├── DimStockItem.csv
│   ├── DimDate.csv
│   └── employee.csv
└── README.md
```

---

## ⚙️ Step 1 — Data Cleaning (`cleandata.ipynb`)

Loads 6 raw CSV files and applies targeted cleaning to each:

| Table | Cleaning Applied |
|---|---|
| `FactSale` | Parsed invoice & delivery dates, removed rows with quantity ≤ 0 |
| `DimCustomer` | Stripped whitespace from columns, cleaned & converted `Credit Limit` to numeric |
| `DimStockItem` | Stripped whitespace, cleaned `Unit Price` and `Recommended Retail Price`, dropped `Color` column |
| `DimEmployee` | Stripped whitespace, dropped `Photo` column, cast `Is Salesperson` to boolean |
| `DimDate` | Parsed dates, extracted `Year` and `Month_Name` columns |
| `DimCity` | Standardized and exported as-is |

**Output:** 6 cleaned CSVs ready for modelling and dashboarding.

---

## 🤖 Step 2 — Profitability Prediction Model (`LR_model.ipynb`)

A binary classification model that predicts whether a transaction will result in **High** or **Low** profit.

**Libraries:** `Pandas`, `NumPy`, `Matplotlib`, `Seaborn`, `Scikit-learn`

**Approach:**
- Merges `Cleaned_FactSale`, `Cleaned_StockItem`, and `Cleaned_DimCustomer`
- Target variable: `Profit > median(Profit)` → 1 (High), 0 (Low)
- Features used:

| Feature | Description |
|---|---|
| `Quantity` | Number of units in the transaction |
| `Unit Price` | Selling price per unit |
| `Recommended Retail Price` | RRP of the stock item |
| `Credit Limit` | Customer's credit limit |

- Train/Test split: **80% / 20%** (`random_state=42`)
- Model: **Linear Regression** used as a classifier (threshold = 0.5)
- Evaluation: **Confusion Matrix** (heatmap) + **Accuracy Score** + **Classification Report**

---

## 📊 Step 3 — Power BI Dashboard (`Final_Dashboard.pbix`)

An interactive 4-page dashboard built on the cleaned data.

### Page 1 — Sales Overview
- **KPI Cards** — Total Sales, Total Profit, Total Orders
- **Line Chart** — Total Sales trend by Month
- **Treemap** — Sales by City
- **Donut Chart** — Profit breakdown by Category
- **Slicer** — Filter by Year

### Page 2 — Product Performance
- **Clustered Bar Chart** — Total Sales by Stock Item
- **Column Chart** — Sales by Category, Buying Group & Buying Package
- **Scatter Chart** — Sales vs Profit per Stock Item (identify high-revenue/low-margin products)
- **Pie Chart** — Chiller vs Non-Chiller stock split
- **Clustered Column Chart** — Monthly sales trend
- **Slicers** — Filter by Package type and Weight

### Page 3 — Teams & Customers
- **Funnel Chart** — Total Sales by Employee (sales team ranking)
- **Bar Chart** — Total Sales by Customer
- **Table** — Customer details: Name, Total Sales, Credit Limit
- **Multi-Row Card** — Employee ranking by Sales and City
- **Treemap** — Package distribution
- **Slicers** — Filter by City and Date range

### Page 4 — Summary
- **KPI Cards** — Total Orders, Sales Last Year (LY), Average Order Value, and additional business KPIs

---

## 🗃️ Data Model

Based on a **star schema** (Wide World Importers-style wholesale dataset):

| Table | Key Columns |
|---|---|
| `FactSale` | Quantity, Profit, Invoice Date, Delivery Date |
| `DimCustomer` | Customer, City, Category, Buying Group, Credit Limit |
| `DimStockItem` | Stock Item, Unit Price, RRP, Package, Is Chiller Stock |
| `DimDate` | Date, Month Name, Year |
| `DimEmployee` | Employee, Is Salesperson |
| `DimCity` | City |

---

## 🚀 How to Run

### Notebooks
```bash
pip install pandas numpy matplotlib seaborn scikit-learn
jupyter notebook
```
Run `cleandata.ipynb` first, then `LR_model.ipynb`.

### Dashboard
1. Download and open `Final_Dashboard.pbix` in [Power BI Desktop](https://powerbi.microsoft.com/desktop/) (free)
2. Use the page tabs and slicers to explore the data interactively

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| Python | Data cleaning & machine learning |
| Pandas & NumPy | Data wrangling |
| Scikit-learn | ML model & evaluation |
| Matplotlib & Seaborn | Visualization inside notebooks |
| Power BI | Interactive business dashboard |

---

## 💡 Key Insights the Project Answers

- Which cities and categories generate the most sales and profit?
- Which sales reps are top performers?
- Which stock items are high-revenue but low-margin?
- Can we predict whether a transaction will be profitable based on pricing and customer data?
- How do sales compare year-over-year?

---

## 📄 License

Free to use for learning and portfolio purposes. Attribution appreciated.
