# ⛓️ SCD Type 2 Data Engineering Pipeline with Snowflake + S3 + Faker

This project showcases a complete **data engineering pipeline** that simulates handling Slowly Changing Dimensions (SCD Type 1 & 2) using **Snowflake**, **Amazon S3**, and **Python Faker**. It mimics a real-world use case where customer information changes over time and needs to be tracked historically.

## 🧱 Tech Stack

- **Snowflake** — Cloud Data Warehouse
- **Amazon S3** — Staging Layer for raw files
- **Faker + Python** — Data simulation
- **Snowpipe** — Automated data ingestion
- **Streams** — Change data capture
- **Docker** — Deployment simulation
- **SQL (SCD1 & SCD2)** — Data transformation logic

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
