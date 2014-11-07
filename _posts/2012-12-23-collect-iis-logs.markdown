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
<p>1. In <strong>IIS Manager</strong>, expand the <strong>local computer</strong>, expand the <strong>Web Sites</strong> directory, right-click the Web site which has problem, and click <strong>Properties</strong>.<br />
2. On the <strong>Web Site</strong> tab, click <strong>Properties</strong> next to the <strong>Active log format</strong> list box.<br />
3. Under <strong>Log file</strong> directory, you can check the logging path and the log file name.<br />
4. Go to the path and find the log files.</p>
<p>IIS 7 log file:</p>
<p>1. In <strong>IIS Manager</strong>, expand the <strong>local computer</strong>.<br />
2. Click <strong>Sites</strong>. Check the <strong>ID</strong> of your website from the <strong>ID</strong> column.<br />
3. Click the web site which has problem. Double-click <strong>Logging</strong> icon on the <strong>Feature View</strong>.<br />
4. On the <strong>Logging</strong> window, you can find log&rsquo;s directory.<br />
5. Go to the folder end with your website ID and find the IIS log files.</p>
