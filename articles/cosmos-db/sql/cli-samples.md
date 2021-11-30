---
title: Azure CLI Samples for Azure Cosmos DB | Microsoft Docs
description: This article lists several Azure CLI code samples available for interacting with Azure Cosmos DB. View API-specific CLI samples.
author: markjbrown
ms.service: cosmos-db
ms.subservice: cosmosdb-sql
ms.topic: sample
ms.date: 11/15/2021
ms.author: mjbrown 
ms.custom: devx-track-azurecli, seo-azure-cli
keywords: cosmos db, azure cli samples, azure cli code samples, azure cli script samples
---

# Azure CLI samples for Azure Cosmos DB Core (SQL) API
[!INCLUDE[appliesto-sql-api](../includes/appliesto-sql-api.md)]

The following table includes links to sample Azure CLI scripts for Azure Cosmos DB. Use the links on the right to navigate to API-specific samples. Common samples are the same across all APIs. Reference pages for all Azure Cosmos DB CLI commands are available in the [Azure CLI Reference](/cli/azure/cosmosdb). Azure Cosmos DB CLI script samples can also be found in the [Azure Cosmos DB CLI GitHub Repository](https://github.com/Azure-Samples/azure-cli-samples/tree/master/cosmosdb).

These samples require Azure CLI version 2.30 or later. Run `az --version` to find the version. If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli)

For Azure CLI samples for other APIs see [CLI Samples for Cassandra](../cassandra/cli-samples.md), [CLI Samples for MongoDB API](../mongodb/cli-samples.md), [CLI Samples for Gremlin](../graph/cli-samples.md), [CLI Samples for Table](../table/cli-samples.md)

## Common Samples

These samples apply to all Azure Cosmos DB APIs

|Task | Description |
|---|---|
| [Add or failover regions](../scripts/cli/common/regions.md?toc=%2fcli%2fazure%2ftoc.json) | Add a region, change failover priority, trigger a manual failover.|
| [Account keys and connection strings](../scripts/cli/common/keys.md?toc=%2fcli%2fazure%2ftoc.json) | List account keys, read-only keys, regenerate keys and list connection strings.|
| [Secure with IP firewall](../scripts/cli/common/ipfirewall.md?toc=%2fcli%2fazure%2ftoc.json)| Create a Cosmos account with IP firewall configured.|
| [Secure new account with service endpoints](../scripts/cli/common/service-endpoints.md?toc=%2fcli%2fazure%2ftoc.json)| Create a Cosmos account and secure with service-endpoints.|
| [Secure existing account with service endpoints](../scripts/cli/common/service-endpoints-ignore-missing-vnet.md?toc=%2fcli%2fazure%2ftoc.json)| Update a Cosmos account to secure with service-endpoints when the subnet is eventually configured.|
|||

## Core (SQL) API Samples

|Task | Description |
|---|---|
| [Create an Azure Cosmos account, database, and container](../scripts/cli/sql/create.md?toc=%2fcli%2fazure%2ftoc.json)| Creates an Azure Cosmos DB account, database, and container for Core (SQL) API. |
| [Create a serverless Azure Cosmos account, database, and container](../scripts/cli/sql/serverless.md?toc=%2fcli%2fazure%2ftoc.json)| Creates a serverless Azure Cosmos DB account, database, and container for Core (SQL) API. |
| [Create an Azure Cosmos account, database, and container with autoscale](../scripts/cli/sql/autoscale.md?toc=%2fcli%2fazure%2ftoc.json)| Creates an Azure Cosmos DB account, database, and container with autoscale for Core (SQL) API. |
| [Throughput operations](../scripts/cli/sql/throughput.md?toc=%2fcli%2fazure%2ftoc.json) | Read, update, and migrate between autoscale and standard throughput on a database and container.|
| [Lock resources from deletion](../scripts/cli/sql/lock.md?toc=%2fcli%2fazure%2ftoc.json)| Prevent resources from being deleted with  resource locks.|
|||
