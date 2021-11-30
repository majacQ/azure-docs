---
title: What is Spatial Analysis?
titleSuffix: Azure Cognitive Services
description: This document explains the basic concepts and features of the Azure Spatial Analysis container.
services: cognitive-services
author: nitinme
manager: nitinme
ms.author: nitinme
ms.service: cognitive-services
ms.subservice: computer-vision
ms.topic: overview
ms.date: 10/06/2021
ms.custom: contperf-fy22q2
---

# What is Spatial Analysis?

You can use Computer Vision Spatial Analysis to ingest streaming video from cameras, extract insights, and generate events to be used by other systems. The service detects the presence and movements of people in video. It can do things like count the number of people entering a space or measure compliance with face mask and social distancing guidelines. By processing video streams from physical spaces, you are able to learn how people use them and maximize the space's value to your organization. 

<!--This documentation contains the following types of articles:
* The [quickstarts](./quickstarts-sdk/analyze-image-client-library.md) are step-by-step instructions that let you make calls to the service and get results in a short period of time. 
* The [how-to guides](./Vision-API-How-to-Topics/HowToCallVisionAPI.md) contain instructions for using the service in more specific or customized ways.
* The [conceptual articles](tbd) provide in-depth explanations of the service's functionality and features.
* The [tutorials](./tutorials/storage-lab-tutorial.md) are longer guides that show you how to use this service as a component in broader business solutions.-->

## What it does
Spatial Analysis ingests video then detects people in the video. After people are detected, the system tracks the people as they move around over time then generates events as people interact with regions of interest. All operations give insights from a single camera's field of view. 

### People counting
This operation counts the number of people in a specific zone over time using the PersonCount operation. It generates an independent count for each frame processed without attempting to track people across frames. This operation can be used to estimate the number of people in a space or generate an alert when a person appears.

![Spatial Analysis counts the number of people in the cameras field of view](https://user-images.githubusercontent.com/11428131/139924111-58637f2e-f2f6-42d8-8812-ab42fece92b4.gif)

### Entrance Counting
This feature monitors how long people stay in an area or when they enter through a doorway. This monitoring can be done using the PersonCrossingPolygon or PersonCrossingLine operations. In retail scenarios, these operations can be used to measure wait times for a checkout line or engagement at a display. Also, these operations could measure foot traffic in a lobby or a specific floor in other commercial building scenarios.

![Spatial Analysis measures dwelltime in checkout queue](https://user-images.githubusercontent.com/11428131/137016574-0d180d9b-fb9a-42a9-94b7-fbc0dbc18560.gif)

### Social distancing and facemask detection 
This feature analyzes how well people follow social distancing requirements in a space. Using the PersonDistance operation, the system automatically calibrates itself as people walk around in the space. Then it identifies when people violate a specific distance threshold (6 ft. or 10 ft.).

![Spatial Analysis visualizes social distance violation events showing lines between people showing the distance](https://user-images.githubusercontent.com/11428131/139924062-b5e10c0f-3cf8-4ff1-bb58-478571c022d7.gif)

Spatial Analysis can also be configured to detect if a person is wearing a protective face covering such as a mask. A mask classifier can be enabled for the PersonCount, PersonCrossingLine, and PersonCrossingPolygon operations by configuring the `ENABLE_FACE_MASK_CLASSIFIER` parameter.

![Spatial Analysis classifies whether people have facemasks in an elevator](https://user-images.githubusercontent.com/11428131/137015842-ce524f52-3ac4-4e42-9067-25d19b395803.png)

## Get started

Follow the [quickstart](spatial-analysis-container.md) to set up the Spatial Analysis container and begin analyzing video.

## Responsible use of Spatial Analysis technology

To learn how to use Spatial Analysis technology responsibly, see the [transparency note](/legal/cognitive-services/computer-vision/transparency-note-spatial-analysis?context=%2fazure%2fcognitive-services%2fComputer-vision%2fcontext%2fcontext). Microsoft's transparency notes help you understand how our AI technology works and the choices system owners can make that influence system performance and behavior. They focus on the importance of thinking about the whole system including the technology, people, and environment.

## Next steps

> [!div class="nextstepaction"]
> [Quickstart: Spatial Analysis container](spatial-analysis-container.md)
