---
layout: post
status: publish
published: true
title: Windows internal (memory, object, process, handles)
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 112
wordpress_url: http://www.webdebug.net:80/?p=112
date: '2012-12-26 09:36:45 +0800'
date_gmt: '2012-12-26 09:36:45 +0800'
categories:
- Windows
tags:
- kernel object
- handle
- GDI object
- user object
- virtual memory
- physical memory
- limit
- Windows
- paged pool
- nonpaged pool
comments: []
---
<p>Want to know more about Windows Kernel? Mark&nbsp;Russinovich wrote a&nbsp;Pushing the Limits series which lead to walk through the Windows internal concepts and mechanisms. Physical&#47;virtual memory, paged&#47;non-paged pool, process, threads, handles, user&#47;GDI objects.</p>
<p><strong><a href="http:&#47;&#47;blogs.technet.com&#47;markrussinovich&#47;archive&#47;2008&#47;07&#47;21&#47;3092070.aspx" target="_blank">Pushing the Limits of Windows: Physical Memory<&#47;a><&#47;strong><br />
One of the most fundamental resources on a computer is physical memory. Windows' memory manager is responsible with populating memory with the code and data of active processes, device drivers, and the operating system itself. Because most systems access more code and data than can fit in physical memory as they run, physical memory is in essence a window into the code and data used over time. The amount of memory can therefore affect performance, because when data or code a process or the operating system needs is not present, the memory manager must bring it in from disk.<br />
Besides affecting performance, the amount of physical memory impacts other resource limits. For example, the amount of non-paged pool, operating system buffers backed by physical memory, is obviously constrained by physical memory. Physical memory also contributes to the system virtual memory limit, which is the sum of roughly the size of physical memory plus the maximum configured size of any paging files. Physical memory also can indirectly limit the maximum number of processes, which I'll talk about in a future post on process and thread limits.</p>
<p><strong><a href="http:&#47;&#47;blogs.technet.com&#47;markrussinovich&#47;archive&#47;2008&#47;11&#47;17&#47;3155406.aspx" target="_blank">Pushing the Limits of Windows: Virtual Memory<&#47;a><&#47;strong><br />
Virtual memory separates a program&rsquo;s view of memory from the system&rsquo;s physical memory, so an operating system decides when and if to store the program&rsquo;s code and data in physical memory and when to store it in a file. The major advantage of virtual memory is that it allows more processes to execute concurrently than might otherwise fit in physical memory.</p>
<p><strong><a href="http:&#47;&#47;blogs.technet.com&#47;markrussinovich&#47;archive&#47;2009&#47;03&#47;26&#47;3211216.aspx">Pushing the Limits of Windows: Paged and Nonpaged Pool<&#47;a><&#47;strong><br />
Paged and nonpaged pools serve as the memory resources that the operating system and device drivers use to store their data structures. The pool manager operates in kernel mode, using regions of the system&rsquo;s virtual address space (described in the Pushing the Limits post on virtual memory) for the memory it sub-allocates. The kernel&rsquo;s pool manager operates similarly to the C-runtime and Windows heap managers that execute within user-mode processes. Because the minimum virtual memory allocation size is a multiple of the system page size (4KB on x86 and x64), these subsidiary memory managers carve up larger allocations into smaller ones so that memory isn&rsquo;t wasted.</p>
<p><strong><a href="http:&#47;&#47;blogs.technet.com&#47;markrussinovich&#47;archive&#47;2009&#47;07&#47;08&#47;3261309.aspx">Pushing the Limits of Windows: Processes and Threads<&#47;a><&#47;strong><br />
A Windows process is essentially container that hosts the execution of an executable image file. It is represented with a kernel process object and Windows uses the process object and its associated data structures to store and track information about the image&rsquo;s execution. For example, a process has a virtual address space that holds the process&rsquo;s private and shared data and into which the executable image and its associated DLLs are mapped. Windows records the process&rsquo;s use of resources for accounting and query by diagnostic tools and it registers the process&rsquo;s references to operating system objects in the process&rsquo;s handle table. Processes operate with a security context, called a token, that identifies the user account, account groups, and privileges assigned to the process.<br />
Finally, a process includes one or more threads that actually execute the code in the process (technically, processes don&rsquo;t run, threads do) and that are represented with kernel thread objects. There are several reasons applications create threads in addition to their default initial thread: processes with a user interface typically create threads to execute work so that the main thread remains responsive to user input and windowing commands; applications that want to take advantage of multiple processors for scalability or that want to continue executing while threads are tied up waiting for synchronous I&#47;O operations to complete also benefit from multiple threads.</p>
<p><strong><a href="http:&#47;&#47;blogs.technet.com&#47;markrussinovich&#47;archive&#47;2009&#47;09&#47;29&#47;3283844.aspx">Pushing the Limits of Windows: Handles<&#47;a><&#47;strong><br />
Handles are data structures that represent open instances of basic operating system objects applications interact with, such as files, registry keys, synchronization primitives, and shared memory. There are two limits related to the number of handles a process can create: the maximum number of handles the system sets for a process and the amount of memory available to store the handles and the objects the application is referencing with its handles.</p>
<p><strong><a href="http:&#47;&#47;blogs.technet.com&#47;markrussinovich&#47;archive&#47;2010&#47;02&#47;24&#47;3315174.aspx">Pushing the Limits of Windows: USER and GDI Objects &ndash; Part 1<&#47;a><&#47;strong><br />
<strong> <a href="http:&#47;&#47;blogs.technet.com&#47;markrussinovich&#47;archive&#47;2010&#47;03&#47;31&#47;3322423.aspx">Pushing the Limits of Windows: USER and GDI Objects &ndash; Part 2<&#47;a><&#47;strong><br />
USER and GDI objects, that represent window elements (like windows and menus) and graphics constructs (like pens, brushes and drawing surfaces). Just like for the other resources I&rsquo;ve discussed in previous posts, exhausting the various USER and GDI resource limits can lead to unpredictable behavior, including application failures and an unusable system.</p>
