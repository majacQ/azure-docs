---
title: "Tutorial: Create a Linux virtual machine scale set" 
description: Learn how to create and deploy a highly available application on Linux VMs using a virtual machine scale set
author: ju-shim
ms.author: jushiman
ms.topic: tutorial
ms.service: virtual-machines
ms.collection: linux
ms.date: 10/15/2021
ms.reviewer: mimckitt
ms.custom: mimckitt

#Customer intent: As an IT administrator, I want to learn about autoscaling VMs in Azure so that I can deploy a highly-available and scalable infrastructure.
---

# Tutorial: Create a virtual machine scale set and deploy a highly available app on Linux 

**Applies to:** :heavy_check_mark: Linux VMs :heavy_check_mark: Uniform scale sets

Virtual machine scale sets with [Flexible orchestration](../flexible-virtual-machine-scale-sets.md) let you create and manage a group of load balanced VMs. The number of VM instances can automatically increase or decrease in response to demand or a defined schedule.

In this tutorial, you deploy a virtual machine scale set in Azure and learn how to:

> [!div class="checklist"]
> * Create a resource group.
> * Create a Flexible scale set with a load balancer.
> * Add nginx to the scale set instances.
> * Open port 80 to HTTP traffic.
> * Test the scale set.


## Scale Set overview

Scale sets provide the following key benefits:
- Easy to create and manage multiple VMs
- Provides high availability and application resiliency by distributing VMs across fault domains
- Allows your application to automatically scale as resource demand changes
- Works at large-scale

With Flexible orchestration, Azure provides a unified experience across the Azure VM ecosystem. Flexible orchestration offers high availability guarantees (up to 1000 VMs) by spreading VMs across fault domains in a region or within an Availability Zone. This enables you to scale out your application while maintaining fault domain isolation that is essential to run quorum-based or stateful workloads, including:
- Quorum-based workloads
- Open-source databases
- Stateful applications
- Services that require high availability and large scale
- Services that want to mix virtual machine types or leverage Spot and on-demand VMs together
- Existing Availability Set applications

Learn more about the differences between Uniform scale sets and Flexible scale sets in [Orchestration Modes](../../virtual-machine-scale-sets/virtual-machine-scale-sets-orchestration-modes.md).



## Create a scale set

Use the Azure portal to create a Flexible scale set.

1. Open the [Azure portal](https://portal.azure.com).
1. Search for and select **Virtual machine scale sets**.
1. Select **Create** on the **Virtual machine scale sets** page. The **Create a virtual machine scale set** will open.
1. Select the subscription that you want to use for **Subscription**.
1. For **Resource group**, select **Create new** and type *myVMSSRG* for the name and then select **OK**.
    :::image type="content" source="media/tutorial-create-vmss/flex-project-details.png" alt-text="Project details.":::
1. For **Virtual machine scale set name**, type *myVMSS*.
1. For **Region**, select a region that is close to you like *East US*.
    :::image type="content" source="media/tutorial-create-vmss/flex-details.png" alt-text="Name and region.":::
1. Leave **Availability zone** as blank for this example.
1. For **Orchestration mode**, select **Flexible**.
1. Leave the default of *1* for fault domain count or choose another value from the drop-down.
   :::image type="content" source="media/tutorial-create-vmss/flex-orchestration.png" alt-text="Choose Flexible orchestration mode.":::
1. For **Image**, select *Ubuntu 18.04 LTS*.
1. For **Size**, leave the default value or select a size like *Standard_E2s_V3*.
1. In **Username** type *azureuser*.
1. For **SSH public key source**, leave the default of **Generate new key pair**, and then type *myKey* for the **Key pair name**.
    :::image type="content" source="media/tutorial-create-vmss/flex-admin.png" alt-text="Screenshot of the Administrator account section where you select an authentication type and provide the administrator credentials.":::
1. On the **Networking** tab, under **Load balancing**, select **Use a load balancer**.
1. For **Load balancing options**, leave the default of **Azure load balancer**.
1. For **Select a load balancer**, select **Create new**.
    :::image type="content" source="media/tutorial-create-vmss/load-balancer-settings.png" alt-text="Load balancer settings.":::
1. On the **Create a load balancer** page, type in a name for your load balancer and **Public IP address name**.
1. For **Domain name label**, type in a name to use as a prefix for your domain name. This name must be unique.
1. When you are done, select **Create**.
    :::image type="content" source="media/tutorial-create-vmss/flex-load-balancer.png" alt-text="Create a load balancer.":::
1. Back on the **Networking** tab, leave the default name for the backend pool.
1. On the **Scaling** tab, leave the default instance count as *2*, or add in your own value. This is the number of VMs that will be created, so be aware of the costs and the limits on your subscription if you change this value.
1. Leave the **Scaling policy** set to *Manual*.
    :::image type="content" source="media/tutorial-create-vmss/flex-scaling.png" alt-text="Scaling policy settings.":::
1. Select the **Advanced** tab.
1. Under **Custom data and cloud init**, copy the following and paste it into the **Custom data** text box:
    ```yml
    #cloud-config
    package_upgrade: true
    packages:
      - nginx
      - nodejs
      - npm
    write_files:
      - owner: www-data:www-data
      - path: /etc/nginx/sites-available/default
        content: |
          server {
            listen 80;
            location / {
              proxy_pass http://localhost:3000;
              proxy_http_version 1.1;
              proxy_set_header Upgrade $http_upgrade;
              proxy_set_header Connection keep-alive;
              proxy_set_header Host $host;
              proxy_cache_bypass $http_upgrade;
            }
          }
      - owner: azureuser:azureuser
      - path: /home/azureuser/myapp/index.js
        content: |
          var express = require('express')
          var app = express()
          var os = require('os');
          app.get('/', function (req, res) {
            res.send('Hello World from host ' + os.hostname() + '!')
          })
          app.listen(3000, function () {
            console.log('Hello world app listening on port 3000!')
          })
    runcmd:
      - service nginx restart
      - cd "/home/azureuser/myapp"
      - npm init
      - npm install express -y
      - nodejs index.js
    ```
1. When you are done, select **Review + create**.
1. Once you see that validation has passed, you can select **Create** at the bottom of the page to deploy your scale set.
1. When the **Generate new key pair** window opens, select **Download private key and create resource**. Your key file will be download as **myKey.pem**. Make sure you know where the `.pem` file was downloaded, you will need the path to it in the next step.
1. When the deployment is complete, select **Go to resource** to see your scale set.


## View the VMs in your scale set

On the page for the scale set, select **Instances** from the left menu. 

You will see a list of VMs that are part of your scale set. This list includes:

- The name of the VM
- The computer name used by the VM.
- The current status of the VM, like *Running*.
- The *Provisioning state* of the VM, like *Succeeded*.

:::image type="content" source="media/tutorial-create-vmss/instances.png" alt-text="Table of information about the scale set instances.":::


## Open port 80 

Open port 80 on your scale set by adding an inbound rule to your network security group (NSG).

1. On the page for your scale set, select **Networking** from the left menu. The **Networking** page will open.
1. Select **Add inbound port rule**. The **Add inbound security rule** page will open.
1. Under **Service**, select *HTTP* and then select **Add** at the bottom of the page.

## Test your scale set

Test your scale set by connecting to it from a browser.

1. One the **Overview** page for your scale set, copy the Public IP address.
1. Open another tab in your browser and paste the IP address into the address bar.
1. When the page loads, take a note of the compute name that is shown. 
1. Refresh the page until you see the computer name change. 

## Delete your scale set

When you are done, you should delete the resource group, which will delete everything you deployed for your scale set.

1. On the page for your scale set, select the **Resource group**. The page for your resource group will open.
1. At the top of the page, select **Delete resource group**.
1. In the **Are you sure you want to delete** page, type in the name of your resource group and then select **Delete**.

## Next steps
In this tutorial, you created a virtual machine scale set. You learned how to:

> [!div class="checklist"]
> * Create a resource group.
> * Create a Flexible scale set with a load balancer.
> * Add nginx to the scale set instances.
> * Open port 80 to HTTP traffic.
> * Test the scale set.

Advance to the next tutorial to learn more about load balancing concepts for virtual machines.

> [!div class="nextstepaction"]
> [Load balance virtual machines](tutorial-load-balancer.md)
