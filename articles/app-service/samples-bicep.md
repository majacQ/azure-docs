---
title: Bicep samples
description: Find Bicep samples for some of the common App Service scenarios. Learn how to automate your App Service deployment or management tasks.
author: seligj95
tags: azure-service-management

ms.topic: sample
ms.date: 8/26/2021
ms.author: jordanselig
ms.custom: mvc, fasttrack-edit
---
# Bicep files for App Service

The following table includes links to Bicep files for Azure App Service. For quickstarts and further information about Bicep, see [Bicep documentation](../azure-resource-manager/bicep/index.yml).

To learn about the Bicep syntax and properties for App Services resources, see [Microsoft.Web resource types](/azure/templates/microsoft.web/allversions).

| Deploying an app | Description |
|-|-|
| [App Service plan and basic Linux app](https://github.com/Azure/bicep/tree/main/docs/examples/101/web-app-linux) | Deploys an App Service app that is configured for Linux. |
| [App Service plan and basic Windows app](https://github.com/Azure/bicep/tree/main/docs/examples/101/web-app-windows) | Deploys an App Service app that is configured for Windows. |
| [Website with container](https://github.com/Azure/bicep/tree/main/docs/examples/101/website-with-container) | Deploys a website from a docker image configured for Linux. |
| **Configuring an app** | **Description** |
| [App with conditional logging](https://github.com/Azure/bicep/tree/main/docs/examples/201/web-app-conditional-log)| Deploys an App Service app with a conditional for logging enablement. |
| [App with log analytics module](https://github.com/Azure/bicep/tree/main/docs/examples/201/web-app-loganalytics-mod)| Deploys an App Service app with log analytics. |
| [App with regional VNet integration](https://github.com/Azure/bicep/tree/main/docs/examples/101/app-service-regional-vnet-integration)| Deploys an App Service app with regional VNet integration enabled. |
|**App with connected resources**| **Description** |
| [App with CosmosDB](https://github.com/Azure/bicep/tree/main/docs/examples/101/cosmosdb-webapp)| Deploys an App Service app on Linux with CosmosDB. |
| [App with MySQL](https://github.com/Azure/bicep/tree/main/docs/examples/101/webapp-managed-mysql)| Deploys an App Service app on Windows with Azure Database for MySQL. |
| [App with a database in Azure SQL Database](https://github.com/Azure/bicep/tree/main/docs/examples/201/web-app-sql-database)| Deploys an App Service app and a database in Azure SQL Database at the Basic service level. |
| [App connected to a backend webapp](https://github.com/Azure/bicep/tree/main/docs/examples/101/webapp-privateendpoint-vnet-injection)| Deploys two web apps (frontend and backend) securely connected together with VNet injection and Private Endpoint. |
| [App with a database, managed identity, and monitoring](https://github.com/Azure/bicep/tree/main/docs/examples/301/web-app-managed-identity-sql-db)| Deploys an App Service App with a database, managed identity, and monitoring. |
|**App Service Environment**| **Description** |
| [Create an App Service environment v2](https://github.com/Azure/bicep/tree/main/docs/examples/201/web-app-asev2-create) | Creates an App Service environment v2 in your virtual network. |
| | |