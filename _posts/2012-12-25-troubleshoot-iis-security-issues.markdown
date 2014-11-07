---
layout: post
status: publish
published: true
title: Troubleshoot SSL issues
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 80
wordpress_url: http://localhost:80/?p=80
date: '2012-12-25 13:23:29 +0800'
date_gmt: '2012-12-25 13:23:29 +0800'
categories:
- IIS
- Troubleshooting
tags:
- IIS
- SSL
- Security
- Certificate
- https
comments: []
---
<p><strong><a href="http://www.iis.net/learn/troubleshoot/security-issues/troubleshooting-ssl-related-issues-server-certificate" target="_blank">Troubleshooting SSL related issues (Server Certificate)</a></strong><br />
Published on April 9, 2012 by Kaushal Kumar Panday</p>
<p>This document will help you in troubleshooting SSL issues related to IIS only. Client Certificates troubleshooting will not be covered in this document. Server Certificates are meant for Server Authentication and we will be dealing only with Server Certificates in this document.<br />
If the Client certificates section is set to &ldquo;Require&rdquo; and then you run into issues, then please don&rsquo;t refer this document. This is meant for troubleshooting SSL Server certificates issue only.<br />
It is important to know that every certificate comprises of a public key (used for encryption) and a private key (used for decryption). The private key is known only to the server.<br />
The default port for https is 443.</p>
<p>&nbsp;</p>
