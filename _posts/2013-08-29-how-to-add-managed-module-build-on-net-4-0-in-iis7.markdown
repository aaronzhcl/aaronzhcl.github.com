---
layout: post
status: publish
published: true
title: How to add managed module build on .NET 4.0 in IIS7
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 385
wordpress_url: http://www.webdebug.net/?p=385
date: '2013-08-29 08:39:01 +0800'
date_gmt: '2013-08-29 08:39:01 +0800'
categories:
- IIS
tags:
- IIS
- managed module
- net 4.0
comments: []
---
<p>Basic steps to add managed module to IIS,</p>
<p>1. Write the code you want to run on every request, as a .net 3.5 Class Library.<br />
2. Compile it as a strong-named assembly.<br />
3. Install the assembly in the GAC.<br />
4. In IIS7 manager, select the server name in connections, click Modules, click "Add managed module" in actions.<br />
5. Write a name for the module and choose your newly installed assembly in the type dropdown.<br />
6. Make sure the site uses an application pool running in integrated mode.</p>
<p>&nbsp;</p>
<p><strong>One question remains though!</strong></p>
<p>There are now two GAC's, Microsoft.NET for .net 4.0, and Windows GAC for pre .net 4.0. Because I created my assembly in .net 3.5, it was installed in Windows GAC, and therefore it was avalable in the type dropdown in IIS manager.</p>
<p>When I created my assembly in .net 4.0, it was installed in the Microsoft.NET GAC, and as a result, it was NOT avalable in the type dropdown in IIS manager.</p>
<p>After working with this for a bit, I managed to make it work. What I had to do was:</p>
<p>1. Create the .net 4.0 Class Library, and compile it as a strong named assembly</p>
<p>2. Install it in the .net 4.0 GAC by using the gacutil, located in Program Files (x86)\Microsoft SDKs\Windows\v7.0A\bin\NETFX 4.0 Tools</p>
<p>(Or make Visual Studio compile, sign and install the assembly automatically)</p>
<p>3. Add this line under <code><modules></code> in applicationHost.config: (it has to be done manually, it can't be done in the manager)</p>
<pre><code><add name="MyName" type="NameSpace.ClassName" preCondition="managedHandler,runtimeVersionv4.0" /></code></pre><br />
<a href="http://stackoverflow.com/questions/9210550/module-registered-in-iis7-doenst-work" target="_blank">http://stackoverflow.com/questions/9210550/module-registered-in-iis7-doenst-work</a></p>
