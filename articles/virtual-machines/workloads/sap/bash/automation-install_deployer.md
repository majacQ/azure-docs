---
online version: https://github.com/Azure/sap-hana
schema: 2.0.0
author: kimforss
ms.author: kimforss
ms.reviewer: kimforss
ms.date: 10/21/2021
ms.topic: reference
ms.service: virtual-machines-sap
title: install_deployer.sh
description: Bootstrap a new deployer in the control plane using a shell script.
---

# install_deployer.sh

## Synopsis
You can use the script `install_deployer.sh` to set up a new deployer VM in the control plane.

## Syntax

```bash
install_deployer.sh [ --parameterfile ] <String> 
[-i | --auto-approve]
```

## Description
The script `install_deployer.sh` sets up a new deployer in the control plane.

The deployer VM has installation of Ansible and Terraform. You use the deployer VM to deploy the SAP artifacts.


## Examples

### Example 1

```bash
install_deployer.sh --parameterfile MGMT-WEEU-DEP00-INFRASTRUCTURE.tfvars
```

## Parameters

### `--parameterfile`
Sets the parameter file for the deployer VM. For more information, see [Configuring the control plane](../automation-configure-control-plane.md#deployer).

```yaml
Type: String
Aliases: `-p`

Required: True
```

### `--auto-approve`
Enables silent deployment.

```yaml
Type: SwitchParameter
Aliases: `-i`

Required: False
```

### `--help`
Shows help for the script.

```yaml
Type: SwitchParameter
Aliases: `-h`

Required: False
```


## Notes
v0.9 - Initial version


Copyright (c) Microsoft Corporation.
Licensed under the MIT license.

## Related links

[GitHub repository: SAP deployment automation framework](https://github.com/Azure/sap-automation)
