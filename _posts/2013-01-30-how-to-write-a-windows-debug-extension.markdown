---
layout: post
status: publish
published: true
title: How to write a windows debug extension
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 185
wordpress_url: http://www.webdebug.net:80/?p=185
date: '2013-01-30 15:47:17 +0800'
date_gmt: '2013-01-30 15:47:17 +0800'
categories:
- Troubleshooting
- Windows
tags:
- windbg
- debug extension
comments: []
---
<p><strong><a href="http:&#47;&#47;blogs.msdn.com&#47;b&#47;andrew_richards&#47;archive&#47;2011&#47;04&#47;23&#47;writing-a-debugging-tools-for-windows-extension.aspx" target="_blank">Writing a 'Debugging Tools for Windows' Extension<&#47;a><&#47;strong><br />
By Andrew Richards</p>
<p>Writing a Debugging Tools for Windows Extension - Part 1 - March 2011<br />
Covers the build environment and the basics of Output, reading Memory and reading Registers</p>
<p>Writing a Debugging Tools for Windows Extension - Part 2 - May 2011<br />
Covers the how of Debugger Markup Language (DML)</p>
<p>Writing a Debugging Tools for Windows Extension - Part 3 - June 2011<br />
Covers the how and why to use Debugger Clients and Debugger Output Callbacks</p>
<p><a href="http:&#47;&#47;www.codeproject.com&#47;Articles&#47;6522&#47;Debug-Tutorial-Part-4-Writing-WINDBG-Extensions" target="_blank"><strong>Debug Tutorial Part 4: Writing WINDBG Extensions<&#47;strong><&#47;a></p>
<p>By Toby Opferman</p>
<p>Welcome to the fourth installment of this debugging series. In this installment, we will be getting a bit away from actual debugging for a bit and dive into creating helpful debugging aids. I definitely would never condone writing debugging aids just to write them. I would find a reason to write something, perhaps something you do all the time that gets tedious. Once you have found something you would love to automate, I would then see how you could automate it.</p>
<p>This is what I have done. During my debugging escapades, I&nbsp;<b>always<&#47;b>&nbsp;search the stack and other locations for strings. Why do I do this? People are not computers, we understand language rather than numbers. This being the case, a lot of applications and even drivers are written based upon strings. I would not say everything is a string, but there's usually a string somewhere. If you think about it, you really don't need strings at all. We could all just use numbers and never use another string again. Some may think well, when you expose a UI of course, you're going to eventually run into a string somewhere... Well, doesn't have to be that way, now does it? I mean, I'm not even talking about just User Interfaces, I'm talking about the guts of programs that aren't even exposed to the user at all. Programmers are still human and like to talk in some language beyond binary. This being the case, even the internals of applications sometimes use strings to represent things. You can find strings just about anywhere, even in drivers.</p>
<p><a href="http:&#47;&#47;www.drdobbs.com&#47;writing-a-kdwindbg-debugger-extension-dl&#47;184416518?pgno=1" target="_blank"><strong>Writing a kd&#47;WinDbg Debugger Extension DLL<&#47;strong><&#47;a><br />
By Myk Willis</p>
<p>I&rsquo;ll focus on writing debugger extensions for kernel-mode code, because extensions are typically most useful when debugging device drivers. You can use the same interface for user-mode debugging, but you should be aware that many of the low-level services provided by the debugger function properly only when debugging kernel-mode code. The example extensions presented assume you have the NT DDK and are debugging NT drivers on an Intel x86 platform.</p>
<p><strong><a href="http:&#47;&#47;mcfunley.com&#47;the-debugger-extension-part-1-what-is-a-dbgeng-extension" target="_blank">The Debugger Extension, Part 1: What Is a DbgEng Extension?<&#47;a><&#47;strong></p>
<p>By Dan McKinley</p>
<p>A better question to start off might be: "what is DbgEng?" Frequent visitors may have seen me refer to WinDbg and the Debugging Tools for Windows somewhat interchangably. There are actually two other debuggers in the package called CDB and NTSD. CDB, NTSD, and WinDbg are all written on top of the same debugger engine, implemented in dbgeng.dll.</p>
<p>An extension for the debugger engine is a dll with a specific set of exported functions. Commands that are callable from the debugger are implemented as additional exported functions. SOS, SieExtPub, and other modules I may have mentioned before are all debugger extensions in this vein. The full syntax for calling an extension function from within the debugger is:</p>
