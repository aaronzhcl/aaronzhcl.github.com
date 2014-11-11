---
layout: post
status: publish
published: true
title: Troubleshoot IIS high CPU issue
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 89
wordpress_url: http://localhost:80/?p=89
date: '2012-12-26 06:53:33 +0800'
date_gmt: '2012-12-26 06:53:33 +0800'
categories:
- IIS
- Troubleshooting
tags:
- IIS
- high CPU
comments: []
---
<p><strong><a href="http://www.iis.net/learn/troubleshoot/performance-issues/troubleshooting-high-cpu-in-an-iis-7x-application-pool" target="_blank">Troubleshooting High CPU in an IIS 7.x Application Pool</a></strong></p>
<p>Published on April 9, 2012 by Jim Cheshire</p>
<p>This troubleshooter will help you to identify the cause of sustained high CPU in an IIS application pool. It&rsquo;s important to keep in mind that it is normal for CPU usage to increase as a web application serves requests. However, if you consistently see CPU remain at a high level (in the area of 80% or greater) for prolonged periods, the performance of your application will suffer. For that reason, it&rsquo;s important to understand the cause of sustained high CPU so that it can be addressed and corrected if possible.</p>
<!--more-->
<p><a href="http://blogs.msdn.com/b/mike/archive/2007/12/06/troubleshooting-high-cpu-performance-issues.aspx" target="_blank"><strong>Troubleshooting High CPU performance issues</strong></a><br />
By Mike Laing</p>
<p><a href="http://blogs.msdn.com/b/mike/archive/2007/12/06/troubleshooting-high-cpu-performance-issues.aspx" target="_blank">Part 1</a><br />
<a href="http://blogs.msdn.com/b/mike/archive/2008/02/26/troubleshooting-high-cpu-performance-issues-part-2.aspx" target="_blank">Part 2</a></p>
<p>Troubleshooting high CPU hang problems can be done with two tools: Performance Monitor, and a debugger. We use Performance Monitor to get a 'perfmon' log of the high cpu behavior, and we use the debugger to get a hang dump of the process that is spiking the cpu. Then we analyze the info in the perfmon log and associate it with the info in the debug dump file.</p>
<p><a href="http://blogs.msdn.com/b/tess/archive/2006/06/22/asp-net-case-study-high-cpu-in-gc-large-objects-and-high-allocation-rates.aspx" target="_blank"><strong>ASP.NET Case Study: High CPU in GC - Large objects and high allocation rates</strong></a><br />
By Tess Ferrandez</p>
<p><strong>Problem description:</strong><br />
At times the application will be very slow to respond and the CPU usage is very high (70-80%).<br />
<strong>Troubleshooting steps:</strong><br />
I have already tipped you off in the title that the issue will be High CPU in GC, but how do we even get to that conclusion? The answer is performance monitor...<br />
A high CPU issue is generally one of 3 things<br />
&middot; An infinite loop<br />
&middot; Too much load (i.e. too many requests doing lots of small things, so no one single thing is a culprit)<br />
&middot; Too much churning in the Garbage Collector.</p>
<p>&nbsp;</p>
