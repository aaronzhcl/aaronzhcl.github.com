---
layout: post
status: publish
published: true
title: How to Capture WinHttp trace
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 379
wordpress_url: http://www.webdebug.net/?p=379
date: '2013-08-28 06:35:57 +0800'
date_gmt: '2013-08-28 06:35:57 +0800'
categories:
- Data Collection
tags:
- network
- winhttp
- trace
comments: []
---
<p>Since&nbsp; there are multiple ways to gather this in the Windows 2008 and 2008R2 I thought this might be helpful to outline this for the different platforms and how to gather this for fellow ARR troubleshooters.</p>
<h2>Windows 2008</h2><br />
1. Start the Tracing . From a command prompt run the following command:</p>
<blockquote><p>netsh winhttp set tracing trace-file-prefix="C:\TEMP\WinHttpLog" level=verbose format=hex state=enabled max-trace-file-size=1048576000</blockquote><br />
2.Recycle the IIS Application Pool.</p>
<p>3. Reproduce the issue.</p>
<p>4. Stop the Tracing. From a command prompt run the following command:</p>
<blockquote><p>netsh winhttp set tracing state=disabled</blockquote><br />
5. Review the trace with Notepad or any Text editor.</p>
<p>NOTE: The Identity of the&nbsp; IIS application pool will require write access to the&nbsp; log location&nbsp; c:\Temp in this example:</p>
<p>This type of tracing is process bitness specific, so if you are looking at a 32 bit process running from 64 bit OS, you need to use: c:\windows\syswow64\cmd.exe, rather than using the regular 64 bit cmd.exe (start a run a cmd.exe)</p>
<!--more-->
<h2>Windows 2008 R2</h2></p>
<h3>Method 1</h3><br />
This method will output the Winhttp API calls , but not raw data for network communication. From a command prompt run the following command:</p>
<p>1. Start the tracing</p>
<blockquote><p>netsh winhttp set tracing trace-file-prefix="C:\Temp\Test3" level=verbose format=hex</blockquote></p>
<blockquote><p>netsh winhttp set tracing output=file max-trace-file-size=512000 state=enabled</blockquote><br />
2.Recycle the IIS Application Pool.</p>
<p>3. Reproduce the issue.</p>
<p>4. Stop the Tracing. From a command prompt run the following command:</p>
<blockquote><p>netsh winhttp set tracing state=disabled</blockquote><br />
5. Review the trace with Notepad or any Text editor.</p>
<p><strong>NOTE</strong>: The Identity of the IIS application pool will require write access to the log location c:\Temp in this example:</p>
<p>This type of tracing is process bitness specific, so if you are looking at a 32 bit process running from 64 bit OS, you need to use: c:\windows\syswow64\cmd.exe, rather than using the regular 64 bit cmd.exe (start a run a cmd.exe)</p>
<h3>Method 2</h3><br />
To get the raw data communication at network layer and the Winhttp&nbsp; Api calls.</p>
<p>1. Start the tracing: From a command prompt run the following command:</p>
<blockquote><p>netsh trace start scenario=InternetClient capture=yes <strong>report=yes</strong></blockquote></p>
<blockquote><p>Note the etl file location for example:</p>
<p>Trace File:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; C:\Users\<your user name>\AppData\Local\Temp\NetTraces\NetTrace.etl</blockquote><br />
2.Recycle the IIS Application Pool.</p>
<p>3. Reproduce the issue.</p>
<p>4. Stop the tracing: From a command prompt run the following command:</p>
<blockquote><p>netsh trace stop</blockquote><br />
5. Read the Trace by opening it in Netmon 3.4.</p>
<h3>Method 3</h3><br />
The ETW format for winhttp API is available on windows 2008 R2 and win7 via the Event Viewer</p>
<p>1.&nbsp; Open event viewer. Go to &ldquo;View&rdquo; menu --> make sure &ldquo;Show Analytic and debug logs&rdquo; is checked.</p>
<p>2. Open &ldquo;Applications and Services logs&rdquo; -- > Open &ldquo;Microsoft&rdquo; -- > Open &ldquo;Windows &ndash;> Winhttp &ndash;> Diagnostic.</p>
<p><a href="http://blogs.iis.net/blogs/richma/clip_image002_50AD7A2B.jpg"><img title="clip_image002" alt="clip_image002" src="http://blogs.iis.net/blogs/richma/clip_image002_thumb_3DF88074.jpg" width="413" height="164" border="0" /></a></p>
<p>3. Highlight &ldquo;Diagnostic&rdquo; under Winhttp tree and right click mouse, then click &ldquo;enable log&rdquo;.</p>
<p>4.&nbsp; Reproduce the issue then you can review the logs.</p>
<p>&nbsp;</p>
<p><a href="http://blogs.iis.net/richma/archive/2012/08/24/winhttp-tracing-options-for-troubleshooting-with-application-request-routing.aspx" target="_blank">Winhttp Tracing Options for Troubleshooting with Application Request Routing </a>By Richard Marr</p>
