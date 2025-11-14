# Automated Flight Delay ETL Pipeline on GCP

## Overview
This project implements a **daily ETL pipeline** for Spark Airways to process flight data stored as JSON in **Google Cloud Storage (GCS)**. The pipeline calculates **average flight delays** by flight number and distance and stores the results in **BigQuery** for analytics.  

The pipeline is fully automated using **Apache Airflow**, leverages **PySpark** for transformations, and dynamically manages resources on GCP for efficiency.  

---

## Technologies
- **PySpark & Spark SQL** – data transformation and aggregation  
- **Apache Airflow (Cloud Composer)** – pipeline orchestration  
- **Google Cloud Storage (GCS)** – raw and transformed data storage  
- **BigQuery** – analytics and partitioned tables  
- **Google Cloud Dataproc** – ephemeral Spark cluster  
- **Shell scripting** – for BigQuery table creation  

---

## Pipeline Architecture

![Pipeline](resources/pipeline.png)

**ETL Steps:**

1. **BigQuery Table Setup** – Create `avg_delays_by_flight_nums` and `avg_delays_by_distance` tables using BQ shell scripts.  
2. **Cluster Provisioning** – Spin up an ephemeral **Dataproc cluster** for Spark processing.  
3. **Data Extraction & Transformation** – Load daily JSON files into PySpark, calculate average delays using Spark SQL, and produce output tables.  
4. **Save to GCS** – Store transformed data in a GCS output bucket.  
5. **Load to BigQuery** – Load the transformed data from GCS into partitioned BigQuery tables.  
6. **Cleanup** – Delete the Dataproc cluster and temporary GCS output files.  
7. **Automation** – Use **Airflow DAGs** to schedule and automate the entire ETL pipeline.  

---

## Features
- **Dynamic Scheduling:** Runs daily to handle new flight data automatically.  
- **Scalable Processing:** Uses ephemeral Dataproc clusters to efficiently process large datasets.  
- **Partitioned BigQuery Tables:** Optimized for analytics and query performance.  
- **End-to-End Automation:** Airflow orchestrates all steps from extraction to loading.  

---

## Usage
1. Upload daily JSON flight data to the GCS input bucket.  
2. Deploy Airflow DAGs to Cloud Composer.  
3. Monitor pipeline execution via the Airflow UI.  
4. Query results in BigQuery for analytics.  
