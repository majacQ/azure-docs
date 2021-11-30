---
title: Declare resources in Bicep
description: Describes how to declare resources to deploy in Bicep.
author: mumian
ms.author: jgao
ms.topic: conceptual
ms.date: 11/12/2021
---

# Resource declaration in Bicep

This article describes the syntax you use to add a resource to your Bicep file.

## Declaration

Add a resource declaration by using the `resource` keyword. You set a symbolic name for the resource. The symbolic name isn't the same as the resource name. You use the symbolic name to reference the resource in other parts of your Bicep file.

```bicep
resource <symbolic-name> '<full-type-name>@<api-version>' = {
  <resource-properties>
}
```

So, a declaration for a storage account can start with:

```bicep
resource stg 'Microsoft.Storage/storageAccounts@2021-04-01' = {
  ...
}
```

Symbolic names are case-sensitive. They may contain letters, numbers, and underscores (`_`). They can't start with a number. A resource can't have the same name as a parameter, variable, or module.

For the available resource types and version, see [Bicep resource reference](/azure/templates/). Bicep doesn't support `apiProfile`, which is available in [Azure Resource Manager templates (ARM templates) JSON](../templates/syntax.md).

To conditionally deploy a resource, use the `if` syntax. For more information, see [Conditional deployment in Bicep](conditional-resource-deployment.md).

```bicep
resource <symbolic-name> '<full-type-name>@<api-version>' = if (condition) {
  <resource-properties>
}
```

To deploy more than one instance of a resource, use the `for` syntax. You can use the `batchSize` decorator to specify whether the instances are deployed serially or in parallel. For more information, see [Iterative loops in Bicep](loops.md).

```bicep
@batchSize(int) // optional decorator for serial deployment
resource <symbolic-name> '<full-type-name>@<api-version>' = [for <item> in <collection>: {
  <properties-to-repeat>
}]
```

You can also use the `for` syntax on the resource properties to create an array.

```bicep
resource <symbolic-name> '<full-type-name>@<api-version>' = {
  properties: {
    <array-property>: [for <item> in <collection>: <value-to-repeat>]
  }
}
```

## Resource name

Each resource has a name. When setting the resource name, pay attention to the [rules and restrictions for resource names](../management/resource-name-rules.md).

```bicep
resource stg 'Microsoft.Storage/storageAccounts@2019-06-01' = {
  name: 'examplestorage'
  ...
}
```

Typically, you'd set the name to a parameter so you can pass in different values during deployment.

```bicep
@minLength(3)
@maxLength(24)
param storageAccountName string

resource stg 'Microsoft.Storage/storageAccounts@2019-06-01' = {
  name: storageAccountName
  ...
}
```

## Location

Many resources require a location. You can determine if the resource needs a location either through intellisense or [template reference](/azure/templates/). The following example adds a location parameter that is used for the storage account.

```bicep
resource stg 'Microsoft.Storage/storageAccounts@2019-06-01' = {
  name: 'examplestorage'
  location: 'eastus'
  ...
}
```

Typically, you'd set location to a parameter so you can deploy to different locations.

```bicep
param location string = resourceGroup().location

resource stg 'Microsoft.Storage/storageAccounts@2019-06-01' = {
  name: 'examplestorage'
  location: location
  ...
}
```

Different resource types are supported in different locations. To get the supported locations for an Azure service, See [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).  To get the supported locations for a resource type, use Azure PowerShell or Azure CLI.

# [PowerShell](#tab/azure-powershell)

```azurepowershell-interactive
((Get-AzResourceProvider -ProviderNamespace Microsoft.Batch).ResourceTypes `
  | Where-Object ResourceTypeName -eq batchAccounts).Locations
```

# [Azure CLI](#tab/azure-cli)

```azurecli-interactive
az provider show \
  --namespace Microsoft.Batch \
  --query "resourceTypes[?resourceType=='batchAccounts'].locations | [0]" \
  --out table
```

---

## Tags

You can apply tags to a resource during deployment. Tags help you logically organize your deployed resources. For examples of the different ways you can specify the tags, see [ARM template tags](../management/tag-resources.md#arm-templates).

## Managed identities for Azure resources

Some resources support [managed identities for Azure resources](../../active-directory/managed-identities-azure-resources/overview.md). Those resources have an identity object at the root level of the resource declaration.

You can use either system-assigned or user-assigned identities.

The following example shows how to configure a system-assigned identity for an Azure Kubernetes Service cluster.

```bicep
resource aks 'Microsoft.ContainerService/managedClusters@2020-09-01' = {
  name: clusterName
  location: location
  tags: tags
  identity: {
    type: 'SystemAssigned'
  }
```

The next example shows how to configure a user-assigned identity for a virtual machine.

```bicep
param userAssignedIdentity string

resource vm 'Microsoft.Compute/virtualMachines@2020-06-01' = {
  name: vmName
  location: location
  identity: {
    type: 'UserAssigned'
    userAssignedIdentities: {
      '${userAssignedIdentity}': {}
    }
  }
```

## Resource-specific properties

The preceding properties are generic to most resource types. After setting those values, you need to set the properties that are specific to the resource type you're deploying.

Use intellisense or [Bicep resource reference](/azure/templates/) to determine which properties are available and which ones are required. The following example sets the remaining properties for a storage account.

```bicep
resource stg 'Microsoft.Storage/storageAccounts@2019-06-01' = {
  name: 'examplestorage'
  location: 'eastus'
  sku: {
    name: 'Standard_LRS'
    tier: 'Standard'
  }
  kind: 'StorageV2'
  properties: {
    accessTier: 'Hot'
  }
}
```

## Dependencies

When deploying resources, you may need to make sure some resources exist before other resources. For example, you need a logical SQL server before deploying a database. You establish this relationship by marking one resource as dependent on the other resource. Order of resource deployment can be influenced in two ways: [implicit dependency](#implicit-dependency) and [explicit dependency](#explicit-dependency)

Azure Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order. When resources aren't dependent on each other, Resource Manager deploys them in parallel. You only need to define dependencies for resources that are deployed in the same Bicep file.

### Implicit dependency

An implicit dependency is created when one resource declaration references another resource in the same deployment. For example, *dnsZone* is referenced by the second resource definition in the following example:

```bicep
resource dnsZone 'Microsoft.Network/dnszones@2018-05-01' = {
  name: 'myZone'
  location: 'global'
}

resource otherResource 'Microsoft.Example/examples@2020-06-01' = {
  name: 'exampleResource'
  properties: {
    // get read-only DNS zone property
    nameServers: dnsZone.properties.nameServers
  }
}
```

A nested resource also has an implicit dependency on its containing resource.

```bicep
resource myParent 'My.Rp/parentType@2020-01-01' = {
  name: 'myParent'
  location: 'West US'

  // depends on 'myParent' implicitly
  resource myChild 'childType' = {
    name: 'myChild'
  }
}
```

When an implicit dependency exists, **don't add an explicit dependency**.

For more information about nested resources, see [Set name and type for child resources in Bicep](./child-resource-name-type.md).

### Explicit dependency

An explicit dependency is declared with the `dependsOn` property. The property accepts an array of resource identifiers, so you can specify more than one dependency.

The following example shows a DNS zone named `otherZone` that depends on a DNS zone named `dnsZone`:

```bicep
resource dnsZone 'Microsoft.Network/dnszones@2018-05-01' = {
  name: 'demoeZone1'
  location: 'global'
}

resource otherZone 'Microsoft.Network/dnszones@2018-05-01' = {
  name: 'demoZone2'
  location: 'global'
  dependsOn: [
    dnsZone
  ]
}
```

While you may be inclined to use `dependsOn` to map relationships between your resources, it's important to understand why you're doing it. For example, to document how resources are interconnected, `dependsOn` isn't the right approach. You can't query which resources were defined in the `dependsOn` element after deployment. Setting unnecessary dependencies slows deployment time because Resource Manager can't deploy those resources in parallel.

Even though explicit dependencies are sometimes required, the need for them is rare. In most cases, you can use a symbolic name to imply the dependency between resources. If you find yourself setting explicit dependencies, you should consider if there's a way to remove it.

### Visualize dependencies

Visual Studio Code provides a tool for visualizing the dependencies. Open a Bicep file in Visual Studio Code, and then select the visualizer button on the upper left corner.  The following screenshot shows the dependencies of a virtual machine.

:::image type="content" source="./media/resource-declaration/bicep-resource-visualizer.png" alt-text="Screenshot of Visual Studio Code Bicep resource visualizer":::

## Existing resources

To reference a resource that's outside of the current Bicep file, use the `existing` keyword in a resource declaration.

When using the `existing` keyword, provide the `name` of the resource. The following example gets an existing storage account in the same resource group as the current deployment.

```bicep
resource stg 'Microsoft.Storage/storageAccounts@2019-06-01' existing = {
  name: 'examplestorage'
}

output blobEndpoint string = stg.properties.primaryEndpoints.blob
```

Optionally, you can set the `scope` property to access a resource in a different scope. The following example references an existing storage account in a different resource group.

```bicep
resource stg 'Microsoft.Storage/storageAccounts@2019-06-01' existing = {
  name: 'examplestorage'
  scope: resourceGroup(exampleRG)
}

output blobEndpoint string = stg.properties.primaryEndpoints.blob
```

If you attempt to reference a resource that doesn't exist, you get the `NotFound` error and your deployment fails.

For more information about setting the scope, see [Scope functions for Bicep](bicep-functions-scope.md).

The preceding examples don't deploy the storage account. Instead, you can access properties on the existing resource by using the symbolic name.

## Next steps

- To conditionally deploy a resource, see [Conditional deployment in Bicep](./conditional-resource-deployment.md).
