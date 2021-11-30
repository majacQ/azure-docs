---
title: IoT connector Microsoft Power BI - Azure Healthcare APIs
description: In this article, you'll learn how to use IoT connector and Power BI 
author: msjasteppe
ms.service: healthcare-apis
ms.subservice: fhir
ms.topic: conceptual
ms.date: 11/10/2021
ms.author: jasteppe
---

# IoT connector and Microsoft Power BI

In this article, we'll explore using IoT connector and Microsoft Power Business Intelligence (BI).

## IoT connector and Power BI reference architecture

The reference architecture below shows the basic components of using Microsoft cloud services to enable Power BI on top of Internet of Medical Things (IoMT) and Fast Healthcare Interoperability Resources (FHIR&#174;) data. 

You can even embed Power BI dashboards inside the Microsoft Teams client to further enhance care team coordination. For more information on embedding Power BI in Teams, visit [here](/power-bi/collaborate-share/service-embed-report-microsoft-teams).

:::image type="content" source="media/iot-concepts/iot-connector-power-bi.png" alt-text="Screenshot of IoT connector and Power BI." lightbox="media/iot-concepts/iot-connector-power-bi.png":::

IoT connector can ingest IoT data from most IoT devices or gateways whatever the location, data center, or cloud. 

We do encourage the use of Azure IoT services to assist with device/gateway connectivity.

:::image type="content" source="media/iot-concepts/iot-connector-iot-hub-power-bi.png" alt-text="Screenshot of IoT connector, IoT Hub, and Power BI." lightbox="media/iot-concepts/iot-connector-iot-hub-power-bi.png":::

For some solutions, Azure IoT Central can be used in place of Azure IoT Hub.

Azure IoT Edge can be used in with IoT Hub to create an on-premise endpoint for devices and/or in-device connectivity.

:::image type="content" source="media/iot-concepts/iot-connector-iot-edge-power-bi.png" alt-text="Screenshot of IoT connector, IoT Hub, IoT Edge, and Power BI." lightbox="media/iot-concepts/iot-connector-iot-edge-power-bi.png":::

## Next steps

In this article, you've learned about IoT connector and Power BI integration. For an overview of IoT connector, see

>[!div class="nextstepaction"]
>[IoT connector overview](iot-connector-overview.md)

(FHIR&#174;) is a registered trademark of [HL7](https://hl7.org/fhir/) and is used with the permission of HL7.
