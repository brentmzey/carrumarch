# Data Pipeline Architecture for Carrum Health

This project outlines a data pipeline architecture designed to empower data-driven marketing campaigns by utilizing data from multiple sources. The architecture is visualized using Mermaid.js and provides a scalable and cost-effective solution for processing and delivering click data to marketing platforms.

## Overview

The architecture is designed to handle data ingestion, transformation, and delivery across a variety of platforms and formats, enabling real-time insights into user interactions with a simple (pretend) app.

## Architecture Components

- **Data Sources**:
  - **Postgres DB**: Storing first-party click data from the app backend.
  - **3rd Party Realtime API**: Providing the most recent click timestamps for buttons A and B.
  - **Cloud Bucket**: Delivering batch CSV files containing historical click data for button C.

- **Ingestion & Orchestration** (AWS):
  - **Airflow**: Schedules and orchestrates daily data processing workflows.
  - **S3 Data Lake**: Stores raw and staging data in Parquet format for efficient processing.
  - **Lambda**: Processes CSV file arrivals and stores them in S3.
  - **Fargate**: Runs scheduled tasks for extracting data and preparing it for transformation.

- **Data Warehouse & Transformation**:
  - **Snowflake**: Centralizes data storage and facilitates queries at scale.
  - **dbt (Data Build Tool)**: Implements SQL transformations to prepare optimized click data.

- **Reverse ETL & Data Delivery**:
  - **Fargate**: Facilitates transformation and delivery of data to marketing systems.
  - **Marketing SFTP**: Supports the bulk upload of CSV files.
  - **Marketing API**: Sends JSON payloads to update user profiles in real-time.

## Data Flow

1. **Extraction**: Airflow triggers extraction jobs using Fargate to pull data from Postgres and the 3rd party API.
2. **File Processing**: Lambda processes CSV arrivals and loads data into the S3 Data Lake.
3. **Loading**: Data is loaded into Snowflake from S3.
4. **Transformation**: dbt runs SQL models to transform raw data into user segments with recent click aggregation.
5. **Delivery**: Transformed data is prepared for delivery to the marketing platform via SFTP or API.

## Key Features

- **Scalable and Cost-Efficient**: Utilizes AWS serverless technologies to optimize costs and scale with demand.
- **Data Freshness**: Ensures all delivered data is recent and aligns with marketing strategies.
- **Complex Transformations**: Leverages dbt and Snowflake for robust data processing and transformation logic.

## Assumptions & Considerations

- Designed to handle approximately 10 million users.
- Data quality and validation checks at each integration point ensure reliability.
- Strategic use of ELT processes by storing raw data initially, then transforming as needed.

## Future Enhancements

- Integration with additional data sources.
- Real-time analytics for immediate campaign adaptability and insights.

This architecture provides a comprehensive solution for delivering actionable insights to the Carrum Health marketing team, enabling targeted and effective data-driven campaigns.