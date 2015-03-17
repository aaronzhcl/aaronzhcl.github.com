---
layout: post
status: publish
published: true
title: IIS Performance Optimization Guideline
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
date: '2015-03-17 02:56:23 +0800'
date_gmt: '2015-03-17 02:56:23 +0800'
categories:
- IIS
tags:
- IIS
- Performance
comments: []
---

Internet Information Services (IIS) exposes numerous configuration parameters that affect IIS performance. This topic describes several of these parameters and provides general guidance for setting the parameter values to improve IIS performance.

## Reduced Security Footprint, Customized Installation Options

Because IIS7 is a completely modular Web server, Administrators have complete control over the surface area of the Web server. This enables several key advantages over previous versions of IIS:

- Improve performance and reduce memory footprint. By removing unused server features, Administrators can also reduce the memory usage of the server, and improve performance by reducing the amount of feature code that executes on every request to the Web application.

- Build custom / specialized servers. By selecting a particular set of server features, Administrators can build custom servers that are optimized for performing a specific function within the datacenter, such as edge caching or load balancing. Administrators can add custom features to extend or replace any existing functionality using your own or third party server components built on the new extensibility APIs. The componentized architecture will provide long term benefits to the IIS community, by facilitating the development of new server features as they are needed both inside Microsoft and among third party developers.

<!--more-->

## Tune Application Pools through Recycling

Recycling a worker process improves the IIS’s reliability. Recycling is beneficial for faulty Web applications that memory leaks typically cause. Through recycling, the user enables IIS to periodically restart worker processes that are currently servicing an application pool. Users can configure recycling for a worker process using a number of criteria:

- Once a predetermined number of minutes of inactivity have passed. The default setting is 1740 minutes.
- Once a worker process has serviced a predefined number of requests. The default setting is 35,000 connections.
- After the virtual memory usage by the worker process attains a specific threshold.
- At a specific time of the day.

## Log only essential information or completely disable IIS logging

IIS logging should be minimized or even disabled in a production environment. To disable logging follow these steps: 

1. Click Start, point to All Programs, click Administrative Tools, and then click Internet Information Services (IIS) Manager.
2. In the Connections pane, click to expand Sites, click to select the Web site for which you would like to disable logging, click to select Features View, and then double-click the Logging feature.
3. Click Disable in the Actions pane to disable logging for this Web site.

## Disable IIS ASP debugging in production environments

IIS ASP debugging should be disabled in a production environment. To disable IIS ASP debugging follow these steps: 

1. Click Start, point to All Programs, click Administrative Tools, and then click Internet Information Services (IIS) Manager.
2. In the Connections pane, click to expand Sites, click to select the web site for which you would like to disable ASP debugging, click to select Features View, and then double-click the ASP feature.
3. Click to expand Compilation, click to expand Debugging Properties, and verify that both Enable Client-side Debugging and Enable Server-side Debugging are set to False.
4. If necessary, click Apply in the Actions pane.

## Disable debugging for ASP.NET Applications and Web Services 

Ensure that the debug="false" on the *compilation* element in the web.config file of each and every ASP.NET application on the server. The default during development is "true" and it is a common mistake to allow this development time setting to find its way onto production servers during deployment. You don't need it set to true in production and it often leads to memory overhead and inefficiencies.

For more information about what the consequence for setting debug="true", check [ASP.NET Memory: If your application is in production… then why is debug=true](http://blogs.msdn.com/b/tess/archive/2006/04/13/575364.aspx)

## Tune the value of the ASP Threads Per Processor Limit property

The ASP Threads Per Processor Limit property specifies the maximum number of worker threads per processor that IIS creates. Increase the value for the Threads Per Processor Limit until the processor utilization meets at least 50 percent or above. This setting can dramatically influence the scalability of your Web applications and the performance of your server in general. Because this property defines the maximum number of ASP requests that can execute simultaneously, this setting should remain at the default value unless your ASP applications are making extended calls to external components. In this case, you may increase the value of Threads Per Processor Limit. Doing so allows the server to create more threads to handle more concurrent requests. The default value of Threads Per Processor Limit is 25. The maximum recommended value for this property is 100.

To increase the value for the Threads Per Processor Limit follow these steps:

1. Click Start, point to All Programs, click Administrative Tools, and then click Internet Information Services (IIS) Manager.
2. In the Connections pane, select the web server, click to select Features View, and then double-click the ASP feature.
3. Click to expand Limits Properties under Behavior, click Threads Per Processor Limit, enter the desired value for Threads Per Processor Limit and click Apply in the Actions pane.

For more information about how to modify the properties in the &lt;limits&gt; element of the IIS 7.5/7.0 &lt;asp&gt; element, see [ASP Limits &lt;limits&gt; ](http://go.microsoft.com/fwlink/?LinkId=157483). 

Note: Because this property can only be applied at the server level, modification of this property affects all Web sites that run on the server.

## Tune the value of the ASP Queue Length property

The goal of tuning this property is to ensure good response time while minimizing how often the server sends the HTTP 503 (Server Too Busy) error to clients when the ASP request queue is full. If the value of ASP Queue Length property is too low, the server will send the HTTP 503 error with greater frequency. If the value of ASP Queue Length property is too high, users might perceive that the server is not responding when in fact their request is waiting in the queue. By watching the queue during periods of high traffic, you should discern a pattern of web request peaks and valleys. Make note of the peak value, and set the value of the ASP Queue Length property just above the peak value. Use the queue to handle short-term spikes, ensure response time, and throttle the system to avoid overload when sustained, unexpected spikes occur. If you do not have data for adjusting the ASP Queue Length property, a good starting point will be to set a one-to-one ratio of queues to total threads. For example, if the ASP Threads Per Processor Limit property is set to 25 and you have four processors (4 * 25 = 100 threads), set the ASP Queue Length property to 100 and tune from there.

To increase the value for the Queue Length property follow these steps: 

1. Click Start, point to All Programs, click Administrative Tools, and then click Internet Information Services (IIS) Manager.
2. In the Connections pane, select the Web server, click to select Features View, and then double-click the ASP feature.
3. Click to expand Limits Properties under Behavior, click Queue Length, enter the desired value for Queue Length and then click Apply in the Actions pane.

For more information about how to modify the properties in the &lt;limits&gt; element of the IIS 7.5/7.0 &lt;asp&gt; element, see [ASP Limits &lt;limits&gt; ](http://go.microsoft.com/fwlink/?LinkId=157483).

Note: Because this property can only be applied at the server level, modification of this property affects all Web sites that run on the server.

## Tune the MaxPoolThreads registry entry

This setting specifies the number of pool threads to create per processor. Pool threads watch the network for requests and process incoming requests. The MaxPoolThreads count does not include threads that are consumed by ISAPI applications. Generally, you should not create more than 20 threads per processor. MaxPoolThreads is a REG_DWORD registry entry located at HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\InetInfo\Parameters\ with a default value of 4.

## Disable WCF services tracing

Use the Configuration Editor Tool (SvcConfigEditor.exe) to disable WCF services tracing in a production environment. For more information about the Configuration Editor Tool, see [Configuration Editor Tool (SvcConfigEditor.exe)](http://go.microsoft.com/fwlink/?LinkID=127070).

## Configure ASP.NET 2.0 MaxConcurrentRequests for IIS 7.5/7.0 Integrated mode

When ASP.NET 2.0 is hosted on IIS 7.5/7.0 in Integrated Mode, the use of threads is handled differently than on IIS 7.5/7.0 in Classic Mode. When ASP.NET 2.0 is hosted on IIS 7.5 in Integrated mode, ASP.NET 2.0 restricts the number of concurrently executing requests instead of the number of threads concurrently executing requests. For synchronous scenarios, this will indirectly limit the number of threads because the number of requests will be the same as the number of threads. But for asynchronous scenarios, the number of requests and threads will likely be very different because you could have far more requests than threads. When you run ASP.NET 2.0 on IIS 7.5 in integrated mode, the minFreeThreads and minLocalRequestFreeThreads of the “httpRuntime” element in the machine.config are ignored. For IIS 7.5 Integrated mode, a DWORD named MaxConcurrentRequestsPerCPU within HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\2.0.50727.0 determines the number of concurrent requests per CPU. By default, the registry key does not exist and the number of requests per CPU is limited to 12. .NET Framework 3.5 SP1 includes an update to the v2.0 binaries that supports configuring IIS application pools via the aspnet.config file. This configuration applies to integrated mode only (Classic/ISAPI mode ignores these settings).The new aspnet.config config section with default values is listed below:

&lt;system.web&gt;
   &lt;applicationPool maxConcurrentRequestsPerCPU=&quot;12&quot; maxConcurrentThreadsPerCPU=&quot;0&quot; requestQueueLimit=&quot;5000&quot;/&gt;
&lt;/system.web&gt;

By large number of concurrent reqests, I mean between 12 and 5000 per CPU.

1. For v2.0 and v3.5 set a DWORD registry value @ HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\2.0.50727.0\MaxConcurrentRequestsPerCPU = 5000.  Restart IIS
2. For v3.5, you can alternatively set <system.web><applicationPool maxConcurrentRequestsPerCPU="5000"/></system.web> in the aspnet.config file.  If the value is set in both places, the aspnet.config setting overrides the registry setting.
3. For v4.0, the default maxConcurrentRequestsPerCPU is 5000, so you don't need to do anything.
4. Increase the HTTP.sys queue limit, which has a default of 1000.  If the operating system is x64 and you have 2 GB of RAM or more, setting it to 5000 should be fine.  If it is too low, you may see HTTP.sys reject requests with a 503 status.  Open IIS Manager and the Advanced Settings for your Application Pool, then change the value of "Queue Length".
5. If your ASP.NET application is using web services (WFC or ASMX) or System.Net to communicate with a backend over HTTP you may need to increase connectionManagement/maxconnection.  For ASP.NET applications, this is limited to 12 * #CPUs by the autoConfig feature.  This means that on a quad-proc, you can have at most 12 * 4 = 48 concurrent connections to an IP end point.  Because this is tied to autoConfig, the easiest way to increase maxconnection in an ASP.NET application is to set System.Net.ServicePointManager.DefaultConnectionLimit programatically, from Application_Start, for example.  Set the value to the number of concurrent System.Net connections you expect your application to use.  I've set this to Int32.MaxValue and not had any side effects, so you might try that--this is actually the default used in the native HTTP stack, WinHTTP.  If you're not able to set System.Net.ServicePointManager.DefaultConnectionLimit programmatically, you'll need to disable autoConfig , but that means you also need to set maxWorkerThreads and maxIoThreads.  You won't need to set minFreeThreads or minLocalRequestFreeThreads if you're not using classic/ISAPI mode.
6. If your application sees a large number of concurrent requests at start-up or has a bursty load, where concurrency increases suddenly, you will need to make the application asynchronous because the CLR ThreadPool does not respond well to these loads.  The CLR ThreadPool injects new threads at a rate of about 2 per second.  This is true for all versions of the CLR (v1.0 thru v4.0) at the time of this writing.  If concurrency is bursty and the request thread blocks (e.g. on a backend with latency), the injection rate of 2 threads per second will make your application respond very poorly to this work load.  The fix is to stop blocking on threads by using asynchronous I/O to communicate with the backend with latency.  If you cannot make the application asynchronous, you will need to increase minWorkerThreads.  I don't like to increase minWorkerThreads.  It has a side effect on high-throughput synchronous requests that don't block on threads, because the thread count is artificially high.

For more information about configuring ASP.NET Thread Usage on IIS 7.5, see [Thomas Marquardt&#39;s Blog on ASP.NET Thread Usage on IIS 7.0 ](http://go.microsoft.com/fwlink/?LinkId=157518).

## Configure ASP.NET 4 MaxConcurrentRequests for IIS 7.5/7.0 Integrated mode

With .NET Framework 4, the default setting for maxConcurrentRequestsPerCPU is 5000 which is a very large number and therefore will allow plenty of asynchronous requests to execute concurrently. For more information, see [&lt;applicationPool&gt; Element ](Web Settings) (http://go.microsoft.com/fwlink/?LinkID=205339).

For IIS 7.5/7.0 Integrated mode, a DWORD named MaxConcurrentRequestsPerCPU within HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\4.0.30319.0 determines the number of concurrent requests per CPU. By default, the registry key does not exist and the number of requests per CPU is limited to 5000.

## Enable IIS HTTP compression

To more efficiently use available bandwidth, enable IIS HTTP compression. HTTP compression provides faster transmission time between compression-enabled browsers and IIS, regardless of whether your content is served from local storage or a UNC resource.

To configure compression at the Web server level: 

1. Click Start, point to All Programs, click Administrative Tools, and then click Internet Information Services (IIS) Manager.
2. In the Connections pane, select the Web server, click to select Features View, and then double-click the Compression feature.
3. Set the desired compression options and then click Apply in the Actions pane.

To configure compression at the Web site level: 

1. Click Start, point to All Programs, click Administrative Tools, and then click Internet Information Services (IIS) Manager.
2. In the Connections pane, click to expand Sites, click to select the Web site for which you would like to configure compression, click to select Features View, and then double-click the Compression feature.
3. Set the desired compression options and then click Apply in the Actions pane.

## Configure HTTP expires header

This feature helps to minimize the number of http requests send to IIS by website visitors. HTTP expires header will help the client browser to cache webpages and its elements such as images, CSS etc.  To set http expires you need to click on HTTP response headers in the IIS, and then click on “set common headers”. Next select ‘expire web contents” and select the number of days or hours—this is total time your contents will be cached in the client’s browser.

## Enable output caching

When you enable output caching, IIS will keep a copy of requested webpages. If a new user requests the very same webpage located in the cache, IIS will send the copy from its cache without reprocessing the contents. Output caching can significantly improve your server response time for dynamic contents.

## Connection limits in IIS 7.5

This option can give you to control the connection in three ways: controlling connection timeout, controlling maximum bandwidth per website, controlling concurrent connections.

The default connection timeout for IIS 7.5 is 120 seconds, which means after this time http session will be terminated. When a user visit a page and keeps the page open for indefinite time without any activity, the IIS need to keep the connection alive—this causes IIS to spend computing resources for this connection to keep alive. For better performance, you need to keep this limit as low as possible, but not too short. For example, you can set this limit to 70 seconds. To change connection timeout you need to right click on website in IIS, and click on “manage website” .Then select “advanced settings”. Next, click on connection limits and set the value for connection timeout.

## Http connection timeout in IIS

This connection limit option will allow you to set the maximum bandwidth per second and the maximum concurrent connection per second.  The maximum allowed bandwidth make a site use only a certain amount of bandwidth per second—thus improving the performance of other sites in a shared web-hosting environment.

Controlling the number of concurrent connection is another way to improve IIS performance and to improve the security of IIS as well. This option will allow only the specified number of clients to connect to the website at a given moment. So, if any malicious program tries to send numerous connection requests will be rejected by the IIS, and thus prevent your server becoming overloaded with requests during a DDoS attack.

After changing the performance settings, check the performance level of your server by gradually increasing load to a desired level. You can also consider using Google page speed tool to check whether page-loading time has been improved.

## Reference

- [Optimizing IIS Performance](https://msdn.microsoft.com/en-us/library/ee377050(v=bts.70).aspx)
- [ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0](http://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)

