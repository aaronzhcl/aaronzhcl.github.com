---
layout: post
status: publish
published: true
title: Collect WinINET trace
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 70
wordpress_url: http://localhost:19634/?p=70
date: '2012-12-24 14:28:18 +0800'
date_gmt: '2012-12-24 14:28:18 +0800'
categories:
- browser
- Data Collection
tags:
- browser
- WinINET
- network
comments:
- id: 21379
  author: brazilian hair straightening
  author_email: domenicgavin@gmail.com
  author_url: http://brazilianhairsa.co.za/
  date: '2014-08-24 23:23:39 +0800'
  date_gmt: '2014-08-24 23:23:39 +0800'
  content: "This piece of writing offers clear idea for the \r\nnew viewers of blogging,
    that truly how to do blogging."
---
<p>Windows 7 or above</p>
<p>(Optional) Clear IE cache<br />
1. Start command line with elevated privilege<br />
2. Execute command<br />
<code>netsh trace start scenario=InternetClient level=5 capture=yes report=yes fileMode=single maxSize=0 correlation=yes tracefile=c:\temp\trace.etl<&#47;code><br />
3. Reproduce the issue<br />
4. Stop tracing with command<br />
<code>netsh trace stop<&#47;code><br />
5. Trace is generated in c:\temp with two files below<br />
<code>c:\temp\trace.etl<br />
c:\temp\trace.cab<&#47;code></p>
