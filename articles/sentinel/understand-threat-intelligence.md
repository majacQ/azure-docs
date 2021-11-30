---
title: Understand threat intelligence in Microsoft Sentinel | Microsoft Docs
description: Understand how threat intelligence feeds are connected to, managed, and used in Microsoft Sentinel to analyze data, detect threats, and enrich alerts.
author: batamig
ms.topic: conceptual
ms.date: 11/09/2021
ms.author: bagol
ms.custom: ignite-fall-2021
---

# Understand threat intelligence in Microsoft Sentinel

[!INCLUDE [Banner for top of topics](./includes/banner.md)]

## Introduction to threat intelligence

[!INCLUDE [reference-to-feature-availability](includes/reference-to-feature-availability.md)]

Cyber threat intelligence (CTI) is information describing known existing or potential threats to systems and users. This type of information takes many forms, from written reports detailing a particular threat actor’s motivations, infrastructure, and techniques, to specific observations of IP addresses, domains, file hashes, and other artifacts associated with known cyber threats. CTI is used by organizations to provide essential context to unusual activity, so that security personnel can quickly take action to protect their people, information, and other assets. CTI can be sourced from many places, such as open-source data feeds, threat intelligence-sharing communities, commercial intelligence feeds, and local intelligence gathered in the course of security investigations within an organization.

Within a Security Information and Event Management (SIEM) solution like Microsoft Sentinel, the most commonly used form of CTI is threat indicators, also known as Indicators of Compromise or IoCs. Threat indicators are data that associate observed artifacts such as URLs, file hashes, or IP addresses with known threat activity such as phishing, botnets, or malware. This form of threat intelligence is often called *tactical threat intelligence* because it can be applied to security products and automation in large scale to detect potential threats to an organization and protect against them. In Microsoft Sentinel, you can use threat indicators to help detect malicious activity observed in your environment and provide context to security investigators to help inform response decisions.

Integrate threat intelligence (TI) into Microsoft Sentinel through the following activities:

- **Import threat intelligence** into Microsoft Sentinel by enabling **data connectors** to various TI [platforms](connect-threat-intelligence-tip.md) and [feeds](connect-threat-intelligence-taxii.md).

- **View and manage** the imported threat intelligence in **Logs** and in the **Threat Intelligence** blade of Microsoft Sentinel.

- **Detect threats** and generate security alerts and incidents using the built-in **Analytics** rule templates based on your imported threat intelligence.

- **Visualize key information** about your imported threat intelligence in Microsoft Sentinel with the **Threat Intelligence workbook**.

Microsoft enriches all imported threat intelligence indicators with [GeoLocation and WhoIs data](#view-your-geolocation-and-whois-data-enrichments-public-preview), which is displayed together with other indicator details.

> [!TIP]
> Threat Intelligence also provides useful context within other Microsoft Sentinel experiences such as **Hunting** and **Notebooks**. For more information, see [Jupyter Notebooks in Microsoft Sentinel](https://techcommunity.microsoft.com/t5/azure-sentinel/using-threat-intelligence-in-your-jupyter-notebooks/ba-p/860239) and [Tutorial: Get started with Jupyter notebooks and MSTICPy in Microsoft Sentinel](notebook-get-started.md).
>

## Import threat intelligence with data connectors

Just like all the other event data in Microsoft Sentinel, threat indicators are imported using data connectors. There are two data connectors in Microsoft Sentinel provided specifically for threat indicators, **Threat Intelligence - TAXII** for industry-standard STIX/TAXII feeds and **Threat Intelligence Platforms** for integrated and curated TI feeds. You can use either data connector alone, or both connectors together, depending on where your organization sources threat indicators.

See this catalog of [threat intelligence integrations](threat-intelligence-integration.md) available with Microsoft Sentinel.

### Add threat indicators to Microsoft Sentinel with the Threat Intelligence Platforms data connector

Many organizations use threat intelligence platform (TIP) solutions to aggregate threat indicator feeds from a variety of sources, to curate the data within the platform, and then to choose which threat indicators to apply to various security solutions such as network devices, EDR/XDR solutions, or SIEMs such as Microsoft Sentinel. If your organization uses an [integrated TIP solution](connect-threat-intelligence-tip.md), the **Threat Intelligence Platforms data connector** allows you to use your TIP to import threat indicators into Microsoft Sentinel.

Because the TIP data connector works with the [Microsoft Graph Security tiIndicators API](/graph/api/resources/tiindicator) to accomplish this, it can also be used by any custom threat intelligence platform that communicates with the tiIndicators API to send indicators to Microsoft Sentinel (and to other Microsoft security solutions like Microsoft 365 Defender).

:::image type="content" source="media/understand-threat-intelligence/threat-intel-import-path.png" alt-text="Threat intelligence import path":::

For more information on the TIP solutions integrated with Microsoft Sentinel, see [Integrated threat intelligence platform products](threat-intelligence-integration.md#integrated-threat-intelligence-platform-products).

**To import threat indicators to Microsoft Sentinel from your integrated TIP or custom threat intelligence platform**:

1. Obtain an **Application ID** and **Client Secret** from your Azure Active Directory

1. Input this information into your TIP solution or custom application

1. Enable the Threat Intelligence Platforms data connector in Microsoft Sentinel

For more information, see [Connect your threat intelligence platform to Microsoft Sentinel](connect-threat-intelligence-tip.md).

### Add threat indicators to Microsoft Sentinel with the Threat Intelligence - TAXII data connector

The most widely-adopted industry standard for the transmission of threat intelligence is a [combination of the STIX data format and the TAXII protocol](https://oasis-open.github.io/cti-documentation/). If your organization obtains threat indicators from solutions that support the current STIX/TAXII version (2.0 or 2.1), you can use the **Threat Intelligence - TAXII** data connector to bring your threat indicators into Microsoft Sentinel. The Threat Intelligence - TAXII data connector enables a built-in TAXII client in Microsoft Sentinel to import threat intelligence from TAXII 2.x servers.

:::image type="content" source="media/understand-threat-intelligence/threat-intel-taxii-import-path.png" alt-text="TAXII import path":::

**To import STIX-formatted threat indicators to Microsoft Sentinel from a TAXII server**:

1. Obtain the TAXII server API Root and Collection ID

1. Enable the Threat Intelligence - TAXII data connector in Microsoft Sentinel

For more information, see [Connect Microsoft Sentinel to STIX/TAXII threat intelligence feeds](connect-threat-intelligence-taxii.md).

## View and manage your threat indicators

You can view your successfully imported threat indicators, regardless of the source feed or the connector used, in the **ThreatIntelligenceIndicator** table (under the **Microsoft Sentinel** group) in **Logs** which is where all your Microsoft Sentinel event data is stored. This table is the basis for threat intelligence queries performed by other Microsoft Sentinel features such as Analytics and Workbooks.

Your results should look similar to the sample threat indicator shown below:

:::image type="content" source="media/understand-threat-intelligence/threat-intel-sample-query.png" alt-text="Sample query data":::

You can also view and manage your indicators in the new **Threat Intelligence** blade, accessible from the main Microsoft Sentinel menu. You can sort, filter, and search your imported threat indicators without even writing a Log Analytics query. This feature also allows you to create threat indicators directly within the Microsoft Sentinel interface, as well as perform two of the most common threat intelligence administrative tasks: indicator tagging and creating new indicators related to security investigations.

Tagging threat indicators is an easy way to group them together to make them easier to find. Typically, you might apply a tag to indicators related to a particular incident, or to those representing threats from a particular known actor or well-known attack campaign. You can tag threat indicators individually, or multi-select indicators and tag them all at once. Shown below is an example of tagging multiple indicators with an incident ID. Since tagging is free-form, a recommended practice is to create standard naming conventions for threat indicator tags. You can apply multiple tags to each indicator.

:::image type="content" source="media/understand-threat-intelligence/threat-intel-tagging-indicators.png" alt-text="Apply tags to threat indicators" lightbox="media/understand-threat-intelligence/threat-intel-tagging-indicators.png":::

For more details on viewing and managing your threat indicators, see [Work with threat indicators in Microsoft Sentinel](work-with-threat-indicators.md#view-your-threat-indicators-in-microsoft-sentinel).

### View your GeoLocation and WhoIs data enrichments (Public preview)

Microsoft enriches each indicator with extra GeoLocation and WhoIs data, providing more context for investigations where the selected indicator of compromise (IOC) is found.

You can view GeoLocation and WhoIs data on the **Threat Intelligence** pane for each indicator of compromise that you've imported into Microsoft Sentinel.

For example, use GeoLocation data to find details like *Organization* or *Country* for the indicator, and WhoIs data to find data like *Registrar* and *Record creation* data.

## Detect threats with threat indicator-based analytics

The most important use case for threat indicators in SIEM solutions like Microsoft Sentinel is to power analytics rules for threat detection. These indicator-based rules compare raw events from your data sources against your threat indicators to detect security threats in your organization. In Microsoft Sentinel **Analytics**, you create analytics rules that run on a schedule and generate security alerts. The rules are driven by queries, along with configurations that determine how often the rule should run, what kind of query results should generate security alerts and incidents, and which if any automations to trigger in response.

While you can always create new analytics rules from scratch, Microsoft Sentinel provides a set of built-in rule templates, created by Microsoft security engineers, that you can use as-is or modify to meet your needs. You can readily identify the rule templates that use threat indicators, as they are all titled beginning with "**TI map**…". All these rule templates operate similarly, with the only difference being which type of threat indicators are used (domain, email, file hash, IP address, or URL) and which event type to match against. Each template lists the required data sources needed for the rule to function, so you can see at a glance if you have the necessary events already imported in Microsoft Sentinel. When you edit and save an existing rule template or create a new rule, it is enabled by default.

You can find your enabled rule in the **Active rules** tab of the **Analytics** section of Microsoft Sentinel. You can edit, enable, disable, duplicate or delete the active rule from there. The new rule runs immediately upon activation, and from then on will run on its defined schedule.

According to the default settings, each time the rule runs on its schedule, any results found will generate a security alert. Security alerts in Microsoft Sentinel can be viewed in the **Logs** section of Microsoft Sentinel, in the **SecurityAlert** table under the **Microsoft Sentinel** group.

In Microsoft Sentinel, the alerts generated from analytics rules also generate security incidents which can be found in **Incidents** under **Threat Management** on the Microsoft Sentinel menu. Incidents are what your security operations teams will triage and investigate to determine the appropriate response actions. You can find detailed information in this [Tutorial: Investigate incidents with Microsoft Sentinel](./investigate-cases.md).

For more details on using threat indicators in your analytics rules, see [Work with threat indicators in Microsoft Sentinel](work-with-threat-indicators.md#detect-threats-with-threat-indicator-based-analytics).

## Workbooks provide insights about your threat intelligence

Workbooks provide powerful interactive dashboards that give you insights into all aspects of Microsoft Sentinel, and threat intelligence is no exception. You can use the built-in **Threat Intelligence workbook** to visualize key information about your threat intelligence, and you can easily customize the workbook according to your business needs. You can even create new dashboards combining many different data sources so you can visualize your data in unique ways. Since Microsoft Sentinel workbooks are based on Azure Monitor workbooks, there is already extensive documentation available, and many more templates. A great place to start is this article on how to [Create interactive reports with Azure Monitor workbooks](../azure-monitor/visualize/workbooks-overview.md).

There is also a rich community of [Azure Monitor workbooks on GitHub](https://github.com/microsoft/Application-Insights-Workbooks) where you can download additional templates and contribute your own templates.

For more details on using and customizing the Threat Intelligence workbook, see [Work with threat indicators in Microsoft Sentinel](work-with-threat-indicators.md#workbooks-provide-insights-about-your-threat-intelligence).

## Next steps

In this document, you learned about the threat intelligence capabilities of Microsoft Sentinel, including the Threat Intelligence blade. For practical guidance on using Microsoft Sentinel's threat intelligence capabilities, see the following articles:

- Connect Microsoft Sentinel to [STIX/TAXII threat intelligence feeds](./connect-threat-intelligence-taxii.md).
- [Connect threat intelligence platforms](./connect-threat-intelligence-tip.md) to Microsoft Sentinel.
- See which [TIP platforms, TAXII feeds, and enrichments](threat-intelligence-integration.md) can be readily integrated with Microsoft Sentinel.
- [Work with threat indicators](work-with-threat-indicators.md) throughout the Microsoft Sentinel experience.
- Detect threats with [built-in](./detect-threats-built-in.md) or [custom](./detect-threats-custom.md) analytics rules in Microsoft Sentinel
- [Investigate incidents](./investigate-cases.md) in Microsoft Sentinel.
