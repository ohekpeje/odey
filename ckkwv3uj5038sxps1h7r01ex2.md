---
title: "The smart way to move your Web app resources across Regions in Azure."
datePublished: Mon Feb 08 2021 17:41:33 GMT+0000 (Coordinated Universal Time)
cuid: ckkwv3uj5038sxps1h7r01ex2
slug: the-smart-way-to-move-your-web-app-resources-across-regions-in-azure
tags: azure, web-app, web-application, regions

---

Over time users of Azure web app might want to change the regions of the application from where it was deployed initially. This is due to certain factors like where most requests are made from to reduce latency.

By design, Azure web app resources are region-specific and cannot be moved across regions. The only way to achieve this is by creating and deploying the website in the intended region and most Azure web app users would not like to go through the whole process again.

To successfully move your web app to another region, follow the listed steps provided.

### Clone your web app.

- Create the destination App Service Plan.

- Clone the App Service into the same Resource Group and region as the destination App Service Plan. (This would ensure that the clone is now in the same webspace).

- Delete the App Service that I am trying to move.

- Clone the Clone with the same name as the original App Service.

- Delete the first clone.

**Note: **You need to have a Premium app service plan to clone the App (you can upgrade the App Service Plan to Premium temporarily and after cloning the application, you can downgrade back to Basic/Free tier).


- Select the Web App you want to clone.

- In the menu on the left, there’s a search bar, look for “clone”.

![clone 1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612799746540/kD6BUlmnv.png)


- You would be unable to use the name of the app you want to clone as the name already exists.

- Use a different name in the App name field.

- Create a new Resource Group.

![clone 2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612799751311/5CAS15aTG.png)

- After successful creation, the cloned web app shows in the region of the new resource group you had created earlier.

![clone 4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612799760808/YcJ8NGU4_.png)

- You can now** delete the original** web app.

- In the newly cloned app, select the clone option again and this time you can use the name of the original web app without conflicts.

![clone 5.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612799764380/LN1AAZxIk.png)

Before and after images showing the new region for the testiptest web app.

![clone 7.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1612799776520/KC_SJolnX.png)


### References:

For more information on Azure resources that can be moved and not moved, review his shared articles listed.

- https://docs.microsoft.com/en-us/azure/app-service/manage-move-across-regions

- https://docs.microsoft.com/en-us/azure/azure-resource-manager/management/region-move-support#microsoftweb

