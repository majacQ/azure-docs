---
title: Find error codes
description: Describes how to find error codes to troubleshoot Azure resources deployed with Azure Resource Manager templates (ARM templates) or Bicep files.
tags: top-support-issue
ms.topic: troubleshooting
ms.date: 11/04/2021
ms.custom: devx-track-azurepowershell
---

# Find error codes

When an Azure resource deployment fails using Azure Resource Manager templates (ARM templates) or Bicep files, and error code is received. This article describes how to find error codes so you can troubleshoot the problem. For more information about error codes, see [common deployment errors](common-deployment-errors.md).

## Error types

There are three types of errors that are related to a deployment:

- **Validation errors** occur before a deployment begins and are caused by syntax errors in your file. Your editor can identify these errors.
- **Preflight validation errors** occur when a deployment command is run but resources aren't deployed. These errors are found without starting the deployment. For example, if a parameter value is incorrect, the error is found in preflight validation.
- **Deployment errors** occur during the deployment process and can only be found by assessing the deployment's progress.

All types of errors return an error code that you use to troubleshoot the deployment. Validation and preflight errors are shown in the activity log but don't appear in your deployment history. A Bicep file with syntax errors doesn't compile into JSON and isn't shown in the activity log.

To identify syntax errors, you can use [Visual Studio Code](https://code.visualstudio.com) with the latest [Bicep extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-bicep) or [Azure Resource Manager Tools extension](https://marketplace.visualstudio.com/items?itemName=msazurermtools.azurerm-vscode-tools).

## Validation errors

Templates are validated during the deployment process and error codes are displayed. Before you run a deployment, you can run validation tests with Azure PowerShell or Azure CLI to identify validation and preflight errors.

# [Portal](#tab/azure-portal)

An ARM template can be deployed from the portal. If the template has syntax errors, you'll see a validation error when you try to run the deployment. For more information about portal deployments, see [deploy resources from custom template](../templates/deploy-portal.md#deploy-resources-from-custom-template).

The following example attempts to deploy a storage account and a validation error occurs.

:::image type="content" source="media/find-error-code/validation-error.png" alt-text="Screenshot of an Azure portal validation error.":::

Select the message for more details. The template has a syntax error with error code `InvalidTemplate`. The **Summary** shows an expression is missing a closing parenthesis.

:::image type="content" source="media/find-error-code/validation-details.png" alt-text="Screenshot of a validation error message that shows a syntax error.":::

# [PowerShell](#tab/azure-powershell)

To validate an ARM template before deployment run [Test-AzResourceGroupDeployment](/powershell/module/az.resources/test-azresourcegroupdeployment).

```azurepowershell
Test-AzResourceGroupDeployment `
  -ResourceGroupName examplegroup `
  -TemplateFile azuredeploy.json
```

The output displays error codes like `InvalidTemplateDeployment` or `AccountNameInvalid` that you can use to troubleshoot and fix the template.

For a Bicep file, the output for a syntax validation problem shows a parameter error.

```Output
Test-AzResourceGroupDeployment: Cannot retrieve the dynamic parameters for the cmdlet.
Cannot find path '/tmp/11111111-1111-1111-1111-111111111111/main.json' because it does not exist.
```

To get more troubleshooting information, use the Bicep [build](../bicep/bicep-cli.md) command. The output shows each error's line and column number in parentheses, and the error message.

```bicep
bicep build main.bicep
```

```Output
/azuredeploy.bicep(22,51) : Error BCP064: Found unexpected tokens in interpolated expression.
/azuredeploy.bicep(22,51) : Error BCP004: The string at this location is not terminated due to an
  unexpected new line character.
```

There are more PowerShell cmdlets available to validate deployment templates:

- [Test-AzDeployment](/powershell/module/az.resources/test-azdeployment) for subscription level deployments.
- [Test-AzManagementGroupDeployment](/powershell/module/az.resources/test-azmanagementgroupdeployment)
- [Test-AzTenantDeployment](/powershell/module/az.resources/test-aztenantdeployment)

# [Azure CLI](#tab/azure-cli)

To validate an ARM template before deployment, run [az deployment group validate](/cli/azure/deployment/group#az_deployment_group_validate).

```azurecli
az deployment group validate \
  --resource-group examplegroup \
  --template-file azuredeploy.json
```

The output displays error codes like `InvalidTemplateDeployment` or `AccountNameInvalid` that you can use to troubleshoot and fix the template.

For a Bicep file, the output shows each error's line and column number in parentheses, and the error message.

```azurecli
az deployment group validate \
  --resource-group examplegroup \
  --template-file main.bicep
```

```Output
/azuredeploy.bicep(22,51) : Error BCP064: Found unexpected tokens in interpolated expression.
/azuredeploy.bicep(22,51) : Error BCP004: The string at this location is not terminated due to an
  unexpected new line character.
```

There are more Azure CLI commands available to validate deployment templates:

- [az deployment sub validate](/cli/azure/deployment/sub#az_deployment_sub_validate)
- [az deployment mg validate](/cli/azure/deployment/mg#az_deployment_mg_validate)
- [az deployment tenant validate](/cli/azure/deployment/tenant#az_deployment_tenant_validate)

---

## Deployment errors

Several operations are processed to deploy an Azure resource. Deployment errors occur when an operation passes validation but fails during deployment. You can view messages about each deployment operation and each deployment for a resource group.

# [Portal](#tab/azure-portal)

To see messages about a deployment's operations, use the resource group's **Activity log**:

1. Sign in to [Azure portal](https://portal.azure.com).
1. Go to **Resource groups** and select the deployment's resource group name.
1. Select **Activity log**.
1. Use the filters to find an operation's error log.

    :::image type="content" source="./media/find-error-code/activity-log.png" alt-text="Screenshot of the resource group's activity log that highlights a failed deployment.":::

1. Select the error log to see the operation's details.

    :::image type="content" source="./media/find-error-code/activity-log-details.png" alt-text="Screenshot of the activity log details that shows a failed deployment's error message.":::

To view a deployment's result:

1. Go to the resource group.
1. Select **Settings** > **Deployments**.
1. Select **Error details** for the deployment.

    :::image type="content" source="media/find-error-code/deployment-error-details.png" alt-text="Screenshot of a resource group's link to error details for a failed deployment.":::

1. The error message and error code `NoRegisteredProviderFound` are shown.

    :::image type="content" source="media/find-error-code/deployment-error-summary.png" alt-text="Screenshot of a message that shows deployment error details.":::

# [PowerShell](#tab/azure-powershell)

To see a deployment's operations messages with PowerShell, use [Get-AzResourceGroupDeploymentOperation](/powershell/module/az.resources/get-azresourcegroupdeploymentoperation).

To show all the operations for a deployment:

```azurepowershell
Get-AzResourceGroupDeploymentOperation `
  -DeploymentName exampledeployment `
  -ResourceGroupName examplegroup
```

To specify a specific property type:

```azurepowershell
(Get-AzResourceGroupDeploymentOperation `
  -DeploymentName exampledeployment `
  -ResourceGroupName examplegroup).StatusCode
```

To get a deployment's result, use [Get-AzResourceGroupDeployment](/powershell/module/az.resources/get-azresourcegroupdeployment).

```azurepowershell
Get-AzResourceGroupDeployment `
  -DeploymentName exampledeployment `
  -ResourceGroupName examplegroup
```

# [Azure CLI](#tab/azure-cli)

To see a deployment's operations messages with Azure CLI, use [az deployment operation group list](/cli/azure/deployment/operation/group#az_deployment_operation_group_list).

To show all the operations for a deployment:

```azurecli
az deployment operation group list \
  --name exampledeployment \
  --resource-group examplegroup \
  --query "[*].properties"
```

To specify a specific property type:

```azurecli
az deployment operation group list \
  --name exampledeployment \
  --resource-group examplegroup \
  --query "[*].properties.statusCode"
```

To get a deployment's result, use [az deployment group show](/cli/azure/deployment/group#az_deployment_group_show).

```azurecli
az deployment group show \
  --resource-group examplegroup \
  --name exampledeployment
```

---

## Next steps

- [Common deployment errors](common-deployment-errors.md)
- [Enable debug logging](enable-debug-logging.md)
- [Create troubleshooting template](create-troubleshooting-template.md)
