# 🛒 Store Sales Analysis

Exploratory data analysis (EDA) on retail store transaction data, covering data cleaning, feature engineering, outlier detection, and sales visualizations.

---

## 📁 Project Structure

```
├── store.csv           # Raw input data
├── analysis.ipynb      # Main analysis notebook
└── report.csv          # Cleaned output dataset
```

---

## 📦 Requirements

Install dependencies with:

```bash
pip install pandas numpy matplotlib seaborn
```

---

## 🗂️ Dataset

The dataset (`store.csv`) contains retail order records with the following fields:

| Column | Description |
|---|---|
| `order_id` | Unique order identifier |
| `order_date` / `ship_date` | Order and shipping timestamps |
| `ship_mode` | Shipping method used |
| `customer_id` / `customer_name` | Customer identifiers |
| `segment` | Customer segment (Consumer, Corporate, etc.) |
| `country`, `city`, `state`, `region` | Geographic fields |
| `postal_code` | Delivery postal code |
| `category` / `sub-category` | Product classification |
| `product_id` / `product_name` | Product identifiers |
| `sales` | Revenue from the order |

---

## 🔧 Data Cleaning

The following preprocessing steps are applied:

- **Column normalization** — headers lowercased and spaces replaced with underscores
- **Duplicate removal** — exact duplicate rows dropped
- **Null handling** — missing `postal_code` values filled with `0` and cast to `int`
- **Date parsing** — `order_date` and `ship_date` converted to `datetime`
- **Categorical encoding** — object columns with low cardinality cast to `category` dtype

---

## ⚙️ Feature Engineering

Three new columns are derived from existing data:

| Feature | Description |
|---|---|
| `year` | Year extracted from `order_date` |
| `month` | Month extracted from `order_date` |
| `quarter` | Quarter extracted from `order_date` |
| `delivery_days` | Days elapsed between order and ship date |

---

## 📊 Analysis & Visualizations

### Revenue Overview
- Total revenue computed across all orders

### Sales by Category
- Horizontal bar chart comparing revenue across product categories

### Sales by Region
- Bar chart breaking down revenue by geographic region

### Top 10 Products
- Horizontal bar chart of the ten highest-grossing products by total sales

### Monthly Sales Trend
- Line chart showing aggregated monthly revenue over time, grouped by year and month

### Outlier Detection
Sales outliers are identified using the **IQR method**:

```
Lower bound = Q1 − 1.5 × IQR
Upper bound = Q3 + 1.5 × IQR
```

Transactions outside this range are flagged and counted.

---

## ▶️ Usage

1. Place `store.csv` in the project root directory.
2. Open and run `analysis.ipynb` top to bottom.
3. The cleaned dataset is saved to your Desktop as `report.csv`.

> **Note:** The output path is currently hardcoded to `C:\Users\user\Desktop\report.csv`. Update this in the final cell to match your local environment.

---

## 📤 Output

The final cleaned and enriched DataFrame is exported as a CSV with all original columns plus the engineered features (`year`, `month`, `quarter`, `delivery_days`).
