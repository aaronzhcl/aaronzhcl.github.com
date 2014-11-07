---
layout: post
status: publish
published: true
title: Collect IIS high CPU dump with procdump
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 66
wordpress_url: http://localhost:19634/?p=66
date: '2012-12-24 14:15:00 +0800'
date_gmt: '2012-12-24 14:15:00 +0800'
categories:
- IIS
- Data Collection
tags:
- IIS
- dump
- procdump
comments: []
---
<p>1. Download procdump from <a href="http://technet.microsoft.com/en-us/sysinternals/dd996900.aspx">http://technet.microsoft.com/en-us/sysinternals/dd996900.aspx</a><br />
2.&nbsp;Create a folder for saving the dumps like c:\dumps<br />
3.&nbsp;Start a command prompt and switch to the procdump folder.<br />
4.&nbsp;Run the command in command line (Generate 3 dumps if CPU is above 80% for more than 20 seconds)<br />
<code>procdump -c 80 -s 20 -n 3 -ma -o {PID of the high cpu w3wp process} c:\dumps</code></p>
<p><strong>Note</strong>:<br />
1. If application pool recycles, w3wp process stops (crash or auto stop due to idle), need to rerun the command when the process starts again<br />
2. User session cannot logout<br />
3. !runaway information may lost from dumps, work around <a href="http://forum.sysinternals.com/procdump-12-and-runaway_topic19909.html">http://forum.sysinternals.com/procdump-12-and-runaway_topic19909.html</a></p>
