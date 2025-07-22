This project implements a serverless, incremental data ingestion pipeline using Azure Data Factory (ADF) to transfer data from Azure PostgreSQL Flexible Server to Azure Data Lake Storage Gen2 (ADLS Gen2) in a structured and cost-effective way.

## 📊 Data Flow Diagram - Incremental Load Pipeline

```mermaid
flowchart TD
    A[Azure PostgreSQL] --> B[ADF Pipeline]
    B --> C[ADLS Gen2 Storage]
    B --> D[Azure Table Storage Watermark]

    subgraph Pipeline_Flow
        B1[Lookup Watermark] --> B2[Copy Incremental Data]
        B2 --> B3[Write to ADLS]
        B3 --> B4[Get Max Timestamp]
        B4 --> B5[Update Watermark]
    end

    A --> B1
    B5 --> D
