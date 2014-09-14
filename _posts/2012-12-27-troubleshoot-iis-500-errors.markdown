---
layout: post
status: publish
published: true
title: Troubleshoot IIS 500 errors
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 143
wordpress_url: http://www.webdebug.net:80/?p=143
date: '2012-12-27 16:15:17 +0800'
date_gmt: '2012-12-27 16:15:17 +0800'
categories:
- IIS
- Troubleshooting
tags:
- IIS
- '500'
comments:
- id: 16338
  author: Sharron
  author_email: jocelynpogue@gmx.net
  author_url: http://Toney.blogger.de
  date: '2014-07-15 19:10:20 +0800'
  date_gmt: '2014-07-15 19:10:20 +0800'
  content: "Finally i quit my day job, now i earn a lot of money on-line you should
    try too, just search in google - \r\nbluehand roulette system"
---
<p><strong>IIS 6<&#47;strong></p>
<ul>
<li><b>500 - Internal server error.<&#47;b>&nbsp;You see this error message for many server-side errors. Your event viewer logs may contain more information about why this error occurs. Additionally, you can disable friendly HTTP error messages to receive a detailed description of the error. For more information about how to disable friendly HTTP error messages, click the following article number to view the article in the Microsoft Knowledge Base:
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;294807">294807<&#47;a>&nbsp;HOW TO: Disable Internet Explorer 5 'Show Friendly HTTP Error Messages' Feature on the Server Side<&#47;div><&#47;li></p>
<li><b>500.12 - Application restarting.<&#47;b>&nbsp;This indicates that you tried to load an ASP page while IIS was restarting the application. This message should disappear when you refresh the page. If you refresh the page and the message appears again, it may be caused by antivirus software that is scanning your Global.asa file. For additional information, click the article number below to view the article in the Microsoft Knowledge Base:
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;248013&#47;EN-US">248013<&#47;a>&nbsp;Err Msg: HTTP Error 500-12 Application Restarting<&#47;div><&#47;li></p>
<li><b>500-100.ASP - ASP error.<&#47;b>&nbsp;You receive this error message when you try to load an ASP page that has errors in the code. To obtain more specific information about the error, disable friendly HTTP error messages. By default, this error is only enabled on the default Web site. For more information about how to see this error on non-default Web sites, click the following article number to view the article in the Microsoft Knowledge Base:
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;261200">261200<&#47;a>&nbsp;HTTP 500 error message displays instead of ASP error message from 500-100.asp<&#47;div><&#47;li><br />
<&#47;ul><br />
<strong>IIS 7, IIS 7.5, IIS 8<&#47;strong></p>
<table id="MT3" cellspacing="0">
<tbody>
<tr>
<td>500<&#47;td></p>
<td>Internal server error.<&#47;td></p>
<td>This HTTP status code may occur for many server-side reasons. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942031">942031<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 500.0 - Internal Server Error"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>500.11<&#47;td></p>
<td>Application is shutting down on the web server.<&#47;td></p>
<td>The request is not processed because the destination application pool is shutting down. Wait for the worker process to finish shutting down, and then try the request again. If this problem persists, the web application may be experiencing problems that prevent the web application from shutting down correctly.<&#47;td><br />
<&#47;tr></p>
<tr>
<td>500.12<&#47;td></p>
<td>Application is busy restarting on the web server.<&#47;td></p>
<td>The request is not processed because the destination application pool is restarting. This HTTP status code should disappear when you refresh the page. If this HTTP status code appears again after you refresh the page, the problem may be caused by antivirus software that is scanning the Global.asa file. If this problem persists, the web application may be experiencing problems that prevent the web application from restarting correctly.<&#47;td><br />
<&#47;tr></p>
<tr>
<td>500.13<&#47;td></p>
<td>Web server is too busy.<&#47;td></p>
<td>The request is not processed because the server is too busy to accept any new incoming requests. Typically, this HTTP status code means that the number of incoming concurrent requests exceeds the number that the&nbsp;IIS 7.0, IIS 7.5, or IIS 8.0&nbsp;web application can process. This problem may occur because the performance configuration settings are set too low, the hardware is insufficient, or a bottleneck occurs in the&nbsp;IIS 7.0, IIS 7.5, or IIS 8.0&nbsp;web application. A common troubleshooting method is to generate a memory dump file of the&nbsp;IIS 7.0, IIS 7.5, or IIS 8.0 processes when the error is occurring and then to debug the memory dump file.<&#47;td><br />
<&#47;tr></p>
<tr>
<td>500.15<&#47;td></p>
<td>Direct requests for Global.asax are not allowed.<&#47;td></p>
<td>A direct request for the Global.asa file or for the Global.asax file is made. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942030">942030<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 500.15 - Direct request for global.asa are not allowed"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>500.19<&#47;td></p>
<td>Configuration data is invalid.<&#47;td></p>
<td>This HTTP status code occurs because of a problem in the associated Applicationhost.config file or in the associated Web.config file. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942055">942055<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 500.19 - Internal Server Error"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>500.100<&#47;td></p>
<td>Internal ASP error.<&#47;td></p>
<td>An error occurs during the processing of an Active Server Pages (ASP) page. To obtain more specific information about the error, disable friendly HTTP error messages in the web browser. Additionally, the IIS log may show an ASP error number that corresponds to the error that occurs. For more information about ASP error messages and about the meaning of ASP error messages, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;294271">294271<&#47;a>ASP error codes<&#47;div><&#47;td><br />
<&#47;tr><br />
<&#47;tbody><br />
<&#47;table></p>
