---
layout: post
status: publish
published: true
title: Fix Common IE Problems
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 274
wordpress_url: http://www.webdebug.net:80/?p=274
date: '2013-07-12 02:58:02 +0800'
date_gmt: '2013-07-12 02:58:02 +0800'
categories:
- browser
tags:
- browser
- Web Standards
- Compability
- docmode
- Standard Mode
comments: []
---
<p><strong>Fix Common IE Problems: Update your Docmode for Web Standards</strong></p>
<p><a href="http://blog.reybango.com/2012/01/09/fix-common-ie-problems-update-your-docmode-for-web-standards/" target="_blank">http://blog.reybango.com/2012/01/09/fix-common-ie-problems-update-your-docmode-for-web-standards/</a></p>
<p>Document compatibility defines how a browser renders your website.&nbsp; The more specific you are at telling the browser what to expect, the better the experience for your users. When using web standards like HTML5, start by <a href="http://msdn.microsoft.com/en-us/library/cc288325(v=VS.85).aspx">explicitly declaring</a> the HTML5 document type:</p>
<div>
<div id="highlighter_765222">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td>
<div>
<div><code><!DOCTYPE html></code></div><br />
</div></td><br />
</tr><br />
</tbody><br />
</table><br />
</div><br />
</div><br />
This markup triggers <a href="http://msdn.microsoft.com/en-us/library/cc288325(v=VS.85).aspx">standards mode</a> in Internet Explorer 9 and 10.&nbsp; And it also works well in Chrome and Firefox.&nbsp; Four steps will get your site ready for many browsers and devices:</p>
<p>Step 1: Validate that your site uses standards mode</p>
<p>Step 2: Implement docmode for web standards</p>
<p>Step 3: Determine why your site is not in Standards Mode</p>
<p>Step 4: Resolve common IE problems when updating docmode</p>
<p>Other reasons my page does not render correctly:</p>
<p>For further detail, try these articles:</p>
<ul>
<li><a href="http://msdn.microsoft.com/en-us/library/cc288325(v=VS.85).aspx">Defining Document Capability</a> @ MSDN</li>
<li><a href="http://msdn.microsoft.com/en-us/library/gg699340(v=VS.85).aspx">Investigating Document Mode Issues</a> @ MSDN</li>
<li><a href="http://blogs.msdn.com/b/ie/archive/2011/12/14/interoperable-html5-quirks-mode-in-ie10.aspx">Interoperable Quirks Mode in IE10</a> @ IE Blog</li>
<li><a href="http://ie.microsoft.com/testdrive/HTML5/CompatInspector/">Compatibility Inspector tool</a> @ IETestDrive.com</li>
<li><a href="http://www.w3.org/QA/Tips/Doctype">Don&rsquo;t Forget to Add a Doctype</a> @ W3C.org</li><br />
</ul><br />
&nbsp;</p>
<p><strong>How Do I Fix My Site Today?</strong></p>
<p><a href="http://msdn.microsoft.com/library/ee318404.aspx" target="_blank">http://msdn.microsoft.com/library/ee318404.aspx</a></p>
<p>This document will take you through the steps required to fix your site so that it will properly render in Windows Internet Explorer 8.</p>
<ul>
<li><a href="#intro">Introduction</a></li>
<li><a href="#quick">The Quick Short-Term Fix</a></li>
<li><a href="#tag">How to Modify Each Page</a></li>
<li><a href="#auto">How to Configure the Server to Modify Each Page Automatically</a></li>
<li><a href="#perm">The Recommended Permanent Solution</a></li>
<li><a href="#set">Setting the Compatibility Mode to IE8 Standards</a></li>
<li><a href="#legacy">Using Conditional Comments to Keep Your Site Working With Legacy Browsers</a></li><br />
</ul></p>
