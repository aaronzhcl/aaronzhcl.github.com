---
layout: post
status: publish
published: true
title: Browser Connection Limit
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 431
wordpress_url: http://webdebug.net/?p=431
date: '2013-12-25 03:02:34 +0800'
date_gmt: '2013-12-25 03:02:34 +0800'
categories:
- browser
- Performance
tags:
- browser
- connection limit
- connection per host
comments: []
---
<h2>HTTP 1.1 RFC 2616</h2><br />
As RFC2616 recommended,</p>
<p>Clients that use persistent connections SHOULD limit the number of simultaneous connections that they maintain to a given server. A single-user client SHOULD NOT maintain more than 2 connections with any server or proxy. A proxy SHOULD use up to 2*N connections to another server or proxy, where N is the number of simultaneously active users. These guidelines are intended to improve HTTP response times and avoid congestion.</p>
<p>This means the client should control the connections on a per host basis. If&nbsp; a website gets resource from multiple hosts (www.host1.com, www.host2.com, www.host3.com ..), the client can open 2 connections for each host name.</p>
<!--more-->
<p>Yahoo website performance rules "<a href="http://developer.yahoo.com/performance/rules.html#num_http" target="_blank">Minimize Http Requests</a>" are also recommending website should minimize http requests to server as connections limit might caused resource downloading pending on get connections.</p>
<h2>Browser Configuration</h2><br />
Earlier versions of browsers strictly followed this standards and soon they find 2 connections per host are not efficient enough for modern web applications. <a href="http://www.browserscope.org/?category=network" target="_blank">This link</a> provides testing result for connection limits on different versions of browsers.</p>
<p><a href="http://webdebug.net/wp-content/uploads/2013/12/connections.png"><img class="alignnone size-full wp-image-432" alt="connections" src="http://webdebug.net/wp-content/uploads/2013/12/connections.png" width="540" height="451" /></a></p>
<p>Different browsers has different settings to control the this limit.</p>
<p>IE can refer to <a href="http://support.microsoft.com/kb/282402" target="_blank">KB28242</a>, this setting applies to IE6 - IE9, while IE10/11 can use the following registry key to set the limit, range from 2-128.</p>
<p>HKLM\SOFTWARE\<b>Wow6432Node</b>\Microsoft\Internet Explorer\Main\FeatureControl\FEATURE_MAXCONNECTIONSPERSERVER</p>
<p>In Firefox these values are controlled by the <code>network.http.max-persistent-connections-per-server</code> and <code>network.http.max-connections-per-server</code> settings in about:config.</p>
<p>For Chrome it looks this feature are still <a href="http://code.google.com/p/chromium/issues/detail?id=85323" target="_blank">under discussion</a>.</p>
<h2>Effect of Proxies</h2><br />
Note that if you&rsquo;re behind a proxy (at work, etc.) your download characteristics change. If web clients behind a proxy issued too many simultaneous requests an intelligent web server might interpret that as a DoS attack and block that IP address. Browser developers are aware of this issue and throttle back the number of open connections.</p>
<p>In Firefox the <code>network.http.max-persistent-connections-per-proxy</code> setting has a default value of 4. If you try the <a href="http://stevesouders.com/hpws/max-connections.php">Max Connections</a> test page while behind a proxy it loads painfully slowly opening no more than 4 connections at a time to download 180 images. IE8 drops back to 2 connections per server when it&rsquo;s behind a proxy, so loading the <a href="http://stevesouders.com/hpws/max-connections.php">Max Connections</a> test page shows an upperbound of 60 open connections. Keep this in mind if you&rsquo;re comparing notes with others &ndash; if you&rsquo;re at home and they&rsquo;re at work you might be seeing different behavior because of a proxy in the middle.</p>
<h2>Testing</h2><br />
Steve Souders provides a max-connection testing page to test this behavior.</p>
<p><a href="http://stevesouders.com/hpws/max-connections.php" target="_blank">http://stevesouders.com/hpws/max-connections.php</a></p>
<p>I created a testing page for clients to test what is the connection limit for clients.</p>
<p><a href="http://webdebug.net/toolbox/max-connections.html" target="_blank">http://webdebug.net/toolbox/max-connections.html</a></p>
