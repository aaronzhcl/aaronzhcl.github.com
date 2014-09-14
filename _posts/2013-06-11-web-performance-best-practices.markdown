---
layout: post
status: publish
published: true
title: Web Performance Best Practices
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 202
wordpress_url: http://www.webdebug.net:80/?p=202
date: '2013-06-11 07:05:21 +0800'
date_gmt: '2013-06-11 07:05:21 +0800'
categories:
- browser
tags:
- browser
- css
- webkit
- performance
comments: []
---
<p><strong><a href="https:&#47;&#47;developers.google.com&#47;speed&#47;docs&#47;best-practices&#47;rules_intro" target="_blank">Web Performance Best Practices<&#47;a><&#47;strong></p>
<p>by google</p>
<p>When you profile a web page with Page Speed, it evaluates the page's conformance to a number of different&nbsp;<i>rules<&#47;i>.&nbsp;These rules are general front-end best practices you can apply at any stage of web development. We provide documentation of each of the rules here, so whether or not you run the Page Speed tool &mdash; maybe you're just developing a brand new site and aren't ready to test it &mdash; you can refer to these pages at any time.&nbsp;We give you specific tips and suggestions for how you can best implement the rules and incorporate them into your development process.</p>
<ul>
<li><a href="https:&#47;&#47;developers.google.com&#47;speed&#47;docs&#47;best-practices&#47;caching">Optimizing caching<&#47;a>&nbsp;&mdash; keeping your application's data and logic&nbsp;<i>off<&#47;i>&nbsp;the network altogether<&#47;li>
<li><a href="https:&#47;&#47;developers.google.com&#47;speed&#47;docs&#47;best-practices&#47;rtt">Minimizing round-trip times<&#47;a>&nbsp;&mdash; reducing the number of serial request-response cycles<&#47;li>
<li><a href="https:&#47;&#47;developers.google.com&#47;speed&#47;docs&#47;best-practices&#47;request">Minimizing request overhead<&#47;a>&nbsp;&mdash; reducing upload size<&#47;li>
<li><a href="https:&#47;&#47;developers.google.com&#47;speed&#47;docs&#47;best-practices&#47;payload">Minimizing payload size<&#47;a>&nbsp;&mdash; reducing the size of responses, downloads, and cached pages<&#47;li>
<li><a href="https:&#47;&#47;developers.google.com&#47;speed&#47;docs&#47;best-practices&#47;rendering">Optimizing browser rendering<&#47;a>&nbsp;&mdash; improving the browser's layout of a page<&#47;li>
<li><a href="https:&#47;&#47;developers.google.com&#47;speed&#47;docs&#47;best-practices&#47;mobile">Optimizing for mobile<&#47;a><sup>New!<&#47;sup>&nbsp;&mdash; tuning a site for the characteristics of mobile networks and mobile devices<&#47;li><br />
<&#47;ul><br />
<strong><a href="http:&#47;&#47;developer.yahoo.com&#47;performance&#47;rules.html" target="_blank">Best Practices for Speeding Up Your Web Site<&#47;a><&#47;strong><br />
by Yahoo<br />
The Exceptional Performance team has identified a number of best practices for making web pages fast. The list includes 35 best practices divided into 7 categories.<br />
<strong><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rules.php" target="_blank">14 Rules for Faster-Loading Web Sites<&#47;a><&#47;strong></p>
<p>by&nbsp;Steve Souders</p>
<p>These pages are the companion web site for the book&nbsp;<a href="http:&#47;&#47;www.amazon.com&#47;gp&#47;product&#47;0596529309?ie=UTF8&amp;tag=stevsoud-20&amp;linkCode=as2&amp;camp=1789&amp;creative=9325&amp;creativeASIN=0596529309">High Performance Web Sites<&#47;a>. The examples referenced in the book are hosted here. Navigate through the rules listed below to find the associated examples. Each rule page also contains a link to the&nbsp;<a href="http:&#47;&#47;developer.yahoo.com&#47;performance&#47;rules.html">Yahoo! Developer Network Performance Blog<&#47;a>. There you will find a brief summary of the rule along with comments.</p>
<ul>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-min-http.php">Rule 1 - Make Fewer HTTP Requests<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-cdn.php">Rule 2 - Use a Content Delivery Network<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-expires.php">Rule 3 - Add an Expires Header<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-gzip.php">Rule 4 - Gzip Components<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-css-top.php">Rule 5 - Put Stylesheets at the Top<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-js-bottom.php">Rule 6 - Put Scripts at the Bottom<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-expr.php">Rule 7 - Avoid CSS Expressions<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-inline.php">Rule 8 - Make JavaScript and CSS External<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-dns.php">Rule 9 - Reduce DNS Lookups<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-minify.php">Rule 10 - Minify JavaScript<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-redir.php">Rule 11 - Avoid Redirects<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-js-dupes.php">Rule 12 - Remove Duplicate Scripts<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-etags.php">Rule 13 - Configure ETags<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;stevesouders.com&#47;hpws&#47;rule-ajax.php">Rule 14 - Make AJAX Cacheable<&#47;a><&#47;li><br />
<&#47;ul></p>
