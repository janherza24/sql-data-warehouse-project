# SQL Data Warehouse Project

![SQL](https://img.shields.io/badge/SQL-Data%20Warehouse-blue)
![Database](https://img.shields.io/badge/Database-SQL%20Server-red)
![ETL](https://img.shields.io/badge/ETL-Pipeline-green)
![Architecture](https://img.shields.io/badge/Architecture-Bronze%2FSilver%2FGold-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 🚀 Overview
This project demonstrates a comprehensive data warehousing and analytics solution, from building a data warehouse to generating actionable insights. Designed as a portfolio project, it highlights industry best practices in data engineering and analytics.

---

## 💡 Specifications

- **Data Sources**: Import data from two source systems (ERP and CRM) provided as CSV files.
- **Data Quality**: Cleanse and resolve data quality issues prior to analysis.
- **Integration**: Combine both sources into a unified analytical data model.
- **Scope**: Focus on the latest dataset only (no historization).
- **Documentation**: Provide clear documentation for both technical and business users.

---

## 💡 Business Impact

This project simulates a real-world data engineering scenario where data from multiple source systems (CRM and ERP) is integrated into a centralized data warehouse.

By implementing this solution, the following business value is enabled:

- Improved decision-making through centralized and reliable data.
- Faster analytical queries using a dimensional model (Star Schema).
- Clear visibility into sales performance and customer behavior. 
- Scalable architecture for future data growth and integration.

---

## 🎯 Business Objective

The goal of this project is to provide a structured data platform to answer key business questions such as:

- Who are the most valuable customers?
- What products generate the highest revenue?
- How do sales evolve over time?
- What are the main purchasing patterns?

---

## 🏗️ Architecture

The solution is based on a **Medallion Architecture (Multi-hop Architecture)** combined with a **Dimensional Modeling approach (Kimball methodology)**.

This design separates data processing into progressive refinement layers, improving data quality, reliability, and analytical performance.

### 🔄 Data Flow

`Source Systems (CSV Files) → Bronze → Silver → Gold (Views) → Analytics`

---

### 🥉 Bronze Layer — *Raw Data Ingestion Layer*

- Implements a **raw ingestion pattern inside a relational database**
- Data is loaded using `BULK INSERT`
- No transformations are applied
- Tables are **fully reloaded (TRUNCATE + INSERT)** on each execution

**Purpose:**
- Preserve raw data as-is  
- Enable reprocessing and traceability  

---

### 🥈 Silver Layer — *Cleansed & Conformed Layer*

- Implements **ELT transformations (Extract, Load, Transform)**
- Applies:
  - Data normalization (categorical values)
  - Data cleansing (`TRIM`, NULL handling)
  - Data correction (recalculated metrics)
  - Deduplication using window functions (`ROW_NUMBER()`)
- Integrates multiple sources (CRM + ERP)

**Purpose:**
- Produce **clean, consistent, and reliable datasets**  
- Serve as the foundation for analytical modeling  

---

### 🥇 Gold Layer — *Presentation / Data Mart Layer*

- Implements a **Star Schema (Dimensional Model)**
- Built using **SQL views (virtual data mart)** instead of physical tables
- Includes:
  - Fact: `fact_sales`
  - Dimensions: `dim_customers`, `dim_products`
- Uses **late-binding joins** between facts and dimensions

**Purpose:**
- Provide **business-ready, query-optimized datasets**  
- Support BI and analytical workloads  

---

### 📌 Key Architectural Decisions

- **Medallion Architecture** for layered data refinement  
- **Kimball Dimensional Modeling** for analytics  
- **ELT pattern** (transformations after load)  
- **Full reload strategy** (no incremental loads)  
- **View-based Gold layer** (no data duplication)  
- Transformation logic centralized in SQL  

---

### ⚠️ Design Trade-offs

- Full reload simplifies the pipeline but does not scale for large datasets  
- Views reduce storage but may impact performance at scale  
- No historization (SCD Type 2 not implemented)  
- No orchestration layer (e.g., Airflow)  

This represents a **foundational data platform design**, ready to evolve into a production-grade architecture.

---

## 🏗️ Architecture & Design Diagrams

All architectural components are documented in the `/docs` folder:

- `data_architecture.png` → Overall architecture  
- `data_flow.png` → Data movement across layers  
- `data_integration.png` → Source integration logic  
- `data_model.png` → Dimensional model (Star Schema) 

---

## 🗄️ Data Modeling

The Gold layer is designed using a **Star Schema**, implemented through SQL views:

### Fact View
- `fact_sales` → Transactional sales data

### Dimension Views
- `dim_customers` → Customer attributes  
- `dim_products` → Product attributes  

### Design Principles

- Surrogate keys (`*_key`) generated using window functions.
- Foreign key relationships handled logically in views.
- Clear separation between facts and dimensions.
- Business-aligned naming conventions.
- Gold layer implemented using **views instead of physical tables**.

---

## ⚙️ ETL / ELT Process

The pipeline follows an **ELT approach**, where transformations are performed inside the database.

### 1. Bronze Layer 🥉
- Full reload strategy using `TRUNCATE + BULK INSERT`.
- Raw ingestion from CSV files.
- No transformations applied.

### 2. Silver Layer 🥈
- Data cleansing and standardization.
- Deduplication using window functions.
- Data normalization (dates, strings, categorical values).
- Business rule enforcement (e.g., recalculating sales, fixing invalid values).
- Integration between CRM and ERP sources.

### 3. Gold Layer 🥇
- Business-ready views creation (Star Schema).
- Data enrichment from multiple sources.
- Logical modeling using fact and dimension views.
- No data duplication (query-time transformation).

---

## 🧠 Data Engineering Decisions

- Full reload strategy implemented in Bronze and Silver layers  
- ELT approach: transformations handled inside SQL Server  
- Data quality issues resolved during Silver transformations  
- Gold layer implemented as views to improve maintainability and avoid duplication  
- Window functions used for deduplication and surrogate key generation  

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

- Null value validation.
- Duplicate detection.
- Referential integrity checks.
- Validation between Silver and Gold layers.

Scripts available in: `tests/`

---

## 📊 Analytics & KPIs

The Gold layer enables business-level analysis:

- Total Revenue.
- Sales by Customer.
- Product Performance.
- Sales Trends Over Time.

---

## 📸 Sample Results

Example of analytical query output from the Gold layer:

![Query Results](docs/query_results.png)

---

## 📈 Key Insights (Example)

Using the data warehouse, the following insights can be derived:

- Top customers contribute a significant portion of total revenue  
- Certain product categories dominate overall sales performance  
- Sales trends reveal potential seasonality patterns  

---

## 🧾 Naming Conventions

Full documentation:

`docs/naming_conventions.md`

---

## ▶️ How to Run

1. Initialize the database  
`scripts/init_database.sql`

2. Load Bronze layer  
`scripts/bronze/proc_load_bronze.sql`

3. Load Silver layer  
`scripts/silver/proc_load_silver.sql`

4. Create Gold views  
`scripts/gold/ddl_gold.sql`

5. Run data quality checks  
`tests/quality_checks_silver.sql`  
`tests/quality_checks_gold.sql`

---

## 🛠️ Tech Stack

- SQL (core transformations).
- Microsoft SQL Server.
- CSV files (data sources).
- Dimensional Modeling (Kimball methodology).

---

## 💡 Future Improvements

- Implement incremental loading strategy.
- Add orchestration (Airflow).
- Automate data quality checks.
- Integrate BI tools (Power BI / Tableau).

---

## 🚀 License

This project is licensed under the [MIT License](LICENSE).

---

## 👨‍💻 About us
Hi there! I'm Jan Hernandez.
