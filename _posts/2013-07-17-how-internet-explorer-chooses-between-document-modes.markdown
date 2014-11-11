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
<p>By default, Windows Internet Explorer 8 uses IE8 mode, Windows Internet Explorer 9 uses IE9 mode, etc. However, Windows Internet Explorer uses several criteria to determine which document mode to use. For example, if an HTML page contains a valid&nbsp;<code><!DOCTYPE></code>&nbsp;declaration (see&nbsp;<a href="http://go.microsoft.com/fwlink/?LinkId=89880" target="_blank">[HTML]</a>), Internet Explorer uses one of the standards-based document modes. But, if there is no valid&nbsp;<code><!DOCTYPE></code>&nbsp;declaration<code>,</code>&nbsp;Internet Explorer uses quirks mode.</p>
<!--more-->
<p>The following rules determine how Internet Explorer selects the document mode:</p>
<ol>
<li>The&nbsp;<strong>Developer Tools</strong>&nbsp;setting overrides any document mode specified by a webpage. The setting remains active for the lifetime of the tab.</li>
<li>In Internet Explorer 9, if the document is hosted in an&nbsp;<strong>iframe</strong>&nbsp;element, the document mode is determined by the document mode of the top-level webpage. Subdocuments cannot be rendered in IE9 mode unless the top-level document is also in IE9 mode.</li>
<li>A&nbsp;<strong>meta</strong>&nbsp;tag with a value of&nbsp;<code>X-UA-Compatible</code>&nbsp;or a HTTP response header can override items in the&nbsp;<strong>Compatibility View Settings</strong>&nbsp;list and the doctype unless the&nbsp;<strong>X-UA-Compatible</strong>&nbsp;value is a Compatibility View setting, such as&nbsp;<code>IE=EmulateIE7</code>&nbsp;or&nbsp;<code>IE=EmulateIE8</code>.</li>
<li>The Compatibility View settings can force a webpage to be displayed in a less-standard document mode.</li>
<li>If none of these rules apply, the&nbsp;<code><!DOCTYPE></code>&nbsp;declaration determines whether the webpage renders in a standards mode, Almost Standards mode, or quirks mode.</li><br />
</ol></p>
<table>
<tbody>
<tr>
<td id="ShadedCell" style="border: 1px solid #bbb;"><!DOCTYPE> declaration</td></p>
<td id="ShadedCell1" style="border: 1px solid #bbb;">Document Mode Impact</td><br />
</tr></p>
<tr>
<td style="border: 1px solid #bbb;"><strong>HTML 4.0 and higher</strong><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0//EN"></p>
<p><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN"></p>
<p><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0//EN" "http://www.w3org/TR/html4/strict.dtd"></p>
<p><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3org/TR/html4/strict.dtd"></p>
<p><strong>XHTML with or without a system identifier</strong></p>
<p><!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3org/TR/xhtml11/DTD/xhtml11.dtd"></p>
<p><!DOCTYPE html PUBLIC "-//W3C//DTD XHTML Basic 1.0//EN" "http://www.w3org/TR/xhtml-basic/xhtml-basic10.dtd"></p>
<p><!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3org/TR/xhtml1/DTD/xhtml1-strict.dtd"></p>
<p><strong>Unknown</strong></p>
<p><!DOCTYPE html></td></p>
<td style="border: 1px solid #bbb;">Standards mode</td><br />
</tr></p>
<tr>
<td style="border: 1px solid #bbb;"><strong>XHTML Transitional or Frameset</strong><!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"></p>
<p><!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN"></p>
<p><!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhmlt1-transitional.dtd"></p>
<p><strong>HTML 4.0 or HTML 4.01 Transitional or Frameset with a system identifier</strong></p>
<p><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN" "http://www.w3org/TR/html4/loose.dtd"></p>
<p><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3org/TR/html4/loose.dtd"></p>
<p><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN" "http://www.w3org/TR/1999/REC-html401-19991224/loose.dtd"></td></p>
<td style="border: 1px solid #bbb;">"Almost Standards" mode (standards mode in IE7)</td><br />
</tr></p>
<tr>
<td style="border: 1px solid #bbb;"><strong>HTML 4 and lower, or no DOCTYPE</strong><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN"></p>
<p><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN"></p>
<p><!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN"></p>
<p>None</td></p>
<td style="border: 1px solid #bbb;">Quirks mode</td><br />
</tr><br />
</tbody><br />
</table><br />
<strong>Reference</strong></p>
<p><a href="http://msdn.microsoft.com/en-us/library/ff406036(v=vs.85).aspx" target="_blank">http://msdn.microsoft.com/en-us/library/ff406036(v=vs.85).aspx</a></p>
