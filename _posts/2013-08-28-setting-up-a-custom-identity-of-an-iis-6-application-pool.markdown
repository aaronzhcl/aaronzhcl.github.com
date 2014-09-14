---
layout: post
status: publish
published: true
title: Setting up a custom identity of an IIS 6 application pool
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 376
wordpress_url: http://www.webdebug.net/?p=376
date: '2013-08-28 06:29:05 +0800'
date_gmt: '2013-08-28 06:29:05 +0800'
categories:
- IIS
tags:
- IIS6
- custom identity
comments: []
---
<p>Sometime you need to set up a custom identity for IIS6 application pools, but if you directly do that, you may receive the following errors in event log.</p>
<p><em>Event Type:&nbsp;&nbsp; &nbsp;Warning<&#47;em><br />
<em> Event Source:&nbsp;&nbsp; &nbsp;W3SVC<&#47;em><br />
<em> Event Category:&nbsp;&nbsp; &nbsp;None<&#47;em><br />
<em> Event ID:&nbsp;&nbsp; &nbsp;1021<&#47;em><br />
<em> Description:<&#47;em><br />
<em> The identity of application pool, 'xxx' is invalid.&nbsp; If it remains invalid when the first request for the application pool is processed, the application pool will be disabled.&nbsp; The data field contains the error number.For more information, see Help and Support Center at http:&#47;&#47;go.microsoft.com&#47;fwlink&#47;events.asp.<&#47;em><br />
<em> Data:<&#47;em><br />
<em> <strong>69 05 07 80<&#47;strong><&#47;em></p>
<p>Error code <strong>0x80070569<&#47;strong> means "Logon failure: the user has not been granted the requested logon type at this computer."</p>
<p>The right approach to setup a custom identity for IIS6 application pool is below,</p>
<p>1. Create the service account and set the <strong>password cannot be changed<&#47;strong> and <strong>password never expire<&#47;strong>.</p>
<p>2. Add the service account to<strong> IIS_WPG<&#47;strong> group.</p>
<p>3. Go to local policy - user rights assignment, add the user to "<strong>Log on as a service<&#47;strong>".</p>
<p><a href="http:&#47;&#47;blogs.msdn.com&#47;b&#47;friis&#47;archive&#47;2010&#47;10&#47;08&#47;steps-for-setting-up-a-custom-identity-of-an-iis-6-application-pool.aspx" target="_blank">http:&#47;&#47;blogs.msdn.com&#47;b&#47;friis&#47;archive&#47;2010&#47;10&#47;08&#47;steps-for-setting-up-a-custom-identity-of-an-iis-6-application-pool.aspx<&#47;a></p>
