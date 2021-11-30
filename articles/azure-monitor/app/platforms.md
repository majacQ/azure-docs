---
title: 'Application Insights: languages, platforms, and integrations | Microsoft Docs'
description: Languages, platforms, and integrations available for Application Insights
ms.topic: conceptual
ms.date: 10/29/2021

ms.reviewer: olegan
---

# Supported languages

* [C#|VB (.NET)](./asp-net.md)
* [Java](./java-in-process-agent.md)
* [JavaScript](./javascript.md)
* [Node.js](./nodejs.md)
* [Python](./opencensus-python.md)

## Supported platforms and frameworks

### Azure Service Integration (Portal Enablement, ARM Deployments)
* [Azure VM and Azure virtual machine scale sets](./azure-vm-vmss-apps.md)
* [Azure App Service](./azure-web-apps.md)
* [Azure Functions](../../azure-functions/functions-monitoring.md)
* [Azure Cloud Services](./cloudservices.md), including both web and worker roles

### Auto-instrumentation (enable without code changes)
* [ASP.NET - for web apps hosted with IIS](./status-monitor-v2-overview.md)
* [ASP.NET Core - for web apps hosted with IIS](./status-monitor-v2-overview.md)
* [Java](./java-in-process-agent.md)

### Manual instrumentation / SDK (some code changes required)
* [ASP.NET](./asp-net.md)
* [ASP.NET Core](./asp-net-core.md)
* [Node.js](./nodejs.md)
* [Python](./opencensus-python.md)
* [JavaScript - Web](./javascript.md)
  * [React](./javascript-react-plugin.md)
  * [React Native](./javascript-react-native-plugin.md)
  * [Angular](./javascript-angular-plugin.md)
* [Windows desktop applications, services, and worker roles](./windows-desktop.md)
* [Universal Windows app](../app/mobile-center-quickstart.md) (App Center)
* [Android](../app/mobile-center-quickstart.md) (App Center)
* [iOS](../app/mobile-center-quickstart.md) (App Center)

> [!NOTE]
> OpenTelemetry-based instrumentation is available in PREVIEW state for [C#, Node.js, and Python](opentelemetry-enable.md). Please review the limitations noted at the beginning of each langauge's official documentation. Those who require a full-feature experience should use the existing Application Insights SDKs.

## Logging frameworks
* [ILogger](./ilogger.md)
* [Log4Net, NLog, or System.Diagnostics.Trace](./asp-net-trace-logs.md)
* [Java, Log4J, or Logback](java-2x-trace-logs.md)
* [LogStash plugin](https://github.com/Azure/azure-diagnostics-tools/tree/master/Logstash/logstash-output-applicationinsights)
* [Azure Monitor](/archive/blogs/msoms/application-insights-connector-in-oms)

## Export and data analysis
* [Power BI](https://powerbi.microsoft.com/blog/explore-your-application-insights-data-with-power-bi/)
* [Stream Analytics](./export-power-bi.md)

## Unsupported SDKs
Several other community-supported Application Insights SDKs exist. However, Azure Monitor only provides support when using the supported instrumentation options listed on this page. We're constantly assessing opportunities to expand our support for other languages. Follow [Azure Updates for Application Insights](https://azure.microsoft.com/updates/?query=application%20insights) for the latest SDK news.
