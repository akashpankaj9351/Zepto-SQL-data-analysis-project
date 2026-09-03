# 🛒 Zepto E-commerce SQL Data Analysis Project

This is a SQL data analyst project based on an e-commerce inventory dataset scraped from [Zepto](https://www.zeptonow.com/) — one of India's fastest-growing quick-commerce startups. It covers the full workflow from raw data exploration to business-focused analysis.

## 📌 Project Overview

The goal was to simulate how data analysts in e-commerce/retail work behind the scenes, using SQL to:

✅ Set up a messy, real-world e-commerce inventory **database**

✅ Perform **Exploratory Data Analysis (EDA)** to explore product categories, availability, and pricing inconsistencies

✅ Implement **Data Cleaning** to handle null values, remove invalid entries, and convert pricing from paise to rupees

✅ Write **business-driven SQL queries** to derive insights around **pricing, inventory, stock availability, revenue**, and more

## 📁 Dataset Overview

The dataset was sourced from [Kaggle](https://www.kaggle.com/datasets/palvinder2006/zepto-inventory-dataset/data?select=zepto_v2.csv) and was originally scraped from Zepto's official product listings.

Each row represents a unique SKU (Stock Keeping Unit) for a product. Duplicate product names exist because the same product may appear multiple times in different package sizes, weights, discounts, or categories — exactly how real catalog data looks.

🧾 **Columns:**
- **sku_id:** Unique identifier for each product entry (Synthetic Primary Key)
- **name:** Product name as it appears on the app
- **category:** Product category like Fruits, Snacks, Beverages, etc.
- **mrp:** Maximum Retail Price (originally in paise, converted to ₹)
- **discountPercent:** Discount applied on MRP
- **discountedSellingPrice:** Final price after discount (also converted to ₹)
- **availableQuantity:** Units available in inventory
- **weightInGms:** Product weight in grams
- **outOfStock:** Boolean flag indicating stock availability
- **quantity:** Number of units per package (mixed with grams for loose produce)

## 🔧 Project Workflow

### 1. Database & Table Creation

```sql
CREATE TABLE zepto (
  sku_id SERIAL PRIMARY KEY,
  category VARCHAR(120),
  name VARCHAR(150) NOT NULL,
  mrp NUMERIC(8,2),
  discountPercent NUMERIC(5,2),
  availableQuantity INTEGER,
  discountedSellingPrice NUMERIC(8,2),
  weightInGms INTEGER,
  outOfStock BOOLEAN,
  quantity INTEGER
);
```

### 2. Data Import

- Loaded the CSV using pgAdmin's import feature.
- If the import feature doesn't work, use this instead:

```sql
\copy zepto(category,name,mrp,discountPercent,availableQuantity,
            discountedSellingPrice,weightInGms,outOfStock,quantity)
FROM 'data/zepto_v2.csv' WITH (FORMAT csv, HEADER true, DELIMITER ',', QUOTE '"', ENCODING 'UTF8');
```

- Faced encoding issues (UTF-8 error), fixed by re-saving the CSV using CSV UTF-8 format.

### 3. 🔍 Data Exploration

- Counted total records in the dataset
- Viewed a sample of the dataset to understand structure and content
- Checked for null values across all columns
- Identified distinct product categories
- Compared in-stock vs out-of-stock product counts
- Detected products appearing multiple times as different SKUs

### 4. 🧹 Data Cleaning

- Identified and removed rows where MRP or discounted selling price was zero
- Converted `mrp` and `discountedSellingPrice` from paise to rupees for consistency

### 5. 📊 Business Insights

- Found top 10 best-value products based on discount percentage
- Identified high-MRP products currently out of stock
- Estimated potential revenue per product category
- Filtered expensive products (MRP > ₹500) with minimal discount
- Ranked top 5 categories offering the highest average discounts
- Calculated price per gram to identify value-for-money products
- Grouped products by weight into Low, Medium, and Bulk categories
- Measured total inventory weight per product category

<!-- 
Optional: Add a few of your own takeaways here once you've reviewed your query results, e.g.:
- Category X had the highest average discount at Y%
- Z products were high-MRP but out of stock, indicating a possible demand/supply gap
-->

## 🛠️ How to Use This Project

1. **Clone the repository**
   ```bash
   git clone https://github.com/akashpankaj9351/Zepto-SQL-data-analysis-project.git
   cd Zepto-SQL-data-analysis-project
   ```

2. **Open the SQL file** (table creation, data exploration, cleaning, and business analysis)

3. **Load the dataset into pgAdmin or any other PostgreSQL client**
   - Create a database and run the SQL file
   - Import the dataset (convert to UTF-8 if necessary)

## 📜 License

MIT — feel free to fork, star, and build on this project.

## 👨‍💻 About Me

Hey, I'm Akash Pankaj — building this project as part of my journey into data analytics.

🔗 GitHub: [akashpankaj9351](https://github.com/akashpankaj9351)

<!-- Add your LinkedIn or other social links here -->

