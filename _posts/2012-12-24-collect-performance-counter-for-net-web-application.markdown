---
layout: post
status: publish
published: true
title: Collect performance counter for .Net web application
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 63
wordpress_url: http://localhost:19634/?p=63
date: '2012-12-24 14:08:10 +0800'
date_gmt: '2012-12-24 14:08:10 +0800'
categories:
- IIS
- ASP.NET
- Data Collection
tags:
- IIS
- performance counter
- .NET
comments: []
---
<p>1. Execute the following command line to create the performance logs (need admin privilege)<br />
<code>logman.exe create counter MSPerf-15Sec -f bincirc -max 500 -c "\Processor(*)\*" "\Memory\*" "\Process(*)\*" "\ASP.Net(*)\*" "\ASP.Net Applications(*)\*" "\.NET CLR Exceptions(*)\*" "\.NET CLR Memory(*)\*" "\.NET CLR Loading(*)\*" -si 00:00:15 -o C:\MSLog\MSPerf-15Sec.blg</code><br />
2. Start logging with the following command line.<br />
<code>logman.exe start MSPerf-15Sec</code><br />
3. Execute the following command line to stop the performance collecting.<br />
<code>logman.exe stop MSPerf-15Sec</code><br />
4. The performance log in generated in folder c:\MSLog</p>
