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
<p>As documented by <a href="http://support.microsoft.com/kb/q286350" target="_blank">Microsoft KB</a> it is easy to capture crash dump when the application is up and running. However there are cases application crashes during startup. How to capture such crash dump during application startup?</p>
<p>Here are a few ways to achieve the goal.</p><br />
<h2>1. ProcDump</h2>
<p><a href="http://technet.microsoft.com/en-us/sysinternals/dd996900" target="_blank">ProcDump</a> support a -x parameter launch a process and then monitor it for exceptions:</p>
<p><strong>-x</strong><br>Launch the specified image with optional arguments. If it is a Modern Application or Package, ProcDump will start on the next activation (only).</p>
<p>Example:</p>
<p><strong>C:\>procdump -e 1 -f "" -x c:\dumps consume.exe</strong></p><br />
<h2>2. WinDBG</h2>
<p>You can install <a href="http://www.microsoft.com/whdc/devtools/debugging/">WinDBG</a> on the client machine and then use File &ndash; Open Executable to launch&nbsp; the application, press <strong><em>g</em></strong> (Go) and wait for the process to crash then type <strong>*.dump /mfh [dump file name] *</strong>. Now you have dump file that you can debug.</p><br />
<h2>3. GFlags</h2>
<p>If you can't easily start the program under the debugger (for example, if it is actually a Windows service), <a href="http://bugslasher.net/2010/10/14/how-to-debug-a-windows-service/">use <code>gflags</code> to make Windows start the program under the debugger.</a> This will create a subkey for your program filename <a href="http://msdn.microsoft.com/library/vstudio/a329t4ed%28v=vs.100%29">under the <code>Image File Execution Options</code> registry key.</a></p><br />
<h2>4. Postmortem debugger</h2>
<p><a href="http://msdn.microsoft.com/library/windows/hardware/ff542967" target="_blank">Enable Postmortem debugger</a>.</p><br />
<h2>5. WER</h2>
<p>If you can't run a debugger, not even ProcDump, you can use Windows' built-in crash dump facility to create a dump automatically:</p>
<p>Starting with Windows Server 2008 and Windows Vista with Service Pack 1 (SP1), Windows Error Reporting (WER) can be configured so that full user-mode dumps are collected and stored locally after a user-mode application crashes. Applications that do their own custom crash reporting, including .NET applications, are not supported by this feature.</p>
<p><a title="http://msdn.microsoft.com/library/windows/desktop/bb787181" href="http://msdn.microsoft.com/library/windows/desktop/bb787181" target="_blank">http://msdn.microsoft.com/library/windows/desktop/bb787181</a></p><br />
<h2>6. ADPlus</h2>
<p>Monitoring for a certain process to start and to crash:
<p><strong>adplus.exe -crash -pmn notepad -o C:\Dumps</strong>
<p>The parameter passed to adplus in &ndash;pmn is the name of the process to monitor and the parameter after &ndash;o is the directory where the DMP files will be collected.</p></p>
