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
<p>1. Download and then install the <strong>DebugDiag</strong> from <a href="http://www.microsoft.com/download/en/details.aspx?id=26798">http://www.microsoft.com/download/en/details.aspx?id=26798</a><br />
2. Run <strong>DebugDiag Tool 1.2</strong> and click <strong>Add Rule</strong> button.<br />
3. Select <strong>Crash</strong> and click <strong>Next</strong>.<br />
4. Choose <strong>A specific IIS web application pool</strong> and click <strong>Next</strong>.<br />
5. Choose the application pool which is crashing.<br />
6. Click <strong>Next</strong> in <strong>Advanced Configuration</strong> (Optional), click on <strong>Breakpoints</strong> and then click on <strong>Add Breakpoint.</strong><br />
7. Choose <strong>Ntdll!ZwTerminateProcess</strong> from the list and change the<strong> Action Type</strong> to <strong>Full User Dump</strong> and<strong> Action Limit</strong> to <strong>5</strong> and click <strong>OK</strong>.<br />
8. Click on <strong>Save</strong> and <strong>Close.</strong><br />
9. Click next and name your rule and specify the <strong>UserDump locations</strong>.<br />
10. Select <strong>Activate the rule now</strong>.</p>
