## Improving Availability on your application running on PAAS.

After deploying our applications to the cloud, we often ask ourselves how to what can be doen to ensure maximum uptime of the applications in the event of any unforeseen events that may occur to the datacenter such as Platform upgrades, VM movements etc. All and more of those events are expected to occur and the platform will continue to be upgraded to improve performance and security.

This article outlines the crucial steps that you can take to ensure that your app is cloud-ready. By taking these steps, you will ensure that any events in the data centre will have negligible effects on your app and that your app will be more resilient and future proof.

However, you can make your app resilient to all these incidents. To guarantee the maximum uptime for your app.

**Always On:** This feature keeps your application loaded even when there's no request. This setting is somewhat similar to “*Idle Time-out*” setting on the IIS application pool. When your web app is recycled, it will take Azure some time to bring it up the site when it’s accessed next time (in my experience it may take about 5-10 seconds) which could be frustrating for the user.  So enabling “Always On” setting on Azure web app increases application responsiveness, especially if the application is not very frequently accessed by users.

![Always on.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610711512258/6JU0lqBJK.png)
Note: This feature is available when your application is running from B1 app service plan and above.

**ARR Affinity:** Also known as Affinity cookie. Azure app service uses  [Application Request Routing](https://docs.microsoft.com/en-us/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) IIS Extension to distribute your connecting users between your active instances serving up the content. ARR cleverly identifies the user by assigning them a special cookie (known as an affinity cookie), which allows the service to choose the right instance the user was using to serve subsequent requests made by that user. This means, a client establishes a session with an instance and it will keep talking to the same instance until his session has expired.

For example, let us say we have two instances named A and B for site XYZ.
You requested XYZ, and the request was routed to instance A. Whenever you visit XYZ, your request will be handled by A until the cookie session expires.

![ARR.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610711577841/y7fM0_Avh.png)
Note: If you are running your web app on multiple instances, it is recommended that this feature is turned off so that request is evenly routed amongst your instances.

**Auto-Heal:** Imagine a feature that works to fix your app if it encounters any unexpected issue. Sounds too good to be true?, well, with Auto-Heal, this is possible. 

In a production application, Auto-heal helps to ensure high availability and resilience. Although Auto-Heal is not an eventual fix for performance issues the application may encounter, it allows the application to quickly recover from unexpected states whether they are platform or application and stay available for customers.

*Proactive Auto-Heal* is an extension to the auto-healing feature of Azure App Service. It monitors for high memory and slow response situations and recycles the app when one of these conditions is met.

![Auto Heal.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610711596285/XFac960tT.png)

**Scale-out:** To increase availability it is recommended that you scale-out the web app to run on at least two instances because one instance can be down when the App service platform is undergoing an upgrade. Therefore, your web app process will be restarted and will experience downtime.

To prevent any downtime, you can manually scale-out your app to two instances, or you could make use of the Autoscale feature to scale your app based on metrics you have configured.

![Scale Auto.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610711617338/Bjcs9zgh4.png)

Note: This feature is available from the B1 pricing plan.
The Auto Scale feature is available from the S1 app service plan (Production workload).

**Local Cache:** By design, the content of your Azure App Service site is stored in Azure Storage and shared between the app service instances. The Azure App Service Local Cache feature provides a web role view of your content. This content is a write-but-discard cache of your storage content that is created asynchronously on-site startup. When the cache is ready, the site is switched to run against the cached content.

Note: You can increase the size up to 2GB (2000MB) per app. Note that it will take longer to load local cache as the size increases.
Use Application Initialization:

**Health Check**: Health Check feature automatically removes a faulty instance from rotation, thus improving availability.

This feature will ping the specified health check path on all instances of your web app every minute. If an instance does not respond within 10 minutes (5 pings), the instance is determined to be unhealthy and our service will stop routing requests to it. It is highly recommended for production apps.

![Health Check.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1610714050018/OUpu90l5D.png)
Note: Health Check feature only works for applications that are hosted on more than one instance

**Azure Traffic Manager:** Azure Traffic Manager is a DNS-based traffic load balancer that enables you to distribute traffic optimally to services across global Azure regions while providing high availability and responsiveness.

The web users may experience a delay accessing the site if they browse the site from any other geographic location than where the website is hosted. Also, if the site is deployed only in one region, it could be affected by downtime in the case of a region-wide outage.

You can set WEBSITE_HEALTHCHECK_MAXUNHEALTHYWORKERPERCENT app setting to a value between 0 and 100. Setting this to a higher value means more unhealthy instances will be removed (the default value is 50).

**Enable Application Insights:** Application Insights is a Service provider that you can use to monitor live your web application. It includes analytics tools that can help to diagnose issues. Additionally, it helps to monitor Response times, Requests rates, Failures, Exceptions.

**Conclusion**: In this, we discussed ways you can ensure high availability of your web application hosted on the Azure platform with disruption of service your site may render.

*If you enjoyed the article, consider sharing it so more people can benefit from it! Also, feel free to share your thoughts. #2Articles1Week
*

**References **:

- [Application Request Routing Version 2 Overview | Microsoft Docs](https://docs.microsoft.com/en-us/iis/extensions/planning-for-arr/application-request-routing-version-2-overview) 

-  [Get started with autoscale in Azure - Azure Monitor | Microsoft Docs](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/autoscale-get-started) 

- [Local cache - Azure App Service | Microsoft Docs](https://docs.microsoft.com/en-us/azure/app-service/overview-local-cache) 
 
- [Get started with autoscale in Azure - Azure Monitor | Microsoft Docs](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/autoscale-get-started) 
 
- [Azure Traffic Manager | Microsoft Docs](https://docs.microsoft.com/en-us/azure/traffic-manager/traffic-manager-overview) 
 
- [What is Azure Application Insights? - Azure Monitor | Microsoft Docs](https://docs.microsoft.com/en-us/azure/azure-monitor/app/app-insights-overview) 