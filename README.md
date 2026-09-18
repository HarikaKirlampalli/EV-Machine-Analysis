# EV-Machine-Analysis
EV Charging Management using MySQL
# EV Machine Analysis

## SQL & Data Analytics Project

> A MySQL-based data analytics project for analyzing electric vehicle sales, manufacturers, vehicle specifications, state-wise demand, categories, and charging infrastructure.

---

## 📌 Project Overview

**EV Machine Analysis** is a relational database and SQL analytics project focused on understanding the Electric Vehicle (EV) market through structured data.

The project brings together information about:
- EV manufacturers
- Vehicle categories
- EV models and specifications
- State-wise EV sales
- Sales revenue
- Charging stations

Using **MySQL and SQL**, the project performs basic, intermediate, and advanced analysis to identify sales trends, top-performing manufacturers, popular EV models, state-wise demand, vehicle performance, and charging infrastructure.

---

## 🎯 Project Objectives

- Analyze total EV units sold.
- Identify the top-performing EV manufacturers.
- Find the best-selling EV models.
- Analyze state-wise EV sales.
- Compare yearly EV sales and revenue.
- Analyze EV categories.
- Compare battery capacity and driving range.
- Analyze charging station availability.
- Use SQL joins and aggregation for business analysis.
- Apply advanced SQL techniques such as subqueries and window functions.

---

## ❓ Problem Statement

The EV industry generates data across multiple areas such as vehicles, manufacturers, sales, geographical regions, and charging infrastructure.

Raw data alone does not provide clear business insights.

This project uses a relational MySQL database to answer questions such as:

- Which manufacturer sells the most EVs?
- Which EV model is the best-selling?
- Which state has the highest EV demand?
- Which EV has the highest driving range?
- Which category performs best in terms of sales?
- How are EV sales changing year by year?
- Which states may require more charging infrastructure?

---

## 🗄️ Database Information

| Property | Details |
|---|---|
| Database | MySQL |
| Database Name | `ev_machine_analysis` |
| Tables | 6 |
| Query Levels | Basic, Intermediate, Advanced |
| Project Domain | Data Analytics |
| Tool | MySQL Workbench |

---

## 📊 Database Tables

| Table | Purpose |
|---|---|
| `manufacturers` | Stores EV manufacturer information |
| `categories` | Stores EV category information |
| `states` | Stores state and regional information |
| `vehicles` | Stores EV model and specification details |
| `ev_sales` | Stores EV sales and revenue records |
| `charging_stations` | Stores charging station information |

---

## 🔗 Entity Relationships

```text
manufacturers
      │
      │ 1 : M
      ▼
   vehicles
      │
      │ 1 : M
      ▼
   ev_sales
      ▲
      │ M : 1
    states
      │
      │ 1 : M
      ▼
charging_stations

categories
      │
      │ 1 : M
      ▼
   vehicles
```

### Relationships

- `manufacturers` → `vehicles`
- `categories` → `vehicles`
- `vehicles` → `ev_sales`
- `states` → `ev_sales`
- `states` → `charging_stations`

Primary Keys and Foreign Keys maintain the relationships between these tables.

---

## 📋 Table Structure

### 1. `manufacturers`

| Column | Description |
|---|---|
| `manufacturer_id` | Primary Key |
| `manufacturer_name` | Manufacturer name |
| `country` | Country |
| `founded_year` | Founded year |

### 2. `categories`

| Column | Description |
|---|---|
| `category_id` | Primary Key |
| `category_name` | Category name |
| `description` | Category description |

### 3. `states`

| Column | Description |
|---|---|
| `state_id` | Primary Key |
| `state_name` | State name |
| `region` | Region |

### 4. `vehicles`

| Column | Description |
|---|---|
| `vehicle_id` | Primary Key |
| `vehicle_name` | EV model name |
| `manufacturer_id` | Foreign Key |
| `category_id` | Foreign Key |
| `battery_capacity_kwh` | Battery capacity |
| `range_km` | Driving range |

### 5. `ev_sales`

| Column | Description |
|---|---|
| `sale_id` | Primary Key |
| `vehicle_id` | Foreign Key |
| `state_id` | Foreign Key |
| `sale_year` | Sales year |
| `sale_month` | Sales month |
| `units_sold` | Number of units sold |
| `revenue` | Sales revenue |

### 6. `charging_stations`

| Column | Description |
|---|---|
| `station_id` | Primary Key |
| `state_id` | Foreign Key |
| `station_count` | Number of stations |
| `charging_type` | Charging type |

---

## 🛠️ Technologies Used

- **MySQL** – Database
- **SQL** – Data querying and analysis
- **MySQL Workbench** – Database development and execution
- **ER Diagram** – Database modeling

---

## 📚 SQL Concepts Used

### Basic SQL
- `SELECT`
- `WHERE`
- `ORDER BY`
- `COUNT()`
- `SUM()`
- `AVG()`
- `MAX()`
- `MIN()`

### Intermediate SQL
- `INNER JOIN`
- Multiple-table joins
- `GROUP BY`
- `HAVING`
- `LIMIT`
- Aggregate functions

### Advanced SQL
- Subqueries
- `CASE`
- `RANK()`
- `DENSE_RANK()`
- `ROW_NUMBER()`
- `LAG()`
- Window functions

---

## 📈 Key Project Results

Based on the current project data:

| Analysis | Result |
|---|---|
| Total EV Units Sold | **5,370** |
| Total Vehicles | **10** |
| Total Manufacturers | **5** |
| Average Vehicle Range | **419.30 km** |
| Highest Vehicle Range | **Ioniq 5 – 631 km** |
| Top Manufacturer | **Tata Motors – 2,500 units** |
| Top-Selling Vehicle | **Nexon EV – 1,430 units** |
| Highest-Sales State | **Tamil Nadu – 1,570 units** |
| Top Category by Sales | **SUV – 3,340 units** |

---

## 🔍 Sample SQL Analysis

### Top-selling vehicle

```sql
SELECT v.vehicle_name,
       SUM(e.units_sold) AS total_sales
FROM ev_sales e
JOIN vehicles v
ON e.vehicle_id = v.vehicle_id
GROUP BY v.vehicle_name
ORDER BY total_sales DESC
LIMIT 1;
```

### Top manufacturer

```sql
SELECT m.manufacturer_name,
       SUM(e.units_sold) AS total_sales
FROM ev_sales e
JOIN vehicles v
ON e.vehicle_id = v.vehicle_id
JOIN manufacturers m
ON v.manufacturer_id = m.manufacturer_id
GROUP BY m.manufacturer_name
ORDER BY total_sales DESC
LIMIT 1;
```

### Vehicles above average range

```sql
SELECT vehicle_name, range_km
FROM vehicles
WHERE range_km > (
    SELECT AVG(range_km)
    FROM vehicles
)
ORDER BY range_km DESC;
```

---

## 📝 SQL Query Classification

The project contains **27 SQL analysis queries**:

| Level | Queries | Focus |
|---|---:|---|
| Basic | 10 | Filtering, sorting, aggregation |
| Intermediate | 10 | Joins, grouping, business analysis |
| Advanced | 10 | Subqueries, ranking, window functions |
| **Total** | **30** | **Complete SQL Analysis** |

---

## 🔄 Project Workflow

```text
EV Market Data
      ↓
Database Design
      ↓
ER Diagram
      ↓
Create MySQL Database
      ↓
Create 6 Tables
      ↓
Insert Data
      ↓
Data Validation
      ↓
SQL Data Analysis
      ↓
Basic → Intermediate → Advanced
      ↓
Business Insights
```

---

## ▶️ How to Run

### 1. Select the database

```sql
USE ev_machine_analysis;
```

### 2. Verify tables

```sql
SHOW TABLES;
```

Expected tables:

```text
categories
charging_stations
ev_sales
manufacturers
states
vehicles
```

### 3. View the data

```sql
SELECT * FROM manufacturers;
SELECT * FROM categories;
SELECT * FROM states;
SELECT * FROM vehicles;
SELECT * FROM ev_sales;
SELECT * FROM charging_stations;
```

### 4. Run the analysis queries

Execute the 30 queries in the following order:

```text
Basic
   ↓
Intermediate
   ↓
Advanced
```

---

## 📁 Project Structure

```text
EV-Machine-Analysis/
│
├── README.md
│
├── SQL/
│   ├── create_database.sql
│   ├── create_tables.sql
│   ├── insert_data.sql
│   └── analysis_queries.sql
│
├── ER-Diagram/
│   └── ev_machine_analysis_er.png
│
└── Documentation/
    └── project_report.pdf
```

---

## 💡 Business Insights

The analysis helps identify:

- Leading EV manufacturers
- Most popular EV models
- High-demand states
- Sales trends over time
- High-performing vehicle categories
- EV battery and range characteristics
- Charging infrastructure distribution

These insights can support decisions related to **EV production, marketing, sales planning, and charging infrastructure development**.

---

## 🚀 Future Scope

The project can be extended with:

- EV price analysis
- Customer review analysis
- Charging cost analysis
- Petrol vs EV comparison
- Population-based EV adoption analysis
- Monthly sales forecasting
- Power consumption analysis
- Power BI / Tableau dashboard
- Machine Learning-based EV sales prediction

---

## 🏁 Conclusion

**EV Machine Analysis** demonstrates how SQL and relational database concepts can be applied to a real-world Data Analytics problem.

The project integrates **manufacturer, category, vehicle, sales, state, and charging station data** into a structured MySQL database.

Through **27 SQL queries ranging from basic to advanced**, the project identifies important EV market trends and business insights.

The project demonstrates practical knowledge of:

```text
Database Design
      +
SQL
      +
Data Analysis
      +
Business Insights
```

---

## 👨‍💻 Project Details

**Project Name:** EV Machine Analysis  
**Domain:** Data Analytics  
**Database:** MySQL  
**Tool:** MySQL Workbench  
**Tables:** 6  
**SQL Queries:** 27 
**Difficulty:** Basic | Intermediate | Advanced  
**Project Type:** Student SQL & Data Analytics Project

---

## ⭐ Skills Demonstrated

`MySQL` · `SQL` · `Data Analytics` · `Database Design` · `ER Diagram` · `Joins` · `Aggregate Functions` · `Subqueries` · `CASE` · `Window Functions` · `Business Analysis`
