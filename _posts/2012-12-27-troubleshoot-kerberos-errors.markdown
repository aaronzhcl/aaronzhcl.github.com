---
layout: post
status: publish
published: true
title: Troubleshoot Kerberos Errors
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 126
wordpress_url: http://www.webdebug.net:80/?p=126
date: '2012-12-27 15:17:58 +0800'
date_gmt: '2012-12-27 15:17:58 +0800'
categories:
- IIS
- Troubleshooting
tags:
- Kerberos
- authentication
- Kerberos delegation
comments: []
---
<p><strong><a href="http://www.microsoft.com/en-us/download/details.aspx?id=21820" target="_blank">Troubleshooting Kerberos Errors</a></strong></p>
<p>Outlines basic troubleshooting strategies. Summarizes issues that typically cause problems with Kerberos authentication. Lists Kerberos error messages, possible causes, and possible resolutions. Describes tools commonly used to troubleshoot Kerberos authentication problems.</p>
<p><strong><a href="http://www.microsoft.com/en-us/download/details.aspx?id=4754" target="_blank">Troubleshooting Kerberos Delegation</a></strong></p>
<p>Explains how to troubleshoot delegation issues that can arise in Kerberos authentication scenarios. Summarizes required infrastructure and describes Windows authentication scenarios. Appendices detail diagnostic tools and examples of IIS to SQL delegation scenarios.</p>
<p><a href="http://blogs.msdn.com/b/asiatech/archive/2011/10/26/iis-7-kerberos-authentication-failure-krb-ap-err-modified.aspx"><strong>Troubleshooting Kerberos Authentication Issue</strong></a><br />
Published on Oct 25, 2011 by Wei Zhao</p>
<p>KRB_AP_ERR_MODIFIED is a common Kerberos failure message. This means some encrypted Kerberos authentication data sent by the client did not decrypt properly at the server.<br />
When a Kerberos client requests a ticket for a specific service, the service is actually identified by its SPN. The KDC grants the client a service ticket that is encrypted using service&rsquo;s secret key. Basically, the AD account password that that matches the SPN requested.<br />
Under some scenarios, KDC may generate a service ticket that encrypted with password of a wrong account (or not expected one). Then, when client provide that ticket to the service for authentication, the service can&rsquo;t decrypt it and authentication failed with KRB_AP_ERR_MODIFED.<br />
In short, this happens because KDC issued a ticket encrypted using password of account A, but on the service side, it tries to decrypt this using the password of account B.<br />
Common cause for this are duplicated SPN, wrong DNS settings, two computers in different domains have the same name, client requests wrong SPN. And from IIS 7, it may due to the wrong setting of IIS (kernel/user mode authentication).</p>
