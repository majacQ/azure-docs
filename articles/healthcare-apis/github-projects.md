---
title: Related GitHub Projects for Azure Healthcare APIs
description: List all Open Source (GitHub) repositories
services: healthcare-apis
author: ginalee-dotcom
ms.service: healthcare-apis
ms.topic: reference
ms.date: 10/18/2021
ms.author: ginle
---
# GitHub Projects

We have many open-source projects on GitHub that provide you the source code and instructions to deploy services for various uses. You are always welcome to visit our GitHub repositories to learn and experiment with our features and products. 

## Healthcare APIs samples

* This repo contains [samples for Healthcare APIs](https://github.com/microsoft/healthcare-apis-samples), including Fast Healthcare Interoperability Resources (FHIR&#174;), DICOM, IoT connector, and data-related services.

## FHIR Server

* [microsoft/fhir-server](https://github.com/microsoft/fhir-server/): open-source FHIR Server,  which is the basis for FHIR service
* For information about the latest releases, see [Release notes](https://github.com/microsoft/fhir-server/releases)
* [microsoft/fhir-server-samples](https://github.com/microsoft/fhir-server-samples): a sample environment

## Data Conversion & Anonymization

#### FHIR Converter

* [microsoft/FHIR-Converter](https://github.com/microsoft/FHIR-Converter): a conversion utility to translate legacy data formats into FHIR
* Integrated with the FHIR service as well as FHIR server for Azure in the form of $convert-data operation
* Ongoing improvements in OSS, and continual integration to the FHIR servers
 
#### FHIR Converter - VS Code Extension

* [microsoft/FHIR-Tools-for-Anonymization](https://github.com/microsoft/FHIR-Tools-for-Anonymization): a set of tools for helping with data (in FHIR format) anonymization
* Integrated with the FHIR service as well as FHIR server for Azure in the form of ‘de-identified export’

#### FHIR Tools for Anonymization

* [microsoft/vscode-azurehealthcareapis-tools](https://github.com/microsoft/vscode-azurehealthcareapis-tools): a VS Code extension that contains a collection of tools to work with Azure Healthcare APIs
* Released to Visual Studio Marketplace
* Used for authoring Liquid templates to be used in the FHIR Converter

## IoT connector

#### Integration with IoT Hub and IoT Central

* [microsoft/iomt-fhir](https://github.com/microsoft/iomt-fhir): integration with IoT Hub or IoT Central to FHIR with data normalization and FHIR conversion of the normalized data
* Normalization: device data information is extracted into a common format for further processing
* FHIR Conversion: normalized and grouped data is mapped to FHIR. Observations are created or updated according to configured templates and linked to the device and patient.
* [Tools to help build the conversation map](https://github.com/microsoft/iomt-fhir/tree/master/tools/data-mapper): visualize the mapping configuration for normalizing the device input data and transform it to the FHIR resources. Developers can use this tool to edit and test the Device and FHIR destination mappings and export them for uploading to the IoT connector in the Azure portal.

#### HealthKit and FHIR Integration

* [microsoft/healthkit-on-fhir](https://github.com/microsoft/healthkit-on-fhir): a Swift library that automates the export of Apple HealthKit Data to a FHIR Server

>[!div class="nextstepaction"]
>[Overview of Azure Healthcare APIs](healthcare-apis-overview.md)

(FHIR&#174;) is a registered trademark of [HL7](https://hl7.org/fhir/) and is used with the permission of HL7. 