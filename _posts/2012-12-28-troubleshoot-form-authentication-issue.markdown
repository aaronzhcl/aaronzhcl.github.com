---
layout: post
status: publish
published: true
title: Troubleshoot Form Authentication Issue
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 147
wordpress_url: http://www.webdebug.net:80/?p=147
date: '2012-12-28 02:55:07 +0800'
date_gmt: '2012-12-28 02:55:07 +0800'
categories:
- IIS
- ASP.NET
- Troubleshooting
tags:
- Form Authentication
- Security
comments: []
---
<p><strong><a href="http://www.iis.net/learn/troubleshoot/security-issues/troubleshooting-forms-authentication" target="_blank">Troubleshooting Forms Authentication</a></strong></p>
<p>Published on April 9, 2012 by Apurva Joshi</p>
<p>Often, while using Forms Authentication in an ASP.NET web application; there is a need to troubleshoot a problem that occurs when a fresh or an ongoing request is intermittently redirected to the application&rsquo;s login page. You can easily debug this problem on Visual Studio IDE by attaching a debugger in a development environment. In production environments, however, the task becomes hectic and problematic. To troubleshoot a random problem like this one, you need to log information related to the problem so that you can narrow down the root cause.</p>
<p>In this troubleshooter guide, we'll briefly cover the Forms Authentication concept. We'll then look into which scenarios lead to a user being redirected to the login page and how to capture data that is relevant to isolating the problem. We'll also cover how to implement an IHttpModule interface to log the Forms Authentication information.</p>
