# Metadata-Driven Azure Data Factory ETL Pipeline

## Overview

Developed an end-to-end Azure Data Factory pipeline to ingest EdTech tutoring data from Excel files in Azure Data Lake Storage Gen2 into Azure SQL Database and incrementally load the processed data into the Data Lake Bronze layer.

The pipeline uses parameterized metadata, dynamic SQL queries, and JSON-based watermark tracking to support both scheduled incremental loads and historical backfills.

## Architecture

```text
Excel File in ADLS Gen2
          ↓
Azure Data Factory
          ↓
Azure SQL Staging Table
          ↓
Incremental CDC Extraction
          ↓
Parquet Files in ADLS Bronze Layer
```

## Key Features

* Built a parameterized, metadata-driven ADF pipeline using schema name, table name, CDC column, start date, and end date configurations.
* Loaded Excel data into Azure SQL with column mapping and data-type conversion.
* Implemented JSON-based watermark tracking to process only newly available records.
* Supported both daily incremental ingestion and historical date-range backfills.
* Generated Snappy-compressed Parquet files with dynamic folder and filename creation.
* Automatically deleted empty output files and updated the CDC watermark after successful loads.

## Technologies Used

* Azure Data Factory
* Azure Data Lake Storage Gen2
* Azure SQL Database
* Parquet
* Snappy Compression
* JSON
* Dynamic ADF Expressions
* GitHub

## Pipeline Workflow

1. Read the Excel dataset from ADLS Gen2.
2. Load the data into the Azure SQL staging table.
3. Read the previous watermark from `cdc.json`.
4. Extract only records newer than the stored watermark.
5. Write the extracted data to the Bronze layer in Parquet format.
6. Delete the output file when no records are found.
7. Update the watermark after a successful load.

## Repository Structure

```text
dataset/         ADF dataset definitions
linkedService/   Azure SQL and ADLS connections
pipeline/        Main ADF pipeline
factory/         Data Factory configuration
```

## Skills Demonstrated

Azure Data Factory pipeline design, ETL development, incremental loading, CDC and watermark handling, metadata-driven processing, dynamic SQL, historical backfills, Azure SQL integration, ADLS Gen2, and Parquet data storage.
