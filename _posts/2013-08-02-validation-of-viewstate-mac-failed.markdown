---
layout: post
status: publish
published: true
title: Validation of viewstate MAC failed
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 305
wordpress_url: http://www.webdebug.net:80/?p=305
date: '2013-08-02 09:28:56 +0800'
date_gmt: '2013-08-02 09:28:56 +0800'
categories:
- ASP.NET
tags:
- MachineKey
- viewstate
- MAC
- ASP.NET
- validationKey
comments:
- id: 16611
  author: ViewStateUserKey and ViewStateMac validation failure | Web Debug
  author_email: ''
  author_url: http://webdebug.net/2014/07/viewstateuserkey-and-viewstatemac-validation-failure/
  date: '2014-07-17 02:56:32 +0800'
  date_gmt: '2014-07-17 02:56:32 +0800'
  content: '[&#8230;] I have posted on the validation of viewstate MAC failure. We
    already know that the validationKey and validation [&#8230;]'
---
<h1>The symptom<&#47;h1><br />
View state is a feature in ASP.NET that allows pages to automatically preserve state without relying on server state (for example, session state). However, issues relating to view state can be difficult to debug. In most cases, when problems with view state occur, you receive the following error message in the Web browser, with little indication of what might be causing the issue:</p>
<blockquote><p>"The viewstate is invalid for this page and might be corrupted"</p>
<p>Validation of viewstate MAC failed. If this application is hosted by a Web Farm or cluster, ensure that configuration specifies the same validationKey and validation algorithm. AutoGenerate cannot be used in a cluster.<&#47;blockquote></p>
<h1>The theory<&#47;h1><br />
This section is from <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;magazine&#47;ff797918.aspx" target="_blank">http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;magazine&#47;ff797918.aspx<&#47;a></p>
<p>The ASP.NET feature to apply a MAC is called EnableViewStateMac, and just like ViewStateEncryptionMode, you can apply it either through a page directive or through the application&rsquo;s web.config file:</p>
<div id="ctl00_MTContentSelector1_mainContentContainer_ctl11_" class="libCScode">
<div dir="ltr" style="background-color: #ddd;">
<pre id="ctl00_MTContentSelector1_mainContentContainer_ctl11_code" class="libCScode"><%@ Page EnableViewStateMac="true" %><&#47;pre><br />
<&#47;div><br />
<&#47;div><br />
Or</p>
<div id="ctl00_MTContentSelector1_mainContentContainer_ctl12_" class="libCScode">
<div dir="ltr" style="background-color: #ddd;">
<pre id="ctl00_MTContentSelector1_mainContentContainer_ctl12_code" class="libCScode"><configuration><br />
   <system.web></p>
<pages enableViewStateMac="true"><&#47;pre><br />
<&#47;div><br />
<&#47;div><br />
To understand what EnableViewStateMac is really doing under the covers, let&rsquo;s first take a high-level look at how view state is written to the page when view state MAC is <em>not<&#47;em> enabled:</p>
<ol>
<li>View state for the page and all participating controls is gathered into a state graph object.<&#47;li>
<li>The state graph is serialized into a binary format.<&#47;li>
<li>The serialized byte array is encoded into a base-64 string.<&#47;li>
<li>The base-64 string is written to the __VIEWSTATE form value in the page.<&#47;li><br />
<&#47;ol><br />
When view state MAC is enabled, there are three additional steps that take place between the previous steps 2 and 3:</p>
<ol>
<li>View state for the page and all participating controls is gathered into a state graph object.<&#47;li>
<li>The state graph is serialized into a binary format.<br />
a.&nbsp;&nbsp;&nbsp;A secret key value is appended to the serialized byte array.<br />
b.&nbsp;&nbsp;&nbsp;A cryptographic hash is computed for the new serialized byte array.<br />
c.&nbsp;&nbsp;&nbsp;The hash is appended to the end of the serialized byte array.<&#47;li></p>
<li>The serialized byte array is encoded into a base-64 string.<&#47;li>
<li>The base-64 string is written to the __VIEWSTATE form value in the page.<&#47;li><br />
<&#47;ol><br />
Whenever this page is posted back to the server, the page code validates the incoming __VIEWSTATE by taking the incoming state graph data (deserialized from the __VIEWSTATE value), adding the same secret key value, and recomputing the hash value. If the new recomputed hash value matches the hash value supplied at the end of the incoming __VIEWSTATE, the view state is considered valid and processing proceeds. Otherwise, the view state is considered to have been tampered with and an exception is thrown.</p>
<p><img title="Figure 3 Applying a Message Authentication Code (MAC)" src="http:&#47;&#47;i.msdn.microsoft.com&#47;ff797918.Sullivan_Figure3_hires%28en-us,MSDN.10%29.png" alt="" align="Middle" &#47;></p>
<p><strong>Applying a Message Authentication Code (MAC)<&#47;strong></p>
<p>The security of this system lies in the secrecy of the secret key value. This value is always stored on the server, either in memory or in a configuration file (more on this later)&mdash;it is never written to the page. Without knowing the key, there would be no way for an attacker to compute a valid view state hash.</p>
<h1>The configuration<&#47;h1><br />
The <strong>ValidationKey<&#47;strong> property is used when <strong>enableViewStateMAC<&#47;strong> is <strong>true<&#47;strong> to create a message authentication code (MAC) to enable ASP.NET to determine whether view state has been tampered with. The <strong>ValidationKey<&#47;strong> property is also used to generate out-of-process, application-specific session IDs to ensure that session state variables are isolated between applications.</p>
<p>Use the "<strong>AutoGenerate<&#47;strong>" option to specify that ASP.NET generates a random key and stores it in the Local Security Authority. The "<strong>AutoGenerate<&#47;strong>" option is part of the default value.</p>
<p>If you add the "<strong>IsolateApps<&#47;strong>" modifier to the "<strong>AutoGenerate<&#47;strong>" <strong>ValidationKey<&#47;strong> value, ASP.NET generates a unique encrypted key for each application by using each application's <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;system.web.httpruntime.appdomainappvirtualpath.aspx">AppDomainAppVirtualPath<&#47;a>. This is the default setting.</p>
<p>If you add the "<strong>IsolateByAppId<&#47;strong>" modifier to the "<strong>AutoGenerate<&#47;strong>" <strong>ValidationKey<&#47;strong> value, ASP.NET generates a unique encrypted key for each application by using each application's <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;system.web.httpruntime.appdomainappid.aspx">AppDomainAppId<&#47;a>. If two distinct applications share a virtual path (perhaps because those applications are running on different ports), this flag can be used to further distinguish them from one another. The &ldquo;<strong>IsolateByAppId<&#47;strong>&rdquo; flag is understood only by ASP.NET 4.5, but it can be used regardless of the <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;system.web.configuration.machinekeysection.compatibilitymode.aspx">MachineKeySection.CompatibilityMode<&#47;a> setting.</p>
<p>If you need to support configuration across a network of Web servers (a Web farm), set the ValidationKey property manually to ensure consistent configuration.</p>
<p>This property is typically set declaratively in the validationKey attribute of the <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;w8h3skw9.aspx">machineKey<&#47;a> element of the Web.config file.</p>
<p>For more information about the machineKey configuration, refer to <a title="How To: Configure MachineKey in ASP.NET 2.0" href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ms998288.aspx" target="_blank">http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ms998288.aspx<&#47;a></p>
<h1>The tools<&#47;h1><br />
Fiddler has build-in Text-Wizard to decode the base64 encoded view state string. You can go to <strong>Inspectors<&#47;strong> - <strong>WebForms<&#47;strong> - Right click <strong>ViewState<&#47;strong> in body listview - Choose <strong>Send to Text-Wizard<&#47;strong></p>
<p>Another online ViewState decoder: <a href="http:&#47;&#47;ignatu.co.uk&#47;ViewStateDecoder.aspx" target="_blank">http:&#47;&#47;ignatu.co.uk&#47;ViewStateDecoder.aspx<&#47;a></p>
<h1>Reference<&#47;h1></p>
<p class="title"><strong>Understanding ASP.NET View State<&#47;strong><&#47;p><br />
<a href="http:&#47;&#47;msdn.microsoft.com&#47;library&#47;ms972976.aspx" target="_blank">http:&#47;&#47;msdn.microsoft.com&#47;library&#47;ms972976.aspx<&#47;a></p>
<p><strong>View State Security<&#47;strong></p>
<p><a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;magazine&#47;ff797918.aspx" target="_blank">http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;magazine&#47;ff797918.aspx<&#47;a></p>
<p><strong>How To: Configure MachineKey in ASP.NET 2.0<&#47;strong></p>
<p><a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ms998288.aspx" target="_blank">http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ms998288.aspx<&#47;a></p>
<p><strong>Troubleshooting the "View state is invalid" error with ASP.NET<&#47;strong></p>
<p><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;829743" target="_blank">http:&#47;&#47;support.microsoft.com&#47;kb&#47;829743<&#47;a></p>
<p><strong>Validation of viewstate MAC failed after installing .NET 3.5 SP1<&#47;strong></p>
<p><a href="http:&#47;&#47;blogs.msdn.com&#47;b&#47;tess&#47;archive&#47;2009&#47;04&#47;14&#47;validation-of-viewstate-mac-failed-after-installing-net-3-5-sp1.aspx" target="_blank">http:&#47;&#47;blogs.msdn.com&#47;b&#47;tess&#47;archive&#47;2009&#47;04&#47;14&#47;validation-of-viewstate-mac-failed-after-installing-net-3-5-sp1.aspx<&#47;a></p>
<p>&nbsp;</p>
