# ⛓️ End-to-End Data Pipeline with AWS EC2, Apache NiFi, AWS S3,Docker and Snowflake (SCD1 & SCD2)

This repository showcases a **real-world end-to-end data pipeline** that simulates change data capture and slowly changing dimensions using a modern **data engineering stack**. The project demonstrates how to ingest streaming data with **Apache NiFi**, land it in **AWS S3**, and automatically load it into **Snowflake**. Once in Snowflake, the pipeline applies **Slowly Changing Dimension (SCD)** Type 1 and Type 2 logic using Snowflake Streams and Tasks to maintain both current and historical records. The entire workflow is orchestrated on an **AWS EC2** instance using **Docker**, making it easy to deploy and reproduce. This project is designed as a portfolio piece to highlight data engineering skills in cloud infrastructure, pipeline automation, and data warehousing best practices.


## 🧱 Tech Stack

- **Amazon EC2** – Cloud VM infrastructure hosting the pipeline (running Docker containers for NiFi and JupyterLab).
- **Snowflake** — Cloud data warehouse where data is loaded and transformed. It holds the staging table as well as the target dimension tables.
- **Amazon S3** — Data lake storage for raw CSV files and for Snowflake to ingest from. Acts as the landing zone for NiFi outputs and a source   for Snowpipe.
- **Faker + Python** — Used to generate synthetic source data (customer records) with realistic values. A JupyterLab notebook uses Faker to                             create CSV files simulating new and updated customer information.
- **Snowpipe** — Snowflake’s continuous ingestion service, set up to automatically load new files from the S3 bucket into a Snowflake staging 
                 table (customer_raw).
- **Snowflake Streams & Tasks** — Used for orchestration of data transformations:  
-Stream on the staging table captures new rows as they arrive (for SCD Type 1).  
-Stream on the main table captures changes in the dimension table (for SCD Type 2 history).  
-Task schedules a stored procedure to merge new data from staging into the main customer table (Type 1).  
-Task schedules a merge from the change stream into the customer_history table (Type 2).  
- **Docker & Docker-Compose** — SQL scripts define the database schema, stage, pipe, and implement the SCD Type-1 and Type-2 transformations using MERGE statements and stored procedures.


---

## 📌 Project Highlights

- 🔁 **SCD Type 2** history tracking: preserves old data with timestamps.
- 💡 Uses **Snowflake Stream** to capture changes from a staging table.
- 📂 Loads raw files from **S3** using Snowpipe and external stage.
- 🧪 Faker generates dynamic test data mimicking real customers.
- 🐳 Docker Compose used for version-controlled environment simulation.

---

## 📂 Folder Structure

- `sql/` — All SQL scripts for table creation, data loading, and SCD transformations.
- `faker.ipynb` — Notebook that generates fake customer data and pushes to S3.
- `architecture/` — Project pipeline diagram.
- `docker-compose.yml` — Sets up supporting services (if any in real scenario).
- `commands.txt` — Helpful CLI and Snowflake commands.

---

## 📊 Architecture

![Architecture](architecture/scd_pipeline_architecture.png)

---

## 🚀 Run the Pipeline

### 1. Create Snowflake Objects
```sql
-- Run sql/1_table_creation.sql
-- Run sql/2_data_loading.sql to create stages, file formats, and pipes
```

### 2. Run Data Generator
```bash
jupyter notebook notebooks/faker.ipynb
# Or run as script to generate fake customer records into S3
```

### 3. Monitor Snowpipe
```sql
SELECT SYSTEM$PIPE_STATUS('customer_s3_pipe');
SELECT * FROM customer_raw;
```

### 4. Apply Transformations
```sql
-- Run sql/3_scd1.sql or sql/4_scd2.sql depending on scenario
```

---

## 📚 Learning Outcomes

- Understand the difference between SCD1 and SCD2.
- Automate data ingestion using Snowpipe.
- Use Python to simulate real-world ETL testing environments.
- Apply Snowflake streams to detect and apply changes.

---

## 🪪 License

This project is for learning and demonstration purposes only. Feel free to fork and extend!
