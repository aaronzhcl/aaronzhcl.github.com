---
layout: post
status: publish
published: true
title: Troubleshoot IIS 400 errors
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 135
wordpress_url: http://www.webdebug.net:80/?p=135
date: '2012-12-27 15:55:29 +0800'
date_gmt: '2012-12-27 15:55:29 +0800'
categories:
- IIS
- Troubleshooting
tags:
- IIS
- '400'
comments: []
---
<p>The Http.sys file blocks IIS from processing the request because of a problem in the request. Typically, this HTTP status code means that the request contains characters or sequences that are not valid or that the request contradicts the security settings in the Http.sys file.</p>
<p><strong><a href="http:&#47;&#47;blogs.msdn.com&#47;b&#47;webtopics&#47;archive&#47;2009&#47;01&#47;29&#47;how-to-troubleshoot-http-400-errors.aspx" target="_blank">How to troubleshoot HTTP 400 errors<&#47;a><&#47;strong><br />
By Mike Laing</p>
<p>When troubleshooting HTTP 400 conditions, first remember that the client has sent a request to IIS that breaks one or more rules that HTTP.sys is enforcing. Then, gather a network trace of the request&#47;response, to see the raw data the client is sending to the server, and the error data the server sends back to the client. Next, get the httperr.log data for the failed request. Finally, use the error message in the browser, the network trace data, and the httperr.log data to pinpoint the failure reason as per KB820729. It is possible that HTTP.sys can be configured to allow the request (although doing so may lower the security level of your IIS server), so check KB820129 to verify.</p>
<p><strong><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;820129&#47;en-us" target="_blank">Http.sys registry settings for IIS<&#47;a><&#47;strong></p>
<p>Http.sys is the kernel mode driver that handles HTTP requests. Several registry values can be configured according to specific requirements. The table in the "More Information" section contains the following information about these registry values:</p>
<ul>
<li>Registry key names<&#47;li>
<li>Default values<&#47;li>
<li>Valid value ranges<&#47;li>
<li>Registry key functions<&#47;li>
<li>WARNING codes (where appropriate)<&#47;li><br />
<&#47;ul></p>
