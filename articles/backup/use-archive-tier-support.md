---
title: Use Archive Tier
description: Learn about using Archive Tier Support for Azure Backup.
ms.topic: conceptual
ms.date: 10/23/2021
ms.custom: devx-track-azurepowershell-azurecli
zone_pivot_groups: backup-client-powershelltier-clitier-portaltier
author: v-amallick
ms.service: backup
ms.author: v-amallick
---

# Use Archive Tier support


::: zone pivot="client-powershelltier"

This article provides the procedure to backup of long-term retention points in the archive tier, and snapshots and the Standard tier using PowerShell.

## Supported workloads

| Workloads | Operations |
| --- | --- |
| Azure Virtual Machines (Preview)   <br><br>  SQL Server in Azure Virtual Machines   | <ul><li>View Archivable Recovery Points    </li><li>View Recommended Recovery Points (Only for Virtual Machines)  </li><li>Move Archivable Recovery Points   </li><li>Move Recommended Recovery Points (Only for Azure Virtual Machines)   </li><li>View Archived Recovery points   </li><li>Restore from archived recovery points   </li></ul> |

## Get started

1. Download the [latest](https://github.com/PowerShell/PowerShell/releases) version of PowerShell from GitHub.

1. Run the following cmdlet in PowerShell:
  
    ```azurepowershell
    install-module -name Az.RecoveryServices -Repository PSGallery -RequiredVersion 4.4.0 -AllowPrerelease -force
    ```

1. Connect to Azure using the [Connect-AzAccount](/powershell/module/az.accounts/connect-azaccount) cmdlet.

1. Sign into your subscription:

   ```azurepowershell
   Set-AzContext -Subscription "SubscriptionName"
   ```

1. Get the vault:

    ```azurepowershell
    $vault = Get-AzRecoveryServicesVault -ResourceGroupName "rgName" -Name "vaultName"
    ```

1. Get the list of backup items:

   - **For Azure Virtual Machines**

       ```azurepowershell
       $BackupItemList = Get-AzRecoveryServicesBackupItem -vaultId $vault.ID -BackupManagementType "AzureVM" -WorkloadType "AzureVM"
       ```

   - **For SQL Server in Azure Virtual Machines**

       ```azurepowershell
       $BackupItemList = Get-AzRecoveryServicesBackupItem -vaultId $vault.ID -BackupManagementType "AzureWorkload" -WorkloadType "MSSQL"
       ```

1. Get the backup item.

   - **For Azure Virtual Machines**

     ```azurepowershell
     $bckItm = $BackupItemList | Where-Object {$_.Name -match '<vmName>'}
     ```

   - **For SQL Server in Azure Virtual Machines**

     ```azurepowershell
     $bckItm = $BackupItemList | Where-Object {$_.FriendlyName -eq '<dbName>' -and $_.ContainerName -match '<vmName>'}
     ```

1. (Optional) Add the date range for which you want to view the recovery points. For example, if you want to view the recovery points from the last 120 days, use the following cmdlet:

   ```azurepowershell
    $startDate = (Get-Date).AddDays(-120)
    $endDate = (Get-Date).AddDays(0) 
   ```
   >[!NOTE]
   >To view recovery points for a different time range, modify the start and the end date accordingly. <br><br> By default, it's taken for the last 30 days.

## Check the archivable status of all recovery points

You can now check the archivable status of all recovery points of a backup item using the following cmdlet:

```azurepowershell
$rp = Get-AzRecoveryServicesBackupRecoveryPoint -VaultId $vault.ID -Item $bckItm -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime() 

$rp | select RecoveryPointId, @{ Label="IsArchivable";Expression={$_.RecoveryPointMoveReadinessInfo["ArchivedRP"].IsReadyForMove}}, @{ Label="ArchivableInfo";Expression={$_.RecoveryPointMoveReadinessInfo["ArchivedRP"].AdditionalInfo}}
```

## Check archivable recovery points

```azurepowershell
$rp = Get-AzRecoveryServicesBackupRecoveryPoint -VaultId $vault.ID -Item $bckItm -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime() -IsReadyForMove $true -TargetTier VaultArchive
```

This lists all recovery points associated with a particular backup item that are ready to be moved to archive (from the start date to the end date). You can also modify the start dates and the end dates.

## Check why a recovery point can't be moved to archive

```azurepowershell
$rp = Get-AzRecoveryServicesBackupRecoveryPoint -VaultId $vault.ID -Item $bckItm -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime() -IsReadyForMove $false -TargetTier VaultArchive
$rp[0].RecoveryPointMoveReadinessInfo["ArchivedRP"]
```

Where `$rp[0]` is the recovery point for which you want to check why it's not archivable.

**Sample output**

```output
IsReadyForMove  AdditionalInfo
--------------  --------------
False           Recovery-Point Type is not eligible for archive move as it is already moved to archive tier
```

## Check recommended set of archivable points (only for Azure VMs)

The recovery points associated with a virtual machine are incremental. When you move a particular recovery point to archive, it's converted into a full backup, and then moved to archive. So, the cost savings associated with moving to archive depends on the churn of the data source.

Therefore, Azure Backup provides a recommended set of recovery points that might save cost, if moved together.

>[!NOTE]
>- The cost savings depends on various reasons and might not be the same for every instance.
>- Cost savings are ensured only when you move all recovery points contained in the recommendation set to the vault-archive tier.

```azurepowershell
$RecommendedRecoveryPointList = Get-AzRecoveryServicesBackupRecommendedArchivableRPGroup -Item $bckItm -VaultId $vault.ID
```

## Move to archive

```azurepowershell
Move-AzRecoveryServicesBackupRecoveryPoint -VaultId $vault.ID -RecoveryPoint $rp[0] -SourceTier VaultStandard -DestinationTier VaultArchive
```

Where, `$rp[0]` is the first recovery point in the list. If you want to move other recovery points, use `$rp[1]`, `$rp[2]`, and so on.

This cmdlet moves an archivable recovery point to archive. It returns a job that can be used to track the move operation, both from portal and with PowerShell.

## View archived recovery points

This cmdlet returns all archived recovery points.

```azurepowershell
$rp = Get-AzRecoveryServicesBackupRecoveryPoint -VaultId $vault.ID -Item $bckItm -Tier VaultArchive -StartDate $startdate.ToUniversalTime() -EndDate $enddate.ToUniversalTime()
```

## Restore with PowerShell

For recovery points in archive, Azure Backup provides an integrated restore methodology.
The integrated restore is a two-step process.

1. Involves rehydrating the recovery points stored in archive.
2. Temporarily store it in the vault-standard tier for a duration (also known as the rehydration duration) ranging from a period of 10 to 30 days. The default is 15 days. There are two different priorities of rehydration – Standard and High priority. Learn more about [rehydration priority](../storage/blobs/archive-rehydrate-overview.md#rehydration-priority).

>[!NOTE]
>
>- The rehydration duration once selected can't be changed and the rehydrated recovery points stay in the standard tier for the rehydration duration.
>- The additional step of rehydration incurs cost.

For more information about the various restore methods for Azure virtual machines, see [Restore an Azure VM with PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm).

```azurepowershell
Restore-AzRecoveryServicesBackupItem -VaultLocation $vault.Location -RehydratePriority "Standard" -RehydrateDuration 15 -RecoveryPoint $rp -StorageAccountName "SampleSA" -StorageAccountResourceGroupName "SArgName" -TargetResourceGroupName $vault.ResourceGroupName -VaultId $vault.ID
```

To restore SQL Server, follow [these steps](backup-azure-sql-automation.md#restore-sql-dbs). The `Restore-AzRecoveryServicesBackupItem` cmdlet requires two additional parameters, `RehydrationDuration` and `RehydrationPriority`.

## View jobs

To view the move and restore jobs, use the following PowerShell cmdlet:

```azurepowershell
Get-AzRecoveryServicesBackupJob -VaultId $vault.ID
```

## Move recovery points to archive tier at scale

You can now use sample scripts to perform at scale operations. [Learn more](https://github.com/hiaga/Az.RecoveryServices/blob/master/README.md) about how to run the sample scripts. You can download the scripts from [here](https://github.com/hiaga/Az.RecoveryServices).

You can perform the following operations using the sample scripts provided by Azure Backup:

- Move all eligible recovery points for a particular database/all databases for a SQL server in Azure VM to the archive tier.
- Move all recommended recovery points for a particular Azure Virtual Machine to the archive tier.
 
You can also write a script as per your requirements or modify the above sample scripts to fetch the required backup items.

::: zone-end



::: zone pivot="client-clitier"

This article provides the procedure to backup of long-term retention points in the archive tier, and snapshots and the Standard tier using command-line interface (CLI).

## Supported workloads

| Workloads | Operations |
| --- | --- |
| Azure Virtual Machines (Preview)   <br><br>  SQL Server in Azure Virtual Machines   <br><br>   SAP HANA in Azure Virtual Machines | <ul><li> View Archivable Recovery Points       </li><li>View Recommended Recovery Points (Only for Virtual Machines)    </li><li>Move Archivable Recovery Points    </li><li>Move Recommended Recovery Points (Only for Azure Virtual Machines)    </li><li>View Archived Recovery points    </li><li>Restore from archived recovery points </li></ul> |


## Get started

1. Download/Upgrade AZ CLI version to 2.26.0 or higher 

   1. Follow the [instructions](/cli/azure/install-azure-cli) to install CLI for the first time.
   1. Run az --upgrade to upgrade an already installed version.

2. Log in  using the following command:

   ```azurecli
   az login
   ```

3. Set Subscription Context:

   ```azurecli
   az account set –s <subscriptionId>
   ```
## View archivable recovery points

You can move the archivable recovery points to the vault-archive tier using the following commands. [Learn more](archive-tier-support.md#supported-workloads) about the eligibility criteria.

- **For Azure Virtual Machines**

  ```azurecli
  az backup recoverypoint list -g {rg} -v {vault} -c {container} -i {item} --backup-management-type {AzureIaasVM} --workload-type {VM}  --target-tier {VaultArchive} --is-ready-for-move {True}
  ```

- For SQL Server in Azure Virtual Machines

  ```azurecli
  az backup recoverypoint list -g {rg} -v {vault} -c {container} -i {item} --backup-management-type {AzureWorkload} --workload-type {MSSQL}  --target-tier {VaultArchive} --is-ready-for-move {True}
  ```

- For SAP HANA in Azure Virtual Machines

  ```azurecli
  az backup recoverypoint list -g {rg} -v {vault} -c {container} -i {item} --backup-management-type {AzureWorkload} --workload-type {SAPHANA}  --target-tier {VaultArchive} --is-ready-for-move {True}
  ```

## Check why a recovery point isn't archivable

Run the following command:

```azurecli
az backup recoverypoint list -g {rg} -v {vault} -c {container} -i {item} --backup-management-type {AzureWorkload / AzureIaasVM} --workload-type {MSSQL / SAPHANA / VM}  --query [].{Name:name,move_ready:properties.recoveryPointMoveReadinessInfo.ArchivedRP.isReadyForMove,additional_details: properties.recoveryPointMoveReadinessInfo.ArchivedRP.additionalInfo
```

You will get a list of all recovery points, whether they are archivable and the reason if they are not archivable

## Check recommended set of archivable points (only for Azure VMs)

Run the following command:

```azurecli
az backup recoverypoint list -g {rg} -v {vault} -c {container} -i {item} --backup-management-type { AzureIaasVM} --workload-type {VM} --recommended-for-archive
```

[Learn more](archive-tier-support.md#archive-recommendations-only-for-azure-virtual-machines) about recommendation set.

>[!Note]
>- Cost savings depends on various reasons and might not be the same for every instance.
>- You can ensure cost savings only when all the recovery points contained in the recommendation set is moved to the vault-archive tier.

## Move to archive

You can move archivable recovery points to the vault-archive tier using the following commands. The name parameter in the command should contain the name of an archivable recovery point.

- **For Azure Virtual Machine**

  ```azurecli
  az backup recoverypoint move -g {rg} -v {vault} -c {container} -i {item} --backup-management-type { AzureIaasVM} --workload-type {VM} --source-tier {VaultStandard} --destination-tier {VaultArchive} --name {rp}
  ```
- **For SQL Server in Azure Virtual Machine**

  ```azurecli
  az backup recoverypoint move -g {rg} -v {vault} -c {container} -i {item} --backup-management-type {AzureWorkload} --workload-type {MSSQL} --source-tier {VaultStandard} --destination-tier {VaultArchive} --name {rp}
  ```
- **For SAP HANA in Azure Virtual Machine**

  ```azurecli
  az backup recoverypoint move -g {rg} -v {vault} -c {container} -i {item} --backup-management-type {AzureWorkload} --workload-type {SAPHANA} --source-tier {VaultStandard} --destination-tier {VaultArchive} --name {rp}
  ```

## View archived recovery points

Use the following commands:

- **For Azure Virtual Machines**

    ```azurecli
    az backup recoverypoint list -g {rg} -v {vault} -c {container} -i {item} --backup-management-type {AzureWorkload } --workload-type {VM} -- tier {VaultArchive}
    ```
- **For SQL Server in Azure Virtual Machines**

    ```azurecli
    az backup recoverypoint list -g {rg} -v {vault} -c {container} -i {item} --backup-management-type {AzureWorkload} --workload-type {MSSQL} -- tier {VaultArchive}
    ```
- **For SAP HANA in Azure Virtual Machines**

    ```azurecli
    az backup recoverypoint list -g {rg} -v {vault} -c {container} -i {item} --backup-management-type {AzureWorkload} --workload-type {SAPHANA} -- tier {VaultArchive}
    ```

## Restore 

Run the following commands:

- **For Azure Virtual Machines**

    ```azurecli
    az backup restore restore-disks -g {rg} -v {vault} -c {container} -i {item} --rp-name {rp} --storage-account {storage_account} --rehydration-priority {Standard / High} --rehydration-duration {rehyd_dur}
    ```

- **For SQL Server in Azure VMs/SAP HANA in Azure VMs**

    ```azurecli
    az backup recoveryconfig show --resource-group saphanaResourceGroup \
        --vault-name saphanaVault \
        --container-name VMAppContainer;Compute;saphanaResourceGroup;saphanaVM \
        --item-name saphanadatabase;hxe;hxe \
        --restore-mode AlternateWorkloadRestore \
        --rp-name 7660777527047692711 \
        --target-item-name restored_database \
        --target-server-name hxehost \
        --target-server-type HANAInstance \
        --workload-type SAPHANA \
        --output json


    az backup restore restore-azurewl -g {rg} -v {vault} --recovery-config {recov_config} --rehydration-priority {Standard / High} --rehydration-duration {rehyd_dur}
    ```

::: zone-end



::: zone pivot="client-portaltier"

This article provides the procedure to backup of long-term retention points in the archive tier, and snapshots and the Standard tier using Azure portal.

## Supported workloads

| Workloads | Operations |
| --- | --- |
| Azure Virtual Machine | <ul><li>View Archived Recovery Points    </li><li>Restore for Archived Recovery points   </li><li>View Archive move and Restore Jobs </li></ul> |
| SQL Server in Azure Virtual Machine/ <br> SAP HANA in Azure Virtual Machines | <ul><li>View Archived Recovery Points    </li><li>Move all archivable recovery to archive   </li><li>Restore from Archived recovery points   </li><li>View Archive move and Restore jobs</li></ul> |

## View archived recovery points

You can now view all the recovery points that have are moved to archive.

:::image type="content" source="./media/use-archive-tier-support/view-recovery-points-list-inline.png" alt-text="Screenshot showing the list of recovery points." lightbox="./media/use-archive-tier-support/view-recovery-points-list-expanded.png":::


## Move archivable recovery points for a particular SQL/SAP HANA database

You can now move all recovery points for a particular SQL/SAP HANA database at one go.

Follow these steps:

1. Select the backup Item (database in SQL Server or SAP HANA in Azure VM) whose recovery points you want to move to the vault-archive tier.

2. Select **click here** to view recovery points that are older than 7 days.

   :::image type="content" source="./media/use-archive-tier-support/view-old-recovery-points-inline.png" alt-text="Screenshot showing the process to view recovery points that are older than 7 days." lightbox="./media/use-archive-tier-support/view-old-recovery-points-expanded.png":::

3. To view all eligible archivable points to be moved to archive, select _Long term retention points can be moved to archive. To move all ‘eligible recovery points’ to archive tier, click here_.

   :::image type="content" source="./media/use-archive-tier-support/view-all-eligible-archivable-points-for-move-inline.png" alt-text="Screenshot showing the process to view all eligible archivable points to be moved to archive." lightbox="./media/use-archive-tier-support/view-all-eligible-archivable-points-for-move-expanded.png":::

   All archivable recovery points appear.


   [Learn more](archive-tier-support.md#supported-workloads) about eligibility criteria.

3. Click **Move Recovery Points to archive** to move all recovery points to the vault-archive tier.

   :::image type="content" source="./media/use-archive-tier-support/move-all-recovery-points-to-vault-inline.png" alt-text="Screenshot showing the option to start the move process of all recovery points to the vault-archive tier." lightbox="./media/use-archive-tier-support/move-all-recovery-points-to-vault-expanded.png":::

   >[!Note]
   >This option moves all the archivable recovery points to vault-archive.

You can monitor the progress in backup jobs.

## Restore

To restore the recovery points that are moved to archive, you need to add the required parameters for rehydration duration and rehydration priority.

:::image type="content" source="./media/use-archive-tier-support/restore-in-portal.png" alt-text="Screenshot showing the process to restore recovery points in the portal.":::

## View jobs

:::image type="content" source="./media/use-archive-tier-support/view-jobs-portal.png" alt-text="Screenshot showing the process to view jobs in the portal.":::

## View Archive Usage in Vault Dashboard

You can also view the archive usage in the vault dashboard.

:::image type="content" source="./media/use-archive-tier-support/view-archive-usage-in-vault-dashboard.png" alt-text="Screenshot showing the archive usage in the vault dashboard.":::


::: zone-end

## Next steps

- [Troubleshoot Archive tier errors](troubleshoot-archive-tier.md)
