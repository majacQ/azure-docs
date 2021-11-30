---
title: Form Recognizer quotas and limits
titleSuffix: Azure Applied AI Services
description: Quick reference, detailed description, and best practices on Azure Form Recognizer service Quotas and Limits
services: cognitive-services
author: vkurpad
manager: nitinme
ms.service: applied-ai-services
ms.subservice: forms-recognizer
ms.topic: conceptual
ms.date: 09/30/2021
ms.author: vikurpad
---

# Form Recognizer service Quotas and Limits

This article contains a quick reference and the **detailed description** of Azure Form Recognizer service Quotas and Limits for all [pricing tiers](https://azure.microsoft.com/pricing/details/form-recognizer/). It also contains some best practices to avoid request throttling. 

For the usage with [Form Recognizer SDK](quickstarts/try-v3-csharp-sdk.md), [Form Recognizer REST API](quickstarts/try-v3-rest-api.md), [Form Recognizer Studio](quickstarts/try-v3-form-recognizer-studio.md) and [Sample Labeling Tool](https://fott-2-1.azurewebsites.net/).

| Quota | Free (F0)<sup>1</sup> | Standard (S0) |
|--|--|--|
| **Concurrent Request limit** | 1 | 15 (default value) |
| Adjustable | No<sup>2</sup> | Yes<sup>2</sup> |
| **Compose Model limit** | 5 | 100 (default value) |


<sup>1</sup> For **Free (F0)** pricing tier see also monthly allowances at the [pricing page](https://azure.microsoft.com/pricing/details/form-recognizer/).
<sup>2</sup> See [best practices](#example-of-a-workload-pattern-best-practice),  and [adjustment instructions](#create-and-submit-support-request).

## Detailed description, Quota adjustment, and best practices
Before requesting a quota increase (where applicable), ensure that it is necessary. Form Recognizer service uses autoscaling to bring the required computational resources in "on-demand"  and at the same time to keep the customer costs low, deprovision unused resources by not maintaining an excessive amount of hardware capacity. Every time your application receives a Response Code 429 ("Too many requests") while your workload is within the defined limits (see [Quotas and Limits quick reference](#form-recognizer-service-quotas-and-limits)) the most likely explanation is that the Service is scaling up to your demand and did not reach the required scale yet, thus it does not immediately have enough resources to serve the request. This state is usually transient and should not last long.

### General best practices to mitigate throttling during autoscaling
To minimize issues related to throttling (Response Code 429), we recommend using the following techniques:
- Implement retry logic in your application
- Avoid sharp changes in the workload. Increase the workload gradually <br/>
*Example.* Your application is using Form Recognizer and your current workload is 10 TPS (transactions per second). The next second you increase the load to 40 TPS (that is four times more). The Service immediately starts scaling up to fulfill the new load, but likely it will not be able to do it within a second, so some of the requests will get Response Code 429.

The next sections describe specific cases of adjusting quotas.
Jump to [Form Recognizer: increasing concurrent request limit](#create-and-submit-support-request)

### Increasing transactions per second request limit
By default the number of concurrent requests is limited to 15 transactions per second for a Form Recognizer resource. For the Standard pricing tier, this amount can be increased. Before submitting the request, ensure you are familiar with the material in [this section](#detailed-description-quota-adjustment-and-best-practices) and aware of these [best practices](#example-of-a-workload-pattern-best-practice).

Increasing the Concurrent Request limit does **not** directly affect your costs. Form Recognizer service uses "Pay only for what you use" model. The limit defines how high the Service may scale before it starts throttle your requests.

Existing value of Concurrent Request limit parameter is **not** visible via Azure portal, Command-Line tools, or API requests. To verify the existing value, create an Azure Support Request.

#### Have the required information ready:
- Form Recognizer Resource ID
- Region

- **How to get information (Base model)**:
  - Go to [Azure portal](https://portal.azure.com/)
  - Select the Form Recognizer Resource for which you would like to increase the transaction limit
  - Select *Properties* (*Resource Management* group)
  - Copy and save the values of the following fields:
    - **Resource ID**
    - **Location** (your endpoint Region)

#### Create and submit support request
Initiate the increase of transactions per second(TPS) limit for your resource by submitting the Support Request:

- Ensure you have the [required information](#have-the-required-information-ready)
- Go to [Azure portal](https://portal.azure.com/)
- Select the Form Recognizer Resource for which you would like to increase the TPS limit
- Select *New support request* (*Support + troubleshooting* group)
- A new window will appear with auto-populated information about your Azure Subscription and Azure Resource
- Enter *Summary* (like "Increase Form Recognizer TPS limit")
- In *Problem type* select "Quota or usage validation"
- Click *Next: Solutions*
- Proceed further with the request creation
- When in *Details* tab enter in the *Description* field:
  - a note, that the request is about **Form Recognizer** quota
  - Provide a TPS expectation you would like to scale to    
  - Azure resource information you [collected before](#have-the-required-information-ready)
  - Complete entering the required information and click *Create* button in *Review + create* tab
  - Note the support request number in Azure portal notifications. You will be contacted shortly for further processing

## Example of a workload pattern best practice
This example presents the approach we recommend following to mitigate possible request throttling due to [Autoscaling being in progress](#detailed-description-quota-adjustment-and-best-practices). It is not an "exact recipe", but merely a template we invite to follow and adjust as necessary.

Let us suppose that a Form Recognizer resource has the default limit set. Start the workload to submit your analyze requests. If you find that you are seeing frequent throttling with response code 429, start by backing off on the GET analyze response request and retry using the 2-3-5-8 pattern. In general it is recommended that you not call the get analyze response more than once every 2 seconds for a corresponding POST request. 

If you find that you are being throttled on the number of POST requests for documents being submitted, consider adding a delay between the requests. If your workload requires a higher degree of concurrent processing, you will then need to create a support request to increase your service limits on transactions per second.

Generally, it is highly recommended to test the workload and the workload patterns before going to production.

