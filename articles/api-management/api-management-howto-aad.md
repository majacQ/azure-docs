---
title: Authorize developer accounts by using Azure Active Directory
titleSuffix: Azure API Management
description: Learn how to authorize users by using Azure Active Directory in API Management.
services: api-management
documentationcenter: API Management
author: dlepow
manager: cfowler
editor: ''

ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 09/20/2021
ms.author: danlep
---

# Authorize developer accounts by using Azure Active Directory in Azure API Management

In this article, you'll learn how to:
> [!div class="checklist"]
> * Enable access to the developer portal for users from Azure Active Directory (Azure AD).
> * Manage groups of Azure AD users by adding external groups that contain the users.

## Prerequisites

- Complete the [Create an Azure API Management instance](get-started-create-service-instance.md) quickstart.
- [Import and publish](import-and-publish.md) an Azure API Management instance.

[!INCLUDE [premium-dev-standard.md](../../includes/api-management-availability-premium-dev-standard.md)]

## Authorize developer accounts by using Azure AD

1. Sign in to the [Azure portal](https://portal.azure.com). 
1. Select ![Arrow icon.](./media/api-management-howto-aad/arrow.png).
1. Search for and select **API Management services**.
1. Select your API Management service instance.
1. Under **Developer portal**, select **Identities**.
1. Select **+Add** from the top to open the **Add identity provider** pane to the right.
1. Under **Type**, select **Azure Active Directory** from the drop-down menu.
    * Once selected, you'll be able to enter other necessary information. 
    * Information includes **Client ID** and **Client secret**. 
    * See more information about these controls later in the article.
1. Save the **Redirect URL** for later.
    
    :::image type="content" source="media/api-management-howto-aad/api-management-with-aad001.png" alt-text="Add identity provider in Azure portal":::

    > [!NOTE]
    > There are two redirect URLs:<br/>
    > * **Redirect URL** points to the latest developer portal of the API Management.
    > * **Redirect URL (deprecated portal)** points to the deprecated developer portal of API Management.
    >
    > We recommended you use the latest developer portal Redirect URL.
   
1. In your browser, open the Azure portal in a new tab. 
1. Navigate to [App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) to register an app in Active Directory.
1. Select **New registration**. On the **Register an application** page, set the values as follows:
    
    * Set **Name** to a meaningful name. e.g., *developer-portal*
    * Set **Supported account types** to **Accounts in this organizational directory only**. 
    * Set **Redirect URI** to the value you saved from step 9. 
    * Select **Register**. 

1.  After you've registered the application, copy the **Application (client) ID** from the **Overview** page. 
1. Switch to the browser tab with your API Management instance. 
1. In the **Add identity provider** window, paste the **Application (client) ID** value into the **Client ID** box.
1. Switch to the browser tab with the App Registration.
1. Select the appropriate app registration.
1. Under the **Manage** section of the side menu, select **Certificates & secrets**. 
1. From the **Certificates & secrets** page, select the **New client secret** button under **Client secrets**. 
    * Enter a **Description**.
    * Select any option for **Expires**.
    * Choose **Add**. 
1. Copy the client **Secret value** before leaving the page. You will need it later. 
1. Under **Manage** in the side menu, select **Authentication**.
1. Under the **Implicit grant and hybrid flows** sections, select the **ID tokens** checkbox.
1. Switch to the browser tab with your API Management instance. 
1. Paste the secret into the **Client secret** field in the **Add identity provider** pane.

    > [!IMPORTANT]
    > Update the **Client secret** before the key expires. 

1. In the **Add identity provider** pane's **Allowed Tenants** field, specify the Azure AD instances' domains to which you want to grant access to the API Management service instance APIs. 
    * You can separate multiple domains with newlines, spaces, or commas.

    > [!NOTE]
    > You can specify multiple domains in the **Allowed Tenants** section. A global administration must grant the application access to directory data before users can sign in from a different domain than the original app registration domain. To grant permission, the global administrator should:
    > 1. Go to `https://<URL of your developer portal>/aadadminconsent` (for example, `https://contoso.portal.azure-api.net/aadadminconsent`).
    > 1. Enter the domain name of the Azure AD tenant to which they want to grant access.
    > 1. Select **Submit**. 

1.  After you specify the desired configuration, select **Add**.

Once changes are saved, users in the specified Azure AD instance can [sign into the developer portal by using an Azure AD account](#log_in_to_dev_portal).

## Add an external Azure AD group

Now that you've enabled access for users in an Azure AD tenant, you can:
* Add Azure AD groups into API Management. 
* Control product visibility using Azure AD groups.

Follow these steps to grant:
* `Directory.Read.All` application permission for Microsoft Graph API and Azure Active Directory Graph API.
* `User.Read` delegated permission for Microsoft Graph API. 

1. Update the first 3 lines of the following PowerShell script to match your environment and run it. 
   ```powershell
   $subId = "Your Azure subscription ID" #e.g. "1fb8fadf-03a3-4253-8993-65391f432d3a"
   $tenantId = "Your Azure AD Tenant or Organization ID" #e.g. 0e054eb4-e5d0-43b8-ba1e-d7b5156f6da8"
   $appObjectID = "Application Object ID that has been registered in AAD" #e.g. "2215b54a-df84-453f-b4db-ae079c0d2619"
   #Login and Set the Subscription
   az login
   az account set --subscription $subId
   #Assign the following permissions: Microsoft Graph Delegated Permission: User.Read, Microsoft Graph Application Permission: Directory.ReadAll,  Azure Active Directory Graph Application Permission: Directory.ReadAll (legacy)
   az rest --method PATCH --uri "https://graph.microsoft.com/v1.0/$($tenantId)/applications/$($appObjectID)" --body "{'requiredResourceAccess':[{'resourceAccess': [{'id': 'e1fe6dd8-ba31-4d61-89e7-88639da4683d','type': 'Scope'},{'id': '7ab1d382-f21e-4acd-a863-ba3e13f7da61','type': 'Role'}],'resourceAppId': '00000003-0000-0000-c000-000000000000'},{'resourceAccess': [{'id': '5778995a-e1bf-45b8-affa-663a9f3f4d04','type': 'Role'}], 'resourceAppId': '00000002-0000-0000-c000-000000000000'}]}"
   ```
2. Log out and log back in to the Azure portal.
3. Navigate to the App Registration page for the application you registered in [the previous section](#authorize-developer-accounts-by-using-azure-ad). 
4. Click **API Permissions**. You should see the permissions granted by the PowerShell script in step 1. 
5. Select **Grant admin consent for {tenantname}** so that you grant access for all users in this directory. 

Now you can add external Azure AD groups from the **Groups** tab of your API Management instance.

1. Under **Developer portal** in the side menu, select **Groups**.
2. Select the **Add Azure AD group** button.

   !["Add A A D group" button](./media/api-management-howto-aad/api-management-with-aad008.png)
1. Select the **Tenant** from the drop-down. 
2. Search for and select the group that you want to add.
3. Press the **Select** button.

Once you add an external Azure AD group, you can review and configure its properties: 
1. Select the name of the group from the **Groups** tab. 
2. Edit **Name** and **Description** information for the group.
 
Users from the configured Azure AD instance can now:
* Sign into the developer portal. 
* View and subscribe to any groups for which they have visibility.

> [!NOTE]
> Learn more about the difference between **Delegated** and **Application** permissions types in [Permissions and consent in the Microsoft identity platform](../active-directory/develop/v2-permissions-and-consent.md#permission-types) article.

## <a id="log_in_to_dev_portal"></a> Developer portal: Add Azure AD account authentication

In the developer portal, you can sign in with Azure AD using the **Sign-in button: OAuth** widget included on the sign-in page of the default developer portal content.

Although a new account will automatically be created when a new user signs in with Azure AD, consider adding the same widget to the sign-up page. The **Sign-up form: OAuth** widget represents a form used for signing up with OAuth.

> [!IMPORTANT]
> You need to [republish the portal](api-management-howto-developer-portal-customize.md#publish) for the Azure AD changes to take effect.

## Legacy developer portal: How to sign in with Azure AD

[!INCLUDE [api-management-portal-legacy.md](../../includes/api-management-portal-legacy.md)]

To sign into the developer portal by using an Azure AD account that you configured in the previous sections:

1. Open a new browser window using the sign-in URL from the Active Directory application configuration. 
2. Select **Azure Active Directory**.

   ![Sign-in page][api-management-dev-portal-signin]

1. Enter the credentials of one of the users in Azure AD.
2. Select **Sign in**.

   ![Signing in with username and password][api-management-aad-signin]

1. If prompted with a registration form, complete with any additional information required. 
2. Select **Sign up**.

   !["Sign up" button on registration form][api-management-complete-registration]

Your user is now signed in to the developer portal for your API Management service instance.

![Developer portal after registration is complete][api-management-registration-complete]

## Next Steps

- Learn how to [Protect your web API backend in API Management by using OAuth 2.0 authorization with Azure AD](./api-management-howto-protect-backend-with-aad.md)
- Learn more about [Azure Active Directory and OAuth2.0](../active-directory/develop/authentication-vs-authorization.md).
- Check out more [videos](https://azure.microsoft.com/documentation/videos/index/?services=api-management) about API Management.
- For other ways to secure your back-end service, see [Mutual Certificate authentication](./api-management-howto-mutual-certificates.md).
- [Create an API Management service instance](./get-started-create-service-instance.md).
- [Manage your first API](./import-and-publish.md).

[api-management-dev-portal-signin]: ./media/api-management-howto-aad/api-management-dev-portal-signin.png
[api-management-aad-signin]: ./media/api-management-howto-aad/api-management-aad-signin.png
[api-management-complete-registration]: ./media/api-management-howto-aad/api-management-complete-registration.png
[api-management-registration-complete]: ./media/api-management-howto-aad/api-management-registration-complete.png

[How to add operations to an API]: ./mock-api-responses.md
[How to add and publish a product]: api-management-howto-add-products.md
[Monitoring and analytics]: api-management-monitoring.md
[Add APIs to a product]: api-management-howto-add-products.md#add-apis
[Publish a product]: api-management-howto-add-products.md#publish-product
[Get started with Azure API Management]: get-started-create-service-instance.md
[API Management policy reference]: ./api-management-policies.md
[Caching policies]: ./api-management-policies.md#caching-policies
[Create an API Management service instance]: get-started-create-service-instance.md

[https://oauth.net/2/]: https://oauth.net/2/
[WebApp-GraphAPI-DotNet]: https://github.com/AzureADSamples/WebApp-GraphAPI-DotNet

[Prerequisites]: #prerequisites
[Configure an OAuth 2.0 authorization server in API Management]: #step1
[Configure an API to use OAuth 2.0 user authorization]: #step2
[Test the OAuth 2.0 user authorization in the Developer Portal]: #step3
[Next steps]: #next-steps

[Sign in to the developer portal by using an Azure AD account]: #Sign-in-to-the-developer-portal-by-using-an-Azure-AD-account
