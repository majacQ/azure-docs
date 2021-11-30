---
title: Delete a VM and attached resources
description: Learn how to delete a VM and the resources attached to the VM.
author: cynthn
ms.service: virtual-machines
ms.subservice: 
ms.topic: how-to
ms.workload: infrastructure
ms.date: 11/19/2021
ms.author: cynthn
ms.custom: template-how-to 

---

# Delete a VM and attached resources

By default, when you delete a VM it only deletes the VM resource, not the networking and disk resources. You can change this default behavior when you create a VM, or update an existing VM, to delete specific resources along with the VM. 


## Set delete options when creating a VM

### [CLI](#tab/cli2)

To specify what happens to the attached resources when you delete a VM, use the `delete-option` parameters. Each can be set to either `Delete`, which permanently deletes the resource when you delete the VM, or `Detach` which only detaches the resource and leaves it in Azure so it can be reused later. Resources that you `Detach`, like disks, will continue to incur charges as applicable.

- `--os-disk-delete-option` - OS disk.
- `--data-disk-delete-option` - data disk.
- `--nic-delete-option` - NIC.

In this example, we create a VM and set the OS disk and NIC to be deleted when we delete the VM.

```azurecli-interactive
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --public-ip-sku Standard \
    --nic-delete-option delete \
    --os-disk-delete-option delete \
    --admin-username azureuser \
    --generate-ssh-keys
```

### [PowerShell](#tab/powershell2)

To specify what happens to the attached resources when you delete a VM, use the `DeleteOption` parameters. Each can be set to either `Delete`, which permanently deletes the resource when you delete the VM, or `Detach` which only detaches the resource and leaves it in Azure so it can be reused later. Resources that you `Detach`, like disks, will continue to incur charges as applicable.

The `DeleteOption` parameters are:
- `-OSDiskDeleteOption` - OS disk.
- `-DataDiskDeleteOption` - data disk.
- `-NetworkInterfaceDeleteOption` - NIC.

In this example, we create a VM and set the OS disk and NIC to be deleted when we delete the VM.

```azurepowershell
New-AzVm `
    -ResourceGroupName "myResourceGroup" `
    -Name "myVM" `
    -OSDiskDeleteOption Delete `
    -NetworkInterfaceDeleteOption Delete `
    -Location "East US" `
    -VirtualNetworkName "myVnet" `
    -SubnetName "mySubnet" `
    -SecurityGroupName "myNetworkSecurityGroup" `
    -PublicIpAddressName "myPublicIpAddress" 
```


### [REST](#tab/rest2)

This example shows how to set the data disk and NIC to be deleted when the VM is deleted.

```rest
PUT 
https://management.azure.com/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachines/myVM?api-version=xx  
{ 
"storageProfile": { 
    "dataDisks": [ 
        { "diskSizeGB": 1023, 
          "name": "myVMdatadisk", 
          "createOption": "Empty", 
          "lun": 0, 
          "deleteOption": “Delete” 
       }    ] 
},  
"networkProfile": { 
      "networkInterfaces": [ 
        { "id": "/subscriptions/.../Microsoft.Network/networkInterfaces/myNIC", 
          "properties": { 
            "primary": true, 
  	    "deleteOption": “Delete” 
          }        } 
      ]  
} 
```


You can also set this property for a Public IP associated with a NIC, so that the Public IP is automatically deleted when the NIC gets deleted.

```rest
PUT https://management.azure.com/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Network/networkInterfaces/test-nic?api-version=xx 
{ 

  "properties": { 

    "enableAcceleratedNetworking": true, 

    "ipConfigurations": [ 

      { 

        "name": "ipconfig1", 

        "properties": { 

          "publicIPAddress": { 

            "id": "/subscriptions/../publicIPAddresses/test-ip", 

          "properties": { 
            “deleteOption”: “Delete” 
            } 
          }, 

          "subnet": { 

            "id": "/subscriptions/../virtualNetworks/rg1-vnet/subnets/default" 

          } 

        } 

      } 

    ] 

  }, 

  "location": "eastus" 

}
```
---


## Update the delete behavior on an existing VM

You can use the Azure REST API to patch a VM to change the behavior when you delete a VM. The following example updates the VM to delete the NIC, OS  disk, and data disk when the VM is deleted.


```rest
PATCH https://management.azure.com/subscriptions/subID/resourceGroups/resourcegroup/providers/Microsoft.Compute/virtualMachines/testvm?api-version=2021-07-01 


{ 
    "properties": {        
        "hardwareProfile": { 
            "vmSize": "Standard_D2s_v3" 
        }, 
        "storageProfile": { 
            "imageReference": { 
                "publisher": "MicrosoftWindowsServer", 
                "offer": "WindowsServer", 
                "sku": "2019-Datacenter", 
                "version": "latest", 
                "exactVersion": "17763.3124.2111130129" 
            }, 
            "osDisk": { 
                "osType": "Windows", 
                "name": "OsDisk_1", 
                "createOption": "FromImage", 
                "caching": "ReadWrite", 
                "managedDisk": { 
                    "storageAccountType": "Premium_LRS", 
                    "id": "/subscriptions/subID/resourceGroups/resourcegroup/providers/Microsoft.Compute/disks/OsDisk_1" 
                }, 
                "deleteOption": "Delete", 
                "diskSizeGB": 127 
            }, 
            "dataDisks": [ 
                { 
                    "lun": 0, 
                    "name": "DataDisk_0", 
                    "createOption": "Attach", 
                    "caching": "None", 
                    "writeAcceleratorEnabled": false, 
                    "managedDisk": { 
                        "storageAccountType": "Premium_LRS", 
                        "id": "/subscriptions/subID/resourceGroups/resourcegroup/providers/Microsoft.Compute/disks/DataDisk_0" 
                    }, 
                    "deleteOption": "Delete", 
                    "diskSizeGB": 1024, 
                    "toBeDetached": false 
                }, 
                { 
                    "lun": 1, 
                    "name": "DataDisk_1", 
                    "createOption": "Attach", 
                    "caching": "None", 
                    "writeAcceleratorEnabled": false, 
                    "managedDisk": { 
                        "storageAccountType": "Premium_LRS", 
                        "id": "/subscriptions/subID/resourceGroups/resourcegroup/providers/Microsoft.Compute/disks/DataDisk_1" 
                    }, 
                    "deleteOption": "Delete", 
                    "diskSizeGB": 1024, 
                    "toBeDetached": false 
                } 
            ] 
        }, 
        "osProfile": { 
            "computerName": "testvm", 
            "adminUsername": "azureuser", 
            "windowsConfiguration": { 
                "provisionVMAgent": true, 
                "enableAutomaticUpdates": true, 
                "patchSettings": { 
                    "patchMode": "AutomaticByOS", 
                    "assessmentMode": "ImageDefault", 
                    "enableHotpatching": false 
                } 
            }, 
            "secrets": [], 
            "allowExtensionOperations": true, 
            "requireGuestProvisionSignal": true 
        }, 
        "networkProfile": { 
            "networkInterfaces": [ 
                { 
                    "id": "/subscriptions/subID/resourceGroups/resourcegroup/providers/Microsoft.Network/networkInterfaces/nic336" 
                , 
                   "properties": { 
                   "deleteOption": "Delete" 
} 
} 
            ] 
        } 
} 
} 
```

## FAQ

### Q: Does this feature work with shared disks?

A: For shared disks, you cannot set the ‘deleteOption’ property to ‘Delete’. You can leave it blank or set it to ‘Detach’


### Q: Which Azure resources support this feature?

A: This feature is supported on all managed disk types used as OS disks and Data disks, NICs, and Public IPs


### Q: Can I use this feature on disks and NICs that are not associated with a VM?

A: No, this feature is only available on disks and NICs associated with a VM.


### Q:	How does this feature work with Flexible virtual machine scale sets?

A: For Flexible virtual machine scale sets the disks, NICs, and PublicIPs have `deleteOption` set to `Delete` by default so these resources are automatically cleaned up when the VMs are deleted. 

For data disks that were explicitly created and attached to the VMs, you can modify this property to ‘Detach’ instead of ‘Delete’ if you want the disks to persist after the VM is deleted.


### Q: Do Spot VMs support this feature?

A: Yes, you can use this feature for Spot VMs just the way you would for on-demand VMs.


### Q: How do I persist the disks, NIC, and Public IPs associated with a VM? 

A: By default, disks, NICs, and Public IPs associated with a VM are persisted when the VM is deleted. If you configure these resources to be automatically deleted, you have the option to revert so that these resources are persisted after the VM is deleted. To persist these resources, set the `deleteOption` property to `Detach` and then these resources will then be persisted when the VM is deleted.


## Next steps

To learn more about basic VM management, see [Tutorial: Create and Manage Linux VMs with the Azure CLI](linux/tutorial-manage-vm.md).
