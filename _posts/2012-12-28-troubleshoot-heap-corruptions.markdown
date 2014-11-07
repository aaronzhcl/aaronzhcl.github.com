---
layout: post
status: publish
published: true
title: Troubleshoot heap corruptions
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 149
wordpress_url: http://www.webdebug.net:80/?p=149
date: '2012-12-28 03:25:22 +0800'
date_gmt: '2012-12-28 03:25:22 +0800'
categories:
- IIS
- Troubleshooting
- Windows
tags:
- dump
- Crash
- heap corruption
- access violation
- gflags
- pageheap
- adplus
comments:
- id: 21574
  author: Emma
  author_email: emma.bruxner@web.de
  author_url: https://youtube.com
  date: '2014-08-26 17:07:43 +0800'
  date_gmt: '2014-08-26 17:07:43 +0800'
  content: "Hi to every , since I am truly eager of reading this website's post to
    be updated daily.\r\n\r\nIt includes good data."
---
<p><a href="http://blogs.msdn.com/b/webdav_101/archive/2010/06/22/detecting-heap-corruption-using-gflags-and-dumps.aspx" target="_blank"><strong>Detecting Heap Corruption Using GFlags and Dumps</strong></a><br />
By Dan's WebDAV 101</p>
<p>One way to check for heap corruption is using gflags.exe in combination with a debugger (you can use ADPlus which will attach a debugger for you) to take a dump. This checking is not a 100% catch-all, however it works fairly well. Using gflags to do this type of check will cause an application (as an example the w3wp.exe for the worker process under IIS for a web application) to crash when there is heap corruption. When a debugger (such as what ADPlus would use) is to the process and there is a detected corruption, a crash dump will be created which can be used to find which module (dll, etc) caused the corruption. There was a similar program in the past called pageheap.exe; however, its functionality has been merged into gflags.exe.</p>
<p><strong><a href="http://blogs.msdn.com/b/carlos/archive/2008/12/10/heap-corruption-a-case-study.aspx" target="_blank">Heap Corruption: A Case Study</a></strong><br />
By Carlo Colombo</p>
<p>Memory corruption, in general, is one of the toughest issues to work with. For several reasons:</p>
<p>It is not immediate, for starting, to understand that a problem (endless loop, unexpected behavior, crash) is caused by a memory corruption.<br />
Historically, user-mode processes with their own virtual address space and the separation of user-mode and kernel mode were meant to provide an isolated environment for code, so that bad code which, for example, could cause a memory corruption, was not able to adversely affect other code. On the other hand, the appearance of "host processes" like svchost.exe for services, dllhost.exe for COM+ applications and w3wp.exe for ASP.NET and Web Services, made again different components run in the same process. There are benefits to it, but the fact that different software shares a common address space means that, when a memory corruption occurs, the whole process is affected. Moreover, it may be difficult to determine which component is at fault.<br />
The consequences of a memory corruption typically manifest themselves at a later time, when the corrupted area is read. At that time it is difficult, if not impossible, to backtrack to the source of the corruption.<br />
In case you wonder, the additional isolation provided by .NET through AppDomains does not help in this case: if memory gets corrupted in an address space there is no way to recover.</p>
<p><a href="http://support.microsoft.com/kb/286470" target="_blank"><strong>How to use Pageheap.exe in Windows XP, Windows 2000, and Windows Server 2003</strong></a></p>
<p>Pageheap.exe sets page heap flags that help to find heap-related corruption. It can also help detect leaks in programs that are running on Windows 2000 Professional Service Pack 2 (SP2) and Windows XP Professional systems.</p>
<p>Pageheap.exe introduces a software validation layer (Page Heap manager) between the application and the system that verifies all dynamic memory operations (allocations, frees, and other heap operations). When Page Heap manager is enabled, the application that is being tested is then started under a debugger. If a problem is encountered, it will cause a debugger break.</p>
<p><strong><a href="http://support.microsoft.com/kb/286350" target="_blank">How to use ADPlus.vbs to troubleshoot "hangs" and "crashes"</a></strong></p>
<p>ADPlus.vbs (ADPlus) is a tool from Microsoft Product Support Services (PSS) that can troubleshoot any process or application that stops responding (hangs) or fails (crashes). Frequently, you can use ADPlus as a replacement tool for the Microsoft Internet Information Server (IIS) Exception Monitor (6.1/7.1) and User Mode Process Dump. These are two separate tools that PSS frequently uses to isolate what causes a process to stop responding (hang) or quit unexpectedly (crash) in a Microsoft Windows DNA environment.</p>
