---
layout: post
status: publish
published: true
title: IIS application pool recycle related
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 95
wordpress_url: http://www.webdebug.net:80/?p=95
date: '2012-12-26 06:52:57 +0800'
date_gmt: '2012-12-26 06:52:57 +0800'
categories:
- IIS
- Troubleshooting
tags:
- IIS
- application pool
- recycle
- session lost
comments: []
---
<p>An application pool is a group of one or more URLs that are served by a worker process or set of worker processes. Any Web directory or virtual directory can be assigned to an application pool. Every application within an application pool shares the same worker process. Because each worker process operates as a separate instance of the worker process executable, W3wp.exe, the worker process that services one application pool is separated from the worker process that services another.</p>
<p>Unexpected application recycle will cause various issues of the web application, check articles below related to this topic,</p>
<p><strong><a href="http://blogs.msdn.com/b/tess/archive/2006/08/02/asp-net-case-study-lost-session-variables-and-appdomain-recycles.aspx" target="_blank">ASP.NET Case Study: Lost session variables and appdomain recycles</a></strong><br />
By Tess Ferrandez</p>
<ul>
<li>What happens when an application domain is recycled?</li>
<li>Why does an application domain recycle?</li>
<li>How do you determine that you have application recycles?</li>
<li>How do you determine what caused an appdomain restart?</li><br />
</ul></p>
