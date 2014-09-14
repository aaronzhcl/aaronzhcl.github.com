---
layout: post
status: publish
published: true
title: Troubleshoot IIS 401 errors
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 129
wordpress_url: http://www.webdebug.net:80/?p=129
date: '2012-12-27 15:47:30 +0800'
date_gmt: '2012-12-27 15:47:30 +0800'
categories:
- IIS
- Troubleshooting
tags:
- IIS
- '401'
comments: []
---
<p><strong>IIS 6<&#47;strong></p>
<p><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;907273" target="_blank"><strong>Troubleshooting HTTP 401 errors in IIS<&#47;strong><&#47;a><br />
<a href="http:&#47;&#47;technet.microsoft.com&#47;library&#47;cc786094(v=WS.10).aspx" target="_blank"><strong>401.1 and 401.2-Authentication Problems<&#47;strong><&#47;a></p>
<p><strong>IIS 7, IIS 7.5, IIS 8<&#47;strong></p>
<table id="MT3" cellspacing="0">
<tbody>
<tr>
<td>401.1<&#47;td></p>
<td>Logon failed<&#47;td></p>
<td>The logon attempt is unsuccessful probably because of a user name or a password that is not valid. For more information about how to resolve this problem, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942044" target="_blank">942044<&#47;a>&nbsp;Error message when you try to run a web application that is hosted on IIS 7.0: "HTTP Error 401.1 - Not Found"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>401.2<&#47;td></p>
<td>Logon failed due to server configuration<&#47;td></p>
<td>This HTTP status code indicates a problem in the authentication configuration settings on the server. For more information about how to resolve this problem, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942043" target="_blank">942043<&#47;a>&nbsp;Error message when you try to visit a webpage that is hosted on IIS 7.0: "HTTP Error 401.2 - Unauthorized"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>401.3<&#47;td></p>
<td>Unauthorized due to ACL on resource<&#47;td></p>
<td>This HTTP status code indicates a problem in the NTFS file system permissions. This problem may occur even if the permissions are correct for the file that you are trying to access. For example, this problem occurs if the IUSR account does not have access to the C:\Winnt\System32\Inetsrv directory. For more information about how to resolve this problem, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942042" target="_blank">942042<&#47;a>&nbsp;Error message when you try to browse a webpage that is hosted on a server that is running IIS 7.0: "HTTP Error 401.3 - Unauthorized"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>401.4<&#47;td></p>
<td>Authorization failed by filter<&#47;td></p>
<td>An ISAPI filter does not let the request be processed because of an authorization problem. For more information about how to resolve this problem, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942079" target="_blank">942079<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 401.4 - Authorization failed by filter"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>401.5<&#47;td></p>
<td>Authorization failed by ISAPI&#47;CGI application<&#47;td></p>
<td>An ISAPI application or a Common Gateway Interface (CGI) application does not let the request be processed because of an authorization problem. For more information about how to resolve this problem, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942078" target="_blank">942078<&#47;a>&nbsp;Error message when you visit a website that is hosted on a computer that is running IIS 7.0: "HTTP Error 401.5 - Authorization failed by ISAPI&#47;CGI application"<&#47;div><&#47;td><br />
<&#47;tr><br />
<&#47;tbody><br />
<&#47;table></p>
