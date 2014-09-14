---
layout: post
status: publish
published: true
title: How to capture a crash dump during application startup
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 529
wordpress_url: http://webdebug.net/?p=529
date: '2014-03-20 07:48:50 +0800'
date_gmt: '2014-03-20 07:48:50 +0800'
categories:
- Data Collection
tags:
- dump
- Crash
- procdump
- gflags
- windbg
- startup
- WER
comments: []
---
<p>As documented by <a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;q286350" target="_blank">Microsoft KB<&#47;a> it is easy to capture crash dump when the application is up and running. However there are cases application crashes during startup. How to capture such crash dump during application startup?<&#47;p>
<p>Here are a few ways to achieve the goal.<&#47;p><br />
<h2>1. ProcDump<&#47;h2>
<p><a href="http:&#47;&#47;technet.microsoft.com&#47;en-us&#47;sysinternals&#47;dd996900" target="_blank">ProcDump<&#47;a> support a -x parameter launch a process and then monitor it for exceptions:<&#47;p>
<p><strong>-x<&#47;strong><br>Launch the specified image with optional arguments. If it is a Modern Application or Package, ProcDump will start on the next activation (only).<&#47;p>
<p>Example:<&#47;p>
<p><strong>C:\>procdump -e 1 -f "" -x c:\dumps consume.exe<&#47;strong><&#47;p><br />
<h2>2. WinDBG<&#47;h2>
<p>You can install <a href="http:&#47;&#47;www.microsoft.com&#47;whdc&#47;devtools&#47;debugging&#47;">WinDBG<&#47;a> on the client machine and then use File &ndash; Open Executable to launch&nbsp; the application, press <strong><em>g<&#47;em><&#47;strong> (Go) and wait for the process to crash then type <strong>*.dump &#47;mfh [dump file name] *<&#47;strong>. Now you have dump file that you can debug.<&#47;p><br />
<h2>3. GFlags<&#47;h2>
<p>If you can't easily start the program under the debugger (for example, if it is actually a Windows service), <a href="http:&#47;&#47;bugslasher.net&#47;2010&#47;10&#47;14&#47;how-to-debug-a-windows-service&#47;">use <code>gflags<&#47;code> to make Windows start the program under the debugger.<&#47;a> This will create a subkey for your program filename <a href="http:&#47;&#47;msdn.microsoft.com&#47;library&#47;vstudio&#47;a329t4ed%28v=vs.100%29">under the <code>Image File Execution Options<&#47;code> registry key.<&#47;a><&#47;p><br />
<h2>4. Postmortem debugger<&#47;h2>
<p><a href="http:&#47;&#47;msdn.microsoft.com&#47;library&#47;windows&#47;hardware&#47;ff542967" target="_blank">Enable Postmortem debugger<&#47;a>.<&#47;p><br />
<h2>5. WER<&#47;h2>
<p>If you can't run a debugger, not even ProcDump, you can use Windows' built-in crash dump facility to create a dump automatically:<&#47;p>
<p>Starting with Windows Server 2008 and Windows Vista with Service Pack 1 (SP1), Windows Error Reporting (WER) can be configured so that full user-mode dumps are collected and stored locally after a user-mode application crashes. Applications that do their own custom crash reporting, including .NET applications, are not supported by this feature.<&#47;p>
<p><a title="http:&#47;&#47;msdn.microsoft.com&#47;library&#47;windows&#47;desktop&#47;bb787181" href="http:&#47;&#47;msdn.microsoft.com&#47;library&#47;windows&#47;desktop&#47;bb787181" target="_blank">http:&#47;&#47;msdn.microsoft.com&#47;library&#47;windows&#47;desktop&#47;bb787181<&#47;a><&#47;p><br />
<h2>6. ADPlus<&#47;h2>
<p>Monitoring for a certain process to start and to crash:
<p><strong>adplus.exe -crash -pmn notepad -o C:\Dumps<&#47;strong>
<p>The parameter passed to adplus in &ndash;pmn is the name of the process to monitor and the parameter after &ndash;o is the directory where the DMP files will be collected.<&#47;p></p>
