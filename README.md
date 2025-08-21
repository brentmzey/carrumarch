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
  - *AWS Step Functions*: Coordinates the entire workflow, ensuring each step happens in the right order.
  - *S3 Data Lake*: Holds both raw and processed data, making it easy to access and analyze.
  - *Lambda Functions*: Handle everything from CSV processing to data enrichment and extraction.

- **Data Warehouse & Transformation**  
  - *Snowflake*: Central repository for all analytics-ready data.
  - *dbt (Data Build Tool)*: Transforms raw data into clean, insightful models using SQL.

- **Reverse ETL & Data Delivery**  
  - *Lambda Functions*: Prepare and deliver data to marketing platforms.
  - *Marketing SFTP*: Supports bulk uploads via CSV.
  - *Marketing API*: Sends JSON payloads for real-time profile updates.

## How Data Flows

1. **Extraction**: Step Functions trigger Lambda jobs to pull data from the database and API.
2. **File Processing**: Lambda functions process incoming CSV files and store them in S3.
3. **Loading**: Data moves from S3 into Snowflake for centralized storage.
4. **Transformation**: dbt runs SQL models to clean and optimize the data.
5. **Delivery**: Lambda functions send the final datasets to marketing platforms, either as CSVs or JSON.

## Features That Make a Difference

- **Serverless by Design**: Built on AWS, the pipeline scales automatically and minimizes maintenance.
- **Data Freshness**: Ensures marketing always works with the most up-to-date information.
- **Quality Control**: Validation checks are woven throughout to maintain data integrity.
- **ELT Approach**: Raw data is stored first, then transformed as needed for flexibility and transparency.

## Looking Ahead

- Adding new data sources to enrich insights.
- Exploring real-time analytics for instant feedback on campaigns.

## Viewing the Architecture Diagram

The pipeline is visualized using Mermaid.js. You can view or edit the diagram using any of these methods:

### 1. Mermaid Live Editor

- Visit [Mermaid Live Editor](https://mermaid-js.github.io/mermaid-live-editor/)
- Copy the contents of [`architecture.mmd`](architecture.mmd) and paste them into the editor.

### 2. Local Markdown Editor

- Use an editor like Typora or Visual Studio Code with a Mermaid extension.
- Open the diagram file and enable preview to see the visualization.

### 3. Command Line (Mermaid CLI)

- Install Mermaid CLI:
  ```bash
  npm install -g @mermaid-js/mermaid-cli
  ```
- Generate a PNG from the diagram:
  ```bash
  mmdc -i architecture.mmd -o diagram.png
  ```

---