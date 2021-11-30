---
title:  "Customer responsibilities running Azure Spring Cloud in vnet"
description: This article describes customer responsibilities running Azure Spring Cloud in vnet.
author: karlerickson
ms.author: karler
ms.service: spring-cloud
ms.topic: conceptual
ms.date: 11/02/2021
ms.custom: devx-track-java
---

# Customer responsibilities for running Azure Spring Cloud in VNET

This article includes specifications for the use of Azure Spring Cloud in a virtual network.

When Azure Spring Cloud is deployed in your virtual network, it has outbound dependencies on services outside of the virtual network. For management and operational purposes, Azure Spring Cloud must access certain ports and fully qualified domain names (FQDNs). Azure Spring Cloud requires these endpoints to communicate with the management plane and to download and install core Kubernetes cluster components and security updates.

By default, Azure Spring Cloud has unrestricted outbound (egress) internet access. This level of network access allows applications you run to access external resources as needed. If you wish to restrict egress traffic, a limited number of ports and addresses must be accessible for maintenance tasks. The simplest solution to secure outbound addresses is use of a firewall device that can control outbound traffic based on domain names. Azure Firewall, for example, can restrict outbound HTTP and HTTPS traffic based on the FQDN of the destination. You can also configure your preferred firewall and security rules to allow these required ports and addresses.

## Azure Spring Cloud resource requirements

The following list shows the resource requirements for Azure Spring Cloud services. As a general requirement, you shouldn't modify resource groups created by Azure Spring Cloud and the underlying network resources.

- Don't modify resource groups created and owned by Azure Spring Cloud.
  - By default, these resource groups are named as `ap-svc-rt_[SERVICE-INSTANCE-NAME]_[REGION]*` and `ap_[SERVICE-INSTANCE-NAME]_[REGION]*`.
  - Don't block Azure Spring Cloud from updating resources in these resource groups.
- Don't modify subnets used by Azure Spring Cloud.
- Don't create more than one Azure Spring Cloud service instance in the same subnet.
- When using a firewall to control traffic, don't block the following egress traffic to Azure Spring Cloud components that operate, maintain, and support the service instance.

## Azure Spring Cloud network requirements

| Destination Endpoint                                         | Port             | Use                                       | Note                                                         |
| ------------------------------------------------------------ | ---------------- | ----------------------------------------- | ------------------------------------------------------------ |
| \*:1194 *or* [ServiceTag](../virtual-network/service-tags-overview.md#available-service-tags) - AzureCloud:1194 | UDP:1194         | Underlying Kubernetes Cluster management. |                                                              |
| \*:443 *or* [ServiceTag](../virtual-network/service-tags-overview.md#available-service-tags) - AzureCloud:443 | TCP:443          | Azure Spring Cloud Service Management.    | Information of service instance "requiredTraffics" could be known in resource payload, under "networkProfile" section. |
| \*:9000 *or* [ServiceTag](../virtual-network/service-tags-overview.md#available-service-tags) - AzureCloud:9000 | TCP:9000         | Underlying Kubernetes Cluster management. |                                                              |
| \*:123 *or* ntp.ubuntu.com:123                                | UDP:123          | NTP time synchronization on Linux nodes.  |                                                              |
| \*.azure.io:443 *or* [ServiceTag](../virtual-network/service-tags-overview.md#available-service-tags) - AzureContainerRegistry:443 | TCP:443          | Azure Container Registry.                 | Can be replaced by enabling *Azure Container Registry* [service endpoint in virtual network](../virtual-network/virtual-network-service-endpoints-overview.md). |
| \*.core.windows.net:443 and \*.core.windows.net:445 *or* [ServiceTag](../virtual-network/service-tags-overview.md#available-service-tags) - Storage:443 and Storage:445 | TCP:443, TCP:445 | Azure Files                        | Can be replaced by enabling *Azure Storage* [service endpoint in virtual network](../virtual-network/virtual-network-service-endpoints-overview.md). |
| \*.servicebus.windows.net:443 *or* [ServiceTag](../virtual-network/service-tags-overview.md#available-service-tags) - EventHub:443 | TCP:443          | Azure Event Hub.                          | Can be replaced by enabling *Azure Event Hubs* [service endpoint in virtual network](../virtual-network/virtual-network-service-endpoints-overview.md). |

## Azure Spring Cloud FQDN requirements/application rules

Azure Firewall provides the FQDN tag **AzureKubernetesService** to simplify the following configurations:

| Destination FQDN                  | Port      | Use                                                          |
| --------------------------------- | --------- | ------------------------------------------------------------ |
| <i>*.azmk8s.io</i>                | HTTPS:443 | Underlying Kubernetes Cluster management.                    |
| <i>mcr.microsoft.com</i>          | HTTPS:443 | Microsoft Container Registry (MCR).                          |
| <i>*.cdn.mscr.io</i>              | HTTPS:443 | MCR storage backed by the Azure CDN.                         |
| <i>*.data.mcr.microsoft.com</i>   | HTTPS:443 | MCR storage backed by the Azure CDN.                         |
| <i>management.azure.com</i>       | HTTPS:443 | Underlying Kubernetes Cluster management.                    |
| <i>*login.microsoftonline.com</i> | HTTPS:443 | Azure Active Directory authentication.                       |
| <i>*login.microsoft.com</i>       | HTTPS:443 | Azure Active Directory authentication.                       |
| <i>packages.microsoft.com</i>     | HTTPS:443 | Microsoft packages repository.                               |
| <i>acs-mirror.azureedge.net</i>   | HTTPS:443 | Repository required to install required binaries like kubenet and Azure CNI. |
| *mscrl.microsoft.com*<sup>1</sup> | HTTPS:80  | Required Microsoft Certificate Chain Paths.                  |
| *crl.microsoft.com*<sup>1</sup>   | HTTPS:80  | Required Microsoft Certificate Chain Paths.                  |
| *crl3.digicert.com*<sup>1</sup>   | HTTPS:80  | Third-Party TLS/SSL Certificate Chain Paths.                 |

<sup>1</sup> Please note that these FQDNs aren't included in the FQDN tag.


## Azure Spring Cloud optional FQDN for third-party application performance management

Azure Firewall provides the FQDN tag **AzureKubernetesService** to simplify the following configurations:

| Destination FQDN                   | Port       | Use                                                          |
| ---------------------------------- | ---------- | ------------------------------------------------------------ |
| <i>collector*.newrelic.com</i>     | TCP:443/80 | Required networks of New Relic APM agents from US region, also see [APM Agents Networks](https://docs.newrelic.com/docs/using-new-relic/cross-product-functions/install-configure/networks/#agents). |
| <i>collector*.eu01.nr-data.net</i> | TCP:443/80 | Required networks of New Relic APM agents from EU region, also see [APM Agents Networks](https://docs.newrelic.com/docs/using-new-relic/cross-product-functions/install-configure/networks/#agents). |
| <i>*.live.dynatrace.com</i>        | TCP:443    | Required network of Dynatrace APM agents.                    |
| <i>*.live.ruxit.com</i>            | TCP:443    | Required network of Dynatrace APM agents.                    |
| <i>*.saas.appdynamics.com</i>      | TCP:443/80 | Required network of AppDynamics APM agents, also see [SaaS Domains and IP Ranges](https://docs.appdynamics.com/display/PAA/SaaS+Domains+and+IP+Ranges). |

## See also

* [Access your application in a private network](access-app-virtual-network.md)
* [Expose applications to the internet using Application Gateway](expose-apps-gateway.md)
