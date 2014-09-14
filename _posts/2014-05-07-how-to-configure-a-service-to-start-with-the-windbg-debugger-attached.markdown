---
layout: post
status: publish
published: true
title: How to configure a service to start with the windbg debugger attached
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 563
wordpress_url: http://webdebug.net/?p=563
date: '2014-05-07 14:06:30 +0800'
date_gmt: '2014-05-07 14:06:30 +0800'
categories:
- Troubleshooting
tags:
- gflags
- windbg
- debug
comments:
- id: 6391
  author: Johna415
  author_email: johna873@gmail.com
  author_url: ''
  date: '2014-05-15 21:42:29 +0800'
  date_gmt: '2014-05-15 21:42:29 +0800'
  content: I do accept as true with all of the concepts you have offered in your post.
    They're really convincing and will definitely work. Still, the posts are very
    brief for beginners. May you please extend them a little from next time? Thanks
    for the post. bdeaekkgbbbd
---
<p>You can use this method to debug services if you want to troubleshoot service-startup-related problems.
<ol>
<li>Configure the "Image File Execution" options. To do this, use one of the following methods:
<ul>
<li>
<h6>Method 1: Use the Global Flags Editor (gflags.exe)<&#47;h6>
<ol>
<li>Start Windows Explorer.
<li>Locate the gflags.exe file on your computer.<br><b>Note<&#47;b> The gflags.exe file is typically located in the following directory: C:\Program Files\Debugging Tools for Windows.
<li>Run the gflags.exe file to start the Global Flags Editor.
<li>In the <strong>Image File Name<&#47;strong> text box, type the image name of the process that hosts the service that you want to debug. For example, if you want to debug a service that is hosted by a process that has MyService.exe as the image name, type MyService.exe.
<li>Under <strong>Destination<&#47;strong>, click to select the <strong>Image File Options<&#47;strong> option.
<li>Under <strong>Image Debugger Options<&#47;strong>, click to select the <strong>Debugger<&#47;strong> check box.
<li>In the <strong>Debugger<&#47;strong> text box, type the full path of the debugger that you want to use. For example, if you want to use the WinDbg debugger to debug a service, you can type a full path that is similar to the following: C:\Program Files\Debugging Tools for Windows\windbg.exe
<li>Click <strong>Apply<&#47;strong>, and then click <strong>OK<&#47;strong> to quit the Global Flags Editor.<&#47;li><&#47;ol>
<li>
<h6>Method 2: Use Registry Editor<&#47;h6>
<ol>
<li>Click <strong>Start<&#47;strong>, and then click <strong>Run<&#47;strong>. The <strong>Run<&#47;strong> dialog box appears.
<li>In the <strong>Open<&#47;strong> box, type regedit, and then click <strong>OK<&#47;strong> to start Registry Editor.
<li><b>Important<&#47;b> This section, method, or task contains steps that tell you how to modify the registry. However, serious problems might occur if you modify the registry incorrectly. Therefore, make sure that you follow these steps carefully. For added protection, back up the registry before you modify it. Then, you can restore the registry if a problem occurs. For more information about how to back up and restore the registry, click the following article number to view the article in the Microsoft Knowledge Base:
<p><a href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;322756">322756<&#47;a> How to back up and restore the registry in Windows
<p>In Registry Editor, locate, and then right-click the following registry subkey:
<p>HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options<&#47;p>
<li>Point to <strong>New<&#47;strong>, and then click <strong>Key<&#47;strong>. In the left pane of Registry Editor, notice that <strong>New Key #1<&#47;strong> (the name of a new registry subkey) is selected for editing.
<li>Type <var>ImageName<&#47;var> to replace <strong>New Key #1<&#47;strong>, and then press ENTER.<br><b>Note <&#47;b><var>ImageName<&#47;var> is a placeholder for the image name of the process that hosts the service that you want to debug. For example, if you want to debug a service that is hosted by a process that has MyService.exe as the image name, type MyService.exe.
<li>Right-click the registry subkey that you created in step e.
<li>Point to <strong>New<&#47;strong>, and then click <strong>String Value<&#47;strong>. In the right pane of Registry Editor, notice that <strong>New Value #1<&#47;strong>, the name of a new registry entry, is selected for editing.
<li>Replace <strong>New Value #1<&#47;strong> with Debugger, and then press ENTER.
<li>Right-click the <strong>Debugger<&#47;strong> registry entry that you created in step h, and then click <strong>Modify<&#47;strong>. The <strong>Edit String<&#47;strong> dialog box appears.
<li>In the <strong>Value data<&#47;strong> text box, type <var>DebuggerPath<&#47;var>, and then click <strong>OK<&#47;strong>.<br><b>Note <&#47;b><var>DebuggerPath<&#47;var> is a placeholder for the full path of the debugger that you want to use. For example, if you want to use the WinDbg debugger to debug a service, you can type a full path that is similar to the following:
<p>C:\Progra~1\Debugg~1\windbg.exe<&#47;p><&#47;li><&#47;ol><&#47;li><&#47;ul>
<li>For the debugger window to appear on your desktop, and to interact with the debugger, make your service interactive. If you do not make your service interactive, the debugger will start but you cannot see it and you cannot issue commands. To make your service interactive, use one of the following methods:
<ul>
<li>
<h6>Method 1: Use the Services console<&#47;h6>
<ol>
<li>Click <strong>Start<&#47;strong>, and then point to <strong>Programs<&#47;strong>.
<li>On the <strong>Programs<&#47;strong> menu, point to <strong>Administrative Tools<&#47;strong>, and then click <strong>Services<&#47;strong>. The <strong>Services<&#47;strong> console appears.
<li>In the right pane of the <strong>Services<&#47;strong> console, right-click <strong><var>ServiceName<&#47;var><&#47;strong>, and then click <strong>Properties<&#47;strong>.<br><b>Note <&#47;b><var>ServiceName<&#47;var> is a placeholder for the name of the service that you want to debug.
<li>On the <strong>Log On<&#47;strong> tab, click to select the <strong>Allow service to interact with desktop<&#47;strong> check box under <strong>Local System account<&#47;strong>, and then click <strong>OK<&#47;strong>.<&#47;li><&#47;ol>
<li>
<h6>Method 2: Use Registry Editor<&#47;h6>
<ol>
<li>In Registry Editor, locate, and then click the following registry subkey:
<p>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\ServiceName
<p><b>Note<&#47;b> Replace <var>ServiceName<&#47;var> with the name of the service that you want to debug. For example, if you want to debug a service named MyService, locate and then click the following registry key:
<p>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\MyService<&#47;p>
<li>Under the <strong>Name<&#47;strong> field in the right pane of Registry Editor, right-click <strong>Type<&#47;strong>, and then click <strong>Modify<&#47;strong>. The <strong>Edit DWORD Value<&#47;strong> dialog box appears.
<li>Change the text in the <strong>Value data<&#47;strong> text box to the result of the binary OR operation with the binary value of the current text and the binary value, 0x00000100, as the two operands. The binary value, 0x00000100, corresponds to the SERVICE_INTERACTIVE_PROCESS constant that is defined in the WinNT.h header file on your computer. This constant specifies that a service is interactive in nature.<&#47;li><&#47;ol><&#47;li><&#47;ul>
<li>When a service starts, the service communicates to the Service Control Manager how long the service must have to start (the time-out period for the service). If the Service Control Manager does not receive a "service started" notice from the service within this time-out period, the Service Control Manager terminates the process that hosts the service. This time-out period is typically less than 30 seconds. If you do not adjust this time-out period, the Service Control Manager ends the process and the attached debugger while you are trying to debug. To adjust this time-out period, follow these steps:
<ol>
<li>In Registry Editor, locate, and then right-click the following registry subkey:
<p>HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control<&#47;p>
<li>Point to <strong>New<&#47;strong>, and then click <strong>DWORD Value<&#47;strong>. In the right pane of Registry Editor, notice that <strong>New Value #1<&#47;strong> (the name of a new registry entry) is selected for editing.
<li>Type ServicesPipeTimeout to replace <strong>New Value #1<&#47;strong>, and then press ENTER.
<li>Right-click the <strong>ServicesPipeTimeout<&#47;strong> registry entry that you created in step c, and then click <strong>Modify<&#47;strong>. The <strong>Edit DWORD Value<&#47;strong> dialog box appears.
<li>In the <strong>Value data<&#47;strong> text box, type <var>TimeoutPeriod<&#47;var>, and then click <strong>OK<&#47;strong><br><b>Note <&#47;b><var>TimeoutPeriod<&#47;var> is a placeholder for the value of the time-out period (in milliseconds) that you want to set for the service. For example, if you want to set the time-out period to 24 hours (86400000 milliseconds), type 86400000.
<li>Restart the computer. You must restart the computer for Service Control Manager to apply this change.<&#47;li><&#47;ol>
<li>Start your Windows service. To do this, follow these steps:
<ol>
<li>Click <strong>Start<&#47;strong>, and then point to <strong>Programs<&#47;strong>.
<li>On the <strong>Programs<&#47;strong> menu, point to <strong>Administrative Tools<&#47;strong>, and then click <strong>Services<&#47;strong>. The <strong>Services<&#47;strong> console appears.
<li>In the right pane of the <strong>Services<&#47;strong> console, right-click <strong><var>ServiceName<&#47;var><&#47;strong>, and then click <strong>Start<&#47;strong>.<br><b>Note <&#47;b><var>ServiceName<&#47;var> is a placeholder for the name of the service that you want to debug.<&#47;li><&#47;ol><&#47;li><&#47;ol><br />
<h5><a><&#47;a>Troubleshooting<&#47;h5>Before you try to debug a service across a network, make sure that the symbols and the source files that the service uses are accessible from the computer where the service will run. To do this, use one of the following methods:
<ul>
<li>Grant at least read-access permissions to everyone for the folder on your computer that contains the symbols and the source files that the service uses.
<li>Copy these symbols and source files that the service uses to the computer where the service will run.<&#47;li><&#47;ul>
<p>&nbsp;<&#47;p>
<p><a title="http:&#47;&#47;support.microsoft.com&#47;kb&#47;824344" href="http:&#47;&#47;support.microsoft.com&#47;kb&#47;824344">http:&#47;&#47;support.microsoft.com&#47;kb&#47;824344<&#47;a><&#47;p></p>
