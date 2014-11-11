---
layout: post
status: publish
published: true
title: Troubleshoot IIS crash issue
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 104
wordpress_url: http://www.webdebug.net:80/?p=104
date: '2012-12-26 07:24:44 +0800'
date_gmt: '2012-12-26 07:24:44 +0800'
categories:
- IIS
- ASP.NET
- Troubleshooting
tags:
- IIS
- DebugDiag
- Crash
- .NET
comments: []
---
<p><a href="http://blogs.msdn.com/b/tess/archive/2009/03/20/debugging-a-net-crash-with-rules-in-debug-diag.aspx" target="_blank"><strong>Debugging a .NET crash with rules in Debug Diag</strong></a><br />
By Tess Ferrandez</p>
<p>Even though debugging might be tricky, setting up rules in Debug Diag is beautifully simple and I personally believe that it would be a good idea for anyone running a web site to have debug diag installed along with a few instructions for the ops personnel on how to set up the rules. Better yet, you can set up the rules in advance and just activate or deactivate them as needed.</p>
<p><strong>Problem description</strong><br />
The application crashes with the following event in the eventlog</p>
<p><code>Log Name: Application<br />
Source: Application Error<br />
Date: 2009-03-20 11:12:09<br />
Event ID: 1000<br />
Task Category: (100)<br />
Level: Error<br />
Keywords: Classic<br />
User: N/A<br />
Computer: MYMACHINE<br />
Description:<br />
Faulting application w3wp.exe, version 7.0.6001.18000, time stamp 0x47919413, faulting module kernel32.dll, version 6.0.6001.18000, time stamp 0x4791a76d, exception code 0xe053534f, fault offset 0x000442eb, process id 0x%9, application start time 0x%10.</code></p>
<!--more-->
<p><a href="http://blogs.msdn.com/b/tess/archive/2006/04/27/asp-net-2-0-crash-case-study-unhandled-exceptions.aspx" target="_blank"><strong>ASP.NET 2.0 Crash case study: Unhandled exceptions</strong></a><br />
By Tess Ferrandez</p>
<p><strong>Problem description</strong><br />
Once in a while ASP.NET crashes and we see events in the system event log like this one</p>
<p><code>Event Type: Warning<br />
Event Source: W3SVC<br />
Event Category: None<br />
Event ID: 1009<br />
Date: 2006-04-25<br />
Time: 09:41:22<br />
PM User: N/A<br />
Computer: SUBSPACE1<br />
Description:<br />
A process serving application pool 'ASP.NET V2.0' terminated unexpectedly. The process id was &lsquo;1732&rsquo;. The process exit code was &lsquo;0xe0434f4d&rsquo;.</code></p>
<p>Or this one</p>
<p><code>Event Type: Warning<br />
Event Source: W3SVC<br />
Event Category: None<br />
Event ID: 1011<br />
Date: 2006-04-25<br />
Time: 09:41:22<br />
User: N/A<br />
Computer: SUBSPACE1<br />
Description:<br />
A process serving application pool 'ASP.NET V2.0' suffered a fatal communication error with the World Wide Web Publishing Service. The process id was '6256'. The data field contains the error number.<br />
</code><br />
And in the application event log we get a pretty cryptic error message like this one</p>
<p><code>Event Type: Error<br />
Event Source: .NET Runtime 2.0 Error Reporting<br />
Event Category: None<br />
Event ID: 5000<br />
Date: 2006-04-25<br />
Time: 09:41:20<br />
User: N/A<br />
Computer: SUBSPACE1<br />
Description:<br />
EventType clr20r3, P1 w3wp.exe, P2 6.0.3790.1830, P3 42435be1, P4 app_code.pn5mfdcr, P5 0.0.0.0, P6 444dcf44, P7 5, P8 5, P9 system.dividebyzeroexception, P10 NIL.</code></p>
<p>I assumed you understand the exception processing in CLR, but if you are not, please refer to the article below.</p>
<p><strong><a href="http://msdn.microsoft.com/en-us/magazine/cc793966.aspx" target="_blank">Unhandled Exception Processing In The CLR</a></strong><br />
By Gaurav Khanna</p>
<p>Contents<br />
Managed Exception Handling<br />
Thread Base and Unhandled Managed Exceptions<br />
Unhandled Managed Exceptions on CLR-Created Threads<br />
Unhandled Exceptions on Non-CLR-Created Threads<br />
Unhandled Exception Processing<br />
AppDomain.UnhandledException Event Notification<br />
Future Concerns</p>
