---
title: 'Security admin rules in Azure Virtual Network Manager (Preview)'
description: Learn about what security admin rules are in Azure Virtual Network Manager.
author: duongau
ms.author: duau
ms.service: virtual-network-manager
ms.topic: conceptual
ms.date: 11/02/2021
ms.custom: template-concept, ignite-fall-2021
---

# Security admin rules in Azure Virtual Network Manager (Preview)

Azure Virtual Network Manager provides two different types of configurations you can deploy across your virtual networks, one of them being a *SecurityAdmin* configuration. A security admin configuration contains a set of rule collections. Each rule collection contains one or more security admin rules. You then associate the rule collection with the network groups that you want to apply the security admin rules to.

> [!IMPORTANT]
> Azure Virtual Network Manager is currently in public preview.
> This preview version is provided without a service level agreement, and it's not recommended for production workloads. Certain features might not be supported or might have constrained capabilities.
> For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

## Security admin rules

A security admin rule allows you to enforce security policy criteria that matches the conditions set. You can only define security administrative rules for resources within the scope of the Azure Virtual Network Manager instance. These security rules have a higher priority than network security group (NSG) rules and will get evaluated before NSG rules. Also note that security admin rules don't change your NSG rules. See the below illustration.

:::image type="content" source="./media/concept-security-admins/traffic-evaluation.png" alt-text="Diagram of how traffic is evaluated with security admin rules and NSG.":::

Security admin rules can be used to enforce security rules. For example, an administrator can deny all high-risk ports or protocol from the Internet with security admin rules because these security admin rules will be evaluated prior to all NSG rules.

> [!IMPORTANT]
> Some services have network intent policies to ensure the network traffic is working as needed for their services. When you use security admin rules, you could break the network intent policies created for those services. For example, creating a deny admin rule can block some traffic allowed by the *SQL managed instance* service, which is defined by their network intent policy. Make sure to review your environment before applying a security admin configuration. For more information, see [How can I explicitly allow SQLMI traffic before having deny rules](faq.md#how-can-i-explicitly-allow-sqlmi-traffic-before-having-deny-rules).

The following are fields you can define in a security admin rule:

## Required fields

### Priority

Security rule priority is determined by an integer between 0 and 99. The lower the value the higher the priority of the rule. For example, a deny rule with a priority of 10 override an allow rule with a priority of 20. 

### <a name = "action"></a>Action

You can define one of three actions for a security rule:

* **Allow**: Allows traffic on the specific port, protocol, and source/destination IP prefixes in the specified direction.
* **Deny**: Block traffic on the specified port, protocol, and source/destination IP prefixes in the specified direction.
* **Always allow**: Regardless of other rules with lower priority or user-defined NSGs, allow traffic on the specified port, protocol, and source/destination IP prefixes in the specified direction.

### Direction

You can specify the direction of traffic for which the rule applies. You can define either inbound or outbound.

### Protocol

Protocols currently supported with security admin rules are:

* TCP
* UDP
* ICMP
* ESP
* AH
* Any protocols

## Optional fields

### Source and destination types

* **IP addresses**: You can provide IPv4 or IPv6 addresses or blocks of address in CIDR notation. To list multiple IP address, separate each IP address with a comma.
* **Service Tag**: You can define specific service tags based on regions or a whole service. See [Available service tags](../virtual-network/service-tags-overview.md#available-service-tags), for the list of supported tags.

### Source and destination ports

You can define specific common ports to block from the source or to the destination. See below for a list of common TCP ports:

| Ports | Service name |
| ----- | ------------ |
| 20, 21 | FTP |
| 22 | SSH |
| 23 | Telnet |
| 25 | SMTP |
| 53 | DNS |
| 80 | HTTP |
| 443 | HTTPS |
| 3389 | RDP |

## Next steps 

Learn how to block network traffic with a [SecurityAdmin configuration](how-to-block-network-traffic-portal.md).
