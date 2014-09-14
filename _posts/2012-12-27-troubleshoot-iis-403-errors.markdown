---
layout: post
status: publish
published: true
title: Troubleshoot IIS 403 errors
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 138
wordpress_url: http://www.webdebug.net:80/?p=138
date: '2012-12-27 16:07:44 +0800'
date_gmt: '2012-12-27 16:07:44 +0800'
categories:
- IIS
- Troubleshooting
tags:
- IIS
- '403'
comments:
- id: 20187
  author: Terrell
  author_email: emile.garrido@zoho.com
  author_url: http://Micheal.wordpress.com
  date: '2014-08-14 04:11:47 +0800'
  date_gmt: '2014-08-14 04:11:47 +0800'
  content: "I see you share interesting stuff here, you can earn some additional cash,
    your blog has huge potential,\r\nfor the monetizing method, just search in google
    \r\n- K2 advices how to monetize a website"
- id: 21750
  author: Stanton
  author_email: marilynnfrance@freenet.de
  author_url: http://Brittany.wikispaces.com
  date: '2014-08-28 05:43:05 +0800'
  date_gmt: '2014-08-28 05:43:05 +0800'
  content: "I read a lot of interesting articles here. Probably you  spend a lot \r\nof
    time writing, i know how to save you a lot of work, there is an online tool that
    creates unique, google friendly posts in seconds, just type in google \r\n- laranitas
    free content source"
---
<p><strong>IIS 6<&#47;strong></p>
<ul>
<li><b>403 - Forbidden.<&#47;b>&nbsp;You can receive this generic 403 status code if the Web site has no default document set, and the site is not set to allow Directory Browsing. For more information about how to resolve this problem, click the following article number to view the article in the Microsoft Knowledge Base:
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;320051">320051<&#47;a>&nbsp;How to configure the default document in Internet Information Services<&#47;div><&#47;li></p>
<li><b>403.1 - Execute access forbidden.<&#47;b>&nbsp;The following are two common causes of this error message:
<ul>
<li>You do not have enough Execute permissions. For example, you may receive this error message if you try to access an ASP page in a directory where permissions are set to None, or you try to execute a CGI script in a directory with Scripts Only permissions. To modify the Execute permissions, right-click the directory in Microsoft Management Console (MMC), click&nbsp;<b>Properties<&#47;b>, click the&nbsp;<b>Directory<&#47;b>&nbsp;tab, and make sure that the&nbsp;<b>Execute Permissions<&#47;b>&nbsp;setting is appropriate for the content that you are trying to access.<&#47;li>
<li>The script mapping for the file type that you are trying to execute is not set up to recognize the verb that you are using (for example, GET or POST). To verify this, right-click the directory in Microsoft Management Console, click<b>Properties<&#47;b>, click the&nbsp;<b>Directory<&#47;b>&nbsp;tab, click&nbsp;<b>Configuration<&#47;b>, and verify that the script mapping for the appropriate file type is set up to allow the verb that you are using.<&#47;li><br />
<&#47;ul><br />
<&#47;li></p>
<li><b>403.2 - Read access forbidden.<&#47;b>&nbsp;Verify that you have set up IIS to allow Read access to the directory. Also, if you are using a default document, verify that the document exists. For additional information about how to resolve this problem, click the article number below to view the article in the Microsoft Knowledge Base:
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;247677&#47;EN-US">247677<&#47;a>&nbsp;Error Message: 403.2 Forbidden: Read Access Forbidden<&#47;div><&#47;li></p>
<li><b>403.3 - Write access forbidden.<&#47;b>&nbsp;Verify that the IIS permissions and the NTFS permissions are set up to grant Write access to the directory.For additional information about how to resolve this problem, click the article number below to view the article in the Microsoft Knowledge Base:
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;248072&#47;EN-US">248072<&#47;a>&nbsp;Error Message: 403.3 Forbidden: Write Access Forbidden<&#47;div><&#47;li></p>
<li><b>403.4 - SSL required.<&#47;b>&nbsp;Disable the&nbsp;<b>Require secure channel<&#47;b>&nbsp;option, or use HTTPS instead of HTTP to access the page.<&#47;li>
<li><b>403.5 - SSL 128 required.<&#47;b>&nbsp;Disable the&nbsp;<b>Require 128-bit encryption<&#47;b>&nbsp;option, or use a browser that supports 128-bit encryption to view the page.<&#47;li>
<li><b>403.6 - IP address rejected.<&#47;b>&nbsp;You have configured the server to deny access to your current IP address. For additional information about how to resolve this problem, click the article number below to view the article in the Microsoft Knowledge Base:
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;248043&#47;EN-US">248043<&#47;a>&nbsp;Error Message: 403.6 - Forbidden: IP Address Rejected<&#47;div><&#47;li></p>
<li><b>403.7 - Client certificate required.<&#47;b>&nbsp;You have configured the server to require a certificate for client authentication, but you do not have a valid client certificate installed.
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;186812&#47;EN-US">186812<&#47;a>&nbsp;PRB: Error Message: 403.7 Forbidden: Client Certificate Required<&#47;div><&#47;li></p>
<li><b>403.8 - Site access denied.<&#47;b>&nbsp;You have set up a domain name restriction for the domain that you are using to access the server.For additional information about how to resolve this problem, click the article number below to view the article in the Microsoft Knowledge Base:
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;248032&#47;EN-US">248032<&#47;a>&nbsp;Error Message: Forbidden: Site Access Denied 403.8<&#47;div><&#47;li></p>
<li><b>403.9 - Too many users.<&#47;b>&nbsp;The number of users who are connected to the server exceeds the connection limit that you have set. For additional information about how to change this limit, click the article number below to view the article in the Microsoft Knowledge Base:
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;248074&#47;EN-US">248074<&#47;a>&nbsp;Error Message: Access Forbidden: Too Many Users Are Connected 403.9<&#47;div><br />
<b>NOTE<&#47;b>: Microsoft Windows 2000 Professional and Windows XP Professional automatically impose a 10-connection limit on IIS. You cannot change this limit.<&#47;li></p>
<li><b>403.12 - Mapper denied access.<&#47;b>&nbsp;The page that you want to access requires a client certificate. However, the user ID that is mapped to the client certificate has been denied access to the file. For additional information, click the article number below to view the article in the Microsoft Knowledge Base:
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;248075&#47;EN-US">248075<&#47;a>&nbsp;Error: HTTP 403.12 - Access Forbidden: Mapper Denied Access<&#47;div><&#47;li><br />
<&#47;ul><br />
&nbsp;</p>
<p><strong>IIS 7, IIS 7.5, IIS 8<&#47;strong></p>
<table id="MT3" cellspacing="0">
<tbody>
<tr>
<td>403.1<&#47;td></p>
<td>Execute access forbidden<&#47;td></p>
<td>The appropriatelevel of the Execute permission is not granted. For more information about how to resolve this problem, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942065">942065<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 403.1 - Forbidden"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.2<&#47;td></p>
<td>Read access forbidden<&#47;td></p>
<td>The appropriate level of the Read permission is not granted. Verify that you have set up&nbsp;IIS 7.0, IIS 7.5, and IIS 8.0 to grant the Read permission to the directory. Additionally, if you use a default document, verify that the default document exists. For more information about how to resolve this problem, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942036">942036<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 403.2 - Forbidden"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.3<&#47;td></p>
<td>Write access forbidden<&#47;td></p>
<td>The appropriate level of the Write permission is not granted. Verify that the&nbsp;IIS 7.0, IIS 7.5, and IIS 8.0 permissions and the NTFS file system permissions are set up to grant the Write permission to the directory.&nbsp;For more information about how to resolve this problem, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942035">942035<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 403.3 - Forbidden"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.4<&#47;td></p>
<td>SSL required<&#47;td></p>
<td>The request is made over a nonsecure channel, and the web application requires a Secure Sockets Layer (SSL) connection. For more information about how to resolve this problem, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942070">942070<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 403.4 - Forbidden"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.5<&#47;td></p>
<td>SSL 128 required<&#47;td></p>
<td>The server is configured to require a 128-bit SSL connection. But, the request is not sent by using 128-bit encryption. For more information about how to resolve this problem, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942069">942069<&#47;a>&nbsp;Error message when you try to browse a webpage that is hosted on IIS 7.0: "HTTP Error 403.5 - Forbidden"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.6<&#47;td></p>
<td>IP address rejected<&#47;td></p>
<td>The server is configured to deny access to the current IP address. For more information about how to resolve this problem, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942068">942068<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 403.6 - IP Address Rejected"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.7<&#47;td></p>
<td>Client certificate required<&#47;td></p>
<td>The server is configured to require a certificate for client authentication. But, the client browser does not have an appropriate client certificate installed. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942067">942067<&#47;a>&nbsp;Error message when you try to run a web application that is hosted on a server that is running IIS 7.0: "HTTP Error 403.7 - Forbidden"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.8<&#47;td></p>
<td>Site access denied<&#47;td></p>
<td>The server is configured to deny requests based on the Domain Name System (DNS) name of the client computer. For more information about how to resolve this problem, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942066">942066<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 403.8 - Forbidden"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.12<&#47;td></p>
<td>Mapper denied access<&#47;td></p>
<td>The page that you want to access requires a client certificate. But, the user ID that is mapped to the client certificate is denied access to the file. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942064">942064<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 403.12 - Client Certificate Denied"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.13<&#47;td></p>
<td>Client certificate revoked<&#47;td></p>
<td>The client browser tries to use a client certificate that was revoked by the issuing certification authority. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942063">942063<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 403.13 - Forbidden"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.14<&#47;td></p>
<td>Directory listing denied<&#47;td></p>
<td>The server is not configured to display a content directory listing, and a default document is not set. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942062">942062<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 403.14 - Forbidden"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.16<&#47;td></p>
<td>Client certificate is untrusted or invalid.<&#47;td></p>
<td>The client browser tries to use a client certificate that is not trusted by the server that is running&nbsp;IIS 7.0, IIS 7.5,&nbsp;or IIS 8.0 or that is not valid.&nbsp;For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942061">942061<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 403.16 - Forbidden"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.17<&#47;td></p>
<td>Client certificate has expired or is not yet valid.<&#47;td></p>
<td>The client browser tries to use a client certificate that is expired or that is not yet valid. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942038">942038<&#47;a>&nbsp;Error message when you try to visit a webpage that is hosted on Internet Information Services 7.0: "HTTP Error 403.17 (Forbidden) - The client certificate has expired"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.18<&#47;td></p>
<td>Cannot execute requested URL in the current application pool.<&#47;td></p>
<td>A custom error page is configured, and the custom error page resides in a different application pool than the application pool of the requested URL. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942037">942037<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 403.18 - Forbidden"<&#47;div><&#47;td><br />
<&#47;tr></p>
<tr>
<td>403.19<&#47;td></p>
<td>Cannot execute CGI applications for the client browser in this application pool.<&#47;td></p>
<td>The identity of the application pool does not have the&nbsp;<b>Replace a process level token<&#47;b>&nbsp;user right. For more information, click the following article number to view the article in the Microsoft Knowledge Base:</p>
<div><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;942048">942048<&#47;a>&nbsp;Error message when you visit a website that is hosted on IIS 7.0: "HTTP Error 403.19 - Forbidden"<&#47;div><&#47;td><br />
<&#47;tr><br />
<&#47;tbody><br />
<&#47;table></p>
