# SQL Data Warehouse Project

![SQL](https://img.shields.io/badge/SQL-Data%20Warehouse-blue)
![Database](https://img.shields.io/badge/Database-SQL%20Server-red)
![ETL](https://img.shields.io/badge/ETL-Pipeline-green)
![Architecture](https://img.shields.io/badge/Architecture-Bronze%2FSilver%2FGold-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 🚀 Overview
This project demonstrates a comprehensive data warehousing and analytics solution, from building a data warehouse to generating actionable insights. Designed as a portfolio project, it highlights industry best practices in data engineering and analytics.

---

## **Table of Contents**

1. [Overview](#Overview)
2. [Business Impact](#Business-Impact)
   - [Bronze Rules](#bronze-rules)
   - [Silver Rules](#silver-rules)
   - [Gold Rules](#gold-rules)
3. [Column Naming Conventions](#column-naming-conventions)
   - [Surrogate Keys](#surrogate-keys)
   - [Technical Columns](#technical-columns)
4. [Stored Procedure](#stored-procedure-naming-conventions)

---

## 💡 Business Impact

This project simulates a real-world data engineering scenario where data from multiple source systems (CRM and ERP) is integrated into a centralized data warehouse.

By implementing this solution, the following business value is enabled:

- Improved decision-making through centralized and reliable data  
- Faster analytical queries using a dimensional model (Star Schema)  
- Clear visibility into sales performance and customer behavior  
- Scalable architecture for future data growth and integration  

This approach reflects how modern data platforms support business intelligence and analytics in production environments.

---

## 🎯 Business Objective
The goal of this project is to provide a structured data platform to answer key business questions such as:

- Who are the most valuable customers?
- What products generate the highest revenue?
- How do sales evolve over time?
- What are the main purchasing patterns?

---

## 🏗️ Architecture

The data warehouse follows a multi-layered architecture:

- 🥉 **Bronze Layer** → Raw data ingestion from source systems (CRM, ERP)  
- 🥈 **Silver Layer** → Data cleansing, standardization, and integration  
- 🥇 **Gold Layer** → Business-ready data modeled as fact and dimension tables

`Source Systems (CRM, ERP) → Bronze → Silver → Gold → Analytics`

---

## 🏗️ Architecture & Design Diagrams
All architectural components are documented in the `/docs` folder:

- `data_architecture.png` → Overall architecture  
- `data_flow.png` → Data movement across layers  
- `data_integration.png` → Source integration logic  
- `data_model.png` → Dimensional model (Star Schema)  

---

## 🗄️ Data Modeling

The Gold layer is designed using a **Star Schema**:

### Fact Tables
- `fact_sales` → Transactional sales data

### Dimension Tables
- `dim_customers` → Customer attributes  
- `dim_products` → Product attributes  

### Design Principles
- Surrogate keys (`*_key`) for all dimensions  
- Foreign keys in fact tables referencing dimensions  
- Clear separation between facts and dimensions  
- Business-aligned naming conventions  

---

## ⚙️ ETL / ELT Process

The pipeline is implemented using SQL scripts and stored procedures:

### 1. Bronze Layer 🥉
- Raw ingestion from CSV files
- No transformations applied

### 2. Silver Layer 🥈
- Data cleansing and standardization  
- Data integration between CRM and ERP  
- Data type normalization  

### 3. Gold Layer 🥇
- Dimensional modeling  
- Fact and dimension table creation  

---

## 📁 Project Structure

```
📁 sql-data-warehouse-project/
│
├── 📘 README.md
├── 📁 docs/
│ ├── 🖼️ data_architecture.png
│ ├── 📘 data_catalog.md
│ ├── 🖼️ data_flow.png
│ ├── 🖼️ data_integration.png
│ ├── 🖼️ data_model.png
│ └── 📘 naming_conventions.md
│
├── 📁 datasets/
│ ├── 📁 source_crm/
│ │ ├── 📄 cust_info.csv
│ │ ├── 📄 prd_info.csv
│ │ └── 📄 sales_details.csv
│ └── 📁 source_erp/
│ │ ├── 📄 CUST_AZ12.csv
│ │ ├── 📄 LOC_A101.csv
│ │ └── 📄 PX_CAT_G1V2.csv
│
├── 📁 scripts/
│ ├── 📁 bronze/
│ │ ├── 🛢️ ddl.bronze.sql
│ │ └── 🛢️ proc_load_bronze.sql
│ ├── 📁 gold/
│ │ └── 🛢️ ddl_gold.sql
│ ├── 📁 silver/
│ │ ├── 🛢️ ddl.silver.sql
│ │ └── 🛢️ proc_load_silver.sql
│ └── 🛢️ init_database.sql
│
├── 📁 tests/
│ ├── 🛢️ quality_checks_gold.sql
│ └── 🛢️ quality_checks_silver.sql
```

---

## ✅ Data Quality

Data quality checks are implemented using SQL scripts:

- Null value validation  
- Duplicate detection  
- Referential integrity checks  
- Validation between Silver and Gold layers  

Scripts available in: `tests/`

---

## 📊 Analytics & KPIs

The Gold layer enables business-level analysis:

- Total Revenue  
- Sales by Customer  
- Product Performance  
- Sales Trends Over Time  

Example:

Cnsulta SQL

---

## 📸 Sample Results

Example of analytical query output from the Gold layer:

![Query Results](docs/query_results.png)

---

## 🧾 Naming Conventions

Full documentation:

`docs/naming_conventions.md`

## ▶️ How to Run
1. Initialize the database:
`scripts/init_database.sql`

2. Load Bronze layer:
`scripts/bronze/proc_load_bronze.sql`

3. Load Silver layer:
`scripts/silver/proc_load_silver.sql`

4. Create Gold layer:
`scripts/gold/ddl_gold.sql`

5. Run data quality checks:
`tests/quality_checks_silver.sql`
`tests/quality_checks_gold.sql`

## 🛠️ Tech Stack
- SQL (core transformations)
- Relational Database (Microsoft SQL Server)
- CSV files (data sources)
- Dimensional Modeling (Kimball methodology)

## 💡 Future Improvements
- Implement incremental loading strategy
- Add orchestration (Airflow)
- Automate data quality checks
- Integrate BI tools (Power BI / Tableau)

## 📈 Key Insights (Example)

Using the data warehouse, the following insights can be derived:

- Top 10 customers contribute to a significant percentage of total revenue  
- Certain product categories dominate overall sales performance  
- Sales show consistent trends based on time (seasonality potential)  

These insights demonstrate how raw data can be transformed into actionable business knowledge.

## 👨‍💻 Author
Jan Hernandez, System Engineer
