---
layout: post
status: publish
published: true
title: Collect IIS hang dump with DebugDiag
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 22
wordpress_url: http://localhost:19634/?p=22
date: '2012-12-23 14:24:08 +0800'
date_gmt: '2012-12-23 14:24:08 +0800'
categories:
- IIS
- Data Collection
tags:
- IIS
- hang
- dump
- DebugDiag
comments: []
---
<p>1. Download and Install <strong>DebugDiag<&#47;strong> on <strong>web server<&#47;strong> from <a href="http:&#47;&#47;www.microsoft.com&#47;download&#47;en&#47;details.aspx?id=26798">http:&#47;&#47;www.microsoft.com&#47;download&#47;en&#47;details.aspx?id=26798<&#47;a><br />
2. Run <strong>Debug Diag Tool 1.2<&#47;strong> and go to <strong>Processes<&#47;strong> tab.<br />
3. Right click the <strong>w3wp<&#47;strong> process and click <strong>Create Full User Dump<&#47;strong> (refer to <strong>command line<&#47;strong> column for the hanging application if there are multiple w3wp process listed)<br />
4. A dialog will pop up after the dump is created and shows the dump location.</p>
