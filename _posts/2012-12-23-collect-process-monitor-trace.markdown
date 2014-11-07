---
layout: post
status: publish
published: true
title: Collect Process Monitor Trace
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 16
wordpress_url: http://localhost:19634/?p=16
date: '2012-12-23 14:05:43 +0800'
date_gmt: '2012-12-23 14:05:43 +0800'
categories:
- IIS
- Data Collection
tags:
- IIS
- Process Monitor
- network
- Process
- File
- Registry
comments: []
---
<p>1. Download and run <strong>Process Monitor</strong> from <a href="http://technet.microsoft.com/en-us/sysinternals/bb896645.aspx">http://technet.microsoft.com/en-us/sysinternals/bb896645.aspx</a><br />
2. On the <strong>Filter</strong> menu, click <strong>Enable Advanced Output</strong>.<br />
3. Reproduce the issue.<br />
4. On the <strong>File</strong> menu, uncheck <strong>Capture Events</strong> to stop capturing.<br />
5. Click <strong>Save</strong> to save the Process Monitor log file.<br />
6. Under <strong>Events</strong> to save, click to select the <strong>All events</strong> check box.<br />
7. Under <strong>Format</strong>, click to select the <strong>Native Process Monitor Format (PML)</strong> check box.</p>
