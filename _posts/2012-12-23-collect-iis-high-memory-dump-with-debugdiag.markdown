---
layout: post
status: publish
published: true
title: Collect IIS high memory dump with DebugDiag
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 44
wordpress_url: http://localhost:19634/?p=44
date: '2012-12-23 15:52:22 +0800'
date_gmt: '2012-12-23 15:52:22 +0800'
categories:
- IIS
- Data Collection
tags:
- IIS
- dump
- DebugDiag
- high memory
comments: []
---
<p>1. Download and then install the <strong>DebugDiag<&#47;strong> from <a href="http:&#47;&#47;www.microsoft.com&#47;download&#47;en&#47;details.aspx?id=26798">http:&#47;&#47;www.microsoft.com&#47;download&#47;en&#47;details.aspx?id=26798 <&#47;a><br />
2. Run <strong>DebugDiag Tool 1.2<&#47;strong> and click <strong>Add Rule<&#47;strong> button.<br />
3. Select <strong>Memory and Handle Leak<&#47;strong> and click <strong>Next<&#47;strong><br />
4. Click on <strong>Process Name<&#47;strong> column to sort by process name. Scroll down to see the <strong>w3wp<&#47;strong>&nbsp;processes.<br />
5. Choose the <strong>w3wp<&#47;strong> process which has memory issue (refer to <strong>commandline<&#47;strong> column for the application pool name if there are multiple w3wp process)<br />
6. On the <strong>Configure Leak Rule<&#47;strong> page, configure parameters as below,</p>
<ul>
<li>Select the <strong>Start memory tracking immediately when rule is activated<&#47;strong> radio button.<&#47;li>
<li>Click <strong>Configure<&#47;strong> in <strong>Userdump Generation<&#47;strong><&#47;li>
<li>Select <strong>Auto-create a crash rule to get userdump on unexpected process exit<&#47;strong>.<&#47;li>
<li>Select the <strong>Generate a userdump when private bytes reach<&#47;strong> check box, and make sure the default value is <strong>800<&#47;strong>.<&#47;li>
<li>Select the <strong>each additional<&#47;strong> check box, and make sure the default is <strong>200<&#47;strong>.(By selecting the virtual bytes reach option, a memory dump will automatically be created when virtual bytes uses 600 MB. If virtual bytes increases by 200 MB, another memory dump will automatically be created.)<&#47;li><br />
<&#47;ul><br />
7. Click <strong>Save &amp; Close<&#47;strong> to get back to <strong>Configure Leak Rule<&#47;strong> page<br />
8. Click <strong>Auto-unload LeakTrack when rule is completed or deactivated<&#47;strong> checkbox and click <strong>Next<&#47;strong>.<br />
9. Click next and name your rule and specify the <strong>UserDump locations<&#47;strong>.<br />
10. Click next and <strong>Activate the Rule now<&#47;strong>.</p>
