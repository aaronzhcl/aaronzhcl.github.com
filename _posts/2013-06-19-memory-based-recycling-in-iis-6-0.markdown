---
layout: post
status: publish
published: true
title: Memory Based Recycling in IIS 6.0
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 221
wordpress_url: http://www.webdebug.net:80/?p=221
date: '2013-06-19 03:41:06 +0800'
date_gmt: '2013-06-19 03:41:06 +0800'
categories:
- IIS
tags:
- IIS
- recycle
- memory
comments:
- id: 11645
  author: web page
  author_email: shiela.salaam@gmail.com
  author_url: http://www.youtube.com/user/PlanetAidInc
  date: '2014-06-18 08:37:32 +0800'
  date_gmt: '2014-06-18 08:37:32 +0800'
  content: "Saturday Dec 1 is World AIDS Day. In the past, this was a day of unhappiness
    and memories.\r\nToday, it's a day of great wish.\r\n\r\nThe worldwide theme this
    year is &ldquo;Getting to Zero&rdquo; -  \r\na vision of a day when there aren't
    any much more HIV infections, and also \r\navoid persons loss of life of AIDS.
    \ In assistance of this goal, Secretary of State Hillary Clinton declared soon
    the U.S.\r\ngovernment&rsquo;s blueprint for &ldquo;Creating an AIDS Free Generation,&rdquo;
    and \r\nit represents a bold {step forward|advan"
---
<p><strong>Memory Based Recycling in IIS 6.0</strong></p>
<p><a href="http://blogs.msdn.com/b/pfedev/archive/2009/01/22/memory-based-recycling-in-iis-6-0.aspx" target="_blank">http://blogs.msdn.com/b/pfedev/archive/2009/01/22/memory-based-recycling-in-iis-6-0.aspx</a></p>
<p>The following points summarize good practices when using memory based recycling:</p>
<ul>
<li>Configure IIS so it logs all recycle events in the System Log.</li>
<li>Use memory recycling only if you understand the application&rsquo;s memory usage patterns.</li>
<li>Use memory based recycling as a temporary workaround until permanent fixes can be found.</li>
<li>Remember that memory based recycling may not work as expected when the application consumes very large amounts of memory in a very short period of time (less than a minute).</li>
<li>Closely monitor recycles and ensure that they are not too many (reducing the performance and/or availability of the application), or too few (allowing memory consumption of the application to create too much memory pressure on the server).</li>
<li>Use overlapped recycling when possible.</li><br />
</ul><br />
<!--more-->
The documentation suggests setting the Virtual Memory threshold as high as 70% of the system&rsquo;s memory, and the Used Memory as high as 60% of the system&rsquo;s memory. However, for recycling purposes, and considering that during the recycle two processes must run concurrently, these settings could prove to be a bit aggressive. As an estimate, for a 32 bit server with 4 GB of RAM, the Virtual Memory should be set to some value between 1.2 GB and 1.5 GB, whereas the Private bytes should be around 0.8 GB to 1 GB. These numbers assume that the application is the only one in the system. Of course, these numbers are quick rules of thumb and do not apply to every case. Different applications have very different memory usage patterns.</p>
<p><a href="http://www.microsoft.com/technet/prodtechnol/WindowsServer2003/Library/IIS/f4e96b27-189c-491f-a941-fec28f5cead1.mspx?mfr=true" target="_blank">Recycling on a Used-Memory Threshold (IIS 6.0)</a></p>
<p><a href="http://www.microsoft.com/technet/prodtechnol/WindowsServer2003/Library/IIS/f4e96b27-189c-491f-a941-fec28f5cead1.mspx?mfr=true" target="_blank">Recycling on a Virtual-Memory Threshold (IIS 6.0)</a></p>
