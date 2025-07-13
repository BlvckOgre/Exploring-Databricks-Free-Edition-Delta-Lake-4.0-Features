# 🚀 Exploring Databricks Free Edition & Delta Lake 4.0 Features

This repository explores and demonstrates the latest capabilities of **Databricks** and **Delta Lake 4.0**, specifically within the **free Databricks Community Edition** environment.

It covers the full data lifecycle — from ingestion to transformation — while showcasing **Delta Lake 4.0 enhancements** including **deletion vectors**, **schema evolution**, **time travel**, **change data feed (CDF)**, and **column mapping**.

---

## 📌 Project Overview

This repo demonstrates:

- 📥 Data ingestion using Databricks notebooks and Autoloader (where applicable)
- 🧩 Transformations using Spark SQL and PySpark
- 🔁 UPSERTs (MERGE INTO) for deduplicating and merging data
- 🔄 Delta Lake Schema Evolution and Schema Overwrite
- 📈 Table Utility Commands for optimization and maintenance
- 🕰️ Data versioning and time travel capabilities
- 📤 Change Data Feed (CDF) to track row-level changes
- 🔐 Deletion Vectors for efficient deletes without rewriting files
- 🧾 Column Mapping (rename columns without rewrite)
- 🔍 Audit and rollback with historical snapshots

---

## 🛠️ Tech Stack

- **Databricks Community Edition**
- **Delta Lake 4.0**
- **Apache Spark 3.4+**
- **PySpark**
- **Notebook Format (.dbc or .ipynb)**

---

## ⚙️ Key Features Demonstrated

### 1. ✅ DeltaTable Upserts (MERGE INTO)
Used to **deduplicate incoming data**, implement **slowly changing dimensions (SCD Type 1/2)**, or manage **event-driven ingestion**.

```sql
MERGE INTO target_table AS t
USING source_table AS s
ON t.id = s.id
WHEN MATCHED THEN UPDATE SET *
WHEN NOT MATCHED THEN INSERT *
```

---

### 2. 🧬 Schema Evolution & Schema Overwrite

- **Schema Evolution:** Automatically updates schema when new columns are added during merge or write.
- **Schema Overwrite:** Manually enforce overwrite of table schema during write operation.

```python
df.write.option("mergeSchema", "true").format("delta").mode("append").save(delta_path)
```

---

### 3. 🧹 Deletion Vectors (Delta Lake 4.0)

Enables **deleting rows without rewriting Parquet files**, greatly improving performance of DELETE operations.

```sql
DELETE FROM table_name WHERE condition
```

> Files remain physically untouched — deletions are tracked via **metadata vectors**.

---

### 4. 🛠 Table Utility Commands

Useful commands used for maintenance:

- `OPTIMIZE`: File compaction
- `VACUUM`: File cleanup
- `DESCRIBE HISTORY`: Table version log
- `RESTORE`: Rollback to previous version

---

### 5. 🕰 Time Travel and Data Versioning

Access previous versions of a Delta Table using:

```sql
SELECT * FROM table_name VERSION AS OF 5
SELECT * FROM table_name TIMESTAMP AS OF '2025-07-01 00:00:00'
```

---

### 6. 📡 Change Data Feed (CDF)

Track **row-level inserts, updates, and deletes** between Delta table versions.

```sql
SELECT * FROM table_name
WHERE _change_type = 'update_postimage'
```

> Enables **incremental processing**, **CDC pipelines**, and **data auditing**.

---

### 7. ✍️ Column Mapping Mode (Delta Lake 4.0)

Allows **renaming columns** without physically rewriting Parquet files — using **name mapping mode**.

```sql
ALTER TABLE my_table RENAME COLUMN old_name TO new_name
```

> Requires: `delta.columnMapping.mode = 'name'`

---

## 📁 Folder Structure

```
├── notebooks/
│   ├── 1_DeltaLake.ipynb
│   ├── 2_DeltaLake.ipynb
│   ├── 3_DeltaLake.ipynb
│   ├── 4_DeltaLake.ipynb
│   ├── 5_DeltaLake.ipynb
│   ├── 6_DeltaLake.ipynb
│   ├── 7_DeltaLake.ipynb
│   ├── 8_DeltaLake.ipynb
│   ├── 9_DeltaLake.ipynb
├── README.md
```

---

## 📚 Learning Goals

By going through this project, you will:

- Understand how to fully leverage **Delta Lake 4.0**'s capabilities in **Databricks Free Edition**
- Learn to build **modular pipelines** with **upsert logic**, **schema handling**, and **audit trails**
- Master modern data lake features like **Time Travel** and **Change Data Feed**

---

## 🔍 References

- [Delta Lake Documentation](https://docs.delta.io/latest/index.html)
- [Databricks Community Edition](https://community.cloud.databricks.com/)
- [Delta 4.0 Release Notes](https://docs.delta.io/latest/releases.html#delta-lake-40)

---

## 🧠 Author & Contributions

Developed by [Dimakato Malope], Data Engineering & Analytics Enthusiast.

Feel free to fork, star ⭐ the repo, or submit a pull request if you'd like to add something!

---

