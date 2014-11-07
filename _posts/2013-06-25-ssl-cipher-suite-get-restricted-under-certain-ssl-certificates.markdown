---
layout: post
status: publish
published: true
title: SSL Cipher-Suite get restricted under certain SSL certificates
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 243
wordpress_url: http://www.webdebug.net:80/?p=243
date: '2013-06-25 09:42:30 +0800'
date_gmt: '2013-06-25 09:42:30 +0800'
categories:
- IIS
- browser
tags:
- SSL
- Certificate
- cipher suite
- windows xp
- restricted
- CNG
- AES
comments:
- id: 763
  author: guest
  author_email: guest@anonymouse.ws
  author_url: ''
  date: '2013-08-03 01:10:54 +0800'
  date_gmt: '2013-08-03 01:10:54 +0800'
  content: "Thank you for the post, it's a life saver!\r\n\r\nAnother solution:\r\n-
    export PFX with private key from respective certificate store\r\n- delete certificate
    associated with Microsoft Strong Cryptographic Provider/CSP\r\n- extract private
    key, primary certificate and root certificate chain to PEM files with OpenSSL\r\n-
    convert PEM files into PKCS#12 PFX with OpenSSL\r\n- import new PFX to respective
    certificate store\r\n- verify certificate is now associated with Microsoft Enhanced
    Cryptographic Provider v1.0/CNG"
- id: 13969
  author: http://www.Edenad.com/94734
  author_email: sherikorner@aol.com
  author_url: http://www.edenad.com/94734
  date: '2014-07-01 03:23:44 +0800'
  date_gmt: '2014-07-01 03:23:44 +0800'
  content: "Whats up this is kinda of off topic but I was wondering if blogs use WYSIWYG
    editors \r\nor if you have to manually code with HTML. I'm starting a blog soon
    but have no coding \r\nexpertise so I wanted to get guidance from someone with
    experience.\r\nAny help would be enormously appreciated!\r\n\r\nReview my web
    blog: http://www.lanzarote-hotels.co.Uk/ (<a href=\"http://www.edenad.com/94734\"
    rel=\"nofollow\">http://www.Edenad.com/94734</a>)"
- id: 18696
  author: gas safe register
  author_email: mercedescadell@hotmail.de
  author_url: http://www.inklabtattoo.com/UserProfile/tabid/42/userId/55990/Default.aspx
  date: '2014-07-30 02:19:35 +0800'
  date_gmt: '2014-07-30 02:19:35 +0800'
  content: "My family every time say that I am killing \r\nmy time here at net, however
    I know I am getting knowledge every day by reading thes pleasant articles.\r\n\r\n\r\nmy
    homepage - <a href=\"http://www.inklabtattoo.com/UserProfile/tabid/42/userId/55990/Default.aspx\"
    rel=\"nofollow\">gas safe register</a>"
---
<p>Some times you will notice certain secure website cannot be viewed by windows xp client, but on windows vista or above it is working fine,</p>
<p><a href="http://serverfault.com/questions/166750/why-does-windows-ssl-cipher-suite-get-restricted-under-certain-ssl-certificates" target="_blank">http://serverfault.com/questions/166750/why-does-windows-ssl-cipher-suite-get-restricted-under-certain-ssl-certificates</a></p>
<p><strong>Problem:</strong></p>
<p>Windows Server 2008 R2 will only support the following ssl cipher suites when using certain certificates on the server:</p>
<blockquote><p>TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA<br />
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA</blockquote><br />
This prevents XP clients from connecting to the server since the XP Cryptographic API doesn't support any AES ciphers by default.<br />
As a result, the following errors appear in the server logs when attempting to connect using internet explorer or remote desktop. (since they use microsoft's CAPI)</p>
<blockquote><p>Schannel Error 36874 "An TLS 1.0 connection was recieved from a remote client application, but dodne of the cipher suites supported by the client are supported by the server. The SSL connection request has failed."<br />
Schannel Error 36888 "The following fatal alert was generated: 40. The internal error state is 1204</blockquote><br />
&nbsp;</p>
<p><strong>Root Cause:</strong></p>
<p>If the certificate being used on the server was generated using the Legacy Key option in the certificate request form, the private key for that certificate will be stored in Microsoft's legacy Cryptographic API framework. When the web server tries to process requests using its new, Cryptographic Next Generation (CNG) framework, it appears that something related to the RSA private key stored in the legacy framework is unavailable to the new framework. As a result, the use of the RSA cipher suites is severely limited.</p>
<p><strong>Solution:</strong><br />
Generate the certificate request using the CNG Key template in the custom certificate request wizard.</p>
<blockquote><p>MMC | Local Computer Certificate Manager | Personal Certificates Folder | (right click) | All Tasks -> Advanced Operations | Create Custom Request | "Proceed without enrollment policy" | <strong>select "(no template) CNG key"</strong> | proceed to complete the certificate request according to your needs.</blockquote><br />
Verifying that the key is in the right place:<br />
<a href="http://msdn.microsoft.com/en-us/library/bb204778(VS.85).aspx">http://msdn.microsoft.com/en-us/library/bb204778(VS.85).aspx</a><br />
<a href="http://www.jensign.com/KeyPal/index.html">http://www.jensign.com/KeyPal/index.html</a></p>
<p>Tools for verifying correct cipher-suites:<br />
<a href="http://pentestit.com/2010/05/16/ssltls-audit-audit-web-servers-ssl-ciphers/">http://pentestit.com/2010/05/16/ssltls-audit-audit-web-servers-ssl-ciphers/</a><br />
<a href="https://www.ssllabs.com/">https://www.ssllabs.com/</a></p>
<p>SSL cipher-suite settings:<br />
<a href="http://support.microsoft.com/kb/245030">http://support.microsoft.com/kb/245030</a><br />
<a href="http://blogs.technet.com/b/steriley/archive/2007/11/06/changing-the-ssl-cipher-order-in-internet-explorer-7-on-windows-vista.aspx">http://blogs.technet.com/b/steriley/archive/2007/11/06/changing-the-ssl-cipher-order-in-internet-explorer-7-on-windows-vista.aspx</a></p>
<p>&nbsp;</p>
