---
title: Set a blob's access tier
titleSuffix: Azure Storage
description: Learn how to specify a blob's access tier when you upload it, or how to change the access tier for an existing blob.
author: tamram

ms.author: tamram
ms.date: 10/25/2021
ms.service: storage
ms.subservice: blobs
ms.topic: how-to
ms.reviewer: fryu
ms.custom: devx-track-azurepowershell
---

# Set a blob's access tier

You can set a blob's access tier in any of the following ways:

- By setting the default online access tier (Hot or Cool) for the storage account. Blobs in the account inherit this access tier unless you explicitly override the setting for an individual blob.
- By explicitly setting a blob's tier on upload. You can create a blob in the Hot, Cool, or Archive tier.
- By changing an existing blob's tier with a Set Blob Tier operation, typically to move from a hotter tier to a cooler one.
- By copying a blob with a Copy Blob operation, typically to move from a cooler tier to a hotter one.

This article describes how manage a blob in an online access tier (Hot or Cool). For more information about how to move a blob to the Archive tier, see [Archive a blob](archive-blob.md). For more information about how to rehydrate a blob from the Archive tier, see [Rehydrate an archived blob to an online tier](archive-rehydrate-to-online-tier.md).

For more information about access tiers for blobs, see [Hot, Cool, and Archive access tiers for blob data](access-tiers-overview.md).

## Set the default access tier for a storage account

The default access tier setting for a general-purpose v2 storage account determines in which online tier a new blob is created by default. You can set the default access tier for a general-purpose v2 storage account at the time that you create the account or by updating an existing account's configuration.

When you change the default access tier setting for an existing general-purpose v2 storage account, the change applies to all blobs in the account for which an access tier has not been explicitly set. Changing the default access tier may have a billing impact. For details, see [Default account access tier setting](access-tiers-overview.md#default-account-access-tier-setting).

#### [Portal](#tab/azure-portal)

To set the default access tier for a storage account at create time in the Azure portal, follow these steps:

1. Navigate to the **Storage accounts** page, and select the **Create** button.
1. Fill out the **Basics** tab.
1. On the **Advanced** tab, under **Blob storage**, set the **Access tier** to either *Hot* or *Cool*. The default setting is *Hot*.
1. Select **Review + Create** to validate your settings and create your storage account.

    :::image type="content" source="media/access-tiers-online-manage/set-default-access-tier-create-portal.png" alt-text="Screenshot showing how to set the default access tier when creating a storage account.":::

To update the default access tier for an existing storage account in the Azure portal, follow these steps:

1. Navigate to the storage account in the Azure portal.
1. Under **Settings**, select **Configuration**.
1. Locate the **Blob access tier (default)** setting, and select either *Hot* or *Cool*. The default setting is *Hot*, if you have not previously set this property.
1. Save your changes.

#### [PowerShell](#tab/azure-powershell)

To change the default access tier setting for a storage account with PowerShell, call the [Set-AzStorageAccount](/powershell/module/az.storage/set-azstorageaccount) command, specifying the new default access tier.

```azurepowershell
$rgName = <resource-group>
$accountName = <storage-account>

# Change the storage account tier to Cool
Set-AzStorageAccount -ResourceGroupName $rgName -Name $accountName -AccessTier Cool
```

#### [Azure CLI](#tab/azure-cli)

To change the default access tier setting for a storage account with PowerShell, call the [Set-AzStorageAccount](/powershell/module/az.storage/set-azstorageaccount) command, specifying the new default access tier.

```azurecli
# Change the storage account tier to Cool
az storage account update \
    --resource-group <resource-group> \
    --name <storage-account> \
    --access-tier Cool
```

---

## Set a blob's tier on upload

When you upload a blob to Azure Storage, you have two options for setting the blob's tier on upload:

- You can explicitly specify the tier in which the blob will be created. This setting overrides the default access tier for the storage account. You can set the tier for a blob or set of blobs on upload to Hot, Cool, or Archive.
- You can upload a blob without specifying a tier. In this case, the blob will be created in the default access tier specified for the storage account (either Hot or Cool).

The following sections describe how to specify that a blob is uploaded to either the Hot or Cool tier. For more information about archiving a blob on upload, see [Archive blobs on upload](archive-blob.md#archive-blobs-on-upload).

### Upload a blob to a specific online tier

To create a blob in the Hot or Cool tier tier, specify that tier when you create the blob. The access tier specified on upload overrides the default access tier for the storage account.

### [Portal](#tab/azure-portal)

To upload a blob or set of blobs to a specific tier from the Azure portal, follow these steps:

1. Navigate to the target container.
1. Select the **Upload** button.
1. Select the file or files to upload.
1. Expand the **Advanced** section, and set the **Access tier** to *Hot* or *Cool*.
1. Select the **Upload** button.

    :::image type="content" source="media/access-tiers-online-manage/upload-blob-to-online-tier-portal.png" alt-text="Screenshot showing how to upload blobs to an online tier in the Azure portal.":::

### [PowerShell](#tab/azure-powershell)

To upload a blob or set of blobs to a specific tier with PowerShell, call the [Set-AzStorageBlobContent](/powershell/module/az.storage/set-azstorageblobcontent) command, as shown in the following example. Remember to replace the placeholder values in brackets with your own values:

```azurepowershell
$rgName = <resource-group>
$storageAccount = <storage-account>
$containerName = <container>

# Get context object
$ctx = New-AzStorageContext -StorageAccountName $storageAccount -UseConnectedAccount

# Create new container.
New-AzStorageContainer -Name $containerName -Context $ctx

# Upload a single file named blob1.txt to the Cool tier.
Set-AzStorageBlobContent -Container $containerName `
    -File "blob1.txt" `
    -Blob "blob1.txt" `
    -Context $ctx `
    -StandardBlobTier Cool

# Upload the contents of a sample-blobs directory to the Cool tier, recursively.
Get-ChildItem -Path "C:\sample-blobs" -File -Recurse | 
    Set-AzStorageBlobContent -Container $containerName `
        -Context $ctx `
        -StandardBlobTier Cool
```

### [Azure CLI](#tab/azure-cli)

To upload a blob to a specific tier with Azure CLI, call the [az storage blob upload](/cli/azure/storage/blob#az_storage_blob_upload) command, as shown in the following example. Remember to replace the placeholder values in brackets with your own values:

```azurecli
az storage blob upload \
    --account-name <storage-account> \
    --container-name <container> \
    --name <blob> \
    --file <file> \
    --tier Cool \
    --auth-mode login
```

To upload a set of blobs to a specific tier with Azure CLI, call the [az storage blob upload-batch](/cli/azure/storage/blob#az_storage_blob_upload_batch) command, as shown in the following example. Remember to replace the placeholder values in brackets with your own values:

```azurecli
az storage blob upload-batch \
    --destination <container> \
    --source <source-directory> \
    --account-name <storage-account> \
    --tier Cool \
    --auth-mode login
```

---

### Upload a blob to the default tier

Storage accounts have a default access tier setting that indicates in which online tier a new blob is created. The default access tier setting can be set to either hot or cool. The behavior of this setting is slightly different depending on the type of storage account:

- The default access tier for a new general-purpose v2 storage account is set to the Hot tier by default. You can change the default access tier setting when you create a storage account or after it is created.
- When you create a legacy Blob Storage account, you must specify the default access tier setting as Hot or Cool when you create the storage account. You can change the default access tier setting for the storage account after it is created.

A blob that doesn't have an explicitly assigned tier infers its tier from the default account access tier setting. You can determine whether a blob's access tier is inferred by using the Azure portal, PowerShell, or Azure CLI.

#### [Portal](#tab/azure-portal)

If a blob's access tier is inferred from the default account access tier setting, then the Azure portal displays the access tier as **Hot (inferred)** or **Cool (inferred)**.

:::image type="content" source="media/access-tiers-online-manage/default-access-tier-portal.png" alt-text="Screenshot showing blobs with the default access tier in the Azure portal.":::

#### [PowerShell](#tab/azure-powershell)

To determine a blob's access tier and whether it is inferred from Azure PowerShell, retrieve the blob, then check its **AccessTier** and **AccessTierInferred** properties.

```azurepowershell
$rgName = "<resource-group>"
$storageAccount = "<storage-account>"
$containerName = "<container>"
$blobName = "<blob>"

# Get the storage account context.
$ctx = New-AzStorageContext -StorageAccountName $storageAccount -UseConnectedAccount

# Get the blob from the service.
$blob = Get-AzStorageBlob -Context $ctx -Container $containerName -Blob $blobName

# Check the AccessTier and AccessTierInferred properties.
# If the access tier is inferred, that property returns true.
$blob.BlobProperties.AccessTier
$blob.BlobProperties.AccessTierInferred
```

#### [Azure CLI](#tab/azure-cli)

To determine a blob's access tier and whether it is inferred from Azure CLI, retrieve the blob, then check its **blobTier** and **blobTierInferred** properties.

```azurecli
az storage blob show \
    --container-name <container> \
    --name <blob> \
    --account-name <storage-account> \
    --query '[properties.blobTier, properties.blobTierInferred]' \
    --output tsv \
    --auth-mode login 
```

---

## Move a blob to a different online tier

You can change the tier of an existing blob in one of two ways:

- By calling the [Set Blob Tier](/rest/api/storageservices/set-blob-tier) operation, either directly or via a [lifecycle management](access-tiers-overview.md#blob-lifecycle-management) policy, to change the blob's tier.
- By calling the [Copy Blob](/rest/api/storageservices/copy-blob) operation to copy a blob from one tier to another. In this case, the source blob remains in the original tier, and a new blob is created in the target tier.

For more information about each of these options, see [Setting or changing a blob's tier](access-tiers-overview.md#setting-or-changing-a-blobs-tier).

Use PowerShell, Azure CLI, or one of the Azure Storage client libraries to move a blob to a different tier.

### Change a blob's tier

When you change a blob's tier, you move that blob and all of its data to the target tier. Calling [Set Blob Tier](/rest/api/storageservices/set-blob-tier) is typically the best option when you are changing a blob's tier from a hotter tier to a cooler one.

# [Portal](#tab/azure-portal)

To change a blob's tier from Hot to Cool in the Azure portal, follow these steps:

1. Navigate to the blob for which you want to change the tier.
1. Select the blob, then select the **Change tier** button.
1. In the **Change tier** dialog, select the target tier.
1. Select the **Save** button.

    :::image type="content" source="media/access-tiers-online-manage/change-blob-tier-portal.png" alt-text="Screenshot showing how to change a blob's tier in the Azure portal":::

#### [PowerShell](#tab/azure-powershell)

To change a blob's tier from Hot to Cool with PowerShell, use the blob's **BlobClient** property to return a .NET reference to the blob, then call the **SetAccessTier** method on that reference. Remember to replace placeholders in angle brackets with your own values:

```azurepowershell
# Initialize these variables with your values.
$rgName = "<resource-group>"
$accountName = "<storage-account>"
$containerName = "<container>"
$blobName = "<blob>"

# Get the storage account context
$ctx = (Get-AzStorageAccount `
        -ResourceGroupName $rgName `
        -Name $accountName).Context

# Change the blob's access tier to Cool.
$blob = Get-AzStorageBlob -Container $containerName -Blob $blobName -Context $ctx
$blob.BlobClient.SetAccessTier("Cool", $null, "Standard")
```

#### [Azure CLI](#tab/azure-cli)

To change a blob's tier from Hot to Cool with Azure CLI, call the [az storage blob set-tier](/cli/azure/storage/blob#az_storage_blob_set_tier) command. Remember to replace placeholders in angle brackets with your own values:

```azurecli
az storage blob set-tier \
    --account-name <storage-account> \
    --container-name <container> \
    --name <blob> \
    --tier Cool \
    --auth-mode login
```

---

### Copy a blob to a different online tier

When you copy a blob to a different tier, you move that blob and all of its data to the target tier. Calling [Copy Blob](/rest/api/storageservices/copy-blob) is recommended for most scenarios where you are moving a blob from Cool to Hot, or rehydrating a blob from the Archive tier.

# [Portal](#tab/azure-portal)

N/A

#### [PowerShell](#tab/azure-powershell)

To copy a blob to from Cool to Hot with PowerShell, call the [Start-AzStorageBlobCopy](/powershell/module/az.storage/start-azstorageblobcopy) command and specify the target tier. Remember to replace placeholders in angle brackets with your own values:

```azurepowershell
# Initialize these variables with your values.
$rgName = "<resource-group>"
$accountName = "<storage-account>"
$srcContainerName = "<source-container>"
$destContainerName = "<dest-container>"
$srcBlobName = "<source-blob>"
$destBlobName = "<dest-blob>"

# Get the storage account context
$ctx = (Get-AzStorageAccount `
        -ResourceGroupName $rgName `
        -Name $accountName).Context

# Copy the source blob to a new destination blob in Hot tier with Standard priority.
Start-AzStorageBlobCopy -SrcContainer $srcContainerName `
    -SrcBlob $srcBlobName `
    -DestContainer $destContainerName `
    -DestBlob $destBlobName `
    -StandardBlobTier Hot `
    -Context $ctx
```

#### [Azure CLI](#tab/azure-cli)

To copy a blob from Cool to Hot with Azure CLI, call the [az storage blob copy start](/cli/azure/storage/blob/copy#az_storage_blob_copy_start) command and specify the target tier. Remember to replace placeholders in angle brackets with your own values:

```azurecli
az storage blob copy start \
    --source-container <source-container> \
    --source-blob <source-blob> \
    --destination-container <dest-container> \
    --destination-blob <dest-blob> \
    --account-name <storage-account> \
    --tier hot \
    --auth-mode login
```

---

## Next steps

- [How to manage the default account access tier of an Azure Storage account](../common/manage-account-default-access-tier.md)
- [Rehydrate an archived blob to an online tier](archive-rehydrate-to-online-tier.md)
