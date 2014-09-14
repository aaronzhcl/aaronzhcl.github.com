---
layout: post
status: publish
published: true
title: Troubleshoot IE memory leak
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 155
wordpress_url: http://www.webdebug.net:80/?p=155
date: '2012-12-29 13:23:49 +0800'
date_gmt: '2012-12-29 13:23:49 +0800'
categories:
- browser
- Troubleshooting
tags:
- browser
- memory leak
- javascript
comments: []
---
<p><a href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;bb250448(v=vs.85).aspx" target="_blank"><strong>Understanding and Solving Internet Explorer Leak Patterns<&#47;strong><&#47;a></p>
<p>The following sections will discuss patterns of memory leaks and point out some common examples of each pattern. One great example of a pattern is the closure feature of JScript, while another example is the use of closures in hooking events. If you're familiar with the event hooking example, you might be able to find and fix many of your memory leaks, but other closure-related issues might go unnoticed.<br />
Now, let's look at the following patterns:</p>
<ul>
<li><strong>Circular References<&#47;strong>&mdash;When mutual references are counted between Internet Explorer's COM infrastructure and any scripting engine, objects can leak memory. This is the broadest pattern.<&#47;li>
<li><strong>Closures<&#47;strong>&mdash;Closures are a specific form of circular reference that pose the largest pattern to existing Web application architectures. Closures are easy to spot because they rely on a specific language keyword and can be searched for generically.<&#47;li>
<li><strong>Cross-Page Leaks<&#47;strong>&mdash;Cross-page leaks are often very small leaks of internal book-keeping objects as you move from site to site. We'll examine the DOM Insertion Order issue, along with a workaround that shows how small changes to your code can prevent the creation of these book-keeping objects.<&#47;li>
<li><strong>Pseudo-Leaks<&#47;strong>&mdash;These aren't really leaks, but can be extremely annoying if you don't understand where your memory is going. We'll examine the script element rewriting and how it appears to leak quite a bit of memory, when it is really performing as required.<&#47;li><br />
<&#47;ul><br />
<a href="http:&#47;&#47;www.codeproject.com&#47;Articles&#47;12231&#47;Memory-Leakage-in-Internet-Explorer-revisited" target="_blank"><strong>Memory Leakage in Internet Explorer - revisited<&#47;strong><&#47;a><br />
By volkan.ozcelik, 12 Nov 2005</p>
<p>In this article, we will review those patterns from a slightly different perspective and support it with diagrams and memory utilization graphs. We will also introduce several subtler leak scenarios. Before we begin, I strongly recommend you to read that article if you have not already read.</p>
<p><a href="http:&#47;&#47;www.ibm.com&#47;developerworks&#47;web&#47;library&#47;wa-sieve&#47;" target="_blank"><strong>Find and resolve browser memory leaks caused by JavaScript and Dojo<&#47;strong><&#47;a><br />
Scan and sift with sIEve<br />
Yi Ming Huang, Software Engineer, IBM</p>
<p>If you're developing Web 2.0 applications that heavily use JavaScript and Ajax technologies, it is likely you will encounter browser memory leaks. The issue can be significant if you have a one-page application, or if a page handles a lot of UI operations. In this article, learn how to detect and correct memory leaks with the sIEve tool. Practical examples of memory leak issues, and the solutions, are included.</p>
<p><a href="http:&#47;&#47;sourceforge.net&#47;projects&#47;ieleak&#47;" target="_blank"><strong>IE Leak Detector (Drip&#47;IE Sieve)<&#47;strong><&#47;a></p>
<p>Both applications host Trident &ndash; IE&rsquo;s rendering engine &ndash; and add detection of memory leak patterns. They let you track memory and DOM usage while using a site and then detect any leaks when you navigate away from that page. Drip is an open source project under the BSD license. Based on Drip, sIEve improves the usability in a few ways including non-modal dialogs and a real-time graph of DOM usage instead of memory usage.</p>
