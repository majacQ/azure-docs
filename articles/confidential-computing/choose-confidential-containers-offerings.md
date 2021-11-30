---
title: Choose container offerings for confidential computing
description: How to choose the right confidential container offerings to meet your security, isolation and developer needs.
author: agowdamsft
ms.service: container-service
ms.topic: conceptual
ms.date: 11/01/2021
ms.author: amgowda
ms.custom: ignite-fall-2021
---

# Choosing confidential container offerings

Azure confidential computing offers multiple types of confidential containers. You can use these containers to support data integrity and confidentiality, and code integrity.

Confidential containers also help with code protection through encryption. You can create hardware-based assurances and hardware root of trust. You can also lower your attack surface area with confidential containers.

## Enclaves confidential containers

You can deploy confidential containers with enclaves. This method of container deployments has the strongest security and compute isolation, with a lower Trusted Computing Base (TCB). Confidential containers based on Intel Software Guard Extensions (SGX) that run in the hardware-based Trusted Execution Environment (TEE) are available. These containers support lifting and shifting your existing container apps. Another option is to allow building custom apps with enclave awareness.

There are two programming and deployment models on Azure Kubernetes Service (AKS). 

**Unmodified containers** support higher programming languages on Intel SGX through the Azure Partner ecosystem of OSS projects. For more information, see the [unmodified containers deployment flow and samples](./confidential-containers.md).

**Enclave-aware containers** use a custom Intel SGX programming model. For more information, see the [the enclave-aware containers deployment flow and samples](./enclave-aware-containers.md). 

![Diagram of enclave confidential containers with Intel SGX, showing isolation and security boundaries.](./media/confidential-containers/confidential-container-intel-sgx.png)

## Learn more

- [Intel SGX Confidential Virtual Machines on Azure](./virtual-machine-solutions-sgx.md)
- [Confidential Containers on Azure](./confidential-containers.md)
