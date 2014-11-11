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
<h1>The symptom</h1><br />
View state is a feature in ASP.NET that allows pages to automatically preserve state without relying on server state (for example, session state). However, issues relating to view state can be difficult to debug. In most cases, when problems with view state occur, you receive the following error message in the Web browser, with little indication of what might be causing the issue:</p>
<blockquote><p>"The viewstate is invalid for this page and might be corrupted"</p>
<!--more-->
<p>Validation of viewstate MAC failed. If this application is hosted by a Web Farm or cluster, ensure that configuration specifies the same validationKey and validation algorithm. AutoGenerate cannot be used in a cluster.</blockquote></p>
<h1>The theory</h1><br />
This section is from <a href="http://msdn.microsoft.com/en-us/magazine/ff797918.aspx" target="_blank">http://msdn.microsoft.com/en-us/magazine/ff797918.aspx</a></p>
<p>The ASP.NET feature to apply a MAC is called EnableViewStateMac, and just like ViewStateEncryptionMode, you can apply it either through a page directive or through the application&rsquo;s web.config file:</p>
<div id="ctl00_MTContentSelector1_mainContentContainer_ctl11_" class="libCScode">
<div dir="ltr" style="background-color: #ddd;">
<pre id="ctl00_MTContentSelector1_mainContentContainer_ctl11_code" class="libCScode"><%@ Page EnableViewStateMac="true" %></pre><br />
</div><br />
</div><br />
Or</p>
<div id="ctl00_MTContentSelector1_mainContentContainer_ctl12_" class="libCScode">
<div dir="ltr" style="background-color: #ddd;">
<pre id="ctl00_MTContentSelector1_mainContentContainer_ctl12_code" class="libCScode"><configuration><br />
   <system.web></p>
<pages enableViewStateMac="true"></pre><br />
</div><br />
</div><br />
To understand what EnableViewStateMac is really doing under the covers, let&rsquo;s first take a high-level look at how view state is written to the page when view state MAC is <em>not</em> enabled:</p>
<ol>
<li>View state for the page and all participating controls is gathered into a state graph object.</li>
<li>The state graph is serialized into a binary format.</li>
<li>The serialized byte array is encoded into a base-64 string.</li>
<li>The base-64 string is written to the __VIEWSTATE form value in the page.</li><br />
</ol><br />
When view state MAC is enabled, there are three additional steps that take place between the previous steps 2 and 3:</p>
<ol>
<li>View state for the page and all participating controls is gathered into a state graph object.</li>
<li>The state graph is serialized into a binary format.<br />
a.&nbsp;&nbsp;&nbsp;A secret key value is appended to the serialized byte array.<br />
b.&nbsp;&nbsp;&nbsp;A cryptographic hash is computed for the new serialized byte array.<br />
c.&nbsp;&nbsp;&nbsp;The hash is appended to the end of the serialized byte array.</li></p>
<li>The serialized byte array is encoded into a base-64 string.</li>
<li>The base-64 string is written to the __VIEWSTATE form value in the page.</li><br />
</ol><br />
Whenever this page is posted back to the server, the page code validates the incoming __VIEWSTATE by taking the incoming state graph data (deserialized from the __VIEWSTATE value), adding the same secret key value, and recomputing the hash value. If the new recomputed hash value matches the hash value supplied at the end of the incoming __VIEWSTATE, the view state is considered valid and processing proceeds. Otherwise, the view state is considered to have been tampered with and an exception is thrown.</p>
<p><img title="Figure 3 Applying a Message Authentication Code (MAC)" src="http://i.msdn.microsoft.com/ff797918.Sullivan_Figure3_hires%28en-us,MSDN.10%29.png" alt="" align="Middle" /></p>
<p><strong>Applying a Message Authentication Code (MAC)</strong></p>
<p>The security of this system lies in the secrecy of the secret key value. This value is always stored on the server, either in memory or in a configuration file (more on this later)&mdash;it is never written to the page. Without knowing the key, there would be no way for an attacker to compute a valid view state hash.</p>
<h1>The configuration</h1><br />
The <strong>ValidationKey</strong> property is used when <strong>enableViewStateMAC</strong> is <strong>true</strong> to create a message authentication code (MAC) to enable ASP.NET to determine whether view state has been tampered with. The <strong>ValidationKey</strong> property is also used to generate out-of-process, application-specific session IDs to ensure that session state variables are isolated between applications.</p>
<p>Use the "<strong>AutoGenerate</strong>" option to specify that ASP.NET generates a random key and stores it in the Local Security Authority. The "<strong>AutoGenerate</strong>" option is part of the default value.</p>
<p>If you add the "<strong>IsolateApps</strong>" modifier to the "<strong>AutoGenerate</strong>" <strong>ValidationKey</strong> value, ASP.NET generates a unique encrypted key for each application by using each application's <a href="http://msdn.microsoft.com/en-us/library/system.web.httpruntime.appdomainappvirtualpath.aspx">AppDomainAppVirtualPath</a>. This is the default setting.</p>
<p>If you add the "<strong>IsolateByAppId</strong>" modifier to the "<strong>AutoGenerate</strong>" <strong>ValidationKey</strong> value, ASP.NET generates a unique encrypted key for each application by using each application's <a href="http://msdn.microsoft.com/en-us/library/system.web.httpruntime.appdomainappid.aspx">AppDomainAppId</a>. If two distinct applications share a virtual path (perhaps because those applications are running on different ports), this flag can be used to further distinguish them from one another. The &ldquo;<strong>IsolateByAppId</strong>&rdquo; flag is understood only by ASP.NET 4.5, but it can be used regardless of the <a href="http://msdn.microsoft.com/en-us/library/system.web.configuration.machinekeysection.compatibilitymode.aspx">MachineKeySection.CompatibilityMode</a> setting.</p>
<p>If you need to support configuration across a network of Web servers (a Web farm), set the ValidationKey property manually to ensure consistent configuration.</p>
<p>This property is typically set declaratively in the validationKey attribute of the <a href="http://msdn.microsoft.com/en-us/library/w8h3skw9.aspx">machineKey</a> element of the Web.config file.</p>
<p>For more information about the machineKey configuration, refer to <a title="How To: Configure MachineKey in ASP.NET 2.0" href="http://msdn.microsoft.com/en-us/library/ms998288.aspx" target="_blank">http://msdn.microsoft.com/en-us/library/ms998288.aspx</a></p>
<h1>The tools</h1><br />
Fiddler has build-in Text-Wizard to decode the base64 encoded view state string. You can go to <strong>Inspectors</strong> - <strong>WebForms</strong> - Right click <strong>ViewState</strong> in body listview - Choose <strong>Send to Text-Wizard</strong></p>
<p>Another online ViewState decoder: <a href="http://ignatu.co.uk/ViewStateDecoder.aspx" target="_blank">http://ignatu.co.uk/ViewStateDecoder.aspx</a></p>
<h1>Reference</h1></p>
<p class="title"><strong>Understanding ASP.NET View State</strong></p><br />
<a href="http://msdn.microsoft.com/library/ms972976.aspx" target="_blank">http://msdn.microsoft.com/library/ms972976.aspx</a></p>
<p><strong>View State Security</strong></p>
<p><a href="http://msdn.microsoft.com/en-us/magazine/ff797918.aspx" target="_blank">http://msdn.microsoft.com/en-us/magazine/ff797918.aspx</a></p>
<p><strong>How To: Configure MachineKey in ASP.NET 2.0</strong></p>
<p><a href="http://msdn.microsoft.com/en-us/library/ms998288.aspx" target="_blank">http://msdn.microsoft.com/en-us/library/ms998288.aspx</a></p>
<p><strong>Troubleshooting the "View state is invalid" error with ASP.NET</strong></p>
<p><a href="http://support.microsoft.com/kb/829743" target="_blank">http://support.microsoft.com/kb/829743</a></p>
<p><strong>Validation of viewstate MAC failed after installing .NET 3.5 SP1</strong></p>
<p><a href="http://blogs.msdn.com/b/tess/archive/2009/04/14/validation-of-viewstate-mac-failed-after-installing-net-3-5-sp1.aspx" target="_blank">http://blogs.msdn.com/b/tess/archive/2009/04/14/validation-of-viewstate-mac-failed-after-installing-net-3-5-sp1.aspx</a></p>
<p>&nbsp;</p>
