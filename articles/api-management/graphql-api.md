---
title: Import a GraphQL API using the Azure portal | Microsoft Docs
titleSuffix: 
description: Learn how API Management supports GraphQL, add a GraphQL API, and GraphQL limitations.
ms.service: api-management
author: dlepow
ms.author: danlep
ms.topic: how-to
ms.date: 10/21/2021
ms.custom: ignite-fall-2021
---

# Import a GraphQL API (preview)

GraphQL is an open-source, industry-standard query language for APIs. Unlike endpoint-based (or REST-style) APIs designed around actions over resources, GraphQL APIs support a broader set of use cases and focus on data types, schemas, and queries.

API Management tackles the security, authentication, and authorization challenges that come with publishing GraphQL APIs. Using API Management to expose your GraphQL APIs, you can:
* Add a GraphQL service as APIs via Azure portal.  
* Secure GraphQL APIs by applying both existing access control policies and a [new policy](graphql-validation-policies.md) to secure and protect against GraphQL-specific attacks. 
* Explore the schema and run test queries against the GraphQL APIs in the Azure and developer portals. 

[!INCLUDE [preview-callout-graphql.md](./includes/preview/preview-callout-graphql.md)]

In this article, you'll:
> [!div class="checklist"]
> * Learn more about the benefits of using GraphQL APIs.
> * Add a GraphQL API to your API Management instance.
> * Test your GraphQL API.
> * Learn the limitations of your GraphQL API in API Management.

## Prerequisites

- An existing API Management instance. [Create one if you haven't already](get-started-create-service-instance.md).
- A GraphQL API. 

## Add a GraphQL API

1. Navigate to your API Management instance.
1. From the side navigation menu, under the **APIs** section, select **APIs**.
1. Under **Define a new API**, select the **GraphQL** icon.

    :::image type="content" source="media/graphql-api/import-graphql-api.png" alt-text="Selecting GraphQL icon from list of APIs":::

1. In the dialog box, select **Full** and complete the required form fields.

    :::image type="content" source="media/graphql-api/create-from-graphql-schema.png" alt-text="Demonstrate fields for creating GraphQL":::

    | Field | Description |
    |----------------|-------|
    | Display name | The name by which your GraphQL API will be displayed. |
    | Name | Raw name of the GraphQL API. Automatically populates as you type the display name. |
    | GraphQL API endpoint | The base URL with your GraphQL API endpoint name. <br /> For example: *`https://example.com/your-GraphQL-name`*. You can also use the common ["Star Wars" GraphQL endpoint](https://swapi-graphql.netlify.app/.netlify/functions/index) as a demo. |
    | Upload schema file | Select to browse and upload your schema file. |
    | Description | Add a description of your API. |
    | URL scheme | Select HTTP, HTTPS, or Both. Default selection: *Both*. |
    | API URL suffix| Add a URL suffix to identify this specific API in this API Management instance. It has to be unique in this API Management instance. |
    | Base URL | Uneditable field displaying your API base URL |
    | Tags | Associate your GraphQL API with new or existing tags. |
    | Products | Associate your GraphQL API with a product to publish it. |
    | Gateways | Associate your GraphQL API with existing gateways. Default gateway selection: *Managed*. |
    | Version this API? | Select to version control your GraphQL API. |
 
1. Click **Create**.

## Test your GraphQL API

1. Navigate to your API Management instance.
1. From the side navigation menu, under the **APIs** section, select **APIs**.
1. Under **All APIs**, select your GraphQL API.
1. Select the **Test** tab to access the Test console. 
1. Under **Headers**:
    1. Select the header from the **Name** drop-down menu.
    1. Enter the value to the **Value** field.
    1. Add more headers by selecting **+ Add header**.
    1. Delete headers using the **trashcan icon**.
1. If you've added a product to your GraphQL API, apply product scope under **Apply product scope**.
1. Under **Query editor**, either:
    1. Select at least one field or subfield from the list in the side menu. The fields and subfields you select appear in the query editor.
    1. Start typing in the query editor to compose a query.
    
        :::image type="content" source="media/graphql-api/test-graphql-query.png" alt-text="Demonstrating adding fields to the query editor":::

1. Under **Query variables**, add variables to reuse the same query or mutation and pass different values.
1. Click **Send**.
1. View the **Response**.

    :::image type="content" source="media/graphql-api/graphql-query-response.png" alt-text="View the test query response":::

1. Repeat preceding steps to test different payloads.
1. When testing is complete, exit test console.

## Limitations

* Only GraphQL pass through is supported. 
* A single GraphQL API in API Management corresponds to only a single GraphQL backend endpoint.

[!INCLUDE [api-management-define-api-topics.md](../../includes/api-management-define-api-topics.md)]

## Next steps
> [!div class="nextstepaction"]
> [Transform and protect a published API](transform-api.md)
