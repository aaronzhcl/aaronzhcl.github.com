---
layout: post
status: publish
published: true
title: Troubleshoot asp.net session lost issues
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 262
wordpress_url: http://www.webdebug.net:80/?p=262
date: '2013-07-10 05:07:50 +0800'
date_gmt: '2013-07-10 05:07:50 +0800'
categories:
- ASP.NET
tags:
- session lost
- InProc
- StateServer
- SQLServer
- MachineKey
comments: []
---
<p>ASP.NET session state supports several different storage options for session data. Each option is identified by a value in the <a href="http://msdn.microsoft.com/en-us/library/system.web.sessionstate.sessionstatemode.aspx">SessionStateMode</a> enumeration. The following list describes the available session state modes:</p>
<!--more-->
<ul>
<li><strong>InProc</strong> mode, which stores session state in memory on the Web server. This is the default.</li>
<li><strong>StateServer</strong> mode, which stores session state in a separate process called the ASP.NET state service. This ensures that session state is preserved if the Web application is restarted and also makes session state available to multiple Web servers in a Web farm.</li>
<li><strong>SQLServer</strong> mode stores session state in a SQL Server database. This ensures that session state is preserved if the Web application is restarted and also makes session state available to multiple Web servers in a Web farm.</li>
<li><strong>Custom</strong> mode, which enables you to specify a custom storage provider.</li>
<li><strong>Off</strong> mode, which disables session state.</li><br />
</ul><br />
ASP.NET provides two events that help you manage user sessions: the Session_OnStart event, which is raised when a new session begins, and the Session_OnEnd event, which is raised when a session is abandoned or expires.</p>
<p><strong>Note:</strong></p>
<p>If the Global.asax file or Web.config file for an ASP.NET application is modified, the application will be restarted. If the current session-state mode is <a href="http://msdn.microsoft.com/en-us/library/system.web.sessionstate.sessionstatemode.aspx">InProc</a>, any values stored in application state or session state will be lost. Be aware that some anti-virus software can update the last-modified date and time of the Global.asax or Web.config file for an application. For information on setting the session state mode, see <a href="http://msdn.microsoft.com/en-us/library/ms178586.aspx">Session-State Modes</a>.</p>
<p>To use StateServer mode in a Web farm, you must have the same encryption keys specified in the <a href="http://msdn.microsoft.com/en-us/library/w8h3skw9.aspx">machineKey</a> element of your Web configuration for all applications that are part of the Web farm. For information on how to create machine keys, see article 313091, "How to create keys by using Visual Basic .NET for use in Forms authentication," in the Microsoft Knowledge Base at http://support.microsoft.com.</p>
<p><b>Session-State Events</b></p>
<p><a href="http://msdn.microsoft.com/en-us/library/ms178583.aspx">http://msdn.microsoft.com/en-us/library/ms178583.aspx</a></p>
<p><b>Detecting Session Timeout in ASP.NET 2.0 Web Applications</b></p>
<p><a href="http://blogs.msdn.com/b/nikhiln/archive/2007/06/21/detecting-session-timeout-in-asp-net-2-0-web-applications.aspx">http://blogs.msdn.com/b/nikhiln/archive/2007/06/21/detecting-session-timeout-in-asp-net-2-0-web-applications.aspx</a></p>
<p>&nbsp;</p>
<p><b>Session-State Modes</b></p>
<p><a href="http://msdn.microsoft.com/en-us/library/ms178586.aspx">http://msdn.microsoft.com/en-us/library/ms178586.aspx</a></p>
<p><b>Configure a State Server to Maintain Session State (IIS 7)</b></p>
<p><a href="http://technet.microsoft.com/en-us/library/cc732412(v=WS.10).aspx">http://technet.microsoft.com/en-us/library/cc732412(v=WS.10).aspx</a></p>
<p><b>Generate a Machine Key for a Web Farm (IIS 7)</b></p>
<p><a href="http://technet.microsoft.com/en-us/library/cc731979(v=ws.10).aspx">http://technet.microsoft.com/en-us/library/cc731979(v=ws.10).aspx</a></p>
<p><b>HOW TO: Configure SQL Server to Store ASP.NET Session State</b></p>
<p><a href="http://support.microsoft.com/kb/317604">http://support.microsoft.com/kb/317604</a></p>
<p><b>Session State Management</b></p>
<p><a href="http://blogs.msdn.com/b/paraga/archive/2005/12/10/502345.aspx">http://blogs.msdn.com/b/paraga/archive/2005/12/10/502345.aspx</a></p>
