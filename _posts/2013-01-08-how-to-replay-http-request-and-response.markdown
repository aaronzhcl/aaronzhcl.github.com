---
layout: post
status: publish
published: true
title: How to replay HTTP request and response
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 179
wordpress_url: http://www.webdebug.net:80/?p=179
date: '2013-01-08 06:29:47 +0800'
date_gmt: '2013-01-08 06:29:47 +0800'
categories:
- browser
- Data Collection
- Troubleshooting
tags:
- Fiddler
- browser
- replay
- autoresponder
- strace
- httpreplay
- network
comments: []
---
<p>You would normally want to replay a page you are troubleshooting first and see if you are able to reproduce the reported behavior. The nice thing about this tool is that you can manipulate many things including browser agents, script, css images, introduce latency and more.</p>
<p><strong><a href="http://blogs.msdn.com/b/askie/archive/2013/01/06/how-to-use-fiddler-autoresponder-to-replay-a-fiddler-trace.aspx" target="_blank">How to use Fiddler Autoresponder to replay a fiddler trace</a></strong><br />
By AxelRMSFT</p>
<!--more-->
<p>In this quick tutorial, we want to show you how to use Fiddler&rsquo;s Autoreponder to replay a previously captured or generated fiddler trace when trying to isolate html code performance or page errors. The Fiddler AutoResponder is an excellent way to replay and reproduce a particular scenario, which makes troubleshooting a lot easier and less invasive when working out of production environments.</p>
<p><strong><a href="http://www.microsoft.com/en-us/download/details.aspx?id=7643" target="_blank">STRACE is a socket/SSL tracer designed to generate LOG for Internet Explorer</a></strong><br />
Another way to replay the http request and response is using Strace, STRACE is a socket/SSL tracer that is based on the "detours" utility. The tool has been specificaly designed to generate LOG for Internet Explorer but it can be used with many other applications.</p>
<p>Using STRACE with Internet Explorer is equivalent to use a (non full) debug build of WININET.DLL to generate a WININET LOG. The STRACE LOG contains clear text HTTP traffic (with socket information) and encrypted/decrypted SSL data.</p>
<p>From the STRACE LOG, you can "replay" a full navigation scenario using the HTTPREPLAY tool. This can be useful to reproduce a problem or browse web sites offline...</p>
