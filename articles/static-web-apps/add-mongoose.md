---
title: "Tutorial: Access data in Cosmos DB using Mongoose with Azure Static Web Apps"
description: Learn to access data in Cosmos DB using Mongoose from an Azure Static Web Apps API function.
author: GeekTrainer
ms.author: chrhar
ms.service: static-web-apps
ms.topic: tutorial
ms.date: 01/25/2021
---

# Tutorial: Access data in Cosmos DB using Mongoose with Azure Static Web Apps

[Mongoose](https://mongoosejs.com/) is the most popular ODM (Object Document Mapping) client for Node.js. Allowing you to design a data structure and enforce validation, Mongoose provides all the tooling necessary to interact with databases that support the Mongoose API. [Cosmos DB](../cosmos-db/mongodb-introduction.md) supports the necessary Mongoose APIs and is available as a back-end server option on Azure.

In this tutorial, you learn how to:

> [!div class="checklist"]
> - Create a Cosmos DB serverless account
> - Create Azure Static Web Apps
> - Update application settings to store the connection string

If you don’t have an Azure subscription, create a [free trial account](https://azure.microsoft.com/free/).

## Prerequisites

- An [Azure account](https://azure.microsoft.com/free/)
- A [GitHub account](https://github.com/join)

## Sign in to Azure

Sign in to the [Azure portal](https://portal.azure.com).

## Create a Cosmos DB serverless database

Begin by creating a [Cosmos DB serverless](../cosmos-db/serverless.md) account. By using a serverless account, you only pay for the resources as they are used and avoid needing to create a full infrastructure.

1. Navigate to [https://portal.azure.com](https://portal.azure.com)
2. Click **Create a resource**
3. Enter **Azure Cosmos DB** in the search box
4. Click **Azure Cosmos DB**
5. Click **Create**
6. If prompted, under **Azure Cosmos DB API for MongoDB** select **Create**
7. Configure your Azure Cosmos DB Account with the following information
    - Subscription: Choose the subscription you wish to use
    - Resource: Click **Create new**, and set the name to **aswa-mongoose**
    - Account name: A unique value is required
    - Location: **West US 2**
    - Capacity mode: **Serverless (preview)**
    - Version: **4.0**
:::image type="content" source="media/add-mongoose/cosmos-db.png" alt-text="Create new Cosmos DB instance":::
8. Click **Review + create**
9. Click **Create**

The creation process will take a few minutes. Later steps will return to the database to gather the connection string.

## Create a static web app

This tutorial uses a GitHub template repository to help you create your application.

1. Navigate to the [starter template](https://github.com/login?return_to=/staticwebdev/mongoose-starter/generate)
2. Choose the **owner** (if using an organization other than your main account)
3. Name your repository **aswa-mongoose-tutorial**
4. Click **Create repository from template**
5. Return to the [Azure portal](https://portal.azure.com)
6. Click **Create a resource**
7. Type **static web app** in the search box
8. Select **Static Web App**
9. Click **Create**
10. Configure your Azure Static Web App with the following information
    - Subscription: Choose the same subscription as before
    - Resource group: Select **aswa-mongoose**
    - Name: **aswa-mongoose-tutorial**
    - Region: **West US 2**
    - Click **Sign in with GitHub**
    - Click **Authorize** if prompted to allow Azure Static Web Apps to create the GitHub Action to enable deployment
    - Organization: Your GitHub account name
    - Repository: **aswa-mongoose-tutorial**
    - Branch: **main**
    - Build presets: Choose **Custom**
    - App location: **/public**
    - Api location: **api**
    - Output location: *leave blank*
    :::image type="content" source="media/add-mongoose/azure-static-web-apps.png" alt-text="Completed Azure Static Web Apps form":::
11. Click **Review and create**
12. Click **Create**
13. The creation process takes a few moments; click on **Go to resource** once the static web app is provisioned

## Configure database connection string

In order to allow the web app to communicate with the database, the database connection string is stored as an [Application Setting](application-settings.md). Setting values are accessible in Node.js using the `process.env` object.

1. Click **Home** in the upper left corner of the Azure portal (or navigate back to [https://portal.azure.com](https://portal.azure.com))
2. Click **Resource groups**
3. Click **aswa-mongoose**
4. Click the name of your database account - it will have a type of **Azure Cosmos DB API for Mongo DB**
5. Under **Settings** click **Connection String**
6. Copy the connection string listed under **PRIMARY CONNECTION STRING**
7. In the breadcrumbs, click **aswa-mongoose**
8. Click **aswa-mongoose-tutorial** to return to the website instance
9. Under **Settings** click **Configuration**
10. Click **Add** and create a new Application Setting with the following values
    - Name: **CONNECTION_STRING**
    - Value: Paste the connection string you copied earlier
11. Click **OK**
12. Click **Save**

## Navigate to your site

You can now explore the static web app.

1. Click **Overview**
1. Click the URL displayed in the upper right
    1. It will look similar to `https://calm-pond-05fcdb.azurestaticapps.net`
1. Click **Please login to see your list of tasks**
1. Click **Grant consent** to access the application
1. Create a new task by typing in a title and clicking **Add task**
1. Confirm the task is displayed (it may take a moment)
1. Mark the task as complete by **clicking the checkbox**
1. **Refresh the page** to confirm a database is being used

## Clean up resources

If you're not going to continue to use this application, delete
the resource group with the following steps:

1. Return to the [Azure portal](https://portal.azure.com)
2. Click **Resource groups**
3. Click **aswa-mongoose**
4. Click **Delete resource group**
5. Type **aswa-mongoose** into the textbox
6. Click **Delete**

## Next steps

Advance to the next article to learn how to configure local development...
> [!div class="nextstepaction"]
> [Setup local development](./local-development.md)
