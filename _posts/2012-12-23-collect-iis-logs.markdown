---
layout: post
status: publish
published: true
title: Collect IIS logs
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 5
wordpress_url: http://localhost:19634/?p=5
date: '2012-12-23 13:36:26 +0800'
date_gmt: '2012-12-23 13:36:26 +0800'
categories:
- IIS
- Data Collection
tags:
- IIS log
- IIS
- network
comments: []
---
<p>IIS 6 log file:</p>
<p>1. In <strong>IIS Manager<&#47;strong>, expand the <strong>local computer<&#47;strong>, expand the <strong>Web Sites<&#47;strong> directory, right-click the Web site which has problem, and click <strong>Properties<&#47;strong>.<br />
2. On the <strong>Web Site<&#47;strong> tab, click <strong>Properties<&#47;strong> next to the <strong>Active log format<&#47;strong> list box.<br />
3. Under <strong>Log file<&#47;strong> directory, you can check the logging path and the log file name.<br />
4. Go to the path and find the log files.</p>
<p>IIS 7 log file:</p>
<p>1. In <strong>IIS Manager<&#47;strong>, expand the <strong>local computer<&#47;strong>.<br />
2. Click <strong>Sites<&#47;strong>. Check the <strong>ID<&#47;strong> of your website from the <strong>ID<&#47;strong> column.<br />
3. Click the web site which has problem. Double-click <strong>Logging<&#47;strong> icon on the <strong>Feature View<&#47;strong>.<br />
4. On the <strong>Logging<&#47;strong> window, you can find log&rsquo;s directory.<br />
5. Go to the folder end with your website ID and find the IIS log files.</p>
