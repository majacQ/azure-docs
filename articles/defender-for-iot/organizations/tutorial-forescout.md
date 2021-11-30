---
title: Integrate Forescout with Microsoft Defender for IoT
description: In this tutorial, you will learn how to integrate Microsoft Defender for IoT with Forescout.
author: ElazarK
ms.author: v-ekrieg
ms.topic: tutorial
ms.date: 11/09/2021
ms.custom: template-tutorial
---

# Tutorial: Integrate Forescout with Microsoft Defender for IoT

> [!Note]
> References to CyberX refer to Microsoft Defender for IoT.

This tutorial will help you learn how to integrate Forescout with Microsoft Defender for IoT.

Microsoft Defender for IoT delivers an ICS, and IoT cybersecurity platform. Defender for IoT is the only platform with ICS aware threat analytics, and machine learning. Defender for IoT provides:

- Immediate insights about ICS the device landscape with an extensive range of details about attributes.

- ICS-aware deep embedded knowledge of OT protocols, devices, applications, and their behaviors.

- Immediate insights into vulnerabilities, and known zero-day threats.

- An automated ICS threat modeling technology to predict the most likely paths of targeted ICS attacks via proprietary analytics.

The Forescout integration helps reduce the time required for industrial and critical infrastructure organizations to detect, investigate, and act on cyber threats.

- Use Microsoft Defender for IoT OT device intelligence to close the security cycle by triggering Forescout policy actions. For example, you can automatically send alert email to SOC administrators when specific protocols are detected, or when firmware details change.

- Correlate Defender for IoT information with other *Forescout eyeExtended* modules that oversee monitoring, incident management, and device control.

The Defender for IoT integration with the Forescout platform provides centralized visibility, monitoring, and control for the IoT, and OT landscape. These bridged platforms enable automated device visibility, management to ICS devices and, siloed workflows. The integration provides SOC analysts with multilevel visibility into OT protocols deployed in industrial environments. Information becomes available such as firmware, device types, operating systems, and risk analysis scores based on proprietary Microsoft Defender for IoT technologies.

In this tutorial, you learn how to:

> [!div class="checklist"]
> - Generate an access token
> - Configure the Forescout platform
> - Verify communication
> - View device attributes in Forescout
> - Create Microsoft Defender for IoT policies in Forescout

If you do not already have an Azure account, you can [create your Azure free account today](https://azure.microsoft.com/free/).

## Prerequisites

- Microsoft Defender for IoT version 2.4 or above

- Forescout version 8.0 or above

- A license for the Forescout eyeExtend module for the Microsoft Defender for IoT Platform.

## Generate an access token

Access tokens allow external systems to access data discovered by Defender for IoT. Access tokens allow that data to be used for external REST APIs,  and over SSL connections. You can generate access tokens in order to access the Microsoft Defender for IoT REST API.

To ensure communication from Defender for IoT to Forescout, you must generate an access token in Defender for IoT.

**To generate an access token**:

1. Sign in to the Defender for IoT sensor that will be queried by Forescout.

1. Select **System Settings** > **Access Tokens** from the **General** section.

1. Select **Generate new token**.

    :::image type="content" source="media/tutorial-forescout/generate-access-tokens-screen.png" alt-text="Screenshot of the access token generation screen.":::

1. Enter a token description in the **New access token** dialog box.

   :::image type="content" source="media/tutorial-forescout/new-forescout-token.png" alt-text="New access token":::

1. Select **Next**. The token is then displayed in the dialog box.

   > [!NOTE]
   > Record the token in a safe place. You will need it when you configure the Forescout Platform.

1. Select **Finish**.

   :::image type="content" source="media/tutorial-forescout/forescout-access-token-added-successfully.png" alt-text="Finish adding token":::

## Configure the Forescout platform

You can now configure the Forescout platform to communicate with a Defender for IoT sensor.

**To configure the Forescout platform**:

1. On the Forescout platform, search for,and install **the Forescout eyeExtend module for CyberX**.

1. Sign in to the CounterACT console.

1. From the Tools menu, select **Options**.

1. Navigate to **Modules** > **CyberX Platform**.

   :::image type="content" source="media/tutorial-forescout/settings-for-module.png" alt-text="Microsoft Defender for IoT module settings":::

1. In the Server Address field, enter the IP address of the Defender for IoT sensor that will be queried by the Forescout appliance.

1. In the Access Token field, enter the access token that was generated earlier.

1. Select **Apply**.

### Change sensors in Forescout

To make the Forescout platform, communicate with a different sensor, the configuration within Forescout has to be changed.

**To change sensors in Forescout**:

1. Create a new access token in the relevant Defender for IoT sensor.

1. Navigate to **Forescout Modules** > **CyberX Platform**.

1. Delete the information displayed in both fields.

1. Sign in to the new Defender for IoT sensor and [generate a new access token](#generate-an-access-token).

1. In the Server Address field, enter the new IP address of the Defender for IoT sensor that will be queried by the Forescout appliance.

1. In the Access Token field, enter the new access token.

1. Select **Apply**.

## Verify communication

Once the connection has been configured, you will need to confirm that the two platforms are communicating.

**To confirm the two platforms are communicating**:

1. Sign in to the Defender for IoT sensor.

1. Navigate to **System Settings** > **Access Tokens**.

The Used field will alert you if the connection between the sensor and the Forescout appliance is not working. If **N/A** is displayed, the connection is not working. If **Used** is displayed, it will indicate the last time an external call with this token was received.

:::image type="content" source="media/tutorial-forescout/forescout-access-token-added-successfully.png" alt-text="Verifies the token was received":::

## View device attributes in Forescout

By integrating Defender for IoT with Forescout, you will be able to view different device's attributes that were detected by Defender for IoT, in the Forescout application.

The following table lists all of the attributes that are visible through the Forescout application:

| Item | Description |
|--|--|
| **Authorized by Microsoft Defender for IoT** | A device detected on your network by Defender for IoT during the network learning period. |
| **Firmware** | The firmware details of the device. For example, model, and version details. |
| **Name** | The name of the device. |
| **Operating System** | The operating system of the device. |
| **Type** | The type of device. For example, a PLC, Historian or Engineering Station. |
| **Vendor** | The vendor of the device. For example, Rockwell Automation. |
| **Risk level** | The risk level calculated by Defender for IoT. |
| **Protocols** | The protocols detected in the traffic generated by the device. |

**To view a device's attributes**:

1. Sign in to the Forescout platform and then navigate to the **Asset Inventory**.

   :::image type="content" source="media/tutorial-forescout/device-firmware-attributes-in-forescout.png" alt-text="View the firmware attributes.":::

1. Select the **CyberX Platform**.

   :::image type="content" source="media/tutorial-forescout/vendor-attributes-in-forescout.png" alt-text="View the vendors attributes.":::

### View more details

After viewing a device's attributes, you can see more details for each device such as Forescout compliance and policy information.

**To view additional details**:

1. Sign in to the Forescout platform and then navigate to the **Asset Inventory**.

1. Select the **CyberX Platform**.

1. From the Device Inventory Hosts section, right-click on a device. The host details dialog box opens with additional information.

## Create Microsoft Defender for IoT policies in Forescout

Forescout policies can be used to automate control and management of devices detected by Defender for IoT. For example,

- Automatically email the SOC administrators when specific firmware versions are detected.

- Add specific Defender for IoT detected devices to a Forescout group for further handling in incident and security workflows, for example with other SIEM integrations.

You can create custom policies in Forescout using Defender for IoT conditional properties.

**To access Defender for IoT properties**:

1. Navigate to **Policy Conditions** > **Properties Tree**.

1. In the Properties Tree, expand the CyberX Platform folder. The Defender for IoT following properties are available.

:::image type="content" source="media/tutorial-forescout/forescout-property-tree.png" alt-text="Properties":::

## Clean up resources

There are no resources to clean up.

## Next steps

In this tutorial, you learned how to get started with the Forescout integration. Continue on to learn about our [Palo Alto integration](./tutorial-palo-alto.md).

> [!div class="nextstepaction"]
> [Next steps button](./tutorial-palo-alto.md)
