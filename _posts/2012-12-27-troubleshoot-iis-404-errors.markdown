---
layout: post
status: publish
published: true
title: Troubleshoot IIS 404 errors
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 141
wordpress_url: http://www.webdebug.net:80/?p=141
date: '2012-12-27 16:11:26 +0800'
date_gmt: '2012-12-27 16:11:26 +0800'
categories:
- IIS
- Troubleshooting
tags:
- IIS
- '404'
comments: []
---
<p><strong>IIS 6<&#47;strong></p>
<p><b>404 - Not found.<&#47;b>&nbsp;This error may occur if the file that you are trying to access has been moved or deleted. It can also occur if you try to access a file that has a restricted file name extension after you install the URLScan tool. You will see &ldquo;Rejected by URLScan" in the w3svc log files after you install the URLScan tool. In this case, you see "Rejected by URLScan" in the log file entry for that request. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;248033">248033<&#47;a>&nbsp;How system administrators can troubleshoot an "HTTP 404 - File not found" error message on a server that is running IIS<&#47;div></p>
<ul>
<li><b>404.1 &ndash; Web Site not accessible on the requested port.&nbsp;<&#47;b>This error indicates that the Web site you are trying to access has an IP address that does not accept requests for the port on which this request came. For more information, click the following article number to view the article in the Microsoft Knowledge Base:
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;248034">248034<&#47;a>&nbsp;IIS Error: 404.1 Web Site Not Found<&#47;div><&#47;li></p>
<li><b>404.2 &ndash; Lockdown policy prevents this request.&nbsp;<&#47;b>In IIS 6.0, this indicates that the request has been prohibited in the Web Service Extensions list. For more information, click the following article numbers to view the articles in the Microsoft Knowledge Base:
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;328419">328419<&#47;a>&nbsp;How to add and remove Web Service Extension files in IIS 6<&#47;div></p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;328505">328505<&#47;a>&nbsp;How to list Web Server Extensions and Extension files in IIS 6.0<&#47;div></p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;328360">328360<&#47;a>&nbsp;How to enable and disable ISAPI extensions and CGI applications in IIS 6.0<&#47;div><&#47;li></p>
<li><b>404.3 - MIME Map policy prevents this request.&nbsp;<&#47;b>This problem occurs if the following conditions are true:
<ol>
<li>The handler mapping for the requested file name extension is not configured.<&#47;li>
<li>The appropriate MIME type is not configured for the Web site or for the application.<&#47;li><br />
<&#47;ol><br />
<&#47;li><br />
<&#47;ul></p>
<p><strong>IIS 7, IIS 7.5, IIS 8<&#47;strong></p>
<table id="MT3" cellspacing="0">
<tbody>
<tr>
<td>404.0<&#47;td></p>
<td>Not found.<&#47;td></p>
<td>The file that you are trying to access was moved or does not exist. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942041">942041<&#47;a>&nbsp;Error message when you try to open a webpage that is hosted on IIS 7.0: "HTTP Error 404.0 - Not Found"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.2<&#47;td></p>
<td>ISAPI or CGI restriction.<&#47;td></p>
<td>The requested ISAPI resource or the requested CGI resource is restricted on the computer. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942040">942040<&#47;a>&nbsp;Error message when you try to visit a webpage that is hosted on a computer that is running IIS 7.0: "HTTP Error 404.2 &ndash; Not Found"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.3<&#47;td></p>
<td>MIME type restriction.<&#47;td></p>
<td>The current MIME mapping for the requested extension type is not valid or is not configured. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942032">942032<&#47;a>&nbsp;Error message when users visit a website that is hosted on a server that is running Internet Information Services 7.0: "HTTP Error 404.3 - Not Found"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.4<&#47;td></p>
<td>No handler configured.<&#47;td></p>
<td>The file name extension of the requested URL does not have a handler that is configured to process the request on the Web server. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942052">942052<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 404.4 - Not Found"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.5<&#47;td></p>
<td>Denied by request filtering configuration.<&#47;td></p>
<td>The requested URL contains a character sequence that is blocked by the server. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942053">942053<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 404.5 - URL Sequence Denied"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.6<&#47;td></p>
<td>Verb denied.<&#47;td></p>
<td>The request is made by using an HTTP verb that is not configured or that is not valid. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942046">942046<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 404.6 - VERB_DENIED"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.7<&#47;td></p>
<td>File extension denied.<&#47;td></p>
<td>The requested file name extension is not allowed. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942045">942045<&#47;a>&nbsp;Error message when you try to browse a webpage that is hosted on IIS 7.0: "HTTP Error 404.7 - FILE_EXTENSION_DENIED"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.8<&#47;td></p>
<td>Hidden namespace.<&#47;td></p>
<td>The requested URL is denied because the directory is hidden. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942047">942047<&#47;a>&nbsp;Error message when you try to visit a webpage that is hosted on IIS 7.0: "HTTP Error 404.8 - HIDDEN_NAMESPACE"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.9<&#47;td></p>
<td>File attribute hidden.<&#47;td></p>
<td>The requested file is hidden. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942049">942049<&#47;a>&nbsp;Error message when you try to visit a website that is hosted on IIS 7.0: "HTTP Error 404.9 - File Attribute Hidden"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.10<&#47;td></p>
<td>Request header too long.<&#47;td></p>
<td>The request is denied because the request headers are too long. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942077">942077<&#47;a>&nbsp;Error message when you visit a website that is hosted on a server that is running Internet Information Services 7.0: "HTTP Error 404.10 - REQUEST_HEADER_TOO_LONG"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.11<&#47;td></p>
<td>Request contains double escape sequence.<&#47;td></p>
<td>The request contains a double escape sequence. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942076">942076<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 404.11 - URL_DOUBLE_ESCAPED"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.12<&#47;td></p>
<td>Request contains high-bit characters.<&#47;td></p>
<td>The request contains high-bit characters, and the server is configured not to allow high-bit characters. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942075">942075<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 404.12 - URL_HAS_HIGH_BIT_CHARS"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.13<&#47;td></p>
<td>Content length too large.<&#47;td></p>
<td>The request contains a Content-Length header. The value of the Content-Length header is larger than the limit that is allowed for the server. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942074">942074<&#47;a>&nbsp;Error message when you visit a website that is hosted on a server that is running Internet Information Services 7.0: "HTTP Error 404.13 - CONTENT_LENGTH_TOO_LARGE"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.14<&#47;td></p>
<td>Request URL too long.<&#47;td></p>
<td>The requested URL exceeds the limit that is allowed for the server. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942073">942073<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 404.14 - URL_TOO_LONG"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.15<&#47;td></p>
<td>Query string too long.<&#47;td></p>
<td>The request contains a query string that is longer than the limit that is allowed for the server. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942071">942071<&#47;a>&nbsp;Error message when you visit a website that is hosted on a server that is running IIS 7.0: "HTTP Error 404.15 - Not Found"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>404.17<&#47;td></p>
<td>Dynamic content mapped to the static file handler.<&#47;td></p>
<td>For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;2019689">2019689<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 404.17 - Not Found"<&#47;div><&#47;td><br />
<&#47;tr><br />
<&#47;tbody><br />
<&#47;table></p>
