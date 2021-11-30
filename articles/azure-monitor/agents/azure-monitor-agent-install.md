---
title: Install the Azure Monitor agent
description: Options for installing the Azure Monitor Agent (AMA) on Azure virtual machines and Azure Arc-enabled servers.
ms.topic: conceptual
author: bwren
ms.author: bwren
ms.date: 09/21/2021
ms.custom: devx-track-azurepowershell, devx-track-azurecli

---

# Install the Azure Monitor agent
This article provides the different options currently available to install the [Azure Monitor agent](azure-monitor-agent-overview.md) on both Azure virtual machines and Azure Arc-enabled servers and also the options to create [associations with data collection rules](data-collection-rule-azure-monitor-agent.md) that define which data the agent should collect.

## Prerequisites
The following prerequisites are required prior to installing the Azure Monitor agent.

- [Managed system identity](../../active-directory/managed-identities-azure-resources/qs-configure-portal-windows-vm.md) must be enabled on Azure virtual machines. This is not required for Azure Arc-enabled servers. The system identity will be enabled automatically if the agent is installed as part of the process for [creating and assigning a data collection rule using the Azure portal](#install-with-azure-portal).
- The [AzureResourceManager service tag](../../virtual-network/service-tags-overview.md) must be enabled on the virtual network for the virtual machine.
- The virtual machine must have access to the following HTTPS endpoints:
  - *.ods.opinsights.azure.com
  - *.ingest.monitor.azure.com
  - *.control.monitor.azure.com

> [!IMPORTANT]
> The Azure Monitor agent does not currently support private links.

## Virtual machine extension details
The Azure Monitor Agent is implemented as an [Azure VM extension](../../virtual-machines/extensions/overview.md) with the details in the following table. It can be installed using any of the methods to install virtual machine extensions including those described in this article.

| Property | Windows | Linux |
|:---|:---|:---|
| Publisher | Microsoft.Azure.Monitor  | Microsoft.Azure.Monitor |
| Type      | AzureMonitorWindowsAgent | AzureMonitorLinuxAgent  |
| TypeHandlerVersion  | 1.0 | 1.5 |

## Extension versions
It is strongly recommended to update to GA+ versions listed below instead of using preview or intermediate versions.

| Release Date | Release notes | Windows | Linux |
|:---|:---|:---|:---|:---|
| June 2021 | General availability announced. <ul><li>All features except metrics destination now generally available</li><li>Production quality, security and compliance</li><li>Availability in all public regions</li><li>Performance and scale improvements for higher EPS</li></ul> [Learn more](https://azure.microsoft.com/updates/azure-monitor-agent-and-data-collection-rules-now-generally-available/) | 1.0.12.0 | 1.9.1.0 |
| July 2021 | <ul><li>Support for direct proxies</li><li>Support for Log Analytics gateway</li></ul> [Learn more](https://azure.microsoft.com/updates/general-availability-azure-monitor-agent-and-data-collection-rules-now-support-direct-proxies-and-log-analytics-gateway/) | 1.1.1.0 | 1.10.5.0 |
| August 2021 | Fixed issue allowing Azure Monitor Metrics as the only destination | 1.1.2.0 | 1.10.9.0<sup>1</sup> |
| September 2021 | <ul><li>Fixed issue causing data loss on restarting the agent</li><li>Addressed regression introduced in 1.1.3.1<sup>2</sup> for Arc Windows servers</li></ul> | 1.1.3.2 | 1.12.2.0 <sup>2</sup> |  

<sup>1</sup> Do not use AMA Linux version 1.10.7.0 
<sup>2</sup> Known regression where it's not working on Arc-enabled servers


## Install with Azure portal
To install the Azure Monitor agent using the Azure portal, follow the process to [create a data collection rule](data-collection-rule-azure-monitor-agent.md#create-rule-and-association-in-azure-portal) in the Azure portal. This allows you to associate the data collection rule with one or more Azure virtual machines or Azure Arc-enabled servers. The agent will be installed on any of these virtual machines that don't already have it.


## Install with Resource Manager template
You can use Resource Manager templates to install the Azure Monitor agent on Azure virtual machines and on Azure Arc-enabled servers and to create an association with data collection rules. You must create any data collection rule prior to creating the association.

Get sample templates for installing the agent and creating the association from the following: 

- [Template to install Azure Monitor agent (Azure and Azure Arc)](../agents/resource-manager-agent.md#azure-monitor-agent-preview) 
- [Template to create association with data collection rule](./resource-manager-data-collection-rules.md)

Install the templates using [any deployment method for Resource Manager templates](../../azure-resource-manager/templates/deploy-powershell.md) such as the following commands.

# [PowerShell](#tab/ARMAgentPowerShell)
```powershell
New-AzResourceGroupDeployment -ResourceGroupName "<resource-group-name>" -TemplateFile "<template-filename.json>" -TemplateParameterFile "<parameter-filename.json>"
```
# [CLI](#tab/ARMAgentCLI)
```powershell
New-AzResourceGroupDeployment -ResourceGroupName "<resource-group-name>" -TemplateFile "<template-filename.json>" -TemplateParameterFile "<parameter-filename.json>"
```
---

## Install with PowerShell
You can install the Azure Monitor agent on Azure virtual machines and on Azure Arc-enabled servers using the PowerShell command for adding a virtual machine extension. 

### Azure virtual machines
Use the following PowerShell commands to install the Azure Monitor agent on Azure virtual machines.
# [Windows](#tab/PowerShellWindows)
```powershell
Set-AzVMExtension -Name AMAWindows -ExtensionType AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -VMName <virtual-machine-name> -Location <location> -TypeHandlerVersion 1.0
```
# [Linux](#tab/PowerShellLinux)
```powershell
Set-AzVMExtension -Name AMALinux -ExtensionType AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -VMName <virtual-machine-name> -Location <location> -TypeHandlerVersion 1.5
```
---

### Azure Arc-enabled servers
Use the following PowerShell commands to install the Azure Monitor agent onAzure Azure Arc-enabled servers.
# [Windows](#tab/PowerShellWindowsArc)
```powershell
New-AzConnectedMachineExtension -Name AMAWindows -ExtensionType AzureMonitorWindowsAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -MachineName <arc-server-name> -Location <arc-server-location>
```
# [Linux](#tab/PowerShellLinuxArc)
```powershell
New-AzConnectedMachineExtension -Name AMALinux -ExtensionType AzureMonitorLinuxAgent -Publisher Microsoft.Azure.Monitor -ResourceGroupName <resource-group-name> -MachineName <arc-server-name> -Location <arc-server-location>
```
---
## Install with Azure CLI
You can install the Azure Monitor agent on Azure virtual machines and on Azure Arc enabled servers using the Azure CLI command for adding a virtual machine extension. 

### Azure virtual machines
Use the following CLI commands to install the Azure Monitor agent on Azure virtual machines.
# [Windows](#tab/CLIWindows)
```azurecli
az vm extension set --name AzureMonitorWindowsAgent --publisher Microsoft.Azure.Monitor --ids <vm-resource-id>
```
# [Linux](#tab/CLILinux)
```azurecli
az vm extension set --name AzureMonitorLinuxAgent --publisher Microsoft.Azure.Monitor --ids <vm-resource-id>
```
---
### Azure Arc-enabled servers
Use the following CLI commands to install the Azure Monitor agent onAzure Azure Arc-enabled servers.

# [Windows](#tab/CLIWindowsArc)
```azurecli
az connectedmachine extension create --name AzureMonitorWindowsAgent --publisher Microsoft.Azure.Monitor --type AzureMonitorWindowsAgent --machine-name <arc-server-name> --resource-group <resource-group-name> --location <arc-server-location>
```
# [Linux](#tab/CLILinuxArc)
```azurecli
az connectedmachine extension create --name AzureMonitorLinuxAgent --publisher Microsoft.Azure.Monitor --type AzureMonitorLinuxAgent --machine-name <arc-server-name> --resource-group <resource-group-name> --location <arc-server-location>
```
---


## Install with Azure Policy
Use the following policies and policy initiatives to automatically install the agent and associate it with a data collection rule, every time you create a virtual machine.

### Built-in policy initiatives
[View prerequisites for agent installation](azure-monitor-agent-install.md#prerequisites). 

Policy initiatives for Windows and Linux virtual machines consist of individual policies that:

- Install the Azure Monitor agent extension on the virtual machine.
- Create and deploy the association to link the virtual machine to a data collection rule.

![Partial screenshot from the Azure Policy Definitions page showing two built-in policy initiatives for configuring the Azure Monitor agent.](media/azure-monitor-agent-install/built-in-ama-dcr-initiatives.png)  

### Built-in policies 
You can choose to use the individual policies from their respective policy initiatives, based on your needs. For example, if you only want to automatically install the agent, use the first policy from the initiative as shown in the following example.  

![Partial screenshot from the Azure Policy Definitions page showing policies contained within the initiative for configuring the Azure Monitor agent.](media/azure-monitor-agent-install/built-in-ama-dcr-policy.png)  

### Remediation
The initiatives or policies will apply to each virtual machine as it's created. A [remediation task](../../governance/policy/how-to/remediate-resources.md) deploys the policy definitions in the initiative to *existing resources*, so you can configure the Azure Monitor agent for any resources that were already created. 

When you create the assignment by using the Azure portal, you have the option of creating a remediation task at the same time. See [Remediate non-compliant resources with Azure Policy](../../governance/policy/how-to/remediate-resources.md) for details on the remediation.

![Screenshot that shows initiative remediation for the Azure Monitor agent.](media/azure-monitor-agent-install/built-in-ama-dcr-remediation.png)

## Diagnostic settings
[Diagnostic settings](../essentials/diagnostic-settings.md) collect resource logs and metrics from Azure resources and route them to multiple locations. A typical location is a Log Analytics workspace, which allows you to analyze the data with [log queries](../logs/log-query-overview.md) and [log alerts](../alerts/alerts-log.md). Use Azure Policy to automatically create a diagnostic setting each time you create a resource.


## Next steps

- [Create a data collection rule](data-collection-rule-azure-monitor-agent.md) to collect data from the agent and send it to Azure Monitor.
