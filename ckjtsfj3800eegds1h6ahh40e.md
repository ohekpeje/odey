---
title: "PaaS vs IaaS (App Services vs VMs) - Performance POV"
datePublished: Tue Jan 12 2021 09:23:39 GMT+0000 (Coordinated Universal Time)
cuid: ckjtsfj3800eegds1h6ahh40e
slug: paas-vs-iaas-app-services-vs-vms-performance-pov
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1610096202206/wyZ9Y3Ct_.png
tags: azure, paas, web-app, iaas, azure-app-services

---

The difference between App Services and Virtual Machines is striking, as one is Infrastructure-as-a-Service, while the other is Platform-as-a-Service. 

The PaaS needs certain configurations and settings to be made, in order to address performance issues or enhancements. With the default setup, it might result in an imperfect performance output, but the gap should not be that substantial. 

Therefore, in order to have a Web App performing at its maximum capacity, we can mention a set of best practices and recommendations, if you’d like. 
 
The design of Azure App Services, which peers tend to be referring to as PaaS, is specifically designed to support the ease of deployment and the ease of scale. By scale, I mean increasing the number and size of VMs your web sites are running on. To attain those 2 objectives Microsoft designed the App Services platform so that the content of your App Service is stored on a File Server which maps to an Azure Blob Storage container. The D:\home directory you see, if/when you access KUDU/SCM  is actually a symlink to the File Server. This architectural design is what supports the scaling out to multiple instances. Each of those instances will point to the same set of source files on the File Server. 
 
The main difference and the reason you will have better performance on IaaS (Azure VM) is that there is no network call to your web sites’ content. The web site content on IaaS is stored on the physical drive of the Azure VM. It is expected that you would get better performance on an Azure VM, however, if you wanted to scale out to more IaaS VMs or scale up to a larger IaaS VM, the effort required is much greater than it is on the Azure App Services platform. 
 
Bottom line, the comparison between App Services and VMs (PaaS vs IaaS) it is rather a tradeoff between flexibility and performance. 
 
We do have some capability on the Azure App Services platform to help minimize the impact these network calls have on performance, for example, local and dynamic cache. 

- https://github.com/projectkudu/kudu/wiki/Configurable-settings#turning-on-the-local-cache-feature 

- https://github.com/projectkudu/kudu/wiki/Configurable-settings#turning-on-the-dynamic-cache-feature 
 


#2Articles1Week Challenge