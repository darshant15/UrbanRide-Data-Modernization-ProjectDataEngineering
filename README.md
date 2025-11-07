# 🚖 UrbanRide Data Modernization Data Engineering Project – End-to-End Azure Cloud Pipeline

![Azure](https://img.shields.io/badge/Platform-Microsoft%20Azure-blue)
![GitHub](https://img.shields.io/badge/Repo-Version--Controlled-lightgrey)
![Pipeline](https://img.shields.io/badge/Data-Pipeline-green)

## 📌 Project Overview

This project demonstrates an **end-to-end Data Engineering pipeline(ELT)** built on the **NYC Taxi dataset**.  
It covers **API-based ingestion, transformation (PySpark), storage in Parquet format, workflow automation, orchestration, and visualization** using Azure services.


---
## 🖼️ Architecture Diagram

![Pipeline Architecture](https://github.com/darshant15/NYC-TAXI-DataEngineering-Project/blob/main/ArchitectureofProject(dataengineer).jpeg)


---
## 🖼️ Management-level And Hierarchy

![Management Level & Hierarchy](https://github.com/darshant15/NYC-TAXI-DataEngineering-Project/blob/main/managementLevel%26Hierarchy.jpeg)

---

## 🚀 Project Highlights

## 🗂️ Data Lake Architecture (Medallion)

* **Bronze (Raw Zone) 🟤**

  * Stores API-ingested taxi data **as-in** (CSV/Parquet)
  * No cleaning or schema enforcement applied

* **Silver (Curated Zone) ⚪**

  * Cleaned, deduplicated, and standardized datasets
  * Applied schema validation, handled nulls, added calculated fields
  * Stored in **Parquet/Delta format** for efficient querying

* **Gold (Analytics Zone) 🟡**

  * Aggregated datasets optimized for analytics
  * Partitioned tables by **year/month** for performance
  * Ready for **Azure Synapse Analytics** & **Power BI dashboards**

---

## 🏗️ Architecture Workflow (with Bronze/Silver/Gold)

1. **Ingestion → Bronze**

   * Data from **APIs & CSV dumps** ingested into **Bronze container** as Parquet files.

2. **Transformation → Silver**

   * Clean & standardize data in **Azure Databricks (PySpark)**.
   * Store curated outputs into **Silver container**.

3. **Aggregation → Gold**

   * Generate final **aggregated datasets**:

     * Trip duration
     * Revenue per borough
     * Busiest pickup/drop-off zones
     * Peak travel hours
   * Store results in **Gold container** for BI & Synapse queries.

4. **Analytics & Visualization**

   * **Power BI dashboards** fetch data directly from the **Gold layer**.

---
- **Automated Ingestion**:  
  - Pulled raw taxi trip data directly from **NYC Taxi & Limousine Commission (TLC) APIs**.  
  - Stored incoming data as **Parquet files** in **Azure Data Lake Storage (ADLS Gen2)** for compression & performance.  

- **Data Lake Architecture**:  
  - **Raw zone** → Direct API dumps in CSV/Parquet.  
  - **Curated zone** → Cleaned, deduplicated, schema-enforced Parquet files.  
  - **Analytics zone** → Aggregated tables optimized for BI reporting.  

- **Dynamic Pipeline Logic**:  
  - Used **if-else conditions** in ADF to branch logic (e.g., different pipelines for Yellow Cab vs. Green Cab).  
  - Implemented **ForEach activity** in ADF for iterating over multiple months/years of trip data ingestion.  
  - Integrated **failure conditions** for retries and logging.  

- **Scalable Data Processing**:  
  - **Azure Databricks (PySpark)** transformations included:  
    - Handling nulls and schema mismatches  
    - Deduplication of rows  
    - Feature engineering: trip duration, cost per mile, speed per trip  
    - Aggregations: revenue by borough, busiest zones, peak travel hours  

- **Analytics-Ready Storage**:  
  - Transformed data loaded into **Azure Synapse Analytics** (Lake DB) for SQL analysis.  
  - Tables partitioned by `year` and `month` for query efficiency.  

- **Visualization**:  
  - Built **Power BI dashboards** showing:  
    - Hourly/Monthly trip patterns  
    - Average fare distribution by distance  
    - Payment methods trend (Card, Cash, Others)  
    - Heatmaps for busiest pickup/drop-off locations  

---

## 🏗️ Architecture Workflow

1. **Data Ingestion** – API calls & CSV downloads for Yellow/Green cab datasets. Data saved as **Parquet files** in `raw-data` zone.  
2. **Orchestration** – **Azure Data Factory** pipeline with:  
   - **Lookup activity** → Get file paths/months  
   - **ForEach loop** → Iterate over all months of taxi data  
   - **If Condition activity** → Split logic for Yellow/Green datasets  
3. **Data Transformation** – In **Azure Databricks (PySpark)**:  
   - Read raw Parquet  
   - Apply transformations & aggregations  
   - Write back to curated zone in Parquet/Delta format  
4. **Data Warehouse** – Loaded curated datasets into **Azure Synapse Analytics** (SQL pools).  
5. **Analytics & Visualization** – Connected Power BI → Synapse for interactive dashboards.  

---

## ⚙️ Tech Stack & Tools (ELT)

- **Azure Data Factory (ADF)** – Orchestration, ForEach, If/Else conditions  
- **Azure Data Lake Storage Gen2 (ADLS)** – Layered raw/curated storage  
- **Azure Databricks (PySpark)** – Transformations, schema enforcement, Parquet writing  
- **Azure Synapse Analytics** – Data warehouse queries  
- **Power BI** – Visual dashboards  
- **GitHub** – Version control  

---

## 📊 Key Insights (Examples)

- 🚖 Trips per hour/day/month – demand forecasting  
- 💳 Payment method trends – card vs. cash  
- 🌍 Borough-level heatmaps – busiest pickup zones  
- 💵 Average fare per mile vs. trip distance  
- ⏱️ Peak congestion hours & average trip duration  

---

## 🚀 How to Run

1. git clone https://github.com/darshant15/NYC-TAXI-DataEngineering-Project.git
cd NYC-TAXI-DataEngineering-Project
2. Configure ADF linked services (API URL, ADLS, Key Vault).
3. Import Databricks notebooks from /notebooks.
4. Trigger ingestion pipelines (ForEach across multiple months).
5. Run PySpark transformations and save to curated zone.
6. Load into Synapse and connect Power BI for dashboarding

---

## 📌 Author

👤 **Darshan T**

* 🔗 [GitHub Profile](https://github.com/darshant15)

---

✨ This project highlights real-world cloud pipeline design: API ingestion, Parquet optimization, ADF orchestration with loops/conditions, PySpark transformations, and BI dashboards.  

---
