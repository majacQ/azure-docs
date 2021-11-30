---
title: Rehydrate an archived blob to an online tier
titleSuffix: Azure Storage
description: Before you can read a blob that is in the Archive tier, you must rehydrate it to either the Hot or Cool tier. You can rehydrate a blob either by copying it from the Archive tier to an online tier, or by changing its tier from Archive to Hot or Cool.
services: storage
author: tamram

ms.service: storage
ms.topic: how-to
ms.date: 11/01/2021
ms.author: tamram
ms.reviewer: fryu
ms.custom: devx-track-azurepowershell
ms.subservice: blobs
---

# Rehydrate an archived blob to an online tier

To read a blob that is in the Archive tier, you must first rehydrate the blob to an online tier (Hot or Cool) tier. You can rehydrate a blob in one of two ways:

- By copying it to a new blob in the Hot or Cool tier with the [Copy Blob](/rest/api/storageservices/copy-blob) operation. Microsoft recommends this option for most scenarios.
- By changing its tier from Archive to Hot or Cool with the [Set Blob Tier](/rest/api/storageservices/set-blob-tier) operation.

When you rehydrate a blob, you can specify the priority for the operation to either standard priority or high priority. A standard-priority rehydration operation may take up to 15 hours to complete. A high-priority operation is prioritized over standard-priority requests and may complete in less than one hour for objects under 10 GB in size. You can change the rehydration priority from *Standard* to *High* while the operation is pending.

You can configure Azure Event Grid to fire an event when rehydration is complete and run application code in response. To learn how to handle an event that runs an Azure Function when the blob rehydration operation is complete, see [Run an Azure Function in response to a blob rehydration event](archive-rehydrate-handle-event.md).

For more information about rehydrating a blob, see [Blob rehydration from the Archive tier](archive-rehydrate-overview.md).

## Rehydrate a blob with a copy operation

To rehydrate a blob from the Archive tier by copying it to an online tier, use PowerShell, Azure CLI, or one of the Azure Storage client libraries. Keep in mind that when you copy an archived blob to an online tier, the source and destination blobs must have different names.

After the copy operation is complete, the destination blob appears in the Archive tier. The destination blob is then rehydrated to the online tier that you specified in the copy operation. When the destination blob is fully rehydrated, it becomes available in the new online tier.

The following examples show how to copy an archived blob with PowerShell or Azure CLI.

### [Portal](#tab/azure-portal)

N/A

### [PowerShell](#tab/azure-powershell)

To copy an archived blob to an online tier with PowerShell, call the [Start-AzStorageBlobCopy](/powershell/module/az.storage/start-azstorageblobcopy) command and specify the target tier and the rehydration priority. Remember to replace placeholders in angle brackets with your own values:

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
    -RehydratePriority Standard `
    -Context $ctx
```

### [Azure CLI](#tab/azure-cli)

To copy an archived blob to an online tier with Azure CLI, call the [az storage blob copy start](/cli/azure/storage/blob/copy#az_storage_blob_copy_start) command and specify the target tier and the rehydration priority. Remember to replace placeholders in angle brackets with your own values:

```azurecli
az storage blob copy start \
    --source-container <source-container> \
    --source-blob <source-blob> \
    --destination-container <dest-container> \
    --destination-blob <dest-blob> \
    --account-name <storage-account> \
    --tier hot \
    --rehydrate-priority standard \
    --auth-mode login
```

---

## Rehydrate a blob by changing its tier

To rehydrate a blob by changing its tier from Archive to Hot or Cool, use the Azure portal, PowerShell, or Azure CLI.

### [Portal](#tab/azure-portal)

To change a blob's tier from Archive to Hot or Cool in the Azure portal, follow these steps:

1. Locate the blob to rehydrate in the Azure portal.
1. Select the **More** button on the right side of the page.
1. Select **Change tier**.
1. Select the target access tier from the **Access tier** dropdown.
1. From the **Rehydrate priority** dropdown, select the desired rehydration priority. Keep in mind that setting the rehydration priority to *High* typically results in a faster rehydration, but also incurs a greater cost.

    :::image type="content" source="media/archive-rehydrate-to-online-tier/rehydrate-change-tier-portal.png" alt-text="Screenshot showing how to rehydrate a blob from the Archive tier in the Azure portal ":::

1. Select the **Save** button.

### [PowerShell](#tab/azure-powershell)

To change a blob's tier from Archive to Hot or Cool with PowerShell, use the blob's **BlobClient** property to return a .NET reference to the blob, then call the **SetAccessTier** method on that reference. Remember to replace placeholders in angle brackets with your own values:

```azurepowershell
# Initialize these variables with your values.
$rgName = "<resource-group>"
$accountName = "<storage-account>"
$containerName = "<container>"
$blobName = "<archived-blob>"

# Get the storage account context
$ctx = (Get-AzStorageAccount `
        -ResourceGroupName $rgName `
        -Name $accountName).Context

# Change the blob's access tier to Hot with Standard priority.
$blob = Get-AzStorageBlob -Container $containerName -Blob $blobName -Context $ctx
$blob.BlobClient.SetAccessTier("Hot", $null, "Standard")
```

### [Azure CLI](#tab/azure-cli)

To change a blob's tier from Archive to Hot or Cool with Azure CLI, call the [az storage blob set-tier](/cli/azure/storage/blob#az_storage_blob_set_tier) command. Remember to replace placeholders in angle brackets with your own values:

```azurecli
az storage blob set-tier \
    --account-name <storage-account> \
    --container-name <container> \
    --name <archived-blob> \
    --tier Hot \
    --rehydrate-priority Standard \
    --auth-mode login
```

---

## Bulk rehydrate a set of blobs

To rehydrate a large number of blobs at one time, call the [Blob Batch](/rest/api/storageservices/blob-batch) operation to call [Set Blob Tier](/rest/api/storageservices/set-blob-tier) as a bulk operation. For a code example that shows how to perform the batch operation, see [AzBulkSetBlobTier](/samples/azure/azbulksetblobtier/azbulksetblobtier/).

## Check the status of a rehydration operation

While the blob is rehydrating, you can check its status and rehydration priority using the Azure portal, PowerShell, or Azure CLI. The status property may return *rehydrate-pending-to-hot* or *rehydrate-pending-to-cool*, depending on the target tier for the rehydration operation. The rehydration priority property returns either *Standard* or *High*.

Keep in mind that rehydration of an archived blob may take up to 15 hours, and repeatedly polling the blob's status to determine whether rehydration is complete is inefficient. Using Azure Event Grid to capture the event that fires when rehydration is complete offers better performance and cost optimization. To learn how to run an Azure Function when an event fires on blob rehydration, see [Run an Azure Function in response to a blob rehydration event](archive-rehydrate-handle-event.md).

### [Portal](#tab/azure-portal)

To check the status and priority of a pending rehydration operation in the Azure portal, display the **Change tier** dialog for the blob:

:::image type="content" source="media/archive-rehydrate-to-online-tier/rehydration-status-portal.png" alt-text="Screenshot showing the rehydration status for a blob in the Azure portal":::

When the rehydration is complete, you can see in the Azure portal that the fully rehydrated blob now appears in the targeted online tier.

:::image type="content" source="media/archive-rehydrate-to-online-tier/set-blob-tier-rehydrated.png" alt-text="Screenshot showing the rehydrated blob in the Cool tier and the log blob written by the event handler":::

### [PowerShell](#tab/azure-powershell)

To check the status and priority of a pending rehydration operation with PowerShell, call the [Get-AzStorageBlob](/powershell/module/az.storage/get-azstorageblob) command, and check the **ArchiveStatus** and **RehydratePriority** properties of the blob. If the rehydration is a copy operation, check these properties on the destination blob. Remember to replace placeholders in angle brackets with your own values:

```azurepowershell
$rehydratingBlob = Get-AzStorageBlob -Container $containerName -Blob $blobName -Context $ctx
$rehydratingBlob.BlobProperties.ArchiveStatus
$rehydratingBlob.BlobProperties.RehydratePriority
```

### [Azure CLI](#tab/azure-cli)

To check the status and priority of a pending rehydration operation with Azure CLI, call the [az storage blob show](/cli/azure/storage/blob#az_storage_blob_show) command, and check the **rehydrationStatus** and **rehydratePriority** properties of the destination blob. Remember to replace placeholders in angle brackets with your own values:

```azurecli
az storage blob show \
    --account-name <storage-account> \
    --container-name <container> \
    --name <blob> \
    --query '[rehydratePriority, properties.rehydrationStatus]' \
    --output tsv \
    --auth-mode login
```

---

## Change the rehydration priority of a pending operation

While a standard-priority rehydration operation is pending, you can change the rehydration priority setting for a blob from *Standard* to *High* to rehydrate that blob more quickly.

Note that the rehydration priority setting cannot be lowered from *High* to *Standard* for a pending operation. Also keep in mind that changing the rehydration priority may have a billing impact. For more information, see [Blob rehydration from the Archive tier](archive-rehydrate-overview.md).

### Change the rehydration priority for a pending Set Blob Tier operation

To change the rehydration priority while a standard-priority [Set Blob Tier](/rest/api/storageservices/set-blob-tier) operation is pending, use the Azure portal, PowerShell, Azure CLI, or one of the Azure Storage client libraries.

#### [Portal](#tab/azure-portal)

To change the rehydration priority for a pending operation with the Azure portal, follow these steps:

1. Navigate to the blob for which you want to change the rehydration priority, and select the blob.
1. Select the **Change tier** button.
1. In the **Change tier** dialog, set the access tier to the target online access tier for the rehydrating blob (Hot or Cool). The **Archive status** field shows the target online tier.
1. In the **Rehydrate priority** dropdown, set the priority to *High*.
1. Select **Save**.

    :::image type="content" source="media/archive-rehydrate-to-online-tier/update-rehydration-priority-portal.png" alt-text="Screenshot showing how to update the rehydration priority for a rehydrating blob in Azure portal":::

#### [PowerShell](#tab/azure-powershell)

To change the rehydration priority for a pending operation with PowerShell, make sure that you have installed the [Az.Storage](https://www.powershellgallery.com/packages/Az.Storage) module, version 3.12.0 or later. Next, get the blob's properties from the service. This step is necessary to ensure that you have an object with the most recent property settings. Finally, use the blob's **BlobClient** property to return a .NET reference to the blob, then call the **SetAccessTier** method on that reference.

```azurepowershell
# Get the blob from the service.
$rehydratingBlob = Get-AzStorageBlob -Container $containerName -Blob $blobName -Context $ctx

# Verify that the current rehydration priority is Standard. 
if ($rehydratingBlob.BlobProperties.RehydratePriority -eq "Standard")
{
    # Change rehydration priority to High, using the same target tier.
    if ($rehydratingBlob.BlobProperties.ArchiveStatus -eq "rehydrate-pending-to-hot")
    {
        $rehydratingBlob.BlobClient.SetAccessTier("Hot", $null, "High")
        "Changing rehydration priority to High for blob moving to Hot tier."
    }
    
    if ($rehydratingBlob.BlobProperties.ArchiveStatus -eq "rehydrate-pending-to-cool")
    {
        $rehydratingBlob.BlobClient.SetAccessTier("Cool", $null, "High")
        "Changing rehydration priority to High for blob moving to Cool tier."
    }
}
```

#### [Azure CLI](#tab/azure-cli)

To change the rehydration priority for a pending operation with Azure CLI, first make sure that you have installed the Azure CLI, version 2.29.2 or later. For more information about installing the Azure CLI, see [How to install the Azure CLI](/cli/azure/install-azure-cli).

Next, call the [az storage blob set-tier](/cli/azure/storage/blob#az_storage_blob_set_tier) command with the `--rehydrate-priority` parameter set to *High*. The target tier (Hot or Cool) must be the same tier that you originally specified for the rehydration operation. Remember to replace placeholders in angle brackets with your own values:

```azurecli
# Update the rehydration priority for a blob moving to the Hot tier.
az storage blob set-tier \
    --account-name <storage-account> \
    --container-name <container> \
    --name <blob> \
    --tier Hot \
    --rehydrate-priority High \
    --auth-mode login

# Show the updated property values.
az storage blob show \
    --account-name <storage-account> \
    --container-name <container> \
    --name <blob> \
    --query '[rehydratePriority, properties.rehydrationStatus]' \
    --output tsv \
    --auth-mode login
```

---

### Change the rehydration priority for a pending Copy Blob operation

When you rehydrate a blob by copying the archived blob to an online tier, Azure Storage immediately creates the destination blob in the Archive tier. The destination blob is then rehydrated to the target tier with the priority specified on the copy operation. For more information on rehydrating an archived blob with a copy operation, see [Copy an archived blob to an online tier](archive-rehydrate-overview.md#copy-an-archived-blob-to-an-online-tier).

To perform the copy operation from the Archive tier to an online tier with Standard priority, use PowerShell, Azure CLI, or one of the Azure Storage client libraries. For more information, see [Rehydrate a blob with a copy operation](archive-rehydrate-to-online-tier.md#rehydrate-a-blob-with-a-copy-operation). Next, to change the rehydration priority from *Standard* to *High* for the pending rehydration, call **Set Blob Tier** on the destination blob and specify the target tier.

#### [Portal](#tab/azure-portal)

After you have initiated the copy operation, you'll see in the Azure portal that both the source and destination blob are in the Archive tier. The destination blob is rehydrating with Standard priority.

:::image type="content" source="media/archive-rehydrate-to-online-tier/rehydration-properties-portal-standard-priority.png" alt-text="Screenshot showing destination blob in Archive tier and rehydrating with Standard priority":::

To change the rehydration priority for the destination blob, follow these steps:

1. Select the destination blob.
1. Select the **Change tier** button.
1. In the **Change tier** dialog, set the access tier to the target online access tier for the rehydrating blob (Hot or Cool). The **Archive status** field shows the target online tier.
1. In the **Rehydrate priority** dropdown, set the priority to *High*.
1. Select **Save**.

The destination blob's properties page now shows that it is rehydrating with High priority.

:::image type="content" source="media/archive-rehydrate-to-online-tier/rehydration-properties-portal-high-priority.png" alt-text="Screenshot showing destination blob in Archive tier and rehydrating with High priority":::

#### [PowerShell](#tab/azure-powershell)

After you have initiated the copy operation, check the properties of the destination blob. You'll see that the destination blob is in the Archive tier and is rehydrating with Standard priority.

```azurepowershell
# Initialize these variables with your values.
$rgName = "<resource-group>"
$accountName = "<storage-account>"
$destContainerName = "<container>"
$destBlobName = "<destination-blob>"

# Get the storage account context
$ctx = (Get-AzStorageAccount `
        -ResourceGroupName $rgName `
        -Name $accountName).Context

# Get properties for the destination blob.
$destinationBlob = Get-AzStorageBlob -Container $destContainerName `
    -Blob $destBlobName `
    -Context $ctx

$destinationBlob.BlobProperties.AccessTier
$destinationBlob.BlobProperties.ArchiveStatus
$destinationBlob.BlobProperties.RehydratePriority
```

Next, call the **SetAccessTier** method via PowerShell to change the rehydration priority for the destination blob to *High*, as described in [Change the rehydration priority for a pending Set Blob Tier operation](#change-the-rehydration-priority-for-a-pending-set-blob-tier-operation). The target tier (Hot or Cool) must be the same tier that you originally specified for the rehydration operation. Check the properties again to verify that the blob is now rehydrating with High priority.

#### [Azure CLI](#tab/azure-cli)

After you have initiated the copy operation, check the properties of the destination blob. You'll see that the destination blob is in the Archive tier and is rehydrating with Standard priority.

```azurecli
az storage blob show \
    --account-name <storage-account> \
    --container-name <container> \
    --name <blob> \
    --query '[rehydratePriority, properties.rehydrationStatus]' \
    --output tsv \
    --auth-mode login
```

Next, call the [az storage blob set-tier](/cli/azure/storage/blob#az_storage_blob_set_tier) command with the `--rehydrate-priority` parameter set to *High*, as described in [Change the rehydration priority for a pending Set Blob Tier operation](#change-the-rehydration-priority-for-a-pending-set-blob-tier-operation). The target tier (Hot or Cool) must be the same tier that you originally specified for the rehydration operation. Check the properties again to verify that the blob is now rehydrating with High priority.

---

## See also

- [Hot, Cool, and Archive access tiers for blob data](access-tiers-overview.md).
- [Overview of blob rehydration from the Archive tier](archive-rehydrate-overview.md)
- [Run an Azure Function in response to a blob rehydration event](archive-rehydrate-handle-event.md)
- [Reacting to Blob storage events](storage-blob-event-overview.md)
