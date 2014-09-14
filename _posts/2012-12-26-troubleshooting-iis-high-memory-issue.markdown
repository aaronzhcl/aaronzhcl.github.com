---
layout: post
status: publish
published: true
title: Troubleshooting IIS high memory issue
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 86
wordpress_url: http://localhost:80/?p=86
date: '2012-12-26 06:53:49 +0800'
date_gmt: '2012-12-26 06:53:49 +0800'
categories:
- IIS
- Troubleshooting
tags:
- IIS
- high memory
- memory leak
- native memory
- OutOfMemoryException
- dispose
comments: []
---
<p><a href="http:&#47;&#47;blogs.msdn.com&#47;b&#47;webtopics&#47;archive&#47;2009&#47;05&#47;22&#47;troubleshooting-system.outofmemoryexceptions-in-asp.net.aspx" target="_blank"><strong>Troubleshooting System.OutOfMemoryExceptions in ASP.NET<&#47;strong><&#47;a><br />
By Jim Cheshire</p>
<p>When the .NET Framework was first released, many developers believed the introduction of the garbage collector meant never having to worry about memory management ever again. In fact, while the garbage collector is efficient in managing memory in a managed application, it's still possible for an application's design to cause memory problems.</p>
<p>One of the more common issues we see regarding memory involves System.OutOfMemoryExceptions. After years of helping developers troubleshoot OutOfMemoryExceptions, we've accumulated a short list of the more common causes of these exceptions. Before I go over that list, it's important to first understand the cause of an OutOfMemoryException from a 30,000 foot view.</p>
<p><strong><a href="http:&#47;&#47;www.iis.net&#47;learn&#47;troubleshoot&#47;performance-issues&#47;troubleshooting-native-memory-leak-in-an-iis-7x-application-pool" target="_blank">Troubleshooting native memory leak in an IIS 7.x Application Pool<&#47;a><&#47;strong><br />
Published on April 9, 2012 by Apurva Joshi</p>
<p>This troubleshooter will help you to identify the cause of native memory leak in an IIS application pool. It&rsquo;s important to keep in mind that it is normal for high memory allocation as a web application serves requests. However, if you consistently see both Process\Private Bytes and Process\Virtual Bytes are increasing or Process\Private Bytes and Process\Working Set are increasing and Memory\Available Bytes is decreasing, the memory leak will occur and it may cause an out-of-memory exception.</p>
<p><a href="http:&#47;&#47;blogs.msdn.com&#47;b&#47;tess&#47;archive&#47;2006&#47;02&#47;15&#47;net-memory-leak-xmlserializing-your-way-to-a-memory-leak.aspx" target="_blank"><strong>.NET Memory Leak: XmlSerializing your way to a Memory Leak<&#47;strong><&#47;a><br />
By Tess Ferrandez</p>
<p><strong>Problem Description<&#47;strong><br />
We have continuous memory growth in our ASP.NET application. We don't cache much or use any session state so that doesn't seem to be the problem, but the memory usage just keeps increasing at a steady rate. An attempt to call GC.Collect shows that even a full collection does not reduce the memory usage.</p>
<p><strong><a href="http:&#47;&#47;blogs.msdn.com&#47;b&#47;tess&#47;archive&#47;2009&#47;02&#47;03&#47;net-memory-leak-to-dispose-or-not-to-dispose-that-s-the-1-gb-question.aspx" target="_blank">.NET Memory Leak: To dispose or not to dispose, that&rsquo;s the 1 GB question<&#47;a><&#47;strong><br />
By Tess Ferrandez</p>
<p>I was looking at a memory dump recently for an issue where the process would grow to over 1 GB and return OutOfMemory Exceptions.<br />
The dump itself was 1.34 GB which is basically the memory we have committed (used) so it was pretty big, and the first thing we need to check for in this case is whether we are dealing with an issue with high .NET GC memory usage (lots of .net objects), .NET loader heap usage (lots of dlls) or native memory usage (native heaps or dlls)</p>
