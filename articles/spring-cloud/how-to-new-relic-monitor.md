---
title: "How to monitor Spring Boot apps using New Relic Java agent"
titleSuffix: Azure Spring Cloud
description: Learn how to monitor Spring Boot applications using the New Relic Java agent.
author: karlerickson
ms.author: karler
ms.service: spring-cloud
ms.topic: how-to
ms.date: 04/07/2021
ms.custom: devx-track-java
---

# How to monitor Spring Boot apps using New Relic Java agent (Preview)

This feature enables monitoring of Spring Boot applications in Azure Spring Cloud with the New Relic Java agent.

With the New Relic Java agent, you can:
* Consume the New Relic Java agent.
* Configure the New Relic Java agent using environment variables.
* Check all monitoring data from the New Relic dashboard.

The following video describes how to activate and monitor Spring Boot applications in Azure Spring Cloud using New Relic One.

<br>

> [!VIDEO https://www.youtube.com/embed/4GQPwJSP3ys?list=PLPeZXlCR7ew8LlhnSH63KcM0XhMKxT1k_]

## Prerequisites

* A [New Relic](https://newrelic.com/) account.
* [Azure CLI version 2.0.67 or later](/cli/azure/install-azure-cli).

## Activate the New Relic Java in process agent

Use the following procedure to access the agent:

1. Create an instance of Azure Spring Cloud.

2. Create an application.

    ```azurecli
      az spring-cloud app create --name "appName" --is-public true \
      -s "resourceName" -g "resourceGroupName"
    ```

3. Create a deployment with the New Relic agent and environment variables.

    ```azurecli
    az spring-cloud app deploy --name "appName" --jar-path app.jar \
       -s "resourceName" -g "resourceGroupName" \
       --jvm-options="-javaagent:/opt/agents/newrelic/java/newrelic-agent.jar" \
       --env NEW_RELIC_APP_NAME=appName NEW_RELIC_LICENSE_KEY=newRelicLicenseKey
    ```

Azure Spring Cloud pre-installs the New Relic Java agent to */opt/agents/newrelic/java/newrelic-agent.jar*. Customers can activate the agent from applications' **JVM options**, as well as configure the agent using the [New Relic Java agent environment variables](https://docs.newrelic.com/docs/agents/java-agent/configuration/java-agent-configuration-config-file/#Environment_Variables).

## Portal

You can also activate this agent from portal with the following procedure.

1. Find the app from **Settings**/**Apps** in the navigation pane.

   [ ![Find app to monitor](media/new-relic-monitoring/find-app.png) ](media/new-relic-monitoring/find-app.png)

2. Select the application to jump to the **Overview** page.

   [ ![Overview page](media/new-relic-monitoring/overview-page.png) ](media/new-relic-monitoring/overview-page.png)

3. Select **Configuration** in the left navigation pane to add/update/delete the **Environment Variables** of the application.

   [ ![Update environment](media/new-relic-monitoring/configurations-update-environment.png) ](media/new-relic-monitoring/configurations-update-environment.png)

4. Select **General settings** to add/update/delete the **JVM options** of the application.

   [ ![Update JVM Option](media/new-relic-monitoring/update-jvm-option.png) ](media/new-relic-monitoring/update-jvm-option.png)

5. View the application api/gateway **Summary** page from the New Relic dashboard.

   [ ![App summary page](media/new-relic-monitoring/app-summary-page.png) ](media/new-relic-monitoring/app-summary-page.png)

6. View the application customers-service **Summary** page from the New Relic dashboard.
 
   [ ![Customers-service page](media/new-relic-monitoring/customers-service.png) ](media/new-relic-monitoring/customers-service.png)  

7. View the **Service Map** page from the New Relic dashboard.  

   [ ![Service map page](media/new-relic-monitoring/service-map.png) ](media/new-relic-monitoring/service-map.png)

8. View the **JVMs** page of the application from the New Relic dashboard.

   [ ![JVM page](media/new-relic-monitoring/jvm-page.png) ](media/new-relic-monitoring/jvm-page.png)

9. View the application profile from the New Relic dashboard.

   [ ![Application profile](media/new-relic-monitoring/profile-app.png) ](media/new-relic-monitoring/profile-app.png)

## Automate provisioning

You can also run a provisioning automation pipeline using Terraform or an Azure Resource Manager template (ARM template). This pipeline can provide a complete hands-off experience to instrument and monitor any new applications that you create and deploy.

### Automate provisioning using Terraform

To configure the environment variables in a Terraform template, add the following code to the template, replacing the *\<...>* placeholders with your own values. For more information, see [Manages an Active Azure Spring Cloud Deployment](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/spring_cloud_active_deployment).

```terraform
resource "azurerm_spring_cloud_java_deployment" "example" {
  ...
  jvm_options = "-javaagent:/opt/agents/newrelic/java/newrelic-agent.jar"
  ...
    environment_variables = {
      "NEW_RELIC_APP_NAME": "<app-name>",
      "NEW_RELIC_LICENSE_KEY": "<new-relic-license-key>"
  }
}
```

### Automate provisioning using an ARM template

To configure the environment variables in an ARM template, add the following code to the template, replacing the *\<...>* placeholders with your own values. For more information, see [Microsoft.AppPlatform Spring/apps/deployments](/azure/templates/microsoft.appplatform/spring/apps/deployments?tabs=json).

```ARM template
"deploymentSettings": {
  "environmentVariables": {
    "NEW_RELIC_APP_NAME" : "<app-name>",
    "NEW_RELIC_LICENSE_KEY" : "<new-relic-license-key>"
  },
  "jvmOptions": "-javaagent:/opt/agents/newrelic/java/newrelic-agent.jar",
  ...
}
```

## View New Relic Java Agent logs

By default, Azure Spring Cloud will print the logs of the New Relic Java agent to `STDOUT`. The logs will be mixed with the application logs. You can find the explicit agent version from the application logs.

You can also get the logs of the New Relic agent from the following locations:

* Azure Spring Cloud logs
* Azure Spring Cloud Application Insights
* Azure Spring Cloud LogStream

You can leverage some environment variables provided by New Relic to configure the logging of the New Agent, such as, `NEW_RELIC_LOG_LEVEL` to control the level of logs. For more information, see [New Relic Environment Variables](https://docs.newrelic.com/docs/agents/java-agent/configuration/java-agent-configuration-config-file/#Environment_Variables).

> [!CAUTION]
> We strongly recommend that you *do not* override the logging default behavior provided by Azure Spring Cloud for New Relic. If you do, the logging scenarios in above scenarios will be blocked, and the log file(s) may be lost. For example, you should not pass the following environment variables to your applications. Log file(s) may be lost after restart or redeployment of application(s).
>
> * NEW_RELIC_LOG
> * NEW_RELIC_LOG_FILE_PATH

## New Relic Java Agent update/upgrade

The New Relic Java agent will update/upgrade the JDK regularly. The agent update/upgrade may impact following scenarios.

* Existing applications that use the New Relic Java agent before update/upgrade will be unchanged.
* Existing applications that use the New Relic Java agent before update/upgrade require restart or redeploy to engage the new version of the New Relic Java agent.
* New applications created after update/upgrade will use the new version of the New Relic Java agent.

## Vnet Injection Instance Outbound Traffic Configuration

For a vnet injection instance of Azure Spring Cloud, you need to make sure the outbound traffic is configured correctly for the New Relic Java agent. For more information, see [Networks of New Relic](https://docs.newrelic.com/docs/using-new-relic/cross-product-functions/install-configure/networks/#agents).

## Next steps

* [Distributed tracing and App Insights](how-to-distributed-tracing.md)
