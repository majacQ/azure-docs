---
title: Collect data in custom log formats to Microsoft Sentinel | Microsoft Docs
description: Collect data from custom data sources and ingest it into Microsoft Sentinel using the Log Analytics agent.
author: yelevin
ms.topic: how-to
ms.date: 11/09/2021
ms.author: yelevin
ms.custom: ignite-fall-2021
---

# Collect data in custom log formats to Microsoft Sentinel with the Log Analytics agent

[!INCLUDE [Banner for top of topics](./includes/banner.md)]

[!INCLUDE [reference-to-feature-availability](includes/reference-to-feature-availability.md)]

Many applications log data to text files instead of standard logging services like Windows Event log or Syslog. You can use the Log Analytics agent to collect data in text files of nonstandard formats from both Windows and Linux computers. Once collected, you can either parse the data into individual fields in your queries or extract the data during collection to individual fields.

This article describes how to connect your data sources to Microsoft Sentinel using custom log formats. For more information about supported data connectors that use this method, see [Data connectors reference](data-connectors-reference.md).

Learn all about [custom logs in the Azure Monitor documentation](../azure-monitor/agents/data-sources-custom-logs.md).

Similar to Syslog, there are two steps to configuring custom log collection:

- Install the Log Analytics agent on the Linux or Windows machine that will be generating the logs.

- Configure your application's logging settings.

- Configure the Log Analytics agent from within Microsoft Sentinel.

## Install the Log Analytics agent

Install the Log Analytics agent on the Linux or Windows machine that will be generating the logs.

> [!NOTE]
> Some vendors recommend installing the Log Analytics agent on a separate log server instead of directly on the device. Consult your product's section on the [Data connectors reference](data-connectors-reference.md) page, or your product's own documentation.

Select the appropriate tab below, depending on whether your connector has a data connector page in Microsoft Sentinel.

# [From a specific data connector page](#tab/DCG)

1. From the Microsoft Sentinel navigation menu, select **Data connectors**.

1. Select your device type and then select **Open connector page**.

1. Install and onboard the agent on the device that generates the logs. Choose Linux or Windows as appropriate.

    | Machine type | Instructions |
    | --------- | --------- |
    | **For an Azure Linux VM** | <ol><li>Under **Choose where to install the Linux agent**, expand **Install agent on Azure Linux virtual machine**.<br><br><li>Select the **Download & install agent for Azure Linux Virtual machines >** link.<br><br><li>In the **Virtual machines** blade, select a virtual machine to install the agent on, and then select **Connect**. Repeat this step for each VM you wish to connect. |
    | **For any other Linux machine** | <ol><li>Under **Choose where to install the Linux agent**, expand **Install agent on a non-Azure Linux Machine**.<br><br><li>Select the **Download & install agent for non-Azure Linux machines >** link.<br><br><li>In the **Agents management** blade, select the **Linux servers** tab, then copy the command for **Download and onboard agent for Linux** and run it on your Linux machine.<br><br> If you want to keep a local copy of the Linux agent installation file, select the **Download Linux Agent** link above the "Download and onboard agent" command.|
    | **For an Azure Windows VM** | <ol><li>Under **Choose where to install the Windows agent**, expand **Install agent on Azure Windows virtual machine**.<br><br><li>Select the **Download & install agent for Azure Windows Virtual machines >** link.<br><br><li>In the **Virtual machines** blade, select a virtual machine to install the agent on, and then select **Connect**. Repeat this step for each VM you wish to connect. |
    | **For any other Windows machine** | <ol><li>Under **Choose where to install the Windows agent**, expand **Install agent on a non-Azure Windows Machine**<br><br><li>Select the **Download & install agent for non-Azure Windows machines >** link.<br><br><li>In the **Agents management** blade, on the **Windows servers** tab, select the **Download Windows Agent** link for either 32-bit or 64-bit systems, as appropriate. |

# [Other data sources](#tab/CUS)

1. From the Microsoft Sentinel navigation menu, select **Settings** and then the **Workspace settings** tab.

1. Install and onboard the agent on the device that generates the logs. Choose Linux or Windows as appropriate.

    | Machine type | Instructions |
    | --------- | --------- |
    | **Azure VM (Windows or Linux)** | <ol><li>From the Log Analytics workspace navigation menu, select **Virtual machines**.<br><br><li>In the **Virtual machines** blade, select a virtual machine to install the agent on, and then select **Connect**.<br>Repeat this step for each VM you wish to connect. |
    | **Any other Windows or Linux machine** | <ol><li>From the Log Analytics workspace navigation menu, select **Agents management**.<br><br><li>Select the **Windows servers** or **Linux servers** tab as appropriate.<br><br><li>For Windows, select the **Download Windows Agent** link for either 32-bit or 64-bit systems, as appropriate. For Linux, copy the command for **Download and onboard agent for Linux** and run it from your command line, or select the **Download Linux Agent** link to download a local copy of the installation file. |

---

## Configure the logs to be collected

Many device types have their own data connectors appearing in the **Data connectors** page in Microsoft Sentinel. Some of these connectors require special additional instructions to properly set up log collection in Microsoft Sentinel. These instructions can include the implementation of a parser based on a Kusto function. 

All connectors listed in Microsoft Sentinel will display any specific instructions on their respective connector pages in the portal, as well as in their sections of the [Microsoft Sentinel data connectors reference](data-connectors-reference.md) page.

If your product is not listed in the **Data connectors** page, consult your vendor's documentation for instructions on configuring logging for your device.

## Configure the Log Analytics agent

1. From the connector page, select the **Open your workspace custom logs configuration** link.

    Or, from the Log Analytics workspace navigation menu, select **Custom logs**.

1. In the **Custom tables** tab, select **Add custom log**.

1. In the **Sample** tab, upload a sample of a log file from your device (e.g. access.log or error.log). Then, select **Next**.

1. In the **Record delimiter** tab, select a record delimiter, either **New line** or **Timestamp** (see the instructions on that tab), and select **Next**.

1. In the **Collection paths** tab, select a path type of Windows or Linux, and enter the path to your device's logs based on your configuration. Then, select **Next**.

1. Give your custom log a name and optionally a description and select **Next**.  
    Don't end your name with "_CL", as it will be appended automatically.


## Find your data

To query the custom log data in **Logs**, type the name you gave your custom log (ending in "_CL") in the query window.

## Next steps

In this document, you learned how to collect data from custom log types to ingest into Microsoft Sentinel. To learn more about Microsoft Sentinel, see the following articles:
- Learn how to [get visibility into your data and potential threats](get-visibility.md).
- Get started [detecting threats with Microsoft Sentinel](detect-threats-built-in.md).
- [Use workbooks](monitor-your-data.md) to monitor your data.
