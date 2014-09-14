---
layout: post
status: publish
published: true
title: Collect IIS crash dump with DebugDiag
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 40
wordpress_url: http://localhost:19634/?p=40
date: '2012-12-23 15:22:36 +0800'
date_gmt: '2012-12-23 15:22:36 +0800'
categories:
- IIS
- Data Collection
tags:
- IIS
- dump
- DebugDiag
- Crash
comments: []
---
<p>1. Download and then install the <strong>DebugDiag<&#47;strong> from <a href="http:&#47;&#47;www.microsoft.com&#47;download&#47;en&#47;details.aspx?id=26798">http:&#47;&#47;www.microsoft.com&#47;download&#47;en&#47;details.aspx?id=26798<&#47;a><br />
2. Run <strong>DebugDiag Tool 1.2<&#47;strong> and click <strong>Add Rule<&#47;strong> button.<br />
3. Select <strong>Crash<&#47;strong> and click <strong>Next<&#47;strong>.<br />
4. Choose <strong>A specific IIS web application pool<&#47;strong> and click <strong>Next<&#47;strong>.<br />
5. Choose the application pool which is crashing.<br />
6. Click <strong>Next<&#47;strong> in <strong>Advanced Configuration<&#47;strong> (Optional), click on <strong>Breakpoints<&#47;strong> and then click on <strong>Add Breakpoint.<&#47;strong><br />
7. Choose <strong>Ntdll!ZwTerminateProcess<&#47;strong> from the list and change the<strong> Action Type<&#47;strong> to <strong>Full User Dump<&#47;strong> and<strong> Action Limit<&#47;strong> to <strong>5<&#47;strong> and click <strong>OK<&#47;strong>.<br />
8. Click on <strong>Save<&#47;strong> and <strong>Close.<&#47;strong><br />
9. Click next and name your rule and specify the <strong>UserDump locations<&#47;strong>.<br />
10. Select <strong>Activate the rule now<&#47;strong>.</p>
