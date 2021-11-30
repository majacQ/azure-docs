---
title: Secure traffic between single-tenant workflows and virtual networks
description: Secure traffic between virtual networks, storage accounts, and single-tenant workflows in Azure Logic Apps.
services: logic-apps
ms.suite: integration
ms.reviewer: estfan, azla
ms.topic: how-to
ms.date: 08/31/2021

# As a developer, I want to connect to my single-tenant workflows from virtual networks using private endpoints.
---

# Secure traffic between virtual networks and single-tenant workflows in Azure Logic Apps using private endpoints

To securely and privately communicate between your logic app workflow and a virtual network, you can set up *private endpoints* for inbound traffic and use virtual network integration for outbound traffic.

A private endpoint is a network interface that privately and securely connects to a service powered by Azure Private Link. This service can be an Azure service such as Azure Logic Apps, Azure Storage, Azure Cosmos DB, SQL, or your own Private Link Service. The private endpoint uses a private IP address from your virtual network, which effectively brings the service into your virtual network.

This article shows how to set up access through private endpoints for inbound traffic, outbound traffic, and connection to storage accounts.

For more information, review the following documentation:

- [What is Azure Private Endpoint?](../private-link/private-endpoint-overview.md)

- [What is Azure Private Link?](../private-link/private-link-overview.md)

- [What is single-tenant logic app workflow in Azure Logic Apps?](single-tenant-overview-compare.md)

## Prerequisites

You need to have a new or existing Azure virtual network that includes a subnet without any delegations. This subnet is used to deploy and allocate private IP addresses from the virtual network.

For more information, review the following documentation:

- [Quickstart: Create a virtual network using the Azure portal](../virtual-network/quick-create-portal.md)

- [What is subnet delegation?](../virtual-network/subnet-delegation-overview.md)

- [Add or remove a subnet delegation](../virtual-network/manage-subnet-delegation.md)

<a name="set-up-inbound"></a>

## Set up inbound traffic through private endpoints

To secure inbound traffic to your workflow, complete these high-level steps:

1. Start your workflow with a built-in trigger that can receive and handle inbound requests, such as the Request trigger or the HTTP + Webhook trigger. This trigger sets up your workflow with a callable endpoint.

1. Add a private endpoint to your virtual network.

1. Make test calls to check access to the endpoint. To call your logic app workflow after you set up this endpoint, you must be connected to the virtual network.

### Prerequisites for inbound traffic through private endpoints

In addition to the [virtual network setup in the top-level prerequisites](#prerequisites), you need to have a new or existing single-tenant based logic app workflow that starts with a built-in trigger that can receive requests.

For example, the Request trigger creates an endpoint on your workflow that can receive and handle inbound requests from other callers, including workflows. This endpoint provides a URL that you can use to call and trigger the workflow. For this example, the steps continue with the Request trigger.

For more information, review the following documentation:

- [Create single-tenant logic app workflows in Azure Logic Apps](create-single-tenant-workflows-azure-portal.md)

- [Receive and respond to inbound HTTP requests using Azure Logic Apps](../connectors/connectors-native-reqres.md)

### Create the workflow

1. If you haven't already, create a single-tenant based logic app, and a blank workflow.

1. After the designer opens, add the Request trigger as the first step in your workflow.

   > [!NOTE]
   > You can call Request triggers and webhook triggers only from inside your virtual network. 
   > Managed API webhook triggers and actions won't work because they require a public endpoint to receive calls. 

1. Based on your scenario requirements, add other actions that you want to run in your workflow.

1. When you're done, save your workflow.

For more information, review [Create single-tenant logic app workflows in Azure Logic Apps](create-single-tenant-workflows-azure-portal.md).

#### Copy the endpoint URL

1. On the workflow menu, select **Overview**.

1. On the **Overview** page, copy and save the **Workflow URL** for later use.

   To trigger the workflow, you call or send a request to this URL.

1. Make sure that the URL works by calling or sending a request to the URL. You can use any tool you want to send the request, for example, Postman.

### Set up private endpoint connection

1. On your logic app menu, under **Settings**, select **Networking**.

1. On the **Networking** page, under **Private Endpoint connections**, select **Configure your private endpoint connections**.

1. On the **Private Endpoint connections page**, select **Add**.

1. On the **Add Private Endpoint** pane that opens, provide the requested information about the endpoint.

   For more information, review [Private Endpoint properties](../private-link/private-endpoint-overview.md#private-endpoint-properties).

1. After Azure successfully provisions the private endpoint, try again to call the workflow URL.

   This time, you get an expected `403 Forbidden` error, which is means that the private endpoint is set up and works correctly.

1. To make sure the connection is working correctly, create a virtual machine in the same virtual network that has the private endpoint, and try calling the logic app workflow.

### Considerations for inbound traffic through private endpoints

- If accessed from outside your virtual network, monitoring view can't access the inputs and outputs from triggers and actions.

- Deployment from Visual Studio Code or Azure CLI works only from inside the virtual network. You can use the Deployment Center to link your logic app to a GitHub repo. You can then use Azure infrastructure to build and deploy your code.

  For GitHub integration to work, remove the `WEBSITE_RUN_FROM_PACKAGE` setting from your logic app or set the value to `0`.

- Enabling Private Link doesn't affect outbound traffic, which still flows through the App Service infrastructure.

<a name="set-up-outbound"></a>

## Set up outbound traffic through private endpoints

To secure outbound traffic from your logic app, you can integrate your logic app with a virtual network. By default, outbound traffic from your logic app is only affected by network security groups (NSGs) and user-defined routes (UDRs) when going to a private address, such as `10.0.0.0/8`, `172.16.0.0/12`, and `192.168.0.0/16`.

If you use your own domain name server (DNS) with your virtual network, set your logic app resource's `WEBSITE_DNS_SERVER` app setting to the IP address for your DNS. If you have a secondary DNS, add another app setting named `WEBSITE_DNS_ALT_SERVER`, and set the value also to the IP for your DNS. Also, update your DNS records to point your private endpoints at your internal IP address. Private endpoints work by sending the DNS lookup to the private address, not the public address for the specific resource. For more information, review [Private endpoints - Integrate your app with an Azure virtual network](../app-service/overview-vnet-integration.md#private-endpoints).

> [!IMPORTANT]
> For the Azure Logic Apps runtime to work, you need to have an uninterrupted connection to the backend storage. 
> For Azure-hosted managed connectors to work, you need to have an uninterrupted connection to the managed API service.

### Considerations for outbound traffic through private endpoints

Setting up virtual network integration affects only outbound traffic. To secure inbound traffic, which continues to use the App Service shared endpoint, review [Set up inbound traffic through private endpoints](#set-up-inbound).

For more information, review the following documentation:

- [Integrate your app with an Azure virtual network](../app-service/overview-vnet-integration.md)

- [Network security groups](../virtual-network/network-security-groups-overview.md)

- [Virtual network traffic routing](../virtual-network/virtual-networks-udr-overview.md)

## Connect to storage account with private endpoints

You can restrict storage account access so that only resources inside a virtual network can connect. Azure Storage supports adding private endpoints to your storage account. Your logic app workflows can then use these endpoints to communicate with the storage account. For more information, review [Use private endpoints for Azure Storage](../storage/common/storage-private-endpoints.md).

> [!NOTE]
> The following steps require temporarily enabling public access on your storage account. If you can't enable public 
> access due to your organization's policies, you can still deploy your logic app using a private storage account. However, 
> you have to use an Azure Resource Manager template (ARM template) for deployment. For an example ARM template, review 
> [Deploy logic app using secured storage account with private endpoints](https://github.com/VeeraMS/LogicApp-deployment-with-Secure-Storage).

1. Create different private endpoints for each of the Table, Queue, Blob, and File storage services.

1. Enable temporary public access on your storage account when you deploy your logic app.

   1. In the [Azure portal](https://portal.azure.com), open your storage account resource.

   1. On the storage account resource menu, under **Security + networking**, select **Networking**.

   1. On the **Networking** pane, on the **Firewalls and virtual networks** tab, under **Allow access from**, select **All networks**.

1. Deploy your logic app resource by using either the Azure portal or Visual Studio Code.

1. After deployment finishes, enable integration between your logic app and the private endpoints on the virtual network or subnet that connects to your storage account.

   1. In the [Azure portal](https://portal.azure.com), open your logic app resource.

   1. On the logic app resource menu, under **Settings**, select **Networking**.

   1. Set up the necessary connections between your logic app and the IP addresses for the private endpoints.

   1. To access your logic app workflow data over the virtual network, in your logic app resource settings, set the `WEBSITE_CONTENTOVERVNET` setting to `1`.

   If you use your own domain name server (DNS) with your virtual network, set your logic app resource's `WEBSITE_DNS_SERVER` app setting to the IP address for your DNS. If you have a secondary DNS, add another app setting named `WEBSITE_DNS_ALT_SERVER`, and set the value also to the IP for your DNS. Also, update your DNS records to point your private endpoints at your internal IP address. Private endpoints work by sending the DNS lookup to the private address, not the public address for the specific resource. For more information, review [Private endpoints - Integrate your app with an Azure virtual network](../app-service/overview-vnet-integration.md#private-endpoints).

1. After you apply these app settings, you can remove public access from your storage account.

## Next steps

- [Logic Apps Anywhere: Networking possibilities with Logic Apps (single-tenant)](https://techcommunity.microsoft.com/t5/integrations-on-azure/logic-apps-anywhere-networking-possibilities-with-logic-app/ba-p/2105047)