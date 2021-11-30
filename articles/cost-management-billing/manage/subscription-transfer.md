---
title: Azure subscription and reservation transfer hub
description: This article helps you understand what's needed to transfer Azure subscriptions and provides links to other articles for more detailed information.
author: bandersmsft
ms.reviewer: andalmia
tags: billing
ms.service: cost-management-billing
ms.subservice: billing
ms.topic: conceptual
ms.date: 11/17/2021
ms.author: banders
ms.custom:
---

# Azure subscription and reservation transfer hub

This article describes the types of supported transfers for Azure subscriptions and Azure reservations, referred to as _products_. It also helps you understand what's needed to transfer Azure products between different billing agreements and provides links to other articles for more detailed information about specific transfers. Azure products are created upon different Azure agreement types and a transfer from a source agreement type to another varies depending on the source and destination agreement types. Azure product transfers can be an automatic or a manual process, depending on the source and destination agreement type. If it's a manual process, the agreement types determine how much manual effort is needed.

> [!NOTE]
> There are many types of Azure products, however not every product can be transferred from one type to another. Only supported product transfers are documented in this article. If you need help with a situation that isn't addressed in this article, you can create an [Azure support request](https://go.microsoft.com/fwlink/?linkid=2083458) for assistance.

This article also helps you understand the things you should know _before_ you transfer billing ownership of an Azure product to another account. You might want to transfer billing ownership of your Azure product if you're leaving your organization, or you want your product to be billed to another account. Transferring billing ownership to another account provides the administrators in the new account permission for billing tasks. They can change the payment method, view charges, and cancel the product.

If you want to keep the billing ownership but change the type of product, see [Switch your Azure subscription to another offer](switch-azure-offer.md). To control who can access resources in the product, see [Azure built-in roles](../../role-based-access-control/built-in-roles.md).

If you're an Enterprise Agreement (EA) customer, your enterprise administrators can transfer billing ownership of your products between accounts in the EA portal. For more information, see [Change Azure subscription or account ownership](ea-portal-administration.md#change-azure-subscription-or-account-ownership).

This article focuses on product transfers. However, resource transfer is also discussed because it's required for some product transfer scenarios.

For more information about product transfers between different Azure AD tenants, see [Transfer an Azure subscription to a different Azure AD directory](../../role-based-access-control/transfer-subscription.md).

> [!NOTE]
> Most billing ownership transfers don't change the service tenant of the underlying products. They don't cause any downtime. However, even when a billing tenant does change, the change doesn't affect running services or resources.

## Product transfer planning

As you begin to plan your product transfer, consider the information needed to answer to the following questions:

- Why is the product transfer required?
- What's the wanted timeline for the product transfer?
- What's the product's current offer type and what do you want to transfer it to?
  - Microsoft Online Service Program (MOSP), also known as Pay-As-You-Go (PAYG)
  - Previous Azure offer in CSP
  - New Azure offer in CSP, also referred to as Azure Plan with a Microsoft Partner Agreement (MPA)
  - Enterprise Agreement (EA)
  - Microsoft Customer Agreement (MCA) in the Enterprise motion when you buy Azure services through a Microsoft representative and individual MCA when you buy Azure services through Azure.com
  - Others like MSDN, BizSpark, EOPEN, Azure Pass, and Free Trial
- Do you have the required permissions on the product to accomplish a transfer? Specific permission needed for each transfer type is listed in the following product transfer support table.
  - Only the billing administrator of an account can transfer subscription ownership.
  - Only a billing administrator owner can transfer reservation ownership.
- Are there existing subscriptions that benefit from reservations and will the reservations need to be transferred with the subscription?

You should have an answer for each question before you continue with any transfer.

Answers to the above questions can help you to communicate early with others to set expectations and timelines. Product transfer effort varies greatly, but a transfer is likely to take longer than expected.

Answers for the source and destination offer type questions help define technical paths that you'll need to follow and identify limitations that a transfer combination might have. Limitations are covered in more detail in the next section.

## Product transfer support

The following table describes product transfer support between the different agreement types. Links are provided for more information about each type of transfer.

Currently transfer isn't supported for [Free Trial](https://azure.microsoft.com/offers/ms-azr-0044p/) or [Azure in Open (AIO)](https://azure.microsoft.com/offers/ms-azr-0111p/) products. For a workaround, see [Move resources to new resource group or subscription](../../azure-resource-manager/management/move-resource-group-and-subscription.md).

Support plans can't be transferred. If you have a support plan, you should cancel it for the old agreement and then buy a new one for the new agreement.

Dev/Test products aren't shown in the following table. Transfers for Dev/Test products are handled in the same way as other product types. For example, an EA Dev/Test product transfer is handled in the way an EA product transfer.

> [!NOTE]
> Reservations transfer with most supported product transfers. However, there are some transfers where reservations won't transfer, as noted in the following table.

| Source (current) product agreement type | Destination (future) product agreement type | Notes |
| --- | --- | --- |
| EA | MOSP (PAYG) | <ul><li>Transfer from an EA enrollment to a MOSP subscription requires a [billing support ticket](https://azure.microsoft.com/support/create-ticket/). <li> Reservations don't automatically transfer and transferring them isn't supported. |
| EA | MCA - individual | <ul><li>For details, see [Transfer Azure subscription billing ownership for a Microsoft Customer Agreement](mca-request-billing-ownership.md). <li> Reservations don't automatically transfer so you must open a [billing support ticket](https://azure.microsoft.com/support/create-ticket/) to transfer them. |
| EA | EA | <ul><li>Transferring between EA enrollments requires a [billing support ticket](https://azure.microsoft.com/support/create-ticket/). <li>Reservations don't automatically transfer between enrollments so you must open a [billing support ticket](https://azure.microsoft.com/support/create-ticket/) to transfer them. <li> Transfer within the same enrollment is the same action as changing the account owner. For details, see [Change EA subscription or account ownership](ea-portal-administration.md#change-azure-subscription-or-account-ownership). |
| EA | MCA - Enterprise | <ul><li> Transferring all enrollment products is completed as part of the MCA transition process from an EA. For more information, see [Complete Enterprise Agreement tasks in your billing account for a Microsoft Customer Agreement](mca-enterprise-operations.md). <li> If you want to transfer specific products, not all of the products in an enrollment, see [Transfer Azure subscription billing ownership for a Microsoft Customer Agreement](mca-request-billing-ownership.md). |
| EA | MPA | <ul><li> Only CSP direct bill partners certified as an [Azure Expert Managed Services Provider (MSP)](https://partner.microsoft.com/membership/azure-expert-msp) can request to transfer Azure products for their customers that have a Direct Enterprise Agreement (EA). For more information, see [Get billing ownership of Azure subscriptions to your MPA account](mpa-request-ownership.md). Product transfers are allowed only for customers who have accepted a Microsoft Customer Agreement (MCA) and purchased an Azure plan with the CSP Program. <li> There are limitations and restrictions. For more information, see [Transfer EA subscriptions to a CSP partner](transfer-subscriptions-subscribers-csp.md#transfer-ea-subscriptions-to-a-csp-partner).  |
| MCA - individual | MOSP (PAYG) | <ul><li> For details, see [Transfer billing ownership of an Azure subscription to another account](billing-subscription-transfer.md). <li> Reservations don't automatically transfer and transferring them isn't supported. |
| MCA - individual | MCA - individual | <ul><li>For details, see [Transfer Azure subscription billing ownership for a Microsoft Customer Agreement](mca-request-billing-ownership.md). <li> Self-service reservation transfers are supported. |
| MCA - individual | EA | <ul><li> For details, see [Transfer a subscription to an EA](mosp-ea-transfer.md#transfer-the-subscription-to-the-ea). <li> Self-service reservation transfers are supported. |
| MCA - individual | MCA - Enterprise | <ul><li> For details, see [Transfer Azure subscription billing ownership for a Microsoft Customer Agreement](mca-request-billing-ownership.md).<li> Self-service reservation transfers are supported. |
| MCA - Enterprise | MOSP | <ul><li> Requires a [billing support ticket](https://azure.microsoft.com/support/create-ticket/). <li> Reservations don't automatically transfer and transferring them isn't supported. |
| MCA - Enterprise | MCA - individual | <ul><li> For details, see [Transfer Azure subscription billing ownership for a Microsoft Customer Agreement](mca-request-billing-ownership.md). <li> Reservations don't automatically transfer so you must open a [billing support ticket](https://azure.microsoft.com/support/create-ticket/) to transfer them. |
| MCA - Enterprise | MCA - Enterprise | <ul><li> For details, see [Transfer Azure subscription billing ownership for a Microsoft Customer Agreement](mca-request-billing-ownership.md). <li> Reservations don't automatically transfer so you must open a [billing support ticket](https://azure.microsoft.com/support/create-ticket/) to transfer them.  |
| Previous Azure offer in CSP | Previous Azure offer in CSP | <ul><li> Requires a [billing support ticket](https://azure.microsoft.com/support/create-ticket/). <li> Reservations don't automatically transfer and transferring them isn't supported. |
| Previous Azure offer in CSP | MPA | For details, see [Transfer a customer's Azure subscriptions to a different CSP (under an Azure plan)](/partner-center/transfer-azure-subscriptions-under-azure-plan). |
| MPA | EA | <ul><li> Automatic transfer isn't supported. Any transfer requires resources to move from the existing MPA product manually to a newly created or an existing EA product. <li> Use the information in the [Perform resource transfers](#perform-resource-transfers) section. <li> Reservations don't automatically transfer and transferring them isn't supported. |
| MPA | MPA | <ul><li> For details, see [Transfer a customer's Azure subscriptions to a different CSP (under an Azure plan)](/partner-center/transfer-azure-subscriptions-under-azure-plan). <li> Reservations don't automatically transfer and transferring them isn't supported. |
| MOSP (PAYG) | MOSP (PAYG) | <ul><li> If you're changing the billing owner of the subscription, see [Transfer billing ownership of an Azure subscription to another account](billing-subscription-transfer.md). <li> Reservations don't automatically transfer so you must open a [billing support ticket](https://azure.microsoft.com/support/create-ticket/) to transfer them.  |
| MOSP (PAYG) | MCA - individual | <ul><li> For details, see [Transfer Azure subscription billing ownership for a Microsoft Customer Agreement](mca-request-billing-ownership.md). <li> Self-service reservation transfers are supported. |
| MOSP (PAYG) | EA | For details, see [Transfer a subscription to an EA](mosp-ea-transfer.md#transfer-the-subscription-to-the-ea). |
| MOSP (PAYG) | MCA - Enterprise | <ul><li> For details, see [Transfer Azure subscription billing ownership for a Microsoft Customer Agreement](mca-request-billing-ownership.md). <li> Self-service reservation transfers are supported. |

## Perform resource transfers

Some product transfers require you to manually move Azure resources between subscription. Moving resources can incur downtime and there are various limitations to move Azure resource types such as VMs, NSGs, App Services, and others.

Microsoft doesn't provide a tool to automatically move resources between subscriptions. When needed, you must manually move Azure resources between subscriptions. For details, see [Move resources to a new resource group or subscription](../../azure-resource-manager/management/move-resource-group-and-subscription.md). Extra time and planning are needed when you have a large number of resources to move.

## Other planning considerations

Read the following sections to learn more about other considerations before you start a product transfer.

### Transfer terms and conditions

When you send or accept a transfer you agree to terms and conditions. The following information provides additional details.

#### Send transfer

When you send a transfer request, must select the **Send transfer request** option. By making the selection you also agree to the following terms and conditions:

_By sending this transfer request, you acknowledge and agree that the selected items will transfer to your account as of the Transition Date (date when the transfer completed successfully). You will be responsible to Microsoft for all ongoing, scheduled billings related to the transfer items as of the Transition Date; provided that Microsoft will move any prepaid subscriptions (including reserved instances) to your account. You agree that you may not cancel any prepaid subscriptions transferred to your account._

#### Transfer acceptance

When you accept a transfer, must select the **Review + validate** option. By making the selection you also agree to the following terms and conditions:

_By accepting this transfer request, you acknowledge and agree that the indicated items will transfer to the nominated destination account as of the Transition Date (date when the transfer completed successfully). Any prepaid subscriptions, if selected, (including reserved instances) will be moved to the destination account and, as of the Transition Date, you will no longer be responsible to Microsoft for ongoing payment obligations (if any) related to the transfer items._

### Resources transfer with subscriptions

When only billing ownership is changing, then resources aren't affected. However, when you do a resource move or change the service tenant, then resources could be affected.

### Transfer a product from one account to another

If you're an administrator of two accounts, you can transfer a product between your accounts. Your accounts are conceptually considered accounts of two different users so you can transfer products between your accounts.

To view the steps needed to transfer your product, see [Transfer billing ownership of an Azure subscription](billing-subscription-transfer.md).

### Transferring a product shouldn't create downtime

If you transfer a product to an account in the same Azure AD tenant, there's no effect on the resources running in the subscription. However, context information saved in PowerShell isn't updated so you might have to clear it or change settings. When you do a resource move or change the service tenant, then resources could be affected.

### New account usage and billing history

The only information available to users for the new account is usage and billing history starting from the time of transfer. Usage and billing history doesn't transfer with the product.

### Remaining product credits

If you have a Visual Studio or Microsoft Partner Network product, you get monthly credits. Your credit doesn't carry forward with the product in the new account. The user who accepts the transfer request needs to have a Visual Studio license to accept the transfer request. The product uses the Visual Studio credit that's available in the user's account. For more information, see [Transferring Visual Studio and Partner Network subscriptions](billing-subscription-transfer.md#transfer-visual-studio-and-partner-network-subscriptions).

### Users keep access to transferred resources

Keep in mind that users with access to resources in a product keep their access when billing ownership is transferred. However, [administrator roles](add-change-subscription-administrator.md) and [Azure role assignments](../../role-based-access-control/role-assignments-portal.md) might get removed. Losing access occurs when your account is in an Azure AD tenant other than the product's tenant and the user who sent the transfer request moves the product to your account's tenant.

You can view the users who have Azure role assignments to access resources in the product in the Azure portal. Visit the [Subscription page in the Azure portal](https://portal.azure.com/#blade/Microsoft_Azure_Billing/SubscriptionsBlade). Then select the product you want to check, and then select **Access control (IAM)** from the left-hand pane. Next, select  **Role assignments**  from the top of the page. The role assignments page lists all users who have access on the product.

Even if the [Azure role assignments](../../role-based-access-control/role-assignments-portal.md) are removed during transfer, users in the original owner account might continue to have access to the product through other security mechanisms, including:

- Management certificates that grant the user admin rights to subscription resources. For more information, see [Create and Upload a Management Certificate for Azure](../../cloud-services/cloud-services-certs-create.md).
- Access keys for services like Storage. For more information, see [About Azure storage accounts](../../storage/common/storage-account-create.md).
- Remote Access credentials for services like Azure Virtual Machines.

When the recipient needs to restrict access to resources, they should consider updating any secrets associated with the service. Most resources can be updated. Sign in to the [Azure portal](https://portal.azure.com/) and then on the Hub menu, select **All resources**. Next, Select the resource. Then in the resource page, select **Settings**. There you can view and update existing secrets.

### You pay for usage when you receive ownership

Your account is responsible for payment for any usage that is reported from the time of transfer onwards. There may be some usage that took place before the transfer but was reported afterwards. The usage is included in your account's bill.

### Transfer Enterprise Agreement product ownership

The Enterprise Administrator can update account ownership for any account, even after an original account owner is no longer part of the organization. For more information about transferring Azure Enterprise Agreement accounts, see [Azure Enterprise transfers](ea-transfers.md).

## Next steps

- [Move resources to a new resource group or subscription](../../azure-resource-manager/management/move-resource-group-and-subscription.md).
