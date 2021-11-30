---
title: What's new in Azure Backup
description: Learn about new features in Azure Backup.
ms.topic: conceptual
ms.date: 11/25/2021
author: v-amallick
ms.service: backup
ms.author: v-amallick
---

# What's new in Azure Backup

Azure Backup is constantly improving and releasing new features that enhance the protection of your data in Azure. These new features expand your data protection to new workload types, enhance security, and improve the availability of your backup data. They also add new management, monitoring, and automation capabilities.

You can learn more about the new releases by bookmarking this page or by [subscribing to updates here](https://azure.microsoft.com/updates/?query=backup).

## Updates summary

- October 2021
  - [Multi-user authorization using Resource Guard (in preview)](#multi-user-authorization-using-resource-guard-in-preview)
  - [Multiple backups per day for Azure Files (in preview)](#multiple-backups-per-day-for-azure-files-in-preview)
  - [Azure Backup Metrics and Metrics Alerts (in preview)](#azure-backup-metrics-and-metrics-alerts-in-preview)
- July 2021
  - [Archive Tier support for SQL Server in Azure VM for Azure Backup is now generally available](#archive-tier-support-for-sql-server-in-azure-vm-for-azure-backup-is-now-generally-available)
- May 2021
  - [Backup for Azure Blobs is now generally available](#backup-for-azure-blobs-is-now-generally-available)
- April 2021
  - [Enhancements to encryption using customer-managed keys for Azure Backup (in preview)](#enhancements-to-encryption-using-customer-managed-keys-for-azure-backup-in-preview)
- March 2021
  - [Azure Disk Backup is now generally available](#azure-disk-backup-is-now-generally-available)
  - [Backup center is now generally available](#backup-center-is-now-generally-available)
  - [Archive Tier support for Azure Backup (in preview)](#archive-tier-support-for-azure-backup-in-preview)
- February 2021
  - [Backup for Azure Blobs (in preview)](#backup-for-azure-blobs-in-preview)
- January 2021
  - [Azure Disk Backup (in preview)](#azure-disk-backup-in-preview)
  - [Encryption at rest using customer-managed keys (general availability)](#encryption-at-rest-using-customer-managed-keys)
- November 2020
  - [Azure Resource Manager template for Azure file share (AFS) backup](#azure-resource-manager-template-for-afs-backup)
  - [Incremental backups for SAP HANA databases on Azure VMs (in preview)](#incremental-backups-for-sap-hana-databases-in-preview)
- September 2020
  - [Backup Center (in preview)](#backup-center-in-preview)
  - [Back up Azure Database for PostgreSQL (in preview)](#back-up-azure-database-for-postgresql-in-preview)
  - [Selective disk backup and restore](#selective-disk-backup-and-restore)
  - [Cross Region Restore for SQL Server and SAP HANA databases on Azure VMs (in preview)](#cross-region-restore-for-sql-server-and-sap-hana-in-preview)
  - [Support for backup of VMs with up to 32 disks (general availability)](#support-for-backup-of-vms-with-up-to-32-disks)
  - [Simplified backup configuration experience for SQL in Azure VMs](#simpler-backup-configuration-for-sql-in-azure-vms)
  - [Back up SAP HANA in RHEL Azure Virtual Machines (in preview)](#back-up-sap-hana-in-rhel-azure-virtual-machines-in-preview)
  - [Zone redundant storage (ZRS) for backup data (in preview)](#zone-redundant-storage-zrs-for-backup-data-in-preview)
  - [Soft delete for SQL Server and SAP HANA workloads in Azure VMs](#soft-delete-for-sql-server-and-sap-hana-workloads)

## Multi-user authorization using Resource Guard (in preview)

Azure Backup now supports multi-user authorization (MUA) that allows you to add an additional layer of protection to critical operations on your Recovery Services vaults. For MUA, Azure Backup uses the Azure resource, Resource Guard, to ensure critical operations are performed only with applicable authorization.

For more details, see [how to protect Recovery Services vault and manage critical operations with MUA](/azure/backup/multi-user-authorization).

## Multiple backups per day for Azure Files (in preview)

Low RPO (Recovery Point Objective) is a key requirement for Azure Files that contains the frequently updated, business-critical data. To ensure minimal data loss in the event of a disaster or unwanted changes to file share content, you may prefer to take backups more frequently than once a day.

Using Azure Backup you can now  create a backup policy or modify an existing backup policy to take multiple snapshots in a  day. With this capability, you can also define the duration in which your backup jobs would trigger. This capability empowers you to align your backup schedule with the working hours when there are frequent updates to Azure Files content.

For more details, see [how to configure multiple backups per day via backup policy](./manage-afs-backup.md#create-a-new-policy).

## Azure Backup metrics and metrics alerts (in preview)

Azure Backup now provides a set of built-in metrics via [Azure Monitor](../azure-monitor/essentials/data-platform-metrics.md) that allows you to monitor the health of your backups. You can also configure alert rules that trigger alerts when metrics exceed the defined thresholds.

Azure Backup offers the following key capabilities:
 
- Ability to view out-of-the-box metrics related to the backup and restore health of your backup items along with associated trends.
- Ability to write custom alert rules on these metrics to efficiently monitor the health of your backup items.
- Ability to route fired metric alerts to various notification channels that Azure Monitor supports, such as email, ITSM, webhook, logic apps, and so on.
 
Currently, Azure Backup supports built-in metrics for the following workload types:

- Azure VM
- SQL databases in Azure VM
- SAP HANA databases in Azure VM
- Azure Files.

For more details, see [Monitor the health of your backups using Azure Backup Metrics (preview)](metrics-overview.md).

## Archive Tier support for SQL Server in Azure VM for Azure Backup is now generally available

Azure Backup allows you to move your long-term retention points for Azure Virtual Machines and SQL Server in Azure Virtual Machines to the low-cost Archive Tier. You can also restore from the recovery points in the Vault-archive tier.

In addition to the capability to move the recovery points:

- Azure Backup provides recommendations to move a specific set of recovery points for Azure Virtual Machine backups that'll ensure cost savings.
- You have the capability to move all their recovery points for a particular backup item at one go using sample scripts.
- You can view Archive storage usage on the Vault dashboard.

For more information, see [Archive Tier support](./archive-tier-support.md).

## Backup for Azure Blobs is now generally available

Operational backup for Azure Blobs is a managed-data protection solution that lets you protect your block blob data from various data loss scenarios, such as blob corruptions, blob deletions, and accidental deletion of storage accounts.

Being an operational backup solution, the backup data is stored locally in the source storage account, and can be recovered from a selected point-in-time, giving you a simple and cost-effective means to protect your blob data. To do this, the solution uses the blob point-in-time restore capability available from blob storage.

Operational backup for blobs integrates with the Azure Backup management tools, including Backup Center, to help you manage the protection of your blob data effectively and at-scale. In addition to previously available capabilities, you can now configure and manage operational backup for blobs using the **Data protection** view of the storage accounts, also  [through PowerShell](backup-blobs-storage-account-ps.md). Also, Backup now gives you an enhanced experience for managing role assignments required for configuring operational backup.

For more information, see [Overview of operational backup for Azure Blobs](blob-backup-overview.md).

## Azure Disk Backup is now generally available

Azure Backup offers snapshot lifecycle management to Azure Managed Disks by automating periodic creation of snapshots and retaining these for configured durations using Backup policy.

For more information, see [Overview of Azure Disk Backup](disk-backup-overview.md).

## Backup center is now generally available

Backup center simplifies data protection management at-scale by enabling you to discover, govern, monitor, operate, and optimize backup management from one single central console.

For more information, see [Overview of Backup Center](backup-center-overview.md).

## Archive Tier support for Azure Backup (in preview)

Azure Backup now allows you to reduce the cost of long-term retention backups with the availability of Archive Tier for Azure virtual machines and SQL Server in Azure virtual machines.

For more information, see [Archive Tier support (Preview)](archive-tier-support.md).

## Backup for Azure Blobs (in preview)

Operational backup for Blobs is a managed, local data protection solution that lets you protect your block blobs from various data loss scenarios like corruptions, blob deletions, and accidental storage account deletion. The data is stored locally within the source storage account itself and can be recovered to a selected point in time whenever needed. So it provides a simple, secure, and cost-effective means to protect your blobs.

Operational backup for Blobs integrates with Backup Center, among other Backup management capabilities, to provide a single pane of glass that can help you govern, monitor, operate, and analyze backups at scale.

For more information, see [Overview of operational backup for Azure Blobs (in preview)](blob-backup-overview.md).

## Azure Disk Backup (in preview)

Azure Disk Backup offers a turnkey solution that provides snapshot lifecycle management for [Azure Managed Disks](../virtual-machines/managed-disks-overview.md) by automating periodic creation of snapshots and retaining it for a configured duration using backup policy. You can manage the disk snapshots with zero infrastructure cost and without the need for custom scripting or any management overhead. This is a crash-consistent backup solution that takes point-in-time backup of a managed disk using [incremental snapshots](../virtual-machines/disks-incremental-snapshots.md) with support for multiple backups per day. It's also an agent-less solution and doesn't impact production application performance. It supports backup and restore of both OS and data disks (including shared disks), whether or not they're currently attached to a running Azure virtual machine.

For more information, see [Azure Disk Backup (in preview)](disk-backup-overview.md).

## Encryption at rest using customer-managed keys

Support for encryption at rest using customer-managed keys is now generally available. This gives you the ability to encrypt the backup data in your Recovery Services vaults using your own keys stored in Azure Key Vaults. The encryption key used for encrypting backups in the Recovery Services vault may be different from the ones used for encrypting the source. The data is protected using an AES 256 based data encryption key (DEK), which is, in turn, protected using your keys stored in the Key Vault. Compared to encryption using platform-managed keys (which is available by default), this gives you more control over your keys and can help you better meet your compliance needs.

For more information, see [Encryption of backup data using customer-managed keys](encryption-at-rest-with-cmk.md).

## Azure Resource Manager template for AFS backup

Azure Backup now supports configuring backup for existing Azure file shares using an Azure Resource Manager (ARM) template. The template configures protection for an existing Azure file share by specifying appropriate details for the Recovery Services vault and backup policy. It optionally creates a new Recovery Services vault and backup policy, and registers the storage account containing the file share to the Recovery Services vault.

For more information, see [Azure Resource Manager templates for Azure Backup](backup-rm-template-samples.md).

## Incremental backups for SAP HANA databases (in preview)

Azure Backup now supports incremental backups for SAP HANA databases hosted on Azure VMs. This allows for faster and more cost-efficient backups of your SAP HANA data.

For more information, see [various options available during creation of a backup policy](./sap-hana-faq-backup-azure-vm.yml) and [how to create a backup policy for SAP HANA databases](tutorial-backup-sap-hana-db.md#creating-a-backup-policy).

## Backup Center (in preview)

Azure Backup has enabled a new native management capability to manage your entire backup estate from a central console. Backup Center provides you with the capability to monitor, operate, govern, and optimize data protection at scale in a unified manner consistent with Azure’s native management experiences.

With Backup Center, you get an aggregated view of your inventory across subscriptions, locations, resource groups, vaults, and even tenants using Azure Lighthouse. Backup Center is also an action center from where you can trigger your backup related activities, such as configuring backup, restore, creation of policies or vaults, all from a single place. In addition, with seamless integration to Azure Policy, you can now govern your environment and track compliance from a backup perspective. In-built Azure Policies specific to Azure Backup also allow you to configure backups at scale.

For more information, see [Overview of Backup Center](backup-center-overview.md).

## Back up Azure Database for PostgreSQL (in preview)

Azure Backup and Azure Database Services have come together to build an enterprise-class backup solution for Azure PostgreSQL (now in preview). Now you can meet your data protection and compliance needs with a customer-controlled backup policy that enables retention of backups for up to 10 years. With this, you have granular control to manage the backup and restore operations at the individual database level. Likewise, you can restore across PostgreSQL versions or to blob storage with ease.

For more information, see [Azure Database for PostgreSQL backup](backup-azure-database-postgresql.md).

## Selective disk backup and restore

Azure Backup supports backing up all the disks (operating system and data) in a VM together using the virtual machine backup solution. Now, using the selective disks backup and restore functionality, you can back up a subset of the data disks in a VM. This provides an efficient and cost-effective solution for your backup and restore needs. Each recovery point contains only the disks that are included in the backup operation.

For more information, see [Selective disk backup and restore for Azure virtual machines](selective-disk-backup-restore.md).

## Cross Region Restore for SQL Server and SAP HANA (in preview)

With the introduction of cross-region restore, you can now initiate restores in a secondary region at will to mitigate real downtime issues in a primary region for your environment. This makes the secondary region restores completely customer controlled. Azure Backup uses the backed-up data replicated to the secondary region for such restores.

Now, in addition to support for cross-region restore for Azure virtual machines, the feature has been extended to restoring SQL and SAP HANA databases in Azure virtual machines as well.

For more information, see [Cross Region Restore for SQL databases](restore-sql-database-azure-vm.md#cross-region-restore) and [Cross Region Restore for SAP HANA databases](sap-hana-db-restore.md#cross-region-restore).

## Support for backup of VMs with up to 32 disks

Until now, Azure Backup has supported 16 managed disks per VM. Now, Azure Backup supports backup of up to 32 managed disks per VM.

For more information, see the [VM storage support matrix](backup-support-matrix-iaas.md#vm-storage-support).

## Simpler backup configuration for SQL in Azure VMs

Configuring backups for your SQL Server in Azure VMs is now even easier with inline backup configuration integrated into the VM pane of the Azure portal. In just a few steps, you can enable backup of your SQL Server to protect all the existing databases as well as the ones that get added in the future.

For more information, see [Back up a SQL Server from the VM pane](backup-sql-server-vm-from-vm-pane.md).

## Back up SAP HANA in RHEL Azure virtual machines (in preview)

Azure Backup is the native backup solution for Azure and is BackInt certified by SAP. Azure Backup has now added support for Red Hat Enterprise Linux (RHEL), one of the most widely used Linux operating systems running SAP HANA.

For more information, see the [SAP HANA database backup scenario support matrix](sap-hana-backup-support-matrix.md#scenario-support).

## Zone redundant storage (ZRS) for backup data (in preview)

Azure Storage provides a great balance of high performance, high availability, and high data resiliency with its varied redundancy options. Azure Backup allows you to extend these benefits to the backup data as well, with options to store your backups in locally redundant storage (LRS) and geo-redundant storage (GRS). Now, there are additional durability options with the added support for zone redundant storage (ZRS).

For more information, see [Set storage redundancy for the Recovery Services vault](backup-create-rs-vault.md#set-storage-redundancy).

## Soft delete for SQL Server and SAP HANA workloads

Concerns about security issues, like malware, ransomware, and intrusion, are increasing. These security issues can be costly, in terms of both money and data. To guard against such attacks, Azure Backup provides security features to help protect backup data even after deletion.

One such feature is soft delete. With soft delete, even if a malicious actor deletes a backup (or backup data is accidentally deleted), the backup data is retained for 14 additional days, allowing the recovery of that backup item with no data loss. The additional 14 days of retention for backup data in the "soft delete" state don't incur any cost to you.

Now, in addition to soft delete support for Azure VMs, SQL Server and SAP HANA workloads in Azure VMs are also protected with soft delete.

For more information, see [Soft delete for SQL server in Azure VM and SAP HANA in Azure VM workloads](soft-delete-sql-saphana-in-azure-vm.md).

## Enhancements to encryption using customer-managed keys for Azure Backup (in preview)

Azure Backup now provides enhanced capabilities (in preview) to manage encryption with customer-managed keys. Azure Backup allows you to bring in your own keys to encrypt the backup data in the Recovery Services vaults, thus providing you a better control.

- Supports user-assigned managed identities to grant permissions to the keys to manage data encryption in the Recovery Services vault.
- Enables encryption with customer-managed keys while creating a Recovery Services vault.
  >[!NOTE]
  >This feature is currently in limited preview. To sign up, fill [this form](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR0H3_nezt2RNkpBCUTbWEapURDNTVVhGOUxXSVBZMEwxUU5FNDkyQkU4Ny4u), and write to us at [AskAzureBackupTeam@microsoft.com](mailto:AskAzureBackupTeam@microsoft.com).
- Allows you to use Azure Policies to audit and enforce encryption using customer-managed keys.
>[!NOTE]
>- The above capabilities are supported through the Azure portal only, PowerShell is currently not supported.<br>If you are using PowerShell for managing encryption keys for Backup, we do not recommend to update the keys from the portal.<br>If you update the key from the portal, you can’t use PowerShell to update the encryption key further, till a PowerShell update to support the new model is available. However, you can continue updating the key from the Azure portal.
>- You can use the audit policy for auditing vaults with encryption using customer-managed keys that are enabled after 04/01/2021.  
>- For vaults with the CMK encryption enabled before this date, the policy might fail to apply, or might show false negative results (that is, these vaults may be reported as non-compliant, despite having CMK encryption enabled). [Learn more](encryption-at-rest-with-cmk.md#using-azure-policies-for-auditing-and-enforcing-encryption-utilizing-customer-managed-keys-in-preview).

For more information, see [Encryption for Azure Backup using customer-managed keys](encryption-at-rest-with-cmk.md). 

## Next steps

- [Azure Backup guidance and best practices](guidance-best-practices.md)