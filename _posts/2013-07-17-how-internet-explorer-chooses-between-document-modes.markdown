---
layout: post
status: publish
published: true
title: How Internet Explorer Chooses Between Document Modes
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 281
wordpress_url: http://www.webdebug.net:80/?p=281
date: '2013-07-17 09:13:48 +0800'
date_gmt: '2013-07-17 09:13:48 +0800'
categories:
- browser
tags:
- browser
- document mode
- doctype
comments: []
---
<p>By default, Windows Internet Explorer 8 uses IE8 mode, Windows Internet Explorer 9 uses IE9 mode, etc. However, Windows Internet Explorer uses several criteria to determine which document mode to use. For example, if an HTML page contains a valid&nbsp;<code><!DOCTYPE><&#47;code>&nbsp;declaration (see&nbsp;<a href="http:&#47;&#47;go.microsoft.com&#47;fwlink&#47;?LinkId=89880" target="_blank">[HTML]<&#47;a>), Internet Explorer uses one of the standards-based document modes. But, if there is no valid&nbsp;<code><!DOCTYPE><&#47;code>&nbsp;declaration<code>,<&#47;code>&nbsp;Internet Explorer uses quirks mode.</p>
<p>The following rules determine how Internet Explorer selects the document mode:</p>
<ol>
<li>The&nbsp;<strong>Developer Tools<&#47;strong>&nbsp;setting overrides any document mode specified by a webpage. The setting remains active for the lifetime of the tab.<&#47;li>
<li>In Internet Explorer 9, if the document is hosted in an&nbsp;<strong>iframe<&#47;strong>&nbsp;element, the document mode is determined by the document mode of the top-level webpage. Subdocuments cannot be rendered in IE9 mode unless the top-level document is also in IE9 mode.<&#47;li>
<li>A&nbsp;<strong>meta<&#47;strong>&nbsp;tag with a value of&nbsp;<code>X-UA-Compatible<&#47;code>&nbsp;or a HTTP response header can override items in the&nbsp;<strong>Compatibility View Settings<&#47;strong>&nbsp;list and the doctype unless the&nbsp;<strong>X-UA-Compatible<&#47;strong>&nbsp;value is a Compatibility View setting, such as&nbsp;<code>IE=EmulateIE7<&#47;code>&nbsp;or&nbsp;<code>IE=EmulateIE8<&#47;code>.<&#47;li>
<li>The Compatibility View settings can force a webpage to be displayed in a less-standard document mode.<&#47;li>
<li>If none of these rules apply, the&nbsp;<code><!DOCTYPE><&#47;code>&nbsp;declaration determines whether the webpage renders in a standards mode, Almost Standards mode, or quirks mode.<&#47;li><br />
<&#47;ol></p>
<table>
<tbody>
<tr>
<td id="ShadedCell" style="border: 1px solid #bbb;"><!DOCTYPE> declaration<&#47;td></p>
<td id="ShadedCell1" style="border: 1px solid #bbb;">Document Mode Impact<&#47;td><br />
<&#47;tr></p>
<tr>
<td style="border: 1px solid #bbb;"><strong>HTML 4.0 and higher<&#47;strong><!DOCTYPE HTML PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD HTML 4.0&#47;&#47;EN"></p>
<p><!DOCTYPE HTML PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD HTML 4.01&#47;&#47;EN"></p>
<p><!DOCTYPE HTML PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD HTML 4.0&#47;&#47;EN" "http:&#47;&#47;www.w3org&#47;TR&#47;html4&#47;strict.dtd"></p>
<p><!DOCTYPE HTML PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD HTML 4.01&#47;&#47;EN" "http:&#47;&#47;www.w3org&#47;TR&#47;html4&#47;strict.dtd"></p>
<p><strong>XHTML with or without a system identifier<&#47;strong></p>
<p><!DOCTYPE html PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD XHTML 1.1&#47;&#47;EN" "http:&#47;&#47;www.w3org&#47;TR&#47;xhtml11&#47;DTD&#47;xhtml11.dtd"></p>
<p><!DOCTYPE html PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD XHTML Basic 1.0&#47;&#47;EN" "http:&#47;&#47;www.w3org&#47;TR&#47;xhtml-basic&#47;xhtml-basic10.dtd"></p>
<p><!DOCTYPE html PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD XHTML 1.0 Strict&#47;&#47;EN" "http:&#47;&#47;www.w3org&#47;TR&#47;xhtml1&#47;DTD&#47;xhtml1-strict.dtd"></p>
<p><strong>Unknown<&#47;strong></p>
<p><!DOCTYPE html><&#47;td></p>
<td style="border: 1px solid #bbb;">Standards mode<&#47;td><br />
<&#47;tr></p>
<tr>
<td style="border: 1px solid #bbb;"><strong>XHTML Transitional or Frameset<&#47;strong><!DOCTYPE html PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD XHTML 1.0 Transitional&#47;&#47;EN"></p>
<p><!DOCTYPE html PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD XHTML 1.0 Frameset&#47;&#47;EN"></p>
<p><!DOCTYPE html PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD XHTML 1.0 Transitional&#47;&#47;EN" "http:&#47;&#47;www.w3.org&#47;TR&#47;xhtml1&#47;DTD&#47;xhmlt1-transitional.dtd"></p>
<p><strong>HTML 4.0 or HTML 4.01 Transitional or Frameset with a system identifier<&#47;strong></p>
<p><!DOCTYPE HTML PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD HTML 4.0 Transitional&#47;&#47;EN" "http:&#47;&#47;www.w3org&#47;TR&#47;html4&#47;loose.dtd"></p>
<p><!DOCTYPE HTML PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD HTML 4.01 Transitional&#47;&#47;EN" "http:&#47;&#47;www.w3org&#47;TR&#47;html4&#47;loose.dtd"></p>
<p><!DOCTYPE HTML PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD HTML 4.0 Transitional&#47;&#47;EN" "http:&#47;&#47;www.w3org&#47;TR&#47;1999&#47;REC-html401-19991224&#47;loose.dtd"><&#47;td></p>
<td style="border: 1px solid #bbb;">"Almost Standards" mode (standards mode in IE7)<&#47;td><br />
<&#47;tr></p>
<tr>
<td style="border: 1px solid #bbb;"><strong>HTML 4 and lower, or no DOCTYPE<&#47;strong><!DOCTYPE HTML PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD HTML 3.2 Final&#47;&#47;EN"></p>
<p><!DOCTYPE HTML PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD HTML 4.0 Transitional&#47;&#47;EN"></p>
<p><!DOCTYPE HTML PUBLIC "-&#47;&#47;W3C&#47;&#47;DTD HTML 4.01 Transitional&#47;&#47;EN"></p>
<p>None<&#47;td></p>
<td style="border: 1px solid #bbb;">Quirks mode<&#47;td><br />
<&#47;tr><br />
<&#47;tbody><br />
<&#47;table><br />
<strong>Reference<&#47;strong></p>
<p><a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ff406036(v=vs.85).aspx" target="_blank">http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ff406036(v=vs.85).aspx<&#47;a></p>
