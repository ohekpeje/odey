---
title: "Azure resource providers and types."
datePublished: Mon Jan 04 2021 08:11:48 GMT+0000 (Coordinated Universal Time)
cuid: ckjiacbzx000ygcs1cv6z5zp1
slug: azure-resource-providers-and-types
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1700395365104/8d0caaa3-16a7-42c8-90f7-df73e52dbe04.png
tags: azure, paas, cloud-computing, azure-app-services

---

When deploying resources, you frequently need to retrieve information about the resource providers and types. For example, when you create/deploy a web app, you work with the Microsoft.Web resource provider. This resource if

Before using a resource provider, your Azure subscription must be registered for the resource provider. Registration configures your subscription to work with the resource provider. Some resource providers are registered by default. Other resource providers are registered automatically when you take certain actions. For example, when you create a resource through the portal, the resource provider is typically registered for you. For other scenarios, you may need to manually register a resource provider. See  [Resource Provider](https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/azure-services-resource-providers) 

NOTE: Only register a resource provider when you're ready to use it. The registration step enables you to maintain least privileges within your subscription. A malicious user can't use resource providers that aren't registered.

To see the information regarding your resource providers, you can achieve this in two ways.

Sign in to the  [Azure portal](https://portal.azure.com/).

On the top right where you have your account details, click on the switch directory to access permission.
 
![Picture1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609747644265/4XOCfi1PL.png)
Then click on Resource provider status.

![Picture2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609749315830/WXn5ZJcxG.png)
 
You can also access the Resource provider via the Subscription blade on the Azure portal.
 
![Picture3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609747689433/6HQtksZ5o.png)

To see all resource providers in Azure, and the registration status for your subscription, run the below script in Azure CLI provided on the portal.

az provider list --query "[].{Provider:namespace, Status:registrationState}" --out table

![Picture4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609747715336/vrsZctUKD.png)
 