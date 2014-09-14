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
<p><strong>Fix Common IE Problems: Update your Docmode for Web Standards<&#47;strong></p>
<p><a href="http:&#47;&#47;blog.reybango.com&#47;2012&#47;01&#47;09&#47;fix-common-ie-problems-update-your-docmode-for-web-standards&#47;" target="_blank">http:&#47;&#47;blog.reybango.com&#47;2012&#47;01&#47;09&#47;fix-common-ie-problems-update-your-docmode-for-web-standards&#47;<&#47;a></p>
<p>Document compatibility defines how a browser renders your website.&nbsp; The more specific you are at telling the browser what to expect, the better the experience for your users. When using web standards like HTML5, start by <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;cc288325(v=VS.85).aspx">explicitly declaring<&#47;a> the HTML5 document type:</p>
<div>
<div id="highlighter_765222">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td>
<div>
<div><code><!DOCTYPE html><&#47;code><&#47;div><br />
<&#47;div><&#47;td><br />
<&#47;tr><br />
<&#47;tbody><br />
<&#47;table><br />
<&#47;div><br />
<&#47;div><br />
This markup triggers <a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;cc288325(v=VS.85).aspx">standards mode<&#47;a> in Internet Explorer 9 and 10.&nbsp; And it also works well in Chrome and Firefox.&nbsp; Four steps will get your site ready for many browsers and devices:</p>
<p>Step 1: Validate that your site uses standards mode</p>
<p>Step 2: Implement docmode for web standards</p>
<p>Step 3: Determine why your site is not in Standards Mode</p>
<p>Step 4: Resolve common IE problems when updating docmode</p>
<p>Other reasons my page does not render correctly:</p>
<p>For further detail, try these articles:</p>
<ul>
<li><a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;cc288325(v=VS.85).aspx">Defining Document Capability<&#47;a> @ MSDN<&#47;li>
<li><a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;gg699340(v=VS.85).aspx">Investigating Document Mode Issues<&#47;a> @ MSDN<&#47;li>
<li><a href="http:&#47;&#47;blogs.msdn.com&#47;b&#47;ie&#47;archive&#47;2011&#47;12&#47;14&#47;interoperable-html5-quirks-mode-in-ie10.aspx">Interoperable Quirks Mode in IE10<&#47;a> @ IE Blog<&#47;li>
<li><a href="http:&#47;&#47;ie.microsoft.com&#47;testdrive&#47;HTML5&#47;CompatInspector&#47;">Compatibility Inspector tool<&#47;a> @ IETestDrive.com<&#47;li>
<li><a href="http:&#47;&#47;www.w3.org&#47;QA&#47;Tips&#47;Doctype">Don&rsquo;t Forget to Add a Doctype<&#47;a> @ W3C.org<&#47;li><br />
<&#47;ul><br />
&nbsp;</p>
<p><strong>How Do I Fix My Site Today?<&#47;strong></p>
<p><a href="http:&#47;&#47;msdn.microsoft.com&#47;library&#47;ee318404.aspx" target="_blank">http:&#47;&#47;msdn.microsoft.com&#47;library&#47;ee318404.aspx<&#47;a></p>
<p>This document will take you through the steps required to fix your site so that it will properly render in Windows Internet Explorer 8.</p>
<ul>
<li><a href="#intro">Introduction<&#47;a><&#47;li>
<li><a href="#quick">The Quick Short-Term Fix<&#47;a><&#47;li>
<li><a href="#tag">How to Modify Each Page<&#47;a><&#47;li>
<li><a href="#auto">How to Configure the Server to Modify Each Page Automatically<&#47;a><&#47;li>
<li><a href="#perm">The Recommended Permanent Solution<&#47;a><&#47;li>
<li><a href="#set">Setting the Compatibility Mode to IE8 Standards<&#47;a><&#47;li>
<li><a href="#legacy">Using Conditional Comments to Keep Your Site Working With Legacy Browsers<&#47;a><&#47;li><br />
<&#47;ul></p>
