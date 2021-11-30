---
title: Add Contributor role on the Media Services
description: This topic explains how to add contributor role on the Media Services.
ms.author: itnorman
ms.topic: how-to
ms.date: 10/13/2021
ms.custom: ignite-fall-2021
---

# Add contributor role on the Media Services

This article describes how to assign contributor role on the Media Services.

> [!NOTE]
> If you are creating your Azure Video Analyzer for Media through the Azure portal UI, the selected Managed identity will be automatically assigned with a contributor permission on the selected Media Service account.

## Prerequisites

1. Azure Media Services (AMS)
2. User-assigned managed identity
> [!NOTE]
> You'll need an Azure subscription where you have access to both the [Contributor][docs-role-contributor] role and the [User Access Administrator][docs-role-administrator] role to the Azure Media Services and the User-assigned managed identity. If you don't have the right permissions, ask your account administrator to grant you those permissions. The associated Azure Media Services must be in the same region as the Video Analyzer for Media account.


## Add Contributor role on the Media Services
### [Azure Portal](#tab/portal/)

### Add Contributor role on the Media Services in the Azure portal

1. Sign in at the [Azure portal](https://portal.azure.com/).
    * Using the search bar at the top, enter **Media Services**.
    * Find and select your Media Service resource.
1. In the pane to the left, click **Access control (IAM)**.
    * Click **Add** > **Add role assignment**. If you don't have permissions to assign roles, the **Add role assignment** option will be disabled.
1. In the Role list, select [Contributor][docs-role-contributor] role and click **Next**.
1. In the **Assign access to**, select *Managed identity* radio button.
    * Click **+Select members** button and **Select managed identities** pane should be pop up.
1. **Select** the following:
    * In the **Subscription**, the subscription where the managed identity is located.
    * In the **Managed identity**, select *User-assigned managed identity*.
    * In the **Select** section, search for the Managed identity you'd like to grant contributor permissions on the Media services resource.    
1. Once you have found the security principal, click to select it.
1. To assign the role, click **Review + assign**

<!-- links -->
[docs-role-contributor]: ../../role-based-access-control/built-in-roles.md#contributor
[docs-role-administrator]: ../../role-based-access-control/built-in-roles.md#user-access-administrator
