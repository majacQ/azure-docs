---
title: Built-in triggers and actions
description: Use built-in triggers and actions to create automated workflows that integrate apps, data, services, and systems, to control workflows, and to manage data using Azure Logic Apps.
services: logic-apps
ms.suite: integration
ms.reviewer: estfan, azla
ms.topic: conceptual
ms.date: 11/02/2021
---

# Built-in triggers and actions in Azure Logic Apps

[Built-in triggers and actions](apis-list.md) provide ways for you to [control your workflow's schedule and structure](#control-workflow), [run your own code](#run-code-from-workflows), [manage or manipulate data](#manage-or-manipulate-data), and complete other tasks in your workflows. Different from [managed connectors](managed.md), many built-in operations aren't tied to a specific service, system, or protocol. For example, you can start almost any workflow on a schedule by using the Recurrence trigger. Or, you can have your workflow wait until called by using the Request trigger. All built-in operations run natively in Azure Logic Apps, and most don't require that you create a connection before you use them.

For a smaller number of services, systems and protocols, Azure Logic Apps provides built-in operations, such as Azure API Management, Azure App Services, Azure Functions, and for calling other Azure Logic Apps logic app workflows. The number and range available vary based on whether you create a Consumption plan-based logic app resource that runs in multi-tenant Azure Logic Apps, or a Standard plan-based logic app resource that runs in single-tenant Azure Logic Apps. For more information, review [Single-tenant versus multi-tenant and integration service environment (ISE)](../logic-apps/single-tenant-overview-compare.md). In most cases, the built-in version provides better performance, capabilities, pricing, and so on.

For example, if you create a single-tenant logic app, both built-in operations and [managed connector operations](managed.md) are available for a few services, specifically Azure Blob, Azure Event Hubs, Azure Cosmos DB, Azure Service Bus, DB2, MQ, and SQL Server. In few cases, some built-in operations are available only for one logic app resource type. For example, Batch operations are currently available only for Consumption logic app workflows. In most cases, the built-in version provides better performance, capabilities, pricing, and so on.

The following list describes only some of the tasks that you can accomplish with [built-in triggers and actions](#general-built-in-triggers-and-actions):

- Run workflows using custom and advanced schedules. For more information about scheduling, review the [recurrence behavior section in the connector overview for Azure Logic Apps](apis-list.md#recurrence-behavior).

- Organize and control your workflow's structure, for example, using loops and conditions.

- Work with variables, dates, data operations, content transformations, and batch operations.

- Communicate with other endpoints using HTTP triggers and actions.

- Receive and respond to requests.

- Call your own functions (Azure Functions), web apps (Azure App Services), APIs (Azure API Management), other Azure Logic Apps workflows that can receive requests, and so on.

## General built-in triggers and actions

Azure Logic Apps provides the following built-in triggers and actions:

:::row:::
    :::column:::
        [![Schedule icon][schedule-icon]][schedule-doc]
        \
        \
        [**Schedule**][schedule-doc]
        \
        \
        [**Recurrence**][schedule-recurrence-doc]: Trigger a workflow based on the specified recurrence.
        \
        \
        [**Sliding Window**][schedule-sliding-window-doc]: Trigger a workflow that needs to handle data in continuous chunks.
        \
        \
        [**Delay**][schedule-delay-doc]: Pause your workflow for the specified duration.
        \
        \
        [**Delay until**][schedule-delay-until-doc]: Pause your workflow until the specified date and time.
    :::column-end:::
    :::column:::
        [![HTTP trigger and action icon][http-icon]][http-doc]
        \
        \
        [**HTTP**][http-doc]
        \
        \
        Call an HTTP or HTTPS endpoint by using either the HTTP trigger or action.
        \
        \
        You can also use these other built-in HTTP triggers and actions:
        - [HTTP + Swagger][http-swagger-doc]
        - [HTTP + Webhook][http-webhook-doc]
    :::column-end:::
    :::column:::
        [![Request trigger icon][http-request-icon]][http-request-doc]
        \
        \
        [**Request**][http-request-doc]
        \
        \
        [**When a HTTP request is received**][http-request-doc]: Wait for a request from another workflow, app, or service. This trigger makes your workflow callable without having to be checked or polled on a schedule.
        \
        \
        [**Response**][http-request-doc]: Respond to a request received by the **When a HTTP request is received** trigger in the same workflow.
    :::column-end:::
    :::column:::
        [![Batch icon][batch-icon]][batch-doc]<br>(*Consumption logic app only*)
        \
        \
        [**Batch**][batch-doc]
        \
        \
        [**Batch messages**][batch-doc]: Trigger a workflow that processes messages in batches.
        \
        \
        [**Send messages to batch**][batch-doc]: Call an existing workflow that currently starts with a **Batch messages** trigger.
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [![STFP-SSH icon][sftp-ssh-icon]][sftp-ssh-doc]
        \
        \
        [**STFP-SSH**][sftp-ssh-doc]<br>(*Standard logic app only*)
        \
        \
        Connect to SFTP servers that you can access from the internet by using SSH so that you can work with your files and folders.
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

## Service-based built-in trigger and actions

Azure Logic Apps provides the following built-in actions for the following services:

:::row:::
    :::column:::
        [![Azure API Management icon][azure-api-management-icon]][azure-api-management-doc]
        \
        \
        [**Azure API Management**][azure-api-management-doc]
        \
        \
        Call your own triggers and actions in APIs that you define, manage, and publish using [Azure API Management](../api-management/api-management-key-concepts.md). <p><p>**Note**: Not supported when using [Consumption tier for API Management](../api-management/api-management-features.md).
    :::column-end:::
    :::column:::
        [![Azure App Services icon][azure-app-services-icon]][azure-app-services-doc]
        \
        \
        [**Azure App Services**][azure-app-services-doc]
        \
        \
        Call apps that you create and host on [Azure App Service](../app-service/overview.md), for example, API Apps and Web Apps.
        \
        \
        When Swagger is included, the triggers and actions defined by these apps appear like any other first-class triggers and actions in Azure Logic Apps.
    :::column-end:::
    :::column:::
        [![Azure Blob icon icon][azure-blob-storage-icon]][azure-app-services-doc]
        \
        \
        [**Azure Blob**][azure-blob-storage-doc]<br>(*Standard logic app only*)
        \
        \
        Connect to your Azure Storage account so that you can create and manage blob content.
    :::column-end:::
    :::column:::
        [![Azure Cosmos DB icon][azure-cosmos-db-icon]][azure-cosmos-db-doc]
        \
        \
        [**Azure Cosmos DB**][azure-cosmos-db-doc]<br>(*Standard logic app only*)
        \
        \
        Connect to Azure Cosmos DB so that you can access and manage Azure Cosmos DB documents.
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [![Azure Functions icon][azure-functions-icon]][azure-functions-doc]
        \
        \
        [**Azure Functions**][azure-functions-doc]
        \
        \
        Call [Azure-hosted functions](../azure-functions/functions-overview.md) to run your own *code snippets* (C# or Node.js) within your workflow.
    :::column-end:::
    :::column:::
        [![Azure Logic Apps icon][azure-logic-apps-icon]][nested-logic-app-doc]
        \
        \
        [**Azure Logic Apps**][nested-logic-app-doc]
        \
        \
        Call other workflows that start with the Request trigger named **When a HTTP request is received**.
    :::column-end:::
    :::column:::
        [![Azure Service Bus icon][azure-service-bus-icon]][azure-service-bus-doc]
        \
        \
        [**Azure Service Bus**][azure-service-bus-doc]<br>(*Standard logic app only*)
        \
        \
        Manage asynchronous messages, queues, sessions, topics, and topic subscriptions.
    :::column-end:::
    :::column:::
        [![IBM DB2 icon][ibm-db2-icon]][ibm-db2-doc]
        \
        \
        [**DB2**][ibm-db2-doc]<br>(*Standard logic app only*)
        \
        \
        Connect to IBM DB2 in the cloud or on-premises. Update a row, get a table, and more.
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [![Azure Event Hubs icon][azure-event-hubs-icon]][azure-event-hubs-doc]
        \
        \
        [**Event Hubs**][azure-event-hubs-doc]<br>(*Standard logic app only*)
        \
        \
        Consume and publish events through an event hub. For example, get output from your logic app with Event Hubs, and then send that output to a real-time analytics provider.
    :::column-end:::
    :::column:::
        [![IBM MQ icon][ibm-mq-icon]][ibm-mq-doc]
        \
        \
        [**MQ**][ibm-mq-doc]<br>(*Standard logic app only*)
        \
        \
        Connect to IBM MQ on-premises or in Azure to send and receive messages.
    :::column-end:::
    :::column:::
        [![SQL Server icon][sql-server-icon]][sql-server-doc]
        \
        \
        [**SQL Server**][sql-server-doc]<br>(*Standard logic app only*)
        \
        \
        Connect to your SQL Server on premises or an Azure SQL Database in the cloud so that you can manage records, run stored procedures, or perform queries. <p>**Note**: Single-tenant Azure Logic Apps provides both SQL built-in and managed connector operations, while multi-tenant Azure Logic Apps provides only managed connector operations. <p>For more information, review [Single-tenant versus multi-tenant and integration service environment for Azure Logic Apps](../logic-apps/single-tenant-overview-compare.md).
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

## Run code from workflows

Azure Logic Apps provides the following built-in actions for running your own code in your workflow:

:::row:::
    :::column:::
        [![Azure Functions icon][azure-functions-icon]][azure-functions-doc]
        \
        \
        [**Azure Functions**][azure-functions-doc]
        \
        \
        Call [Azure-hosted functions](../azure-functions/functions-overview.md) to run your own *code snippets* (C# or Node.js) within your workflow.
    :::column-end:::
    :::column:::
        [![Inline Code action icon][inline-code-icon]][inline-code-doc]
        \
        \
        [**Inline Code**][inline-code-doc]
        \
        \
        [**Execute JavaScript Code**][inline-code-doc]: Add and run your own inline JavaScript *code snippets* within your workflow.
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

## Control workflow

Azure Logic Apps provides the following built-in actions for structuring and controlling the actions in your workflow:

:::row:::
    :::column:::
        [![Condition action icon][condition-icon]][condition-doc]
        \
        \
        [**Condition**][condition-doc]
        \
        \
        Evaluate a condition and run different actions based on whether the condition is true or false.
    :::column-end:::
    :::column:::
        [![For Each action icon][for-each-icon]][for-each-doc]
        \
        \
        [**For Each**][for-each-doc]
        \
        \
        Perform the same actions on every item in an array.
    :::column-end:::
    :::column:::
        [![Scope action icon][scope-icon]][scope-doc]
        \
        \
        [**Name**][scope-doc]
        \
        \
        Group actions into *scopes*, which get their own status after the actions in the scope finish running.
    :::column-end:::
    :::column:::
        [![Switch action icon][switch-icon]][switch-doc]
        \
        \
        [**Switch**][switch-doc]
        \
        \
        Group actions into *cases*, which are assigned unique values except for the default case. Run only that case whose assigned value matches the result from an expression, object, or token. If no matches exist, run the default case.
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [![Terminate action icon][terminate-icon]][terminate-doc]
        \
        \
        [**Terminate**][terminate-doc]
        \
        \
        Stop an actively running logic app workflow.
    :::column-end:::
    :::column:::
        [![Until action icon][until-icon]][until-doc]
        \
        \
        [**Until**][until-doc]
        \
        \
        Repeat actions until the specified condition is true or some state has changed.
    :::column-end:::
    :::column:::
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

## Manage or manipulate data

Azure Logic Apps provides the following built-in actions for working with data outputs and their formats:

:::row:::
    :::column:::
        [![Data Operations icon][data-operations-icon]][data-operations-doc]
        \
        \
        [**Data Operations**][data-operations-doc]
        \
        \
        Perform operations with data.
        \
        \
        **Compose**: Create a single output from multiple inputs with various types.
        \
        \
        **Create CSV table**: Create a comma-separated-value (CSV) table from an array with JSON objects.
        \
        \
        **Create HTML table**: Create an HTML table from an array with JSON objects.
        \
        \
        **Filter array**: Create an array from items in another array that meet your criteria.
        \
        \
        **Join**: Create a string from all items in an array and separate those items with the specified delimiter.
        \
        \
        **Parse JSON**: Create user-friendly tokens from properties and their values in JSON content so that you can use those properties in your workflow.
        \
        \
        **Select**: Create an array with JSON objects by transforming items or values in another array and mapping those items to specified properties.
    :::column-end:::
    :::column:::
        ![Date Time action icon][date-time-icon]
        \
        \
        **Date Time**
        \
        \
        Perform operations with timestamps.
        \
        \
        **Add to time**: Add the specified number of units to a timestamp.
        \
        \
        **Convert time zone**: Convert a timestamp from the source time zone to the target time zone.
        \
        \
        **Current time**: Return the current timestamp as a string.
        \
        \
        **Get future time**: Return the current timestamp plus the specified time units.
        \
        \
        **Get past time**: Return the current timestamp minus the specified time units.
        \
        \
        **Subtract from time**: Subtract a number of time units from a timestamp.
    :::column-end:::
    :::column:::
        [![Variables action icon][variables-icon]][variables-doc]
        \
        \
        [**Variables**][variables-doc]
        \
        \
        Perform operations with variables.
        \
        \
        **Append to array variable**: Insert a value as the last item in an array stored by a variable.
        \
        \
        **Append to string variable**: Insert a value as the last character in a string stored by a variable.
        \
        \
        **Decrement variable**: Decrease a variable by a constant value.
        \
        \
        **Increment variable**: Increase a variable by a constant value.
        \
        \
        **Initialize variable**: Create a variable and declare its data type and initial value.
        \
        \
        **Set variable**: Assign a different value to an existing variable.
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

## Integration account built-in actions

Azure Logic Apps provides the following built-in actions, which either require an integration account when using multi-tenant, Consumption plan-based Azure Logic Apps or don't require an integration account when using single-tenant, Standard plan-based Azure Logic Apps:

> [!NOTE]
> Before you can use integration account action in multi-tenant, Consumption plan-based Azure Logic Apps, you must 
> [link your logic app resource to an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md). 
> However, in single-tenant, Standard plan-based Azure Logic Apps, some integration account operations don't require linking your 
> logic app resource to an integration account, for example, Liquid operations and XML operations. To use these actions, you need 
> to have Liquid maps, XML maps, or XML schemas that you can upload through the respective actions in the Azure portal or add to 
> your Visual Studio Code project's **Artifacts** folder using the respective **Maps** and **Schemas** folders.

:::row:::
    :::column:::
        [![Flat file decoding icon][flat-file-decode-icon]][flat-file-decode-doc]
        \
        \
        [**Flat file decoding**][flat-file-decode-doc]
        \
        \
        Encode XML before sending the content to a trading partner.
    :::column-end:::
    :::column:::
        [![Flat file encoding icon][flat-file-encode-icon]][flat-file-encode-doc]
        \
        \
        [**Flat file encoding**][flat-file-encode-doc]
        \
        \
        Decode XML after receiving the content from a trading partner.
    :::column-end:::
    :::column:::
        [![Integration account icon][integration-account-icon]][integration-account-doc]
        \
        \
        [**Integration Account Artifact Lookup**<br>(*Multi-tenant only*)][integration-account-doc]
        \
        \
        Get custom metadata for artifacts, such as trading partners, agreements, schemas, and so on, in your integration account.
    :::column-end:::
    :::column:::
        [![Liquid operations icon][liquid-icon]][json-liquid-transform-doc]
        \
        \
        [**Liquid operations**][json-liquid-transform-doc]
        \
        \
        Convert the following formats by using Liquid templates: <p><p>- JSON to JSON <br>- JSON to TEXT <br>- XML to JSON <br>- XML to TEXT
    :::column-end:::
:::row-end:::
:::row:::
    :::column:::
        [![Transform XML icon][xml-transform-icon]][xml-transform-doc]
        \
        \
        [**Transform XML**][xml-transform-doc]
        \
        \
        Convert the source XML format to another XML format.
    :::column-end:::
    :::column:::
        [![XML validation icon][xml-validate-icon]][xml-validate-doc]
        \
        \
        [**XML validation**][xml-validate-doc]
        \
        \
        Validate XML documents against the specified schema.
    :::column-end:::
    :::column:::
    :::column-end:::
:::row-end:::

## Next steps

> [!div class="nextstepaction"]
> [Create custom APIs that you can call from Azure Logic Apps](../logic-apps/logic-apps-create-api-app.md)

<!-- Built-in icons -->
[azure-api-management-icon]: ./media/apis-list/azure-api-management.png
[azure-app-services-icon]: ./media/apis-list/azure-app-services.png
[azure-blob-storage-icon]: ./media/apis-list/azure-blob-storage.png
[azure-cosmos-db-icon]: ./media/apis-list/azure-cosmos-db.png
[azure-event-hubs-icon]: ./media/apis-list/azure-event-hubs.png
[azure-functions-icon]: ./media/apis-list/azure-functions.png
[azure-logic-apps-icon]: ./media/apis-list/azure-logic-apps.png
[azure-service-bus-icon]: ./media/apis-list/azure-service-bus.png
[batch-icon]: ./media/apis-list/batch.png
[condition-icon]: ./media/apis-list/condition.png
[data-operations-icon]: ./media/apis-list/data-operations.png
[date-time-icon]: ./media/apis-list/date-time.png
[for-each-icon]: ./media/apis-list/for-each-loop.png
[http-icon]: ./media/apis-list/http.png
[http-request-icon]: ./media/apis-list/request.png
[http-response-icon]: ./media/apis-list/response.png
[http-swagger-icon]: ./media/apis-list/http-swagger.png
[http-webhook-icon]: ./media/apis-list/http-webhook.png
[ibm-db2-icon]: ./media/apis-list/ibm-db2.png
[ibm-mq-icon]: ./media/apis-list/ibm-mq.png
[inline-code-icon]: ./media/apis-list/inline-code.png
[schedule-icon]: ./media/apis-list/recurrence.png
[scope-icon]: ./media/apis-list/scope.png
[sftp-ssh-icon]: ./media/apis-list/sftp.png
[sql-server-icon]: ./media/apis-list/sql.png
[switch-icon]: ./media/apis-list/switch.png
[terminate-icon]: ./media/apis-list/terminate.png
[until-icon]: ./media/apis-list/until.png
[variables-icon]: ./media/apis-list/variables.png

<!--Built-in integration account connector icons -->
[flat-file-encode-icon]: ./media/apis-list/flat-file-encoding.png
[flat-file-decode-icon]: ./media/apis-list/flat-file-decoding.png
[integration-account-icon]: ./media/apis-list/integration-account.png
[liquid-icon]: ./media/apis-list/liquid-transform.png
[xml-transform-icon]: ./media/apis-list/xml-transform.png
[xml-validate-icon]: ./media/apis-list/xml-validation.png

<!--Built-in doc links-->
[azure-api-management-doc]: ../api-management/get-started-create-service-instance.md "Create an Azure API Management service instance for managing and publishing your APIs"
[azure-app-services-doc]: ../logic-apps/logic-apps-custom-api-host-deploy-call.md "Integrate logic apps with App Service API Apps"
[azure-blob-storage-doc]: ./connectors-create-api-azureblobstorage.md "Manage files in your blob container with Azure Blob storage connector"
[azure-cosmos-db-doc]: ./connectors-create-api-cosmos-db.md "Connect to Azure Cosmos DB so that you can access and manage Azure Cosmos DB documents"
[azure-event-hubs-doc]: ./connectors-create-api-azure-event-hubs.md "Connect to Azure Event Hubs so that you can receive and send events between logic apps and Event Hubs"
[azure-functions-doc]: ../logic-apps/logic-apps-azure-functions.md "Integrate logic apps with Azure Functions"
[azure-service-bus-doc]: ./connectors-create-api-servicebus.md "Manage messages from Service Bus queues, topics, and topic subscriptions"
[batch-doc]: ../logic-apps/logic-apps-batch-process-send-receive-messages.md "Process messages in groups, or as batches"
[condition-doc]: ../logic-apps/logic-apps-control-flow-conditional-statement.md "Evaluate a condition and run different actions based on whether the condition is true or false"
[data-operations-doc]: ../logic-apps/logic-apps-perform-data-operations.md "Perform data operations such as filtering arrays or creating CSV and HTML tables"
[for-each-doc]: ../logic-apps/logic-apps-control-flow-loops.md#foreach-loop "Perform the same actions on every item in an array"
[http-doc]: ./connectors-native-http.md "Call HTTP or HTTPS endpoints from your logic apps"
[http-request-doc]: ./connectors-native-reqres.md "Receive HTTP requests in your logic apps"
[http-response-doc]: ./connectors-native-reqres.md "Respond to HTTP requests from your logic apps"
[http-swagger-doc]: ./connectors-native-http-swagger.md "Call REST endpoints from your logic apps"
[http-webhook-doc]: ./connectors-native-webhook.md "Wait for specific events from HTTP or HTTPS endpoints"
[ibm-db2-doc]: ./connectors-create-api-db2.md "Connect to IBM DB2 in the cloud or on-premises. Update a row, get a table, and more"
[ibm-mq-doc]: ./connectors-create-api-mq.md "Connect to IBM MQ on-premises or in Azure to send and receive messages"
[inline-code-doc]: ../logic-apps/logic-apps-add-run-inline-code.md "Add and run JavaScript code snippets from your logic apps"
[nested-logic-app-doc]: ../logic-apps/logic-apps-http-endpoint.md "Integrate logic apps with nested workflows"
[query-doc]: ../logic-apps/logic-apps-perform-data-operations.md#filter-array-action "Select and filter arrays with the Query action"
[schedule-doc]: ../logic-apps/concepts-schedule-automated-recurring-tasks-workflows.md "Run logic apps based a schedule"
[schedule-delay-doc]: ./connectors-native-delay.md "Delay running the next action"
[schedule-delay-until-doc]: ./connectors-native-delay.md "Delay running the next action"
[schedule-recurrence-doc]:  ./connectors-native-recurrence.md "Run logic apps on a recurring schedule"
[schedule-sliding-window-doc]: ./connectors-native-sliding-window.md "Run logic apps that need to handle data in contiguous chunks"
[scope-doc]: ../logic-apps/logic-apps-control-flow-run-steps-group-scopes.md "Organize actions into groups, which get their own status after the actions in group finish running"
[sftp-ssh-doc]: ./connectors-sftp-ssh.md "Connect to your SFTP account by using SSH. Upload, get, delete files, and more"
[sql-server-doc]: ./connectors-create-api-sqlazure.md "Connect to Azure SQL Database or SQL Server. Create, update, get, and delete entries in a SQL database table"
[switch-doc]: ../logic-apps/logic-apps-control-flow-switch-statement.md "Organize actions into cases, which are assigned unique values. Run only the case whose value matches the result from an expression, object, or token. If no matches exist, run the default case"
[terminate-doc]: ../logic-apps/logic-apps-workflow-actions-triggers.md#terminate-action "Stop or cancel an actively running workflow for your logic app"
[until-doc]: ../logic-apps/logic-apps-control-flow-loops.md#until-loop "Repeat actions until the specified condition is true or some state has changed"
[variables-doc]: ../logic-apps/logic-apps-create-variables-store-values.md "Perform operations with variables, such as initialize, set, increment, decrement, and append to string or array variable"

<!--Built-in integration account doc links-->
[flat-file-decode-doc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Learn about enterprise integration flat file"
[flat-file-encode-doc]:../logic-apps/logic-apps-enterprise-integration-flatfile.md "Learn about enterprise integration flat file"
[integration-account-doc]: ../logic-apps/logic-apps-enterprise-integration-metadata.md "Manage metadata for integration account artifacts"
[json-liquid-transform-doc]: ../logic-apps/logic-apps-enterprise-integration-liquid-transform.md "Transform JSON with Liquid templates"
[xml-transform-doc]: ../logic-apps/logic-apps-enterprise-integration-transform.md "Transform XML messages"
[xml-validate-doc]: ../logic-apps/logic-apps-enterprise-integration-xml-validation.md "Validate XML messages"
