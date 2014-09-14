---
layout: post
status: publish
published: true
title: Playing videos in HTML
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 287
wordpress_url: http://www.webdebug.net:80/?p=287
date: '2013-07-19 07:59:58 +0800'
date_gmt: '2013-07-19 07:59:58 +0800'
categories:
- browser
tags:
- html
- video
- videojs
- youtube
comments: []
---
<p>Videos can be played in HTML by many different methods.</p>
<p><a href="http:&#47;&#47;www.w3schools.com&#47;html&#47;html_videos.asp" target="_blank">http:&#47;&#47;www.w3schools.com&#47;html&#47;html_videos.asp<&#47;a></p>
<p>The easiest way to play videos (others or your own) in HTML is to use YouTube.</p>
<p><a href="http:&#47;&#47;www.w3schools.com&#47;html&#47;html_youtube.asp" target="_blank">http:&#47;&#47;www.w3schools.com&#47;html&#47;html_youtube.asp<&#47;a></p>
<p>YouTube iFrame<br />
[html]<br />
<iframe width="420" height="345"<br />
 src="http:&#47;&#47;www.youtube.com&#47;embed&#47;XGSy3_Czz8k"><br />
 <&#47;iframe><br />
[&#47;html]</p>
<p>YouTube Embedded<br />
[html]<br />
<embed<br />
 width="420" height="345"<br />
 src="http:&#47;&#47;www.youtube.com&#47;v&#47;XGSy3_Czz8k"<br />
 type="application&#47;x-shockwave-flash"><br />
 <&#47;embed><br />
[&#47;html]</p>
<p>Video js is a another choice to play video online</p>
<p><a href="http:&#47;&#47;www.videojs.com&#47;" target="_blank">http:&#47;&#47;www.videojs.com&#47;<&#47;a></p>
<p>Use Video.JS<br />
In the <head>:</p>
<p>[html]</p>
<link href="http:&#47;&#47;vjs.zencdn.net&#47;4.1&#47;video-js.css"<br />
rel="stylesheet"><br />
<script src="http:&#47;&#47;vjs.zencdn.net&#47;4.1&#47;video.js"><br />
<&#47;script><br />
[&#47;html]</p>
<p>In the <body>:</p>
<p>[html]<br />
<video id="my_video_1" class="video-js vjs-default-skin" controls<br />
 preload="auto" width="640" height="264" poster="my_video_poster.png"<br />
 data-setup="{}"><br />
 <source src="my_video.mp4" type='video&#47;mp4'><br />
 <source src="my_video.webm" type='video&#47;webm'><br />
<&#47;video><br />
[&#47;html]</p>
