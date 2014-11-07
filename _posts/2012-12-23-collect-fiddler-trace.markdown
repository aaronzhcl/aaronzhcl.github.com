---
layout: post
status: publish
published: true
title: Collect Fiddler Trace
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 19
wordpress_url: http://localhost:19634/?p=19
date: '2012-12-23 14:16:33 +0800'
date_gmt: '2012-12-23 14:16:33 +0800'
categories:
- IIS
- browser
- Data Collection
tags:
- IIS
- Fiddler
- browser
- HTTP
- network
comments: []
---
<p>1. Download and install <strong>Fiddler</strong> from <a href="http://www.getfiddler.com/dl/Fiddler2Setup.exe">http://www.getfiddler.com/dl/Fiddler2Setup.exe </a><br />
2. Launch <strong>Fiddler</strong> and click <strong>Clear Cache</strong> button.<br />
3. Go to <strong>File</strong> menu and make sure<strong> Capture Traffic</strong> is checked.<br />
4. Go to <strong>Tools</strong> menu and click <strong>Fiddler Options</strong>, On <strong>Https</strong> tab check <strong>Decrypt Https Traffic</strong> and <strong>Ignore server certificate errors</strong>.<br />
5. Reproduce the issue.<br />
6. Go to <strong>File</strong> menu and click <strong>Save</strong>, choose <strong>All Sessions</strong> and save the trace as a <strong>.saz</strong> file.</p>
