---
 title: include file
 description: include file
 services: iot-hub
 author: robinsh
 ms.service: iot-hub
 ms.topic: include
 ms.date: 10/21/2021
 ms.author: robinsh
 ms.custom: include file
---
<!-- put the ## header in the file that includes this file -->

In this section, you create a device identity in the identity registry in your IoT hub. A device cannot connect to a hub unless it has an entry in the identity registry. For more information, see the [IoT Hub developer guide](../articles/iot-hub/iot-hub-devguide-identity-registry.md#identity-registry-operations).

1. In your IoT hub navigation menu, open **Devices**, then select **Add Device** to add a device in your IoT hub.

    :::image type="content" source="./media/iot-hub-include-create-device/create-identity-portal-vs2019.png" alt-text="Screen capture that shows how to create a device identity in the portal" border="true":::

1. In **Create a device**, provide a name for your new device, such as **myDeviceId**, and select **Save**. This action creates a device identity for your IoT hub. Leave **Auto-generate keys** checked so that the primary and secondary keys will be generated automatically.

    :::image type="content" source="./media/iot-hub-include-create-device/create-a-device-vs2019.png" alt-text="Screen capture that shows how to add a new device" border="true":::

    [!INCLUDE [iot-hub-pii-note-naming-device](iot-hub-pii-note-naming-device.md)]

1. After the device is created, open the device from the list in the **Devices** pane. Copy the **Primary Connection String**. This connection string is used by device code to communicate with the hub.

    By default, the keys and connection strings are masked as they are sensitive information. If you click the eye icon, they are revealed. It is not necessary to reveal them to copy them with the copy button.

    :::image type="content" source="./media/iot-hub-include-create-device/device-details-vs2019.png" alt-text="Screen capture that shows the device connection string" border="true":::

> [!NOTE]
> The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub. It stores device IDs and keys to use as security credentials, and an enabled/disabled flag that you can use to disable access for an individual device. If your application needs to store other device-specific metadata, it should use an application-specific store. For more information, see [IoT Hub developer guide](../articles/iot-hub/iot-hub-devguide-identity-registry.md).
