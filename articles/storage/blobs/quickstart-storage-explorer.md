---
title: Quickstart - Create a blob with Azure Storage Explorer
titleSuffix: Azure Storage
description: Learn how to use Azure Storage Explorer to create a container and a blob, download the blob to your local computer, and view all of the blobs in the container.
services: storage
author: tamram
ms.service: storage
ms.subservice: blobs
ms.topic: quickstart
ms.date: 09/10/2021
ms.author: tamram
ms.custom: mode-other
---

# Quickstart: Use Azure Storage Explorer to create a blob

In this quickstart, you learn how to use [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) to create a container and a blob. Next, you learn how to download the blob to your local computer, and how to view all of the blobs in a container. You also learn how to create a snapshot of a blob, manage container access policies, and create a shared access signature.

## Prerequisites

[!INCLUDE [storage-quickstart-prereq-include](../../../includes/storage-quickstart-prereq-include.md)]

This quickstart requires that you install Azure Storage Explorer. To install Azure Storage Explorer for Windows, Macintosh, or Linux, see [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/).

## Log in to Storage Explorer

On first launch, the **Microsoft Azure Storage Explorer - Connect** window is shown. Storage Explorer provides several ways to connect to storage accounts. The following table lists the different ways you can connect:

|Task|Purpose|
|---|---|
|Add an Azure Account | Redirects you to your organization's sign-in page to authenticate you to Azure. |
|Use a connection string or shared access signature URI | Can be used to directly access a container or storage account with a SAS token or a shared connection string. |
|Use a storage account name and key| Use the storage account name and key of your storage account to connect to Azure storage.|

Select **Add an Azure Account** and click **Sign in..**. Follow the on-screen prompts to sign into your Azure account.

:::image type="content" source="media/quickstart-storage-explorer/storage-explorer-connect.png" alt-text="Screenshot that shows the Microsoft Azure Storage Explorer - Connect window":::

After Storage Explorer finishes connecting, it displays the **Explorer** tab. This view gives you insight to all of your Azure storage accounts as well as local storage configured through the [Azurite storage emulator](../common/storage-use-azurite.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json), [Cosmos DB](../../cosmos-db/storage-explorer.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) accounts, or [Azure Stack](/azure-stack/user/azure-stack-storage-connect-se?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) environments.

:::image type="content" source="media/quickstart-storage-explorer/storage-explorer-main-page.png" alt-text="Screenshot showing Storage Explorer main page":::

## Create a container

To create a container, expand the storage account you created in the proceeding step. Select **Blob Containers**, right-click and select **Create Blob Container**. Enter the name for your blob container. See the [Create a container](storage-quickstart-blobs-dotnet.md#create-a-container) section for a list of rules and restrictions on naming blob containers. When complete, press **Enter** to create the blob container. Once the blob container has been successfully created, it is displayed under the **Blob Containers** folder for the selected storage account.

## Upload blobs to the container

Blob storage supports block blobs, append blobs, and page blobs. VHD files used to back IaaS VMs are page blobs. Append blobs are used for logging, such as when you want to write to a file and then keep adding more information. Most files stored in Blob storage are block blobs.

On the container ribbon, select **Upload**. This operation gives you the option to upload a folder or a file.

Choose the files or folder to upload. Select the **blob type**. Acceptable choices are **Append**, **Page**, or **Block** blob.

If uploading a .vhd or .vhdx file, choose **Upload .vhd/.vhdx files as page blobs (recommended)**.

In the **Upload to folder (optional)** field either a folder name to store the files or folders in a folder under the container. If no folder is chosen, the files are uploaded directly under the container.

:::image type="content" source="media/quickstart-storage-explorer/storage-explorer-upload-blob.png" alt-text="Microsoft Azure Storage Explorer - upload a blob":::

When you select **OK**, the files selected are queued to upload, each file is uploaded. When the upload is complete, the results are shown in the **Activities** window.

## View blobs in a container

In the **Azure Storage Explorer** application, select a container under a storage account. The main pane shows a list of the blobs in the selected container.

:::image type="content" source="media/quickstart-storage-explorer/storage-explorer-list-blobs.png" alt-text="Screenshot that shows how to select a container in Microsoft Azure Storage Explorer":::

## Download blobs

To download blobs using **Azure Storage Explorer**, with a blob selected, select **Download** from the ribbon. A file dialog opens and provides you the ability to enter a file name. Select **Save** to start the download of a blob to the local location.

## Manage snapshots

Azure Storage Explorer provides the capability to take and manage [snapshots](./snapshots-overview.md) of your blobs. To take a snapshot of a blob, right-click the blob and select **Create Snapshot**. To view snapshots for a blob, right-click the blob and select **Manage Snapshots**. A list of the snapshots for the blob are shown in the current tab.

:::image type="content" source="media/quickstart-storage-explorer/storage-explorer-snapshots.png" alt-text="Screenshot showing how to take and manage blob snapshots":::

## Generate a shared access signature

You can use Storage Explorer to generate a shared access signatures (SAS). Right-click a storage account, container, or blob and choose **Get Shared Access Signature...**. Choose the start and expiry time, and permissions for the SAS URL and select **Create**. Storage Explorer generates the SAS token with the parameters you specified and displays it for copying.

:::image type="content" source="media/quickstart-storage-explorer/storage-explorer-shared-access-signature.png" alt-text="Screenshot showing how to generate a SAS":::

When you create a SAS for a storage account, Storage Explorer generates an account SAS. For more information about the account SAS, see [Create an account SAS](/rest/api/storageservices/create-account-sas).

When you create a SAS for a container or blob, Storage Explorer generates a service SAS. For more information about the service SAS, see [Create a service SAS](/rest/api/storageservices/create-service-sas).

> [!NOTE]
> When you create a SAS with Storage Explorer, the SAS is always assigned with the storage account key. Storage Explorer does not currently support creating a user delegation SAS, which is a SAS that is signed with Azure AD credentials.

## Next steps

In this quickstart, you learned how to transfer files between a local disk and Azure Blob storage using **Azure Storage Explorer**. To learn more about working with Blob storage, continue to the Blob storage overview.

> [!div class="nextstepaction"]
> [Introduction to Azure Blob Storage](./storage-blobs-introduction.md)
