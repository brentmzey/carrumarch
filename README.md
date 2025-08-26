# Carrum Health Data Pipeline Architecture

Welcome! This repository documents the data pipeline architecture designed for Carrum Health’s marketing analytics. The goal is to empower the marketing team with timely, reliable insights by connecting multiple data sources and automating the flow from raw data to actionable information.

## Why This Matters

Marketing teams thrive on fresh, accurate data. By integrating diverse sources—ranging from app click logs to third-party APIs and cloud-based CSVs—this pipeline ensures that every campaign is informed by the latest user interactions. The architecture is built to scale, so whether you’re reaching thousands or millions, the data keeps up.

## What’s Inside

- **Data Sources**  
  - *Postgres Database*: Stores click data from the app backend.
  - *Third-Party API*: Provides real-time click events for specific buttons.
  - *Cloud Bucket*: Delivers batch CSV files with historical click data.

- **Ingestion & Orchestration**  
  - Solutions vary based on cloud provider (AWS or Azure).

- **Data Warehouse & Transformation**  
  - *Snowflake*: Central repository for all analytics-ready data (AWS).
  - *Azure Synapse Analytics*: Used for scalable analytics and storage (Azure).
  - *dbt (Data Build Tool)*: Transforms raw data into clean, insightful models using SQL.

- **Reverse ETL & Data Delivery**  
  - Solutions vary: serverless functions prepare and deliver data to marketing platforms.

## AWS Solution Overview

- **Ingestion & Orchestration**  
  - *AWS Step Functions*: Orchestrates the entire workflow.
  - *S3 Data Lake*: Stores raw and processed data.
  - *Lambda Functions*: Handle data processing, enrichment, and delivery.

- **Data Warehouse & Transformation**  
  - *Snowflake*: Houses processed data for analysis.
  - *dbt*: Executes SQL models to transform data.

- **Reverse ETL & Data Delivery**  
  - *Lambda Functions*: Deliver data as CSV via SFTP or JSON via an API.

## Azure Solution Overview

- **Ingestion & Orchestration**  
  - *Azure Logic Apps*: Orchestrates processes.
  - *Azure Data Lake Storage*: Holds raw and processed files.
  - *Azure Functions*: Perform data extraction and CSV processing.

- **Data Warehouse & Transformation**  
  - *Azure Synapse Analytics*: Integrates storage and analytics.
  - *dbt*: Utilized for transforming data within Azure.

- **Reverse ETL & Data Delivery**  
  - *Azure Functions*: Manage data delivery to marketing platforms.

## Comparing AWS and Azure Solutions

- **Scalability and Cost**: Both solutions are inherently scalable via their serverless components. AWS and Azure both provide cost-effective ways to handle large data volumes.
- **Integration and Reliability**: Both ecosystems offer robust services for real-time and batch processing. Choice may depend on existing infrastructure and expertise in a given platform.
- **Flexibility**: Both architectures offer similar flexibility in terms of adding new data sources or adapting to changes in data structures or processing requirements.

## How Data Flows

1. **Extraction**: Orchestration tools trigger functions to pull data from the database and API.
2. **File Processing**: Serverless functions process incoming CSV files and store them in a data lake.
3. **Loading**: Data moves into the data warehouse for centralized storage.
4. **Transformation**: dbt runs SQL models to clean and optimize the data.
5. **Delivery**: Functions send the final datasets to marketing platforms, either as CSVs or JSON.

## Features That Make a Difference

- **Serverless by Design**: Built on AWS or Azure, the pipeline scales automatically and reduces maintenance.
- **Data Freshness**: Ensures marketing always works with up-to-date information.
- **Quality Control**: Validation checks maintain data integrity.
- **ELT Approach**: Raw data is stored first, then transformed as needed for flexibility and transparency.

## Looking Ahead

- Adding new data sources to enrich insights.
- Exploring real-time analytics for instant feedback on campaigns.

## Viewing the Architecture Diagrams

The pipeline is visualized using Mermaid.js. You can view or edit the diagrams using any of these methods:

### 1. Mermaid Live Editor

- Visit [Mermaid Live Editor](https://mermaid-js.github.io/mermaid-live-editor/)
- Copy the contents of [`architecture.mmd`](architecture.mmd) or [`azure-architecture.mmd`](azure-architecture.mmd) and paste them into the editor.

### 2. Local Markdown Editor

- Use an editor like Visual Studio Code with a Mermaid extension.
- Open the diagram file and enable preview to see the visualization.

### 3. Command Line (using local Mermaid CLI)

First, ensure all dependencies are installed:

```bash
npm install
```

To generate the diagrams from the .mmd files, use the following npm script:

```bash
npm run generate-diagrams
```

This command will process the .mmd files and output the respective .png images in the carrum/arch directory.
