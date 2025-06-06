# Superstore_sales_dashboard


# Superstore Sales Performance Dashboard

This project demonstrates how to clean and analyze sales data using **Python (Pandas)** and build an interactive dashboard in **Power BI**. It shows sales performance by **product**, **region**, and **month** using real-world business metrics.

---

## Project Structure

- `Sample - Superstore.csv`: Raw sales dataset
- `Superstore_sales_cleaned.ipynb`: Jupyter Notebook for data cleaning
- `cleaned_superstore_sales.csv`: Cleaned dataset used in Power BI
- `Superstore Sales Dashboard by Joseph.pbix`: Final interactive dashboard
- `screenshots/`:  Dashboard visual snapshots

---

## Step 1: Data Cleaning with Pandas (Jupyter Notebook)

We used Python and Pandas to:
- Import and inspect the dataset
- Handle encoding and format issues
- Convert `Order Date` to datetime
- Create new columns like `MonthYear` for time-based analysis
- Export the cleaned dataset as `.csv`

### Key Code Snippets

import pandas as pd

# Load the dataset
df = pd.read_csv(r"C:\Users\JOSEPH R PAKHUONGTE\Downloads\Sample - Superstore.csv", encoding='latin1')
df.head()

# Understanding the structure (looking for missing values, icoreecrt data types)
df.info()
df.describe(include='all')

# Convert Order Date to Datetime
df['Order Date'] = pd.to_datetime(df['Order Date'], errors='coerce')

# Extract Year-Month for Aggregation
df['Month'] = df['Order Date'].dt.to_period('M').astype(str)

# Drop Irrelevant or Duplicate Columns
df = df.drop(columns=['Row ID', 'Postal Code'], errors='ignore')

# Check for missing values
df.isnull().sum()

# Drop rows with missing essential info
df = df.dropna(subset=['Order Date', 'Region', 'Product Name', 'Sales'])

# Rename Columns for Simplicity
df.rename(columns={
    'Product Name': 'Product',
    'Region': 'Region',
    'Sales': 'Sales'
}, inplace=True)

# Save Cleaned Data
df.to_csv("cleaned_superstore_sales.csv", index=False)
print("✅ Cleaned data saved to 'cleaned_superstore_sales.csv'")

## Power BI Dashboard Creation ##

# Dashboard Objective #
Visualize sales performance by month, region, and product category using interactive charts and filters.

# Visuals Used #
Line Chart: Sales over Time.

Bar Chart: Sales by Region

Donut Chart: Sales by Category

KPI Cards: Total Sales, Orders, Customers.

Slicers: Region

Text box insights and formatted title

## Features ##
Dynamic filters for region

Custom MonthYear column sorted by MonthSort {DAX: MonthYear = FORMAT('cleaned_superstore_sales'[Order Date], "MMM-YYYY")}

Clean layout with KPI section
