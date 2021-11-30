---
title: Grant and request tenant-wide permissions in Microsoft Defender for Cloud
description: Learn how to manage tenant-wide permissions in Microsoft Defender for Cloud
ms.topic: how-to
ms.date: 11/09/2021
---

# Grant and request tenant-wide visibility

[!INCLUDE [Banner for top of topics](./includes/banner.md)]

A user with the Azure Active Directory (AD) role of **Global Administrator** might have tenant-wide responsibilities, but lack the Azure permissions to view that organization-wide information in Microsoft Defender for Cloud. Permission elevation is required because Azure AD role assignments don't grant access to Azure resources. 

## Grant tenant-wide permissions to yourself

To assign yourself tenant-level permissions:

1. If your organization manages resource access with [Azure AD Privileged Identity Management (PIM)](../active-directory/privileged-identity-management/pim-configure.md), or any other PIM tool, the global administrator role must be active for the user following the procedure below.

1. As a Global Administrator user without an assignment on the root management group of the tenant, open Defender for Cloud's **Overview** page and select the **tenant-wide visibility** link in the banner. 

    :::image type="content" source="media/management-groups-roles/enable-tenant-level-permissions-banner.png" alt-text="Enable tenant-level permissions in Microsoft Defender for Cloud.":::

1. Select the new Azure role to be assigned. 

    :::image type="content" source="media/management-groups-roles/enable-tenant-level-permissions-form.png" alt-text="Form for defining the tenant-level permissions to be assigned to your user.":::

    > [!TIP]
    > Generally, the Security Admin role is required to apply policies on the root level, while Security Reader will suffice to provide tenant-level visibility. For more information about the permissions granted by these roles, see the [Security Admin built-in role description](../role-based-access-control/built-in-roles.md#security-admin) or the [Security Reader built-in role description](../role-based-access-control/built-in-roles.md#security-reader).
    >
    > For differences between these roles specific to Defender for Cloud, see the table in [Roles and allowed actions](permissions.md#roles-and-allowed-actions).

    The organizational-wide view is achieved by granting roles on the root management group level of the tenant.  

1. Log out of the Azure portal, and then log back in again.

1. Once you have elevated access, open or refresh Microsoft Defender for Cloud to verify you have visibility into all subscriptions under your Azure AD tenant. 

The simple process above performs a number of operations automatically for you:

1. The user's permissions are temporarily elevated.
1. Using the new permissions, the user is assigned to the desired Azure RBAC role on the root management group.
1. The elevated permissions are removed.

For more details of the Azure AD elevation process, see [Elevate access to manage all Azure subscriptions and management groups](../role-based-access-control/elevate-access-global-admin.md).


## Request tenant-wide permissions when yours are insufficient

If you login to Defender for Cloud and see a banner telling you that your view is limited, you can click through to send a request to the global administrator for your organization. In the request, you can include the role you'd like to be assigned and the global administrator will make a decision about which role to grant. 

It's the global administrator's decision whether to accept or reject these requests. 

> [!IMPORTANT]
> You can only submit one request every seven days.

To request elevated permissions from your global administrator:

1. From the Azure portal, open Microsoft Defender for Cloud.

1. If you see the banner "You're seeing limited information." select it.

    :::image type="content" source="media/management-groups-roles/request-tenant-permissions.png" alt-text="Banner informing a user they can request tenant-wide permissions.":::

1. In the detailed request form, select the desired role and the justification for why you need these permissions.

    :::image type="content" source="media/management-groups-roles/request-tenant-permissions-details.png" alt-text="Details page for requesting tenant-wide permissions from your Azure global administrator.":::

1. Select **Request access**.

    An email is sent to the global administrator. The email contains a link to Defender for Cloud where they can approve or reject the request.

    :::image type="content" source="media/management-groups-roles/request-tenant-permissions-email.png" alt-text="Email to the global administrator for new permissions.":::

    After the global administrator selects **Review the request** and completes the process, the decision is emailed to the requesting user. 

## Next steps

Learn more about Defender for Cloud permissions in the following related page:

- [Permissions in Microsoft Defender for Cloud](permissions.md)
