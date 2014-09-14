---
layout: post
status: publish
published: true
title: Wireshark vs Network Monitor
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 264
wordpress_url: http://www.webdebug.net:80/?p=264
date: '2013-07-10 08:23:30 +0800'
date_gmt: '2013-07-10 08:23:30 +0800'
categories:
- Data Collection
tags:
- Network Monitor
- Wireshark
- network
comments: []
---
<p>1) Wireshark is released under the GNU Public License; its source code is available to all, and if anybody makes a modified version of Wireshark available, they must make it available in source form to everybody to whom they make it available in binary form (see the GPL, Version 2:<br />
<a href="http:&#47;&#47;www.gnu.org&#47;licenses&#47;old-licenses&#47;gpl-2.0.html" target="_blank">http:&#47;&#47;www.gnu.org&#47;licenses&#47;old-licenses&#47;gpl-2.0.html<&#47;a><br />
and the FAQ about it:<br />
<a href="http:&#47;&#47;www.gnu.org&#47;licenses&#47;old-licenses&#47;gpl-2.0-faq.html" target="_blank">http:&#47;&#47;www.gnu.org&#47;licenses&#47;old-licenses&#47;gpl-2.0-faq.html<&#47;a><br />
for a more detailed and perhaps more correct explanation). It is available at no cost.<br />
Microsoft Network Monitor (henceforth referred to as "NetMon") is available at no cost, but its source code is not available.</p>
<p>2) Wireshark dissects packets by directly executing code, written in C, Lua (for versions of Wireshark built with Lua) or, I think, Python (for versions of Wireshark built with the Python interpreter); a third-party plugin:<br />
<a href="http:&#47;&#47;wsgd.free.fr&#47;" target="_blank">http:&#47;&#47;wsgd.free.fr&#47;<&#47;a><br />
allows packet formats to be described in a packet description language. Tools exist to transform some packet description languages (ASN.1, Samba's PIDL interface description language for DCERPC&#47;MSRPC, CORBA IDL) into C code.<br />
NetMon dissects packets by using packet descriptions written in NetMon's own packet description language.</p>
<p>3) Wireshark runs on Windows and a number of UN*Xes (Linux distributions, *BSD, Mac OS X, Solaris, HP-UX, AIX, etc.).<br />
NetMon runs only on Windows (it might be able to run, without support for packet capture, on x86 UN*Xes under Wine).</p>
<p>4) Wireshark can read capture files in a number of formats, including both pcap and pcap-NG format, as well as various formats from other packet analyzers, including NetMon format.<br />
NetMon can read both its native format and pcap format; it supports some features of its native format that Wireshark does not (including, at present, frame comments).</p>
<p>5) Network Monitor can&nbsp;categorize network messages by processes while Wireshark cannot.</p>
<p>6) Network Monitor provides parser for windows native trace like wininet trace or etw trace.</p>
