---
layout: post
status: publish
published: true
title: GC (Garbage Collection) related
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 108
wordpress_url: http://www.webdebug.net:80/?p=108
date: '2012-12-26 07:51:13 +0800'
date_gmt: '2012-12-26 07:51:13 +0800'
categories:
- ASP.NET
tags:
- GC
- garbage collection
- memory issues
- large object heap
- IDisposable
comments: []
---
<p>Do you know GC(Garbage Collection)? Here is a list of questions with answers. You can check whether you can answer them.</p>
<p><a href="http:&#47;&#47;blogs.msdn.com&#47;b&#47;tess&#47;archive&#47;2007&#47;04&#47;10&#47;net-garbage-collector-popquiz-followup.aspx" target="_blank"><strong>.NET Garbage Collector PopQuiz - Followup<&#47;strong><&#47;a><br />
By Tess Ferrandez</p>
<p>1. How many GC threads do we have in a .NET process running the Server version of the GC on a dual-core machine?<br />
2. What GC mode is used in the web development server (cassini) on a quad proc machine? Why? (you can choose from server, workstation or concurrent-workstation)<br />
3. How many finalizer threads do we have in a .NET process running the Server version of the GC on a quad proc machine?<br />
4. When is an object garbage collected?<br />
5. What causes an object to move from Generation 0 to Generation 1 or to Generation 2?<br />
6. If you look at the GC sizes for Generation 0, 1 and 2 in perfmon, why is most of the memory in the process in Gen 2?<br />
...</p>
<p><a href="http:&#47;&#47;blogs.msdn.com&#47;b&#47;tess&#47;archive&#47;2008&#47;04&#47;17&#47;how-does-the-gc-work-and-what-are-the-sizes-of-the-different-generations.aspx" target="_blank"><strong>How does the GC work and what are the sizes of the different generations?<&#47;strong><&#47;a><br />
By Tess Ferrandez</p>
<p><strong>Contents<&#47;strong><br />
What are segments and heaps? How much is allocated for the GC?<br />
What are generations and why do we use a generational GC?<br />
When and how does a collection occur?<br />
What are roots? What keeps an object alive?<br />
What is the Large Object Heap? And why does it exist?<br />
Which GC Flavor fits my application best?<br />
What is the cost of a garbage collection? How can I keep this cost at a minimum?<br />
Additional Resources</p>
<p>&nbsp;</p>
<p>If you want to know more. Here are the in-depth articles related with CLR memory management from MSDN Magazine</p>
<p><a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;magazine&#47;cc163528.aspx" target="_blank"><strong>Investigating Memory Issues<&#47;strong><&#47;a><br />
By Claudio Caldato and Maoni Stephens</p>
<p><strong>Contents<&#47;strong><br />
Tools of the Trade<br />
GC Performance Counters<br />
Windows Performance Counters<br />
Verifying an OOM Exception in a Managed Process<br />
Determining What Caused an OOM Exception<br />
Measure Managed Heap Size<br />
What If Objects Survive?<br />
Is Fragmentation a Problem on Your Managed Heap?<br />
Measuring Time Spent on Garbage Collection<br />
Investigating High CPU Usage</p>
<p><strong><a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;magazine&#47;cc534993.aspx" target="_blank">Large Object Heap Uncovered<&#47;a><&#47;strong><br />
By Maoni Stephens</p>
<p><strong>Contents<&#47;strong><br />
The Large Object Heap and the GC<br />
When a Large Object Gets Collected<br />
LOH Performance Implications<br />
Collecting Performance Data for the LOH<br />
Using a Debugger</p>
<p><strong><a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;magazine&#47;cc163392.aspx" target="_blank">Digging into IDisposable<&#47;a><&#47;strong><br />
By Shawn Farkas</p>
<p><strong>Contents<&#47;strong><br />
Disposable Objects<br />
The Disposable Pattern<br />
Managed vs. Native Resources<br />
Managed Resource Cleanup<br />
Deriving from a Disposable Type<br />
Dispose and Security<br />
SafeHandles<br />
Conclusion</p>
