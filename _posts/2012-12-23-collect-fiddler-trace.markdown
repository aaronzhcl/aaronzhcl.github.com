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
<p>1. Download and install <strong>Fiddler<&#47;strong> from <a href="http:&#47;&#47;www.getfiddler.com&#47;dl&#47;Fiddler2Setup.exe">http:&#47;&#47;www.getfiddler.com&#47;dl&#47;Fiddler2Setup.exe <&#47;a><br />
2. Launch <strong>Fiddler<&#47;strong> and click <strong>Clear Cache<&#47;strong> button.<br />
3. Go to <strong>File<&#47;strong> menu and make sure<strong> Capture Traffic<&#47;strong> is checked.<br />
4. Go to <strong>Tools<&#47;strong> menu and click <strong>Fiddler Options<&#47;strong>, On <strong>Https<&#47;strong> tab check <strong>Decrypt Https Traffic<&#47;strong> and <strong>Ignore server certificate errors<&#47;strong>.<br />
5. Reproduce the issue.<br />
6. Go to <strong>File<&#47;strong> menu and click <strong>Save<&#47;strong>, choose <strong>All Sessions<&#47;strong> and save the trace as a <strong>.saz<&#47;strong> file.</p>
