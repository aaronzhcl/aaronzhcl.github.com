---
layout: post
status: publish
published: true
title: what is browser reflow
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 246
wordpress_url: http://www.webdebug.net:80/?p=246
date: '2013-07-02 05:32:27 +0800'
date_gmt: '2013-07-02 05:32:27 +0800'
categories:
- browser
tags:
- browser
- css
- performance
- reflow
- repaint
- html
- DOM
comments: []
---
<p>Reflow is the name of the web browser process for re-calculating the positions and geometries of elements in the document, for the purpose of re-rendering part or all of the document. Because reflow is a user-blocking operation in the browser, it is useful for developers to understand how to improve reflow time and also to understand the effects of various document properties (DOM depth, CSS rule efficiency, different types of style changes) on reflow time. Sometimes reflowing a single element in the document may require reflowing its parent elements and also any elements which follow it.</p>
<p><strong>Minimizing browser reflow</strong></p>
<p>By Mozilla</p>
<p><a href="http://www-archive.mozilla.org/newlayout/doc/reflow.html" target="_blank">http://www-archive.mozilla.org/newlayout/doc/reflow.html</a></p>
<p><strong>Minimizing browser reflow</strong></p>
<p>By Lindsey Simon</p>
<p><a href="https://developers.google.com/speed/articles/reflow" target="_blank">https://developers.google.com/speed/articles/reflow</a></p>
<p><strong>Browser Reflows &amp; Repaints; How do they affect performance?</strong></p>
<p>By ajaxian.com</p>
<p><a href="http://ajaxian.com/archives/browser-reflows-how-do-they-affect-performance" target="_blank">http://ajaxian.com/archives/browser-reflows-how-do-they-affect-performance</a></p>
