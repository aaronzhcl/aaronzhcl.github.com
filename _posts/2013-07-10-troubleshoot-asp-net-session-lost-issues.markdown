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
<p>ASP.NET session state supports several different storage options for session data. Each option is identified by a value in the <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;system.web.sessionstate.sessionstatemode.aspx">SessionStateMode<&#47;a> enumeration. The following list describes the available session state modes:</p>
<ul>
<li><strong>InProc<&#47;strong> mode, which stores session state in memory on the Web server. This is the default.<&#47;li>
<li><strong>StateServer<&#47;strong> mode, which stores session state in a separate process called the ASP.NET state service. This ensures that session state is preserved if the Web application is restarted and also makes session state available to multiple Web servers in a Web farm.<&#47;li>
<li><strong>SQLServer<&#47;strong> mode stores session state in a SQL Server database. This ensures that session state is preserved if the Web application is restarted and also makes session state available to multiple Web servers in a Web farm.<&#47;li>
<li><strong>Custom<&#47;strong> mode, which enables you to specify a custom storage provider.<&#47;li>
<li><strong>Off<&#47;strong> mode, which disables session state.<&#47;li><br />
<&#47;ul><br />
ASP.NET provides two events that help you manage user sessions: the Session_OnStart event, which is raised when a new session begins, and the Session_OnEnd event, which is raised when a session is abandoned or expires.</p>
<p><strong>Note:<&#47;strong></p>
<p>If the Global.asax file or Web.config file for an ASP.NET application is modified, the application will be restarted. If the current session-state mode is <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;system.web.sessionstate.sessionstatemode.aspx">InProc<&#47;a>, any values stored in application state or session state will be lost. Be aware that some anti-virus software can update the last-modified date and time of the Global.asax or Web.config file for an application. For information on setting the session state mode, see <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ms178586.aspx">Session-State Modes<&#47;a>.</p>
<p>To use StateServer mode in a Web farm, you must have the same encryption keys specified in the <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;w8h3skw9.aspx">machineKey<&#47;a> element of your Web configuration for all applications that are part of the Web farm. For information on how to create machine keys, see article 313091, "How to create keys by using Visual Basic .NET for use in Forms authentication," in the Microsoft Knowledge Base at http:&#47;&#47;support.microsoft.com.</p>
<p><b>Session-State Events<&#47;b></p>
<p><a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ms178583.aspx">http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ms178583.aspx<&#47;a></p>
<p><b>Detecting Session Timeout in ASP.NET 2.0 Web Applications<&#47;b></p>
<p><a href="http:&#47;&#47;blogs.msdn.com&#47;b&#47;nikhiln&#47;archive&#47;2007&#47;06&#47;21&#47;detecting-session-timeout-in-asp-net-2-0-web-applications.aspx">http:&#47;&#47;blogs.msdn.com&#47;b&#47;nikhiln&#47;archive&#47;2007&#47;06&#47;21&#47;detecting-session-timeout-in-asp-net-2-0-web-applications.aspx<&#47;a></p>
<p>&nbsp;</p>
<p><b>Session-State Modes<&#47;b></p>
<p><a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ms178586.aspx">http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ms178586.aspx<&#47;a></p>
<p><b>Configure a State Server to Maintain Session State (IIS 7)<&#47;b></p>
<p><a href="http:&#47;&#47;technet.microsoft.com&#47;en-us&#47;library&#47;cc732412(v=WS.10).aspx">http:&#47;&#47;technet.microsoft.com&#47;en-us&#47;library&#47;cc732412(v=WS.10).aspx<&#47;a></p>
<p><b>Generate a Machine Key for a Web Farm (IIS 7)<&#47;b></p>
<p><a href="http:&#47;&#47;technet.microsoft.com&#47;en-us&#47;library&#47;cc731979(v=ws.10).aspx">http:&#47;&#47;technet.microsoft.com&#47;en-us&#47;library&#47;cc731979(v=ws.10).aspx<&#47;a></p>
<p><b>HOW TO: Configure SQL Server to Store ASP.NET Session State<&#47;b></p>
<p><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;317604">http:&#47;&#47;support.microsoft.com&#47;kb&#47;317604<&#47;a></p>
<p><b>Session State Management<&#47;b></p>
<p><a href="http:&#47;&#47;blogs.msdn.com&#47;b&#47;paraga&#47;archive&#47;2005&#47;12&#47;10&#47;502345.aspx">http:&#47;&#47;blogs.msdn.com&#47;b&#47;paraga&#47;archive&#47;2005&#47;12&#47;10&#47;502345.aspx<&#47;a></p>
