---
layout: post
status: publish
published: true
title: Windows Authentication and Impersonation
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 586
wordpress_url: http://webdebug.net/?p=586
date: '2014-07-11 07:18:49 +0800'
date_gmt: '2014-07-11 07:18:49 +0800'
categories:
- IIS
- ASP.NET
tags: []
comments: []
---
<p>Internet Information Services (IIS) provides several authentication schemes that can be employed when securing a Web application. Common scenarios include using Integrated Windows authentication (NTLM) within a corporate intranet to determine application users' identity based on their Windows login, or specifying a single anonymous identity for a particular application. The Windows identity supplied by IIS can then be used to determine whether the Web application has access to a protected Windows resource, such as a file protected using an Access Control List (ACL), or a network resource such as a file or database server. You can configure ASP.NET to use the Windows identity supplied by IIS using impersonation.</p>
<p>By default, ASP.NET is configured to use <span class="input">Windows<&#47;span> authentication mode, which applies the Windows identity supplied by IIS to the <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;vstudio&#47;system.web.httpcontext.user(v=vs.100).aspx">User<&#47;a> property of the current <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;vstudio&#47;system.web.httpcontext(v=vs.100).aspx">HttpContext<&#47;a> object. This enables you to determine the identity supplied by IIS through the <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;vstudio&#47;system.web.httpcontext.user(v=vs.100).aspx">User<&#47;a> property (the user <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;vstudio&#47;system.security.principal.iidentity.name(v=vs.100).aspx">Name<&#47;a> is blank when anonymous identification is used), <strong>but does not use the supplied identity as the <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;vstudio&#47;system.security.principal.windowsidentity(v=vs.100).aspx">WindowsIdentity<&#47;a> for the current page. The <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;vstudio&#47;system.security.principal.windowsidentity(v=vs.100).aspx">WindowsIdentity<&#47;a> for an application is used when determining if the application has access to a particular file or network resource.<&#47;strong></p>
<p>To configure ASP.NET to impersonate the Windows identity supplied by IIS as the <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;vstudio&#47;system.security.principal.windowsidentity(v=vs.100).aspx">WindowsIdentity<&#47;a> for the ASP.NET application, edit the Web.config file for the application and set the <span class="input">impersonate<&#47;span> attribute of the <span class="input">identity<&#47;span> configuration element to <span class="input">true<&#47;span>, as shown in the following example,</p>
<div id="code-snippet-1" class="codeSnippetContainer">
<div class="codeSnippetContainerCodeContainer">
<div id="CodeSnippetContainerCode_aaac4877-ae04-43bb-97d7-7fa2d7264e51" class="codeSnippetContainerCode" dir="ltr">
<div style="color: black;">
<pre><configuration><br />
  <system.web><br />
    <identity impersonate="true" &#47;><br />
  <&#47;system.web><br />
<&#47;configuration><br />
<&#47;pre><br />
Impersonation is independent of the authentication <span class="input">mode<&#47;span> configured using the <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;vstudio&#47;532aee0e(v=vs.100).aspx">authentication<&#47;a> configuration element. The authentication element is used to determine the <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;vstudio&#47;system.web.httpcontext.user(v=vs.100).aspx">User<&#47;a> property of the current <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;vstudio&#47;system.web.httpcontext(v=vs.100).aspx">HttpContext<&#47;a>. Impersonation is used to determine the <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;vstudio&#47;system.security.principal.windowsidentity(v=vs.100).aspx">WindowsIdentity<&#47;a> of the ASP.NET application.</p>
<p>Table below shows the resulting identities that are obtained from the various identity properties available to ASP.NET application code when your application uses Windows authentication and IIS is configured to use Integrated Windows authentication.</p>
<table class="table">
<tbody>
<tr>
<th>Web.config settings<&#47;th></p>
<th>Variable location<&#47;th></p>
<th>Resultant identity<&#47;th><br />
<&#47;tr></p>
<tr>
<td><identity impersonate="true"&#47;><br />
< authentication mode="Windows" &#47;><&#47;td></p>
<td>HttpContext<br />
WindowsIdentity<br />
Thread<&#47;td></p>
<td>Domain\UserName<br />
Domain\UserName<br />
Domain\UserName<&#47;td><br />
<&#47;tr></p>
<tr>
<td><identity impersonate="false"&#47;><br />
< authentication mode="Windows" &#47;><&#47;td></p>
<td>HttpContext<br />
WindowsIdentity<br />
Thread<&#47;td></p>
<td>Domain\UserName<br />
NT AUTHORITY\NETWORK SERVICE<br />
Domain\UserName<&#47;td><br />
<&#47;tr></p>
<tr>
<td><identity impersonate="true"&#47;><br />
< authentication mode="Forms" &#47;><&#47;td></p>
<td>HttpContext<br />
WindowsIdentity<br />
Thread<&#47;td></p>
<td>Name provided by user<br />
Domain\UserName<br />
Name provided by user<&#47;td><br />
<&#47;tr></p>
<tr>
<td><identity impersonate="false"&#47;><br />
< authentication mode="Forms" &#47;><&#47;td></p>
<td>HttpContext<br />
WindowsIdentity<br />
Thread<&#47;td></p>
<td>Name provided by user<br />
NT AUTHORITY\NETWORK SERVICE<br />
Name provided by user<&#47;td><br />
<&#47;tr><br />
<&#47;tbody><br />
<&#47;table><br />
You can check how to configure Impersonation in IIS in this article.</p>
<p><a href="http:&#47;&#47;technet.microsoft.com&#47;en-us&#47;library&#47;cc730708(v=ws.10).aspx" target="_blank">http:&#47;&#47;technet.microsoft.com&#47;en-us&#47;library&#47;cc730708(v=ws.10).aspx<&#47;a></p>
<h1><&#47;h1></p>
<h1>Reference<&#47;h1><br />
<strong>Explained: Windows Authentication in ASP.NET 2.0<&#47;strong></p>
<p><a href="Explained:%20Windows Authentication in ASP.NET 2.0" target="_blank">http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ff647076.aspx<&#47;a></p>
<p><strong>Using IIS Authentication with ASP.NET Impersonation<&#47;strong></p>
<p><a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;vstudio&#47;134ec8tc(v=vs.100).aspx" target="_blank">http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;vstudio&#47;134ec8tc(v=vs.100).aspx<&#47;a></p>
<p><strong>Configure ASP.NET Impersonation Authentication (IIS 7)<&#47;strong></p>
<p><a href="http:&#47;&#47;technet.microsoft.com&#47;en-us&#47;library&#47;cc730708(v=ws.10).aspx" target="_blank">http:&#47;&#47;technet.microsoft.com&#47;en-us&#47;library&#47;cc730708(v=ws.10).aspx<&#47;a></p>
<p><&#47;div><br />
<&#47;div><br />
<&#47;div><br />
<&#47;div></p>
