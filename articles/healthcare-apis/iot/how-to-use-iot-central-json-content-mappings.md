---
title: IotCentralJsonPathContentTemplate mappings in IoT Connector Device mappings - Azure Healthcare APIs
description: This article describes how IotCentralJsonPathContent mappings with IoT Connector Device mappings templates. 
author: msjasteppe
ms.service: healthcare-apis
ms.subservice: fhir
ms.topic: how-to
ms.date: 11/22/2021
ms.author: jasteppe
---

# How to use IotCentralJsonPathContentTemplate mappings

> [!IMPORTANT]
> Azure Healthcare APIs is currently in PREVIEW. The [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) include additional legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

> [!TIP]
> Check out the [IoMT Connector Data Mapper](https://github.com/microsoft/iomt-fhir/tree/master/tools/data-mapper) tool for editing, testing, and troubleshooting IoT connector Device and FHIR destination mappings. Export mappings for uploading to IoT connector in the Azure portal or use with the [open-source version](https://github.com/microsoft/iomt-fhir) of IoT connector.

This article describes how to use IoTCentralJsonPathContentTemplate mappings with IoT connector Device mappings.

## IotCentralJsonPathContentTemplate

The IotCentralJsonPathContentTemplate also doesn't require DeviceIdExpression and TimestampExpression. It gets used when the messages being evaluated are sent through the [Export Data](../../iot-central/core/howto-export-data.md) feature of [Azure IoT Central](../../iot-central/core/overview-iot-central.md). 

If you're using Azure IoT Central's Data Export feature and custom properties in the message body for the device identity or measurement timestamp, you can still use the JsonPathContentTemplate.

> [!NOTE]
> When using `IotCentralJsonPathContentTemplate`, `TypeMatchExpression` should resolve to the entire message as a JToken. For more information, see the following examples:
 
### Examples

**Heart rate**

*Message*

```json
{
    "applicationId": "1dffa667-9bee-4f16-b243-25ad4151475e",
    "messageSource": "telemetry",
    "deviceId": "1vzb5ghlsg1",
    "schema": "default@v1",
    "templateId": "urn:qugj6vbw5:___qbj_27r",
    "enqueuedTime": "2020-08-05T22:26:55.455Z",
    "telemetry": {
        "Activity": "running",
        "BloodPressure": {
            "Diastolic": 7,
            "Systolic": 71
        },
        "BodyTemperature": 98.73447010562934,
        "HeartRate": 88,
        "HeartRateVariability": 17,
        "RespiratoryRate": 13
    },
    "enrichments": {
      "userSpecifiedKey": "sampleValue"
    },
    "messageProperties": {
      "messageProp": "value"
    }
}
```

*Template*

```json
{
    "templateType": "IotCentralJsonPathContent",
    "template": {
        "typeName": "heartrate",
        "typeMatchExpression": "$..[?(@telemetry.HeartRate)]",
        "values": [
            {
                "required": "true",
                "valueExpression": "$.telemetry.HeartRate",
                "valueName": "hr"
            }
        ]
    }
}
```

**Blood pressure**

*Message*

```json
{
    "applicationId": "1dffa667-9bee-4f16-b243-25ad4151475e",
    "messageSource": "telemetry",
    "deviceId": "1vzb5ghlsg1",
    "schema": "default@v1",
    "templateId": "urn:qugj6vbw5:___qbj_27r",
    "enqueuedTime": "2020-08-05T22:26:55.455Z",
    "telemetry": {
        "Activity": "running",
        "BloodPressure": {
            "Diastolic": 7,
            "Systolic": 71
        },
        "BodyTemperature": 98.73447010562934,
        "HeartRate": 88,
        "HeartRateVariability": 17,
        "RespiratoryRate": 13
    },
    "enrichments": {
      "userSpecifiedKey": "sampleValue"
    },
    "messageProperties": {
      "messageProp": "value"
    }
}
```

*Template*

```json
{
    "templateType": "IotCentralJsonPathContent",
    "template": {
        "typeName": "bloodPressure",
        "typeMatchExpression": "$..[?(@telemetry.BloodPressure.Diastolic && @telemetry.BloodPressure.Systolic)]",
        "values": [
            {
                "required": "true",
                "valueExpression": "$.telemetry.BloodPressure.Diastolic",
                "valueName": "bp_diastolic"
            },
            {
                "required": "true",
                "valueExpression": "$.telemetry.BloodPressure.Systolic",
                "valueName": "bp_systolic"
            }
        ]
    }
}
```

> [!TIP]
> See IoT connector [troubleshooting guide](./iot-troubleshoot-guide.md) for assistance fixing common errors and issues.

## Next steps

In this article, you learned how to use Device mappings. To learn how to use FHIR destination mappings, see

>[!div class="nextstepaction"]
>[How to use FHIR destination mappings](how-to-use-fhir-mappings.md)

(FHIR&#174;) is a registered trademark of [HL7](https://hl7.org/fhir/) and is used with the permission of HL7.
