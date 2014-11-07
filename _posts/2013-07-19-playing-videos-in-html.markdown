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
<p><a href="http://www.w3schools.com/html/html_videos.asp" target="_blank">http://www.w3schools.com/html/html_videos.asp</a></p>
<p>The easiest way to play videos (others or your own) in HTML is to use YouTube.</p>
<p><a href="http://www.w3schools.com/html/html_youtube.asp" target="_blank">http://www.w3schools.com/html/html_youtube.asp</a></p>
<p>YouTube iFrame<br />
[html]<br />
<iframe width="420" height="345"<br />
 src="http://www.youtube.com/embed/XGSy3_Czz8k"><br />
 </iframe><br />
[/html]</p>
<p>YouTube Embedded<br />
[html]<br />
<embed<br />
 width="420" height="345"<br />
 src="http://www.youtube.com/v/XGSy3_Czz8k"<br />
 type="application/x-shockwave-flash"><br />
 </embed><br />
[/html]</p>
<p>Video js is a another choice to play video online</p>
<p><a href="http://www.videojs.com/" target="_blank">http://www.videojs.com/</a></p>
<p>Use Video.JS<br />
In the <head>:</p>
<p>[html]</p>
<link href="http://vjs.zencdn.net/4.1/video-js.css"<br />
rel="stylesheet"><br />
<script src="http://vjs.zencdn.net/4.1/video.js"><br />
</script><br />
[/html]</p>
<p>In the <body>:</p>
<p>[html]<br />
<video id="my_video_1" class="video-js vjs-default-skin" controls<br />
 preload="auto" width="640" height="264" poster="my_video_poster.png"<br />
 data-setup="{}"><br />
 <source src="my_video.mp4" type='video/mp4'><br />
 <source src="my_video.webm" type='video/webm'><br />
</video><br />
[/html]</p>
