---
title: Quickstart - Create a service connection in App Service from Azure portal
description: Quickstart showing how to create a service connection in App Service from Azure portal
author: shizn
ms.author: xshi
ms.service: serviceconnector
ms.topic: overview
ms.date: 10/29/2021
ms.custom: ignite-fall-2021
---

# Quickstart: Create a service connection in App Service from Azure portal

This quickstart shows you how to create a new service connection with Service Connector in App Service from Azure portal.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

This quickstart assumes that you already have at least an App Service running on Azure. If you don't have an App Service, [create one](../app-service/quickstart-dotnetcore.md).

## Sign in to Azure

Sign in to the Azure portal at [https://portal.azure.com/](https://portal.azure.com/) with your Azure account.

## Create a new service connection in App Service

You will use Service Connector to create a new service connection in App Service.

1. Select **All resource** button found on the left of the Azure portal. Type **App Service** in the filter and click the name of the App Service you want to use in the list.
2. Select **Service Connector (Preview)** from the left table of contents. Then select **Create**.
3. Select or enter the following settings.

    | Setting      | Suggested value  | Description                                        |
    | ------------ |  ------- | -------------------------------------------------- |
    | **Subscription** | One of your subscriptions | The subscription where your target service (the service you want to connect to) is. The default value is the subscription that this App Service is in. |
    | **Service Type** | Blob Storage | Target service type. If you don't have a Storage Blob container, you can [create one](../storage/blobs/storage-quickstart-blobs-portal.md) or use an other service type. |
    | **Connection Name** | Generated unique name | The connection name that identifies the connection between your App Service and target service  |
    | **Storage account** | Your storage account | The target storage account you want to connect to. If you choose a different service type, select the corresponding target service instance. |
    | **Client Type** | The same app stack on this App Service | Your application stack that works with the target service you selected. The default value comes from the App Service runtime stack. |

4. Select **Next: Authentication** to select the authentication type. Then select **Connection string** to use access key to connect your Blob storage account.

5. Then select **Next: Review + Create**  to review the provided information. Then select **Create** to create the service connection. It might take 1 minute to complete the operation.

## View service connections in App Service

1. In **Service Connector (Preview)**, you see an App Service connection to the target service.

1. Click **>** button to expand the list, you can see the environment variables required by your application code.

1. Click **...** button and select **Validate**, you can see the connection validation details in the pop-up blade from right.

## Next steps

Follow the tutorials listed below to start building your own application with Service Connector.

> [!div class="nextstepaction"]
> [Tutorial: WebApp + Storage with Azure CLI](./tutorial-csharp-webapp-storage-cli.md)

> [!div class="nextstepaction"]
> [Tutorial: WebApp + PostgreSQL with Azure CLI](./tutorial-django-webapp-postgres-cli.md)
