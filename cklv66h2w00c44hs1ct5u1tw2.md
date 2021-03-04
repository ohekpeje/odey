## Rename an App Service Plan in Azure.

After deployment of your resources in Azure, most users want the option to be able to change the name of the App service plan which they had earlier deployed to a different name. By design App, Service Plans cannot be renamed. 

In this article, you get to learn how to overcome this limitation. We are going to use Custom deployment or Template deployment to achieve the change of name of an app service plan.

Please follow the steps below to use Custom Deployment Template to create App Service Plan.

Go to App Service Plan.
![yt2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1614780446183/b52qwQ7T8p.png)

Download the template.

Edit the Template.json in Notepad++; "defaultValue": "ReleaseAppSvcPlan".
![yt.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1614780407475/u1beTj8Y-.png)

![yt1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1614780419027/YQWfQQE_b.png)

Save the changes.

Go back to the Portal and go to Deploy a Custom template.

![yt3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1614780559111/eQlTOOaih.png)

Click on Build your own template in the editor.

Click on Load File.

![yt4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1614780584481/d0m95bXfp.png)

Import the Template.json.

Click on Save.

![yt5.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1614780636911/IdDLGiJ36.png)

Select the resource group that contains the plan you intend to change the name to.

Check the box "I agree to the terms and conditions stated above".

Click Purchase.

**NOTE**: You can also edit Resource Group, Location and Name.

### REFERENCE:

- %[https://docs.microsoft.com/en-us/azure/azure-resource-manager/]


As always, I would love to know what you think in the comments below.
