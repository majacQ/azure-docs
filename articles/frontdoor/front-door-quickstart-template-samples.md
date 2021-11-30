---
title: Azure Resource Manager template samples - Azure Front Door
description: Learn about Resource Manager template samples for Azure Front Door, including templates for creating a basic Front Door and configuring Front Door rate limiting.
services: frontdoor
documentationcenter: ""
author: duongau
ms.service: frontdoor
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/01/2021
ms.author: duau
---
# Azure Resource Manager deployment model templates for Front Door

The following table includes links to Azure Resource Manager deployment model templates for Azure Front Door.

## Azure Front Door

| Template | Description |
| ---| ---|
| [Create a basic Front Door](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-create-basic)| Creates a basic Front Door configuration with a single backend. |
| [Create a Front Door with multiple backends and backend pools and URL based routing](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-create-multiple-backends)| Creates a Front Door with load balancing configured for multiple backends in ta backend pool and also across backend pools based on URL path. |
| [Onboard a custom domain and managed TLS certificate with Front Door](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-custom-domain)| Add a custom domain to your Front Door and use a Front Door-managed TLS certificate. |
| [Onboard a custom domain and customer-managed TLS certificate with Front Door](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-custom-domain-customer-certificate)| Add a custom domain to your Front Door and use your own TLS certificate by using Key Vault. |
| [Create Front Door with geo filtering](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-geo-filtering)| Create a Front Door that allows/blocks traffic from certain countries/regions. |
| [Control Health Probes for your backends on Front Door](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-health-probes)| Update your Front Door to change the health probe settings by updating the probe path and also the intervals in which the probes will be sent. |
| [Create Front Door with Active/Standby backend configuration](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-priority-lb)| Creates a Front Door that demonstrates priority-based routing for Active/Standby application topology, that is, by default send all traffic to the primary (highest-priority) backend until it becomes unavailable. |
| [Create Front Door with caching enabled for certain routes](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-create-caching)| Creates a Front Door with caching enabled for the defined routing configuration thus caching any static assets for your workload. |
| [Configure Session Affinity for your Front Door host names](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-session-affinity) | Updates a Front Door to enable session affinity for your frontend host, thereby, sending subsequent traffic from the same user session to the same backend. |
| [Configure Front Door for client IP allowlisting or blocklisting](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-waf-clientip)| Configures a Front Door to restrict traffic certain client IPs using custom  access control using client IPs. |
| [Configure Front Door to take action with specific http parameters](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-waf-http-params)| Configures a Front Door to allow or block certain traffic based on the http parameters in the incoming request by using custom rules for access control using http parameters. |
| [Configure Front Door rate limiting](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-rate-limiting)| Configures a Front Door to rate limit incoming traffic for a given frontend host. |
| | |

## Azure Front Door Standard/Premium (Preview)

| Sample | Description |
|-|-|
| [Front Door (quick create)](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-standard-premium/) | Creates a basic Front Door profile including an endpoint, origin group, origin, and route.  |
| [Rule set](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-standard-premium-rule-set/) | Creates a Front Door profile and rule set.  |
| [WAF policy with managed rule set](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-premium-waf-managed/) | Creates a Front Door profile and WAF with managed rule set.  |
| [WAF policy with custom rule](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-standard-premium-waf-custom/) | Creates a Front Door profile and WAF with custom rule.  |
| [WAF policy with rate limit](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-standard-premium-rate-limit/) | Creates a Front Door profile and WAF with a custom rule to perform rate limiting.  |
| [WAF policy with geo-filtering](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-standard-premium-geo-filtering/) | Creates a Front Door profile and WAF with a custom rule to perform geo-filtering.  |
|**App Service origins**| **Description** |
| [App Service](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-standard-premium-app-service-public) | Creates an App Service app with a public endpoint, and a Front Door profile.  |
| [App Service with Private Link](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-premium-app-service-private-link) | Creates an App Service app with a private endpoint, and a Front Door profile.  |
|**Azure Functions origins**| **Description** |
| [Azure Functions](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-standard-premium-function-public/) | Creates an Azure Functions app with a public endpoint, and a Front Door profile.  |
| [Azure Functions with Private Link](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-premium-function-private-link) | Creates an Azure Functions app with a private endpoint, and a Front Door profile.  |
|**API Management origins**| **Description** |
| [API Management (external)](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-standard-premium-api-management-external) | Creates an API Management instance with external VNet integration, and a Front Door profile.  |
|**Storage origins**| **Description** |
| [Storage static website](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-standard-premium-storage-static-website) | Creates an Azure Storage account and static website with a public endpoint, and a Front Door profile.  |
| [Storage blobs with Private Link](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-premium-storage-blobs-private-link) | Creates an Azure Storage account and blob container with a private endpoint, and a Front Door profile.  |
|**Application Gateway origins**| **Description** |
| [Application Gateway](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-standard-premium-application-gateway-public) | Creates an Application Gateway, and a Front Door profile. |
|**Virtual machine origins**| **Description** |
| [Virtual machine with Private Link service](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.network/front-door-premium-vm-private-link) | Creates a virtual machine and Private Link service, and a Front Door profile. |
| | |

## Next steps

- Learn how to [create a Front Door](quickstart-create-front-door.md).
- Learn [how Front Door works](front-door-routing-architecture.md).
