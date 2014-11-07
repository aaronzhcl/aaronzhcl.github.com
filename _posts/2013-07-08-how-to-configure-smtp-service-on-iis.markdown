---
layout: post
status: publish
published: true
title: How to configure SMTP service on IIS
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 256
wordpress_url: http://www.webdebug.net:80/?p=256
date: '2013-07-08 08:25:26 +0800'
date_gmt: '2013-07-08 08:25:26 +0800'
categories:
- IIS
tags:
- IIS
- SMTP
comments: []
---
<p><strong>To install IIS SMTP</strong></p>
<p><strong>Windows 2003</strong><br />
1. Under Add/Remove Programs, choose to Add/Remove a Windows Component.<br />
2. Choose IIS and SMTP, and install. You may need access to your operating system's install CD.<br />
3. Reboot after installation.<br />
<strong></strong></p>
<p><strong>Windows 2008</strong><br />
1. Select Start|Control Panel.<br />
2. Double click Programs and Features.<br />
3. Click Turn Windows Features on and off. This starts the Server Manager.<br />
4. Click Add Features.<br />
5. Check SMTP Server. Click Install.</p>
<p><strong>To setup IIS SMTP</strong></p>
<p><strong>Windows 2003</strong><br />
1. Check whether the SMTP service is running. Right click on My Computer and select Manage.<br />
2. In Computer Management expand Services and Applications.<br />
3. Expand Internet Information Services and right click on Default SMTP Virtual Server and select Properties.<br />
4. Select the Delivery tab and press the Advanced button.<br />
5. In the Smart Host enter the IP Address of your mail server and the Fully qualified domain name of the server listed in the Smart Host for the Fully-qualified domain name.<br />
6. In the Masquerade domain enter the domain name of your primary email domain (e.g. imlogic.com).<br />
7. Press OK to accept the changes.<br />
<strong></strong></p>
<p><strong>Windows 2008</strong><br />
1. Click Start|Administrative Tools|Internet Information Services (IIS) 6.0 Manager.<br />
3. Expand <computername> and right click on SMTP Virtual Server and select Properties.<br />
4. Select the Delivery tab and press the Advanced button.<br />
5. In the Smart Host textbox enter the IP Address of your mail server and the Fully qualified domain name of the server listed in the Smart Host for the Fully-qualified domain name.<br />
6. In the Masquerade domain enter the domain name of your primary email domain (e.g. imlogic.com).<br />
7. Press OK to accept the changes.</p>
<p><strong>To test IIS SMTP</strong></p>
<p>1. Open a text editor<br />
2. Type in the following text :</p>
<p>to:<user><email domain>.com<br />
from:<user><email domain>.com<br />
subject:This is a test.</p>
<p>This is a test.</p>
<p>The following is an example:</p>
<p>to: john@foobar.com<br />
from: jane@symanec.com<br />
subject:This is a test.</p>
<p>This is a test.</p>
<p>Replace the email addresses with ones that exist in your organization.</p>
<p>3. Save the file as a .txt file to the c:\Inetpub\mailroot\Pickup\ folder.<br />
4. You should receive the email message. If the message fails, the following Microsoft KB article gives further IIS SMTP troubleshooting instructions: <a href="http://support.microsoft.com/?id=297700" target="_blank">How to test outbound mail flow with a file in the Pickup folder.</a></p>
<p><strong>Other Resource</strong></p>
<p><strong>Config the Server SMTP IIS6 to send Mail</strong><br />
<a href="http://www.codeproject.com/Articles/8196/Config-the-Server-SMTP-IIS-to-send-Mail" target="_blank">http://www.codeproject.com/Articles/8196/Config-the-Server-SMTP-IIS-to-send-Mail</a><br />
<strong>Configure SMTP E-Mail in IIS 7</strong><br />
<a href="http://www.iis.net/learn/application-frameworks/install-and-configure-php-on-iis/configure-smtp-e-mail-in-iis-7-and-above" target="_blank">http://www.iis.net/learn/application-frameworks/install-and-configure-php-on-iis/configure-smtp-e-mail-in-iis-7-and-above</a></p>
