# North Star Case Study

An end-to-end data and analytics assessment for a fictional urban logistics operator, North Star, covering data cleaning, SQL exploration, statistical modelling, and document-store aggregation. The dataset spans January 2024–December 2025 across 8 delivery hubs, 7 operational zones, and ~1,250 orders.

---

## Repository Structure

```
north-star-case-study/
├── dataset/                        Raw source CSVs (do not modify)
│   ├── data_dictionary.csv         Column definitions for all tables
│   ├── customers.csv
│   ├── orders.csv
│   ├── deliveries.csv
│   ├── drivers.csv
│   ├── vehicles.csv
│   ├── hubs.csv
│   ├── incidents.csv
│   ├── complaints.csv
│   └── app_events.csv
│
├── graphs/                         Contains seperate graph exports (as PNGs) from 3_r_analytics.ipynb
│
├── notebooks/
│   ├── 1_data_preparation.ipynb    Data cleaning and standardisation (Python / pandas)
│   ├── 2_sql_analysis.ipynb        Exploratory SQL queries (R / sqldf)
│   ├── 3_r_analytics.ipynb         Correlation analysis and regression modelling (R / ggplot2)
│   └── 4_pymongo.ipynb             MongoDB collection design and aggregation pipelines (Python / pymongo)
│
└── README.md                       
```

---

## Notebooks

### 1 - Data Preparation
Loads the nine raw CSVs and produces a cleaned version of each. Key steps: zone label standardisation across all tables, timestamp parsing, type coercion for flag and numeric columns, and substitution for missing categorical values. Output is written to a `cleaned/` directory, which is then used by all subsequent notebooks.

### 2 - SQL Analysis
Runs ten SQL queries over the cleaned data using `sqldf` in R, covering delivery status breakdowns, hub and zone performance, complaint rates by service type, vehicle incident rates, and a multi-table join identifying deliveries with both incidents and complaints.

### 3 - R Analytics
Conducts Pearson correlation tests (training score vs driver rating, battery health vs incident rate, route overrides vs customer rating) and fits an linear regression to predict post-delivery customer ratings. Visualisations produced with `ggplot2` and `plotly`.

### 4 - PyMongo
Migrates cleaned data into a MongoDB Atlas cluster (`northstar` database) across three collections: `customer_cases`, `delivery_exceptions`, and `app_activity`. Runs four aggregation pipelines, which helps identify complaint severity by zone, repeat complainers, app failure patterns by device type, and incident types linked to complaints.