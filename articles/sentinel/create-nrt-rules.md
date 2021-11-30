---
title: Work with near-real-time (NRT) detection analytics rules in Microsoft Sentinel | Microsoft Docs
description: This article explains how to view and create near-real-time (NRT) detection analytics rules in Microsoft Sentinel.
author: yelevin
ms.topic: how-to
ms.date: 11/09/2021
ms.author: yelevin
ms.custom: ignite-fall-2021
---
# Work with near-real-time (NRT) detection analytics rules in Microsoft Sentinel

> [!IMPORTANT]
>
> - Near-real-time (NRT) rules are currently in **PREVIEW**. See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

Microsoft Sentinel’s [near-real-time analytics rules](near-real-time-rules.md) provide up-to-the-minute threat detection out-of-the-box. This type of rule was designed to be highly responsive by running its query at intervals just one minute apart.

For the time being, these templates have limited application as outlined below, but the technology is rapidly evolving and growing.

## View near-real-time (NRT) rules

1. From the Microsoft Sentinel navigation menu, select **Analytics**.

1. In the **Active rules** tab of the **Analytics** blade, filter the list for **NRT** templates:

    1. Click the **Rule type** filter, then the drop-down list that appears below.

    1. Unmark **Select all**, then mark **NRT**.

    1. If necessary, click the top of the drop-down list to retract it, then click **OK**.

## Create NRT rules

You create NRT rules the same way you create regular [scheduled-query analytics rules](detect-threats-custom.md):

1. From the Microsoft Sentinel navigation menu, select **Analytics**.

1. Select **Create** from the button bar, then **NRT query rule** from the drop-down list.

    :::image type="content" source="media/create-nrt-rules/create-nrt-rule.png" alt-text="Create a new NRT rule.":::

1. Follow the instructions of the [**analytics rule wizard**](detect-threats-custom.md).

    The configuration of NRT rules is in most ways the same as that of scheduled analytics rules. 

    - You can refer to [**watchlists**](watchlists.md) and [**threat intelligence feeds**](understand-threat-intelligence.md) in your query logic.

    - You can use all of the alert enrichment methods: [**entity mapping**](map-data-fields-to-entities.md), [**custom details**](surface-custom-details-in-alerts.md), and [**alert details**](customize-alert-details.md).

    - You can choose how to group alerts into incidents, and to suppress a query when a particular result has been generated.

    - You can automate responses to both alerts and incidents.

    Because of the [**nature and limitations of NRT rules**](near-real-time-rules.md#considerations), however, the following features of scheduled analytics rules will *not be available* in the wizard:

    - **Query scheduling** is not configurable, since queries are automatically scheduled to run once per minute with a one-minute lookback period. 
    - **Alert threshold** is irrelevant, since an alert is always generated.
    - **Event grouping** configuration is not available, since events are always grouped into the alert created by the rule that captures the events. NRT rules cannot produce an alert for each event.

    In addition, the query itself has the following requirements:

    - The query itself can refer to only one table, and cannot contain unions or joins.

    - You can't run the query across workspaces.

    - Due to the size limits of the alerts, your query should make use of `project` statements to include only the necessary fields from your table. Otherwise, the information you want to surface could end up being truncated.

## Next steps

In this document, you learned how to create near-real-time (NRT) analytics rules in Microsoft Sentinel.

- Learn more about about [near-real-time (NRT) analytics rules in Microsoft Sentinel](near-real-time-rules.md).
- Explore other [analytics rule types](detect-threats-built-in.md).
