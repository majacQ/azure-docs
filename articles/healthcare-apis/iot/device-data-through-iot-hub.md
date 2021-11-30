---
title: Receive device data through Azure IoT Hub - Azure Healthcare APIs
description: In this tutorial, you'll learn how to enable device data routing from IoT Hub into FHIR service through IoT connector.
services: healthcare-apis
author: msjasteppe
ms.service: healthcare-apis
ms.subservice: iomt
ms.topic: tutorial 
ms.date: 11/16/2021
ms.author: jasteppe
---

# Tutorial: Receive device data through Azure IoT Hub

> [!IMPORTANT]
> Azure Healthcare APIs is currently in PREVIEW. The [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

IoT connector provides the capability to collect and ingest health data from various IoT health related or medical devices into the Fast Healthcare Interoperability Resources (FHIR®) service. IoT connector is interoperable and responsive with devices created and managed through Azure IoT Hub for enhanced workflows and ease of use. This tutorial provides the procedure to connect and route device data from Azure IoT Hub to IoT connector.

## Prerequisites

- An active Azure subscription - [Create one for free](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)
- FHIR service resource with at least one IoT connector - [Deploy IoT connector using Azure portal](deploy-iot-connector-in-azure.md)
- Azure IoT Hub resource connected with real or simulated device(s) - [Create an IoT hub using the Azure portal](../../iot-develop/quickstart-send-telemetry-iot-hub.md?pivots=programming-language-csharp)

> [!TIP]
> If you are using an Azure IoT Hub simulated device application, feel free to pick the application of your choice amongst different supported languages and systems.

## Get connection string for IoT connector

Azure IoT Hub requires a connection string to securely connect with your IoT connector. Create a new connection string for your IoT connector as described in [Generate a connection string](../azure-api-for-fhir/iot-fhir-portal-quickstart.md#generate-a-connection-string). Safe this connection string to be used in the next step.

IoT connector uses an Azure Event Hub instance under the hood to receive device messages. The connection string created above is basically the connection string to this underlying Event Hub.

## Connect Azure IoT Hub with IoT connector

Azure IoT Hub supports a feature called [message routing](../../iot-hub/iot-hub-devguide-messages-d2c.md) that provides capability to send device data to various Azure services like Event Hub, Storage Account, and Service Bus. IoT connector uses this feature to connect and send device data from Azure IoT Hub to its Event Hub endpoint.

> [!NOTE] 
> At this time you can only use PowerShell or CLI command to [create message routing](../../iot-hub/tutorial-routing.md) because IoT connector's Event Hub is not hosted on the customer subscription, hence it won't be visible to you through the Azure portal. Though, once the message route objects are added using PowerShell or CLI, they are visible on the Azure portal and can be managed from there.

Setting up a message routing consists of two steps.

### Add an endpoint

This step defines an endpoint to which the IoT Hub would route the data. Create this endpoint using either [Add-AzIotHubRoutingEndpoint](/powershell/module/az.iothub/Add-AzIoTHubRoute) PowerShell command or [az iot hub routing-endpoint create](/cli/azure/iot/hub/route#az_iot_hub_route_create) CLI command, based on your preference.

Here is the list of parameters to use with the command to create an endpoint:

|PowerShell Parameter|CLI Parameter|Description|
|---|---|---|
|ResourceGroupName|resource-group|Resource group name of your IoT Hub resource.|
|Name|hub-name|Name of your IoT Hub resource.|
|EndpointName|endpoint-name|Use a name that you would like to assign to the endpoint being created.|
|EndpointType|endpoint-type|Type of endpoint that IoT Hub needs to connect with. Use literal value of "EventHub" for PowerShell and "eventhub" for CLI.|
|EndpointResourceGroup|endpoint-resource-group|Resource group name for your IoT connector's FHIR service resource. You can get this value from the Overview page of FHIR service.|
|EndpointSubscriptionID|endpoint-subscription-id|Subscription ID for your IoT connector's FHIR service resource. You can get this value from the Overview page of FHIR service.|
|ConnectionString|connection-string|Connection string to your IoT connector. Use the value you obtained in the previous step.|

### Add a message route
This step defines a message route using the endpoint created above. Create a route using either [Add-AzIotHubRoute](/powershell/module/az.iothub/Add-AzIoTHubRoute) PowerShell command or [az iot hub route create](/cli/azure/iot/hub/route) CLI command, based on your preference.

Here is the list of parameters to use with the command to add a message route:

|PowerShell Parameter|CLI Parameter|Description|
|---|---|---|
|ResourceGroupName|g|Resource group name of your IoT Hub resource.|
|Name|hub-name|Name of your IoT Hub resource.|
|EndpointName|endpoint-name|Name of the endpoint you have created above.|
|RouteName|route-name|A name you want to assign to message route being created.|
|Source|source-type|Type of data to send to the endpoint. Use literal value of "DeviceMessages" for PowerShell and "devicemessages" for CLI.|

## Send device message to Azure IoT Hub

Use your device (real or simulated) to send the sample heart rate message shown below to Azure IoT Hub. This message will get routed to IoT connector, where the message will be transformed into a FHIR Observation resource and stored into the FHIR service.

```json
{
  "HeartRate": 80,
  "RespiratoryRate": 12,
  "HeartRateVariability": 64,
  "BodyTemperature": 99.08839032397609,
  "BloodPressure": {
    "Systolic": 23,
    "Diastolic": 34
  },
  "Activity": "walking"
}
```
> [!IMPORTANT]
> Make sure to send the device message that conforms to the [mapping templates](how-to-use-fhir-mappings.md) configured with your IoT connector.

## View device data in FHIR service

You can view the FHIR Observation resource(s) created by IoT connector on the FHIR service using Postman. For information, see [Access the FHIR service using Postman](./../use-postman.md), and make a `GET` request to `https://your-fhir-server-url/Observation?code=http://loinc.org|8867-4` to view Observation FHIR resources with heart rate value submitted in the above sample message.

> [!TIP]
> Ensure that your user has appropriate access to FHIR service data plane. Use [Azure role-based access control (Azure RBAC)](../azure-api-for-fhir/configure-azure-rbac.md) to assign required data plane roles.

## Next steps

In this tutorial, you set up Azure IoT Hub to route device data to IoT connector. Select from below next steps to learn more about IoT connector:

Understand different stages of data flow within IoT connector.

>[!div class="nextstepaction"]
>[IoT connector data flow](iot-data-flow.md)

(FHIR&#174;) is a registered trademark of HL7 and is used with the permission of HL7.
