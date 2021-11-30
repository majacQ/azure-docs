---
title: Get access token using Azure CLI - Azure Healthcare APIs for DICOM service
description: This article explains how to obtain an access token for the DICOM service using the Azure CLI.
author: stevewohl
ms.service: healthcare-apis
ms.subservice: fhir
ms.topic: how-to
ms.date: 07/10/2021
ms.author: aersoy
---

# Get access token for the DICOM service using Azure CLI

> [!IMPORTANT]
> Azure Healthcare APIs is currently in PREVIEW. The [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

In this article, you'll learn how to obtain an access token for the DICOM service using the Azure CLI. When you [deploy the DICOM service](deploy-dicom-services-in-azure.md), you configure a set of users or service principals that have access to the service. If your user object ID is in the list of allowed object IDs, you can access the service using a token obtained using the Azure CLI.

## Prerequisites

Use the Bash environment in Azure Cloud Shell.


[ ![Launch Azure Cloud Shell.](media/launch-cloud-shell.png) ](media/launch-cloud-shell.png#lightbox)

If you prefer, [install](/cli/azure/install-azure-cli) the Azure CLI to run CLI reference commands.

* If you're using a local installation, sign in to the Azure CLI by using the [az login](/cli/azure/reference-index#az_login) command. To finish the authentication process, follow the steps displayed in your terminal. For additional sign-in options, see [Sign in with the Azure CLI](/cli/azure/authenticate-azure-cli).
* When you're prompted, install Azure CLI extensions on first use. For more information about extensions, see [Use extensions with the Azure CLI](/cli/azure/azure-cli-extensions-overview).
* Run [az version](/cli/azure/reference-index#az_version) to find the version and dependent libraries that are installed. To upgrade to the latest version, run [az upgrade](/cli/azure/reference-index#az_upgrade).

## Obtain a token

The DICOM service uses a `resource` or `Audience` with URI equal to the URI of the DICOM server  `https://dicom.healthcareapis.azure.com`. You can obtain a token and store it in a variable (named `$token`) with the following command:


```Azure CLICopy
Try It
$token=$(az account get-access-token --resource=https://dicom.healthcareapis.azure.com --query accessToken --output tsv)
```

## Use with the DICOM service

```Azure CLICopy
Try It
curl -X GET --header "Authorization: Bearer $token"  https://<workspacename-dicomservicename>.dicom.azurehealthcareapis.com/v<version of REST API>/changefeed
```

## Next steps

In this article, you've learned how to obtain an access token for the DICOM service using the Azure CLI. 

>[!div class="nextstepaction"]
>[Overview of the DICOM service](dicom-services-overview.md)
