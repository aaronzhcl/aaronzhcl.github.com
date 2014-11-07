---
layout: post
status: publish
published: true
title: IE Redirection Limit
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 473
wordpress_url: http://webdebug.net/?p=473
date: '2014-02-13 03:18:57 +0800'
date_gmt: '2014-02-13 03:18:57 +0800'
categories:
- browser
tags:
- IE
- IE8
- redirection limit
- MaxHttpRedirects
comments: []
---
<p><a href="http://webdebug.net/wp-content/uploads/2014/02/301-302-redirect.jpg"><img class="alignright size-medium wp-image-488" alt="301-302-redirect" src="http://webdebug.net/wp-content/uploads/2014/02/301-302-redirect-300x155.jpg" width="300" height="155" /></a>Users might get &ldquo;This page can&rsquo;t be displayed&rdquo; error in IE7 or IE8 when a website requires too many redirections to go to the destination page. The question is how much redirection will be considered as &ldquo;too many&rdquo;.</p>
<p>IE7 and IE8 sets the default value of redirection limit as 10, so if a webpage causes more than 10 continuous redirection, &ldquo;Page can&rsquo;t be displayed&rdquo; error will be displayed.</p>
<p>This limit can be changed by adding the following registry key,</p>
<p><strong>HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings</strong></p>
<p><strong>Value: MaxHttpRedirects</strong></p>
<p><strong>Type: DWORD</strong></p>
<p>However, from IE9 IE has increase this value by multiplying a coefficient (11). Since the default value of MaxHttpRedirects is kept as 10, the redirection limit will be 10*11 = 110 since IE9.</p>
<p>If you chance the registry to 20, then the redirection limit will be 20 * 11 = 220.</p>
