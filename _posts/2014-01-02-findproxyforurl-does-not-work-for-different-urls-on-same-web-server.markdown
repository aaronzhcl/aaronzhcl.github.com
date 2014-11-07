---
layout: post
status: publish
published: true
title: FindProxyForURL does not work for different urls on same web server
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 446
wordpress_url: http://webdebug.net/?p=446
date: '2014-01-02 09:18:32 +0800'
date_gmt: '2014-01-02 09:18:32 +0800'
categories:
- browser
tags:
- WPAD
- IE9
- IE
- pac
- proxy
comments: []
---
<p>You may find your original auto proxy configuration script (wpad or pac file) is not working for different urls on same web server&nbsp;using <strong>shExpMatch </strong>in IE9+. This is because a performance enhancement named Automatic Proxy Result Cache are introduced.</p>
<p>When you configure Internet Explorer to use an automatic proxy configuration script, it caches the proxy that is returned by the FindProxyForURL call. The caching mechanism (Automatic Proxy Result Cache) is performed on a host basis (that is, not on an URL basis). This prevents you from using different proxies to gain access to the same Web server.</p>
<p>If you have to use different proxy configuration by urls, you can use the following methods to disable Automatic Proxy Result Cache.</p>
<h3 id="tocHeadRef">Method 1: Modify the registry</h3><br />
You can disable the Automatic Proxy Result Cache by using the following registry key:</p>
<div>
<div>HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\CurrentVersion\Internet Settings</div><br />
Value: EnableAutoproxyResultCache Type: REG_DWORD Data value: 0 = disable caching; 1 (or key not present) = enable automatic proxy caching (this is the default behavior)</p>
<p></div><br />
If the registry key is not present, you can create the registry key by using the following registry file:</p>
<div>Windows Registry Editor Version 5.00<br />
[HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\CurrentVersion\Internet Settings]"EnableAutoProxyResultCache"=dword:00000000"</div></p>
<h3 id="tocHeadRef">Method 2: Modify Group Policy settings</h3></p>
<ol>
<li>Click <strong>Start</strong>, click <strong>Run</strong>, type gpedit.msc, and then click <strong>OK</strong>.</li>
<li>In Group Policy Object Editor, double-click <strong>User Configuration\Administrative Templates\Windows Components\Internet Explorer</strong>.</li>
<li>Double-click <strong>Disable caching of Auto-Proxy scripts</strong>.</li>
<li>Click <strong>Enable</strong>, and then click <strong>OK</strong>.</li><br />
</ol><br />
For more detail you can refer to <a href="http://support.microsoft.com/kb/271361">http://support.microsoft.com/kb/271361</a></p>
