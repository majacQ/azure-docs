---
title: Azure Chaos Studio limitations and known issues
description: Understand current limitations and known issues when using Azure Chaos Studio.
services: chaos-studio
author: johnkemnetz
ms.topic: overview
ms.date: 11/02/2021
ms.author: johnkem
ms.service: chaos-studio
---

# Azure Chaos Studio Preview Limitations and Known Issues

During the public preview of Azure Chaos Studio, there are a few limitations and known issues that the team is aware of and working to resolve.

## Limitations 

* For agent-based faults, the machine must have access to the following **HTTPS endpoints**:
    * http://agentcommunicationservice-frontdoor-canary.trafficmanager.net 
    * If sending telemetry data to Application Insights, the IPs [in this document](../azure-monitor/app/ip-addresses.md) are also required.
* If running an experiment that makes use of the Chaos Agent, the VM must run one of the following **operating systems**:
    * Windows Server 2019, Windows Server 2016, Windows Server 2012, and Windows Server 2012 R2
    * Redhat Enterprise Linux 8.2, SUSE Enterprise Linux 15 SP2, CentOS 8.2, Debian 10 Buster (with unzip installation required), Oracle Linux 7.8 Ubuntu Server 16.04 LTS, and Ubuntu Server 18.04 LTS
* The Chaos Agent is not tested against custom Linux distributions, hardened Linux distributions (for example, FIPS or SELinux)
* The Chaos Studio portal experience has only been tested on the following browsers:
    * **Windows:** Microsoft Edge, Google Chrome, Firefox
    * **MacOS:** Safari, Google Chrome, Firefox

## Known issues
* The **Enable agent-based target** experience in the Azure portal does not also assign the user-assigned managed identity to the virtual machine or virtual machine scale set. This must be done manually or an agent-based fault in an experiment will fail with the error: "Verify that the target is correctly onboarded and proper read permissions are provided to the experiment msi." This can be done after enabling the agent-based target, but may require a reboot.
* Onboarding a target in the Azure portal may fail if you navigate away from the Targets view before onboarding completes.
* When creating an experiment, after clicking **Review + create** there is a delay before the created experiment appears in the experiment list and users must refresh to see the experiment in the list.
* When picking target resources for an agent-based fault in the experiment designer, it is possible to select virtual machines or virtual machine scale sets with an operating system not supported by the fault selected.


## Next steps
Get started creating and running chaos experiments to improve application resilience with Chaos Studio using the links below.
- [Create and run your first experiment](chaos-studio-tutorial-service-direct-portal.md)
- [Learn more about chaos engineering](chaos-studio-chaos-engineering-overview.md)
