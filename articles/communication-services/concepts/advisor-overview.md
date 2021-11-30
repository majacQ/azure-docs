---
title: Leverage Azure Advisor for Azure Communication Services
titleSuffix: An Azure Communication Services concept document
description: Learn about Azure Advisor offerings for Azure Communication Services.
author: probableprime

manager: chpalm
services: azure-communication-services

ms.author: rifox
ms.date: 09/30/2021
ms.topic: conceptual
ms.service: azure-communication-services
ms.subservice: data
---

# Azure Advisor for Azure Communication Services

[Azure Advisor](../../advisor/advisor-overview.md) is a personalized cloud consultant that helps you follow best practices to optimize your Azure deployments. Azure Communication Services is onboarded to Azure Advisor and will post recommendations for ways to optimize your communication resources. You can view these recommendations in the [Azure portal](https://portal.azure.com) in the [Advisor blade](https://portal.azure.com/#blade/Microsoft_Azure_Expert/AdvisorMenuBlade/overview). Recommendations are stored in your [Azure Activity Log](../../azure-monitor/essentials/platform-logs-overview.md), and you can configure alerts for these recommendations via [ARM templates](../../advisor/advisor-alerts-arm.md) or the [portal](../../advisor/advisor-alerts-portal.md). 

## Install the latest SDKs

To ensure all the recent fixes and updates, it's recommended you always stay up to date with the latest SDKs available. If there is a newer version of the SDK(s) you are using available, you will see a recommendation show up in the **Performance** category to update to the latest SDK.

![Azure Advisor example showing recommendation to update chat SDK.](./media/advisor-chat-sdk-update-example.png)

The following SDKs are supported for this feature, along with all their supported languages. Note that this feature will only send recommendations for the newest generally available major release versions of the SDKs. Beta or preview versions will not trigger any recommendations or alerts. You can learn more about the [SDK options](./sdk-options.md) available.

* Calling (client)
* Chat
* SMS
* Identity
* Phone Numbers
* Management
* Network Traversal
* Call Automation

## Next steps

The following documents may be interesting to you:

- [Logging and diagnostics](./logging-and-diagnostics.md)
- [Metrics](./metrics.md)
