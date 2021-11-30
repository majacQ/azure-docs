---
title: Monitor SAP on Azure (preview) | Microsoft Docs
description: Start here to learn how to monitor SAP on Azure.
author: mamccrea
ms.service: virtual-machines-sap
ms.subservice: baremetal-sap
ms.topic: article
ms.custom: subject-monitoring
ms.date: 10/13/2021
ms.author: mamccrea

---

# Monitor SAP on Azure (preview)

When you have critical applications and business processes relying on Azure resources, you'll want to monitor those resources for their availability, performance, and operation. 

This article describes how to monitor SAP running on Azure using Azure Monitor for SAP Solutions. Azure Monitor for SAP Solutions uses specific parts of the [Azure Monitor](../../../azure-monitor/overview.md) infrastructure.

## Overview

Azure Monitor for SAP Solutions is an Azure-native monitoring product for anyone running their SAP landscapes on Azure. It works with both [SAP on Azure Virtual Machines](./hana-get-started.md) and [SAP on Azure Large Instances](./hana-overview-architecture.md).

With Azure Monitor for SAP Solutions, you can collect telemetry data from Azure infrastructure and databases in one central location and visually correlate the data for faster troubleshooting.

You can monitor different components of an SAP landscape, such as Azure virtual machines (VMs), high-availability cluster, SAP HANA database, SAP NetWeaver, and so on, by adding the corresponding **provider** for that component. For more information, see [Deploy Azure Monitor for SAP Solutions by using the Azure portal](azure-monitor-sap-quickstart.md).

Supported infrastructure:

- Azure virtual machine
- Azure Large Instance

Supported databases:
- SAP HANA Database
- Microsoft SQL server

Azure Monitor for SAP Solutions uses the [Azure Monitor](../../../azure-monitor/overview.md) capabilities of [Log Analytics](../../../azure-monitor/logs/log-analytics-overview.md) and [Workbooks](../../../azure-monitor/visualize/workbooks-overview.md). With it, you can:

- Create [custom visualizations](../../../azure-monitor/visualize/workbooks-overview.md#getting-started) by editing the default Workbooks provided by Azure Monitor for SAP Solutions. 
- Write [custom queries](../../../azure-monitor/logs/log-analytics-tutorial.md).
- Create [custom alerts](../../../azure-monitor/alerts/alerts-log.md) by using Azure Log Analytics workspace. 
- Take advantage of the [flexible retention period](../../../azure-monitor/logs/manage-cost-storage.md#change-the-data-retention-period) in Azure Monitor Logs/Log Analytics. 
- Connect monitoring data with your ticketing system.

## What data does Azure Monitor for SAP Solutions collect?

Azure Monitor for SAP Solutions doesn't collect Azure Monitor metrics or resource log data as does many other Azure resources. Instead, it sends custom logs directly to the Azure Monitor Logs system, where you can then use the built-in features of Log Analytics.

Data collection in Azure Monitor for SAP Solutions depends on the providers that you configure. During public preview, the following data is collected.

High-availability Pacemaker cluster telemetry:
- Node, resource, and STONITH block device (SBD) status
- Pacemaker location constraints
- Quorum votes and ring status
- [Others](https://github.com/ClusterLabs/ha_cluster_exporter/blob/master/doc/metrics.md)

SAP HANA telemetry:
- CPU, memory, disk, and network use
- HANA system replication (HSR)
- HANA backup
- HANA host status
- Index server and name server roles
- Database growth
- Top tables
- File system use

Microsoft SQL server telemetry:
- CPU, memory, disk use
- Hostname, SQL instance name, SAP system ID
- Batch requests, compilations, and Page Life Expectancy over time
- Top 10 most expensive SQL statements over time
- Top 12 largest table in the SAP system
- Problems recorded in the SQL Server error log
- Blocking processes and SQL wait statistics over time

Operating system telemetry (Linux): 
- CPU use, fork's count, running and blocked processes 
- Memory use and distribution among used, cached, buffered 
- Swap use, paging, and swap rate 
- File systems usage, number of bytes read and written per block device 
- Read/write latency per block device 
- Ongoing I/O count, persistent memory read/write bytes 
- Network packets in/out, network bytes in/out 

SAP NetWeaver telemetry:

- SAP system and application server availability, including: instance process availability of dispatcher, ICM, gateway, message server, Enqueue Server, IGS Watchdog
- Work process usage statistics and trends
- Enqueue Lock statistics and trends
- Queue usage statistics and trends

## Data sharing with Microsoft

Azure Monitor for SAP Solutions collects system metadata to provide improved support for SAP on Azure. No PII/EUII is collected.

You can enable data sharing with Microsoft when you create Azure Monitor for SAP Solutions resource by choosing *Share* from the drop-down. We recommend that you enable data sharing. Data sharing gives Microsoft support and engineering teams information about your environment, which helps us provide better support for your mission-critical SAP on Azure solution.

## Architecture overview

The following diagram shows, at a high level, how Azure Monitor for SAP Solutions collects telemetry from SAP HANA database. The architecture is the same whether SAP HANA is deployed on Azure VMs or Azure Large Instances.

![Azure Monitor for SAP solutions architecture](https://user-images.githubusercontent.com/75772258/115046700-62ff3280-9ef5-11eb-8d0d-cfcda526aeeb.png)

The key components of the architecture are:
- **Azure portal** – Your starting point. You can navigate to marketplace within Azure portal and discover Azure Monitor for SAP Solutions.
- **Azure Monitor for SAP Solutions resource** - A landing place for you to view monitoring telemetry.
- **Managed resource group** – Deployed automatically as part of the Azure Monitor for SAP Solutions resource deployment. The resources deployed within managed resource group help with collection of telemetry. Key resources deployed and their purposes are:
   - **Azure virtual machine**: Also known as *collector VM*, it's a Standard_B2ms VM. The main purpose of this VM is to host the *monitoring payload*. Monitoring payload refers to the logic of collecting telemetry from the source systems and transferring the data to the monitoring framework. In the preceding diagram, the monitoring payload contains the logic to connect to SAP HANA database over SQL port.
   - **[Azure Key Vault](../../../key-vault/general/basic-concepts.md)**: This resource is deployed to securely hold SAP HANA database credentials and to store information about [providers](./azure-monitor-providers.md).
   - **Log Analytics Workspace**: The destination where the telemetry data is stored.
      - Visualization is built on top of telemetry in Log Analytics using [Azure Workbooks](../../../azure-monitor/visualize/workbooks-overview.md). You can customize visualization. You can also pin your Workbooks or specific visualization within Workbooks to Azure dashboard for autorefresh. The maximum frequency for refresh is every 30 minutes.
      - You can use your existing workspace within the same subscription as SAP monitor resource by choosing this option at deployment.
      - You can use Kusto query language (KQL) to run [queries](../../../azure-monitor/logs/log-query-overview.md) against the raw tables inside Log Analytics workspace. Look at *Custom Logs*.

> [!Note]
> You are responsible for patching and maintaining the VM, deployed in the managed resource group.

> [!Tip]
> You can use an existing Log Analytics workspace for telemetry collection if it's deployed within the same Azure subscription as the resource for Azure Monitor for SAP Solutions.

### Architecture highlights

Here are the key highlights of the architecture:
 - **Multi-instance** - You can monitor multiple instances of a given component type (for example, HANA database, high availability (HA) cluster, Microsoft SQL server, SAP NetWeaver) across multiple SAP SIDs within a VNET with a single resource of Azure Monitor for SAP Solutions.
 - **Multi-provider** - The preceding architecture diagram shows the SAP HANA provider as an example. Similarly, you can configure more providers for corresponding components to collect data from those components. For example, HANA DB, HA cluster, Microsoft SQL server, and SAP NetWeaver. 
 - **Open source** - The source code of Azure Monitor for SAP Solutions is available in [GitHub](https://github.com/Azure/AzureMonitorForSAPSolutions). You can refer to the provider code and learn more about the product, contribute, or share feedback.
 - **Extensible query framework** - SQL queries to collect telemetry data are written in [JSON](https://github.com/Azure/AzureMonitorForSAPSolutions/blob/master/sapmon/content/SapHana.json). More SQL queries to collect more telemetry data can be easily added. You can request specific telemetry data to be added to Azure Monitor for SAP Solutions. Do so by leaving feedback using the link at the end of this article. You can also leave feedback by contacting your account team.

## Analyzing metrics

Azure Monitor for SAP Solutions doesn't support metrics. 

## Analyzing logs

Azure Monitor for SAP Solutions doesn't support resource logs or activity logs. For a list of the tables used by Azure Monitor Logs that can be queried by Log Analytics, see [Monitor SAP on Azure data reference](monitor-sap-on-azure-reference.md#azure-monitor-logs-tables). 

### Sample Kusto queries

> [!IMPORTANT]
> When you select **Logs** from the Azure Monitor for SAP Solutions menu, Log Analytics is opened with the query scope set to the current Azure Monitor for SAP Solutions. This means that log queries will only include data from that resource. If you want to run a query that includes data from other accounts or data from other Azure services, select **Logs** from the **Azure Monitor** menu. See [Log query scope and time range in Azure Monitor Log Analytics](../../../azure-monitor/logs/scope.md) for details.

You can use Kusto queries to help you monitor your Monitor SAP on Azure resources. Here's a sample query that gives you data from a custom log for a specified time range. You specify the time range and the number of rows. In this example, you'll get five rows of data for your selected time range. 

```Kusto
custom log name 
| take 5

```

## Alerts

Azure Monitor alerts proactively notify you when important conditions are found in your monitoring data. They allow you to identify and address issues in your system before your customers notice them.

You can configure alerts in Azure Monitor for SAP Solutions from the Azure portal. For more information, see [Configure Alerts in Azure Monitor for SAP Solutions by using the Azure portal](azure-monitor-alerts-portal.md).

## Create Azure Monitor for SAP Solutions resources

You have several options to deploy Azure Monitor for SAP Solutions and configure providers: 
- You can deploy Azure Monitor for SAP Solutions right from the Azure portal. For more information, see [Deploy Azure Monitor for SAP Solutions by using the Azure portal](azure-monitor-sap-quickstart.md).
- Use Azure PowerShell. For more information, see [Deploy Azure Monitor for SAP Solutions with Azure PowerShell](azure-monitor-sap-quickstart-powershell.md).
- Use the CLI extension. For more information, see the [SAP HANA Command Module](https://github.com/Azure/azure-hanaonazure-cli-extension#sapmonitor).

## Pricing
Azure Monitor for SAP Solutions is a free product (no license fee). You're responsible for paying the cost of the underlying components in the managed resource group. You're also responsible for consumption costs associated with data use and retention. For more information, see standard Azure pricing documents:
- [Azure VM pricing](https://azure.microsoft.com/pricing/details/virtual-machines/linux/)
- [Azure Key vault pricing](https://azure.microsoft.com/pricing/details/key-vault/)
- [Azure storage account pricing](https://azure.microsoft.com/pricing/details/storage/queues/)
- [Azure Log Analytics and alerts pricing](https://azure.microsoft.com/pricing/details/monitor/)

## Next steps

- For a list of custom logs relevant to Azure Monitor for SAP Solutions and information on related data types, see [Monitor SAP on Azure data reference](monitor-sap-on-azure-reference.md).
- For information on providers available for Azure Monitor for SAP Solutions, see [Azure monitor for SAP Solutions providers](azure-monitor-providers.md).
