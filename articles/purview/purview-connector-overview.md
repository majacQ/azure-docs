---
title: Purview Connector Overview
description: This article outlines the different data stores and functionalities supported in Purview
author: linda33wj
ms.author: jingwang
ms.service: purview
ms.subservice: purview-data-map
ms.topic: conceptual
ms.date: 11/23/2021
ms.custom: ignite-fall-2021
---

# Supported data stores

Purview supports the following data stores. Select each data store to learn the supported capabilities and the corresponding configurations in details.

## Purview data sources

|**Category**|  **Data Store**  |**Technical metadata** |**Classification** |**Lineage** | **Access Policy** |
|---|---|---|---|---|---|
| Azure | [Azure Blob Storage](register-scan-azure-blob-storage-source.md)| [Yes](register-scan-azure-blob-storage-source.md#register) | [Yes](register-scan-azure-blob-storage-source.md#scan)| Limited* | [Yes](how-to-access-policies-storage.md) |
||    [Azure Cosmos DB](register-scan-azure-cosmos-database.md)| [Yes](register-scan-azure-cosmos-database.md#register) | [Yes](register-scan-azure-cosmos-database.md#scan)|No*|No|
||    [Azure Data Explorer](register-scan-azure-data-explorer.md)| [Yes](register-scan-azure-data-explorer.md#register) | [Yes](register-scan-azure-data-explorer.md#scan)| No* | No |
||    [Azure Data Lake Storage Gen1](register-scan-adls-gen1.md)| [Yes](register-scan-adls-gen1.md#register) | [Yes](register-scan-adls-gen1.md#scan)| Limited* | No |
||    [Azure Data Lake Storage Gen2](register-scan-adls-gen2.md)| [Yes](register-scan-adls-gen2.md#register) | [Yes](register-scan-adls-gen2.md#scan)| Limited* | [Yes](how-to-access-policies-storage.md) |
|| [Azure Database for MySQL](register-scan-azure-mysql-database.md) | [Yes](register-scan-azure-mysql-database.md#register) | [Yes](register-scan-azure-mysql-database.md#scan) | No* | No |
|| [Azure Database for PostgreSQL](register-scan-azure-postgresql.md) | [Yes](register-scan-azure-postgresql.md#register) | [Yes](register-scan-azure-postgresql.md#scan) | No* | No |
||    [Azure Dedicated SQL pool (formerly SQL DW)](register-scan-azure-synapse-analytics.md)| [Yes](register-scan-azure-synapse-analytics.md#register) | [Yes](register-scan-azure-synapse-analytics.md#scan)| No* | No |
||    [Azure Files](register-scan-azure-files-storage-source.md)|[Yes](register-scan-azure-files-storage-source.md#register) | [Yes](register-scan-azure-files-storage-source.md#scan) | Limited* |  No |
||    [Azure SQL Database](register-scan-azure-sql-database.md)| [Yes](register-scan-azure-sql-database.md#register) |[Yes](register-scan-azure-sql-database.md#scan)| No* | No |
||    [Azure SQL Database Managed Instance](register-scan-azure-sql-database-managed-instance.md)|  [Yes](register-scan-azure-sql-database-managed-instance.md#scan) | [Yes](register-scan-azure-sql-database-managed-instance.md#scan) | No* | No |
||    [Azure Synapse Analytics (Workspace)](register-scan-synapse-workspace.md)| [Yes](register-scan-synapse-workspace.md#register) | [Yes](register-scan-synapse-workspace.md#scan)| [Yes - Synapse pipelines](how-to-lineage-azure-synapse-analytics.md)| No|
|Database| [Amazon RDS](register-scan-amazon-rds.md) | [Yes](register-scan-amazon-rds.md#register-an-amazon-rds-data-source) | [Yes](register-scan-amazon-rds.md#scan-an-amazon-rds-database) | No | No |
||    [Cassandra](register-scan-cassandra-source.md)|[Yes](register-scan-cassandra-source.md#register) | No | [Yes](how-to-lineage-cassandra.md)| No|
|| [DB2](register-scan-db2.md) | [Yes](register-scan-db2.md#register) | No | [Yes](register-scan-db2.md#scan) | No |
||    [Google BigQuery](register-scan-google-bigquery-source.md)| [Yes](register-scan-google-bigquery-source.md#register)| No | [Yes](how-to-lineage-google-bigquery.md)| No|
|| [Hive Metastore Database](register-scan-hive-metastore-source.md) | [Yes](register-scan-hive-metastore-source.md#register) | No | Yes* | No|
|| [MySQL](register-scan-mysql.md) | [Yes](register-scan-mysql.md#register) | No | [Yes](register-scan-mysql.md#scan) | No |
|| [Oracle](register-scan-oracle-source.md) | [Yes](register-scan-oracle-source.md#register)|  No | [Yes*](how-to-lineage-oracle.md) | No|
|| [PostgreSQL](register-scan-postgresql.md) | [Yes](register-scan-postgresql.md#register) | No | [Yes](register-scan-postgresql.md#scan) | No |
|| [Snowflake](register-scan-snowflake.md) | [Yes](register-scan-snowflake.md#register) | No | [Yes](register-scan-snowflake.md#scan) | No |
||    [SQL Server](register-scan-on-premises-sql-server.md)| [Yes](register-scan-on-premises-sql-server.md#register) |[Yes](register-scan-on-premises-sql-server.md#scan) | No* | No|
||    [Teradata](register-scan-teradata-source.md)| [Yes](register-scan-teradata-source.md#register)|  No | [Yes*](how-to-lineage-teradata.md) | No|
|File|[Amazon S3](register-scan-amazon-s3.md)|[Yes](register-scan-amazon-s3.md)| [Yes](register-scan-amazon-s3.md)| Limited* | No|
|Services and apps|    [Erwin](register-scan-erwin-source.md)| [Yes](register-scan-erwin-source.md#register)| No | [Yes](how-to-lineage-erwin.md)| No|
||    [Looker](register-scan-looker-source.md)| [Yes](register-scan-looker-source.md#register)| No | [Yes](how-to-lineage-looker.md)| No|
||    [Power BI](register-scan-power-bi-tenant.md)| [Yes](register-scan-power-bi-tenant.md#register)| No | [Yes](how-to-lineage-powerbi.md)| No|
|| [Salesforce](register-scan-salesforce.md) | [Yes](register-scan-salesforce.md#register) | No | No | No |
||    [SAP ECC](register-scan-sapecc-source.md)| [Yes](register-scan-sapecc-source.md#register) | No | [Yes*](how-to-lineage-sapecc.md) | No|
|| [SAP S/4HANA](register-scan-saps4hana-source.md) | [Yes](register-scan-saps4hana-source.md#register)| No | [Yes*](how-to-lineage-sapecc.md) | No|

\* Besides the lineage on assets within the data source, lineage is also supported if dataset is used as a source/sink in [Data Factory](how-to-link-azure-data-factory.md) or [Synapse pipeline](how-to-lineage-azure-synapse-analytics.md).

> [!NOTE]
> Currently, Purview can't scan an asset that has `/`, `\`, or `#` in its name. To scope your scan and avoid scanning assets that have those characters in the asset name, use the example in [Register and scan an Azure SQL Database](register-scan-azure-sql-database.md#creating-the-scan).

## Scan regions
The following is a list of all the Azure data source (data center) regions where the Purview scanner runs. If your Azure data source is in a region outside of this list, the scanner will run in the region of your Purview instance.

### Purview scanner regions

- Australia East
- Australia Southeast
- Brazil South
- Canada Central
- Central India
- Central US
- East Asia
- East US
- East US 2
- France Central
- Japan East
- Korea Central
- North Central US
- North Europe
- South Africa North
- South Central US
- Southeast Asia
- UAE North
- UK South
- West Central US
- West Europe
- West US
- West US 2

## Next steps

- [Register and scan Azure Blob storage source](register-scan-azure-blob-storage-source.md)