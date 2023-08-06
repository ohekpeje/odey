---
title: "Troubleshooting startup Failures on Azure App Service."
datePublished: Thu Jan 07 2021 06:29:47 GMT+0000 (Coordinated Universal Time)
cuid: ckjmh0okj0069l1s1dqos7ptr
slug: troubleshooting-startup-failures-on-azure-app-service
tags: azure, paas, aspnet-core, troubleshooting, azure-app-services

---

Troubleshooting ASP.NET CORE startup failures can be a real nightmare for developers. Before proceeding further, you would be interested to know that they are different startup errors, each with its own HTTP server code. Below is a list of startup errors you may encounter. List of known [startup errors and meaning](https://docs.microsoft.com/en-us/aspnet/core/test/troubleshoot-azure-iis?view=aspnetcore-5.0).

So, after deployment, when you try to access your application URL on the web browser you might get to experience any of the listed failures. The first step will be to quickly raise a support ticket thinking this is a platform issue (considering that you deployed on Azure PaaS).

**How do we figure out why my application does not start?**

You can do this by merely enabling stdout logging. You probably noticed stdoutLogFile and stdoutLogEnabled attributes on the aspNetCore element. They are very helpful to diagnose issues – especially issues related to application startup.

The ASP.NET Core Module stdout log often records useful error messages not found in the Application Event Log. To enable and view stdout logs:

1. In the Azure Portal, navigate to the web app.
    
2. In the App Service blade, enter kudu in the search box.
    
3. Select Advanced Tools &gt; Go.
    
4. Select Debug console &gt; CMD.
    
5. Navigate to site/wwwroot
    
6. Select the pencil icon to edit the web.config file.
    

![e.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609941706152/3Gwr4AHiK.png align="left")

1. You have to change the stdoutLogEnabled from ‘false’, to ‘**true**’
    
2. And the stdoutLogFile from “.\\logs\\stdout” to "**\\?%home%\\LogFiles**"
    

**Note:** By design when you have the WEBSITE\_RUN\_FROM\_PACKAGE app setting enabled the files are read-only by design. So, when you access kudu to edit the **wwwroot folder**, the 409 conflict error is encountered.

**Warning**: Failure to disable the stdout log can lead to app or server failure. There is no limit on log file size, or the number of log files created. Only use stdout logging to troubleshoot app startup problems.

After all the activities carried out above, you will get a result similar to the screenshot below

![d.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1609941206446/JhGnYl1ug.png align="left")

I hope this helps to fix future issues relating to startup failures.