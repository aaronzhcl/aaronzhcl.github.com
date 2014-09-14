---
layout: post
status: publish
published: true
title: Request Filtering vs URLScan
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 228
wordpress_url: http://www.webdebug.net:80/?p=228
date: '2013-06-21 07:10:12 +0800'
date_gmt: '2013-06-21 07:10:12 +0800'
categories:
- IIS
tags:
- urlscan
- request filtering
- IIS 7
comments: []
---
<p>UrlScan, a security tool, was provided as an add-on to earlier versions of Internet Information Services (IIS) so administrators could enforce tighter security policies on their Web servers. Within IIS 7 and above, all the core features of URLScan have been incorporated into a module called Request Filtering, and a Hidden Segments feature has been added..</p>
<ul>
<li>It gives a tighter level of control over the settings and where they are applied.<&#47;li>
<li>It can be configured from the GUI as well as web.config file.<&#47;li><br />
<&#47;ul><br />
<a href="http:&#47;&#47;www.webdebug.net:80&#47;wp-content&#47;uploads&#47;2013&#47;06&#47;request-filtering.png"><img class="alignnone size-full wp-image-241" alt="request-filtering" src="http:&#47;&#47;www.webdebug.net:80&#47;wp-content&#47;uploads&#47;2013&#47;06&#47;request-filtering.png" width="443" height="264" &#47;><&#47;a></p>
<p>There are plenty of great resources online, I&rsquo;ll provide some links for your reference below.</p>
<p><a href="http:&#47;&#47;www.iis.net&#47;ConfigReference&#47;system.webServer&#47;security&#47;requestFiltering">http:&#47;&#47;www.iis.net&#47;ConfigReference&#47;system.webServer&#47;security&#47;requestFiltering<&#47;a></p>
<p><a href="http:&#47;&#47;learn.iis.net&#47;page.aspx&#47;143&#47;use-request-filtering&#47;">http:&#47;&#47;learn.iis.net&#47;page.aspx&#47;143&#47;use-request-filtering&#47;<&#47;a></p>
<p><a href="http:&#47;&#47;learn.iis.net&#47;page.aspx&#47;504&#47;using-enhanced-request-filtering-features-in-iis&#47;">http:&#47;&#47;learn.iis.net&#47;page.aspx&#47;504&#47;using-enhanced-request-filtering-features-in-iis&#47;<&#47;a></p>
