---
layout: post
status: publish
published: true
title: Build webkit with VS2013 and Windows 8.1
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 470
wordpress_url: http://webdebug.net/?p=470
date: '2014-02-12 08:47:24 +0800'
date_gmt: '2014-02-12 08:47:24 +0800'
categories:
- browser
tags:
- webkit
- build
- vs2013
- windows 8.1
comments:
- id: 15141
  author: Shawnee
  author_email: stephangirdlestone@web.de
  author_url: http://Samantha.blogspot.com
  date: '2014-07-08 11:24:50 +0800'
  date_gmt: '2014-07-08 11:24:50 +0800'
  content: "I see a lot of interesting content on your website.\r\nYou have to spend
    a lot of time writing, i know how to save you \r\na lot of time, there is a tool
    that creates unique, SEO friendly articles \r\nin couple of minutes, just type
    in google  - laranita's free content source"
---
<p><img class="alignright" alt="" src="http://upload.wikimedia.org/wikipedia/commons/e/e8/WebKit_logo.png" width="358" height="358"></p><p>OS: Windows 8.1</p>
<p>IDE: Visual Studio 2013</p>
<ol>
<li>You can build with either Visual Studio 2013 or Visual Studio 2013 express. (Newer versions currently unsupported)<br>Use the default options for the installation.
<li>Install Cygwin<br>Cygwin is a collection of utilities for Windows that includes not only a Subversion client, but also additional tools that are required to build the WebKit source. We have made a downloader available that automatically collects all of the required packages.
<!--more-->
<ol>
<li>Download cygwin-downloader.zip.
<li>Extract the content of the archive to some folder and start cygwin-downloader.exe from that folder. This will download all the Cygwin packages you need.
<li>When all the packages have finished downloading, the Cygwin installer will launch. Choose Install from Local Directory, then click Next until the install is complete. If you are running Vista, the installer won't be able to launch automatically, so you will have to manually launch Cygwin's Setup.exe.
<li>By default Cygwin will install python 2.7 however build webkit need to use python 2.6.8, so you can choose to install cygwin from internet again and choose python 2.6.8 version.
<li>Select Packages: Search "gcc", expand Devel, select "gcc-g++: GNU Compiler Collection(C++)"
<li>Select Packages: Search "gdb", expand Devel, select "gdb: The GNU Debugger"
<li>Open C:\cygwin\etc\profile
<ol>
<li>Modify line 32 to PATH="/bin:${PATH}"
<li>Comment line 44-50 (related to TMP variable) by adding '#' at the beginning of each line. </li></ol></li></ol>
<li>You can download a snapshot of the WebKit source tree from <a href="http://nightly.webkit.org/files/WebKit-SVN-source.tar.bz2">http://nightly.webkit.org/files/WebKit-SVN-source.tar.bz2</a>.
<li>Install the WebKit Support Libraries
<ol>
<li>Download the WebKit Support Libraries to the root of your source tree (C:\cygwin\home\<username>\WebKit). If the file is incorrectly named, rename it to WebKitSupportLibrary.zip. Do not extract its contents.
<li>Install QuickTime SDK and QuickTime or GStreamer<br>Download QuickTime SDK for Windows from <a href="http://developer.apple.com/quicktime/download/">http://developer.apple.com/quicktime/download/</a> and install it to the default location (\Program Files\QuickTime SDK). This is needed for media support for the AppleWin port. </li></ol>
<li>Install DirectX SDK<br>Download the June 2010 DirectX SDK This is needed for accelerated compositing.
<li>Run Tools/Scripts/update-webkit, if it fails to say CURL: ssl version is unsupported, change the Tools/Scripts/update-webkit-dependency line 85 and line 116 from sslv3 to tlsv1.
<li>Run Tools/Scripts/build-webkit or use Visual Studio to open webkit\Source\WebKit\WebKit.vcxproj\webkit.sln and start build. </li></ol>
<p><strong>Common Build Errors</strong></p>
<p><a title="http://trac.webkit.org/wiki/BuildingOnWindows#CommonBuildErrors" href="http://trac.webkit.org/wiki/BuildingOnWindows#CommonBuildErrors" target="_blank">http://trac.webkit.org/wiki/BuildingOnWindows#CommonBuildErrors</a></p></p>
