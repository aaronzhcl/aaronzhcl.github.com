---
layout: post
status: publish
published: true
title: Troubleshooting .NET Memory Issue
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 462
wordpress_url: http://webdebug.net/?p=462
date: '2014-02-04 04:04:07 +0800'
date_gmt: '2014-02-04 04:04:07 +0800'
categories:
- Troubleshooting
- Performance
tags:
- .NET
- OutOfMemoryException
- GC
- garbage collection
- performance
- memory
comments: []
---
<h2><a href="http://msdn.microsoft.com/en-us/magazine/cc163528.aspx" target="_blank">MSDN Magazine - Investigating Memory Issues</a></h2></p>
<div>
<p><a href="http://webdebug.net/wp-content/uploads/2014/02/Main-interface_2.jpg"><img class="alignright size-medium wp-image-486" alt="Main interface_2" src="http://webdebug.net/wp-content/uploads/2014/02/Main-interface_2-300x227.jpg" width="300" height="227" /></a>Uncovering and correcting memory issues in managed applications can be difficult. Memory issues manifest themselves in different ways. For example, you may observe your application's memory usage growing unboundedly, eventually resulting in an Out Of Memory (OOM) exception. (Your application may even throw out-of-memory exceptions when there is plenty of physical memory available.) But any one of the following may indicate a possible memory issue:</p>
<!--more-->
<ul>
<li>An OutOfMemoryException is thrown.</li>
<li>The process is using too much memory for no obvious reason that you can determine.</li>
<li>It appears that garbage collection is not cleaning up objects fast enough.</li>
<li>The managed heap is overly fragmented.</li>
<li>The application is excessively using the CPU.</li><br />
</ul><br />
</div></p>
<div>This column discusses the investigation process and shows you how to collect the data you need to determine what types of memory issues you are dealing with in your applications. This column does not cover how to actually fix problems you find, but it does give some good insights as to where to start.</div></p>
<div></div></p>
<h2><a href="http://msdn.microsoft.com/en-us/library/ee851764%28v=vs.110%29.aspx" target="_blank">Garbage Collection and Performance</a></h2><br />
This topic describes issues related to garbage collection and memory usage. It addresses issues that pertain to the managed heap and explains how to minimize the effect of garbage collection on your applications. Each issue has links to procedures that you can use to investigate problems.</p>
<p>This topic contains the following sections:</p>
<ul>
<li><a href="http://msdn.microsoft.com/en-us/library/ee851764%28v=vs.110%29.aspx#performance_analysis_tools" target="_blank">Performance Analysis Tools</a></li>
<li><a href="http://msdn.microsoft.com/en-us/library/ee851764%28v=vs.110%29.aspx#troubleshooting_performance_issues" target="_blank">Troubleshooting Performance Issues</a></li>
<li><a href="http://msdn.microsoft.com/en-us/library/ee851764%28v=vs.110%29.aspx#troubleshooting_guidelines" target="_blank">Troubleshooting Guidelines</a></li>
<li><a href="http://msdn.microsoft.com/en-us/library/ee851764%28v=vs.110%29.aspx#performance_check_procedures" target="_blank">Performance Check Procedures</a></li><br />
</ul></p>
<h2><strong>CLR GC Toturials</strong></h2></p>
<h3><a href="http://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-33-CLR-GC-Part-1" target="_blank">Defrag Tools: #33 - CLR GC - Part&nbsp;1</a></h3><br />
<iframe style="height: 540px; width: 960px;" src="http://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-33-CLR-GC-Part-1/player?h=540&amp;w=960" height="240" width="320" allowfullscreen="" frameborder="0" scrolling="no"></iframe></p>
<p>Timeline:<br />
[00:00] - What is a Garbage Collector (GC)?<br />
[02:40] - How has the GC changed?<br />
[06:02] - Memory issues<br />
[08:57] - Stress Log (!sos.dumplog)<br />
[10:08] - Troubleshooting and Performance<br />
[12:20] - Demo App<br />
[14:20] - !sos.eeheap -gc<br />
[18:08] - !sos.dumpheap -stat<br />
[20:38] - !sos.dumpheap -mt <mt> (Method Table)<br />
[21:58] - !sos.dumpobj / !sos.do (Dump Object)<br />
[24:15] - Performance Monitoring (SOS, PerfView, Performance Monitor)<br />
[28:06] - Measure immediately after an action, not at a cadence<br />
[29:45] - x clr!WKS::GCHeap::GcCondemnedGeneration (Current GC being collected)<br />
[31:15] - bp clr!WKS::GCHeap::RestartEE (Break after a GC)<br />
[35:30] - More next week...</p>
<h3><a href="http://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-34-CLR-GC-Part-2" target="_blank">Defrag Tools: #34 - CLR GC - Part&nbsp;2</a></h3><br />
<iframe style="height: 540px; width: 960px;" src="http://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-34-CLR-GC-Part-2/player?h=540&amp;w=960" height="240" width="320" allowfullscreen="" frameborder="0" scrolling="no"></iframe></p>
<p>Timeline:<br />
[03:30] - How to approach Performance Analysis<br />
[09:00] - Cadence of Gen 0, 1 and 2 garbage collection<br />
[12:20] - !sos.FindRoots<br />
[14:00] - Stop at Gen 1 GC - !sos.FindRoots -gen 1<br />
[16:09] - End of GC: clr!WKS::GCHeap::RestartEE<br />
[17:10] - Stacks of allocations [CLRProfiler] [PerfView]<br />
[18:39] - Object's Generation - !sos.gcwhere <addr><br />
[19:28] - Generation Segments - !sos.eeheap -gc<br />
[24:52] - VM Hoarding<br />
[28:24] - Heap Summary - !sos.heapstat</p>
<h3><a href="http://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-35-CLR-GC-Part-3" target="_blank">Defrag Tools: #35 - CLR GC - Part&nbsp;3</a></h3><br />
<iframe style="height: 540px; width: 960px;" src="http://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-35-CLR-GC-Part-3/player?h=540&amp;w=960" height="240" width="320" allowfullscreen="" frameborder="0" scrolling="no"></iframe></p>
<p>Timeline:<br />
[00:45] - Internal and Externals Roots<br />
[05:55] - Start of GC: clr!WKS::GCHeap::GarbageCollectGeneration<br />
[07:00] - !sos.dumpheap <heap start addr> <heap end addr>&nbsp; (Range)<br />
[07:30] - !sos.gcroot <addr>&nbsp; (or !sos.gcwhere <addr>)<br />
[09:45] - New Root Types? Dependent Handles (ConditionalWeakTable)<br />
[12:32] - Handle Types<br />
[13:30] - Pinned Handles - Effect on Fragmentation<br />
[15:40] - Large Object Heap's Fragmentation &amp; Coalescence<br />
[17:55] - Pinned Objects<br />
[19:33] - !sos.gchandles<br />
[20:06] - !sos.gchandles -type Pinned<br />
[20:45] - !sos.gchandles -type AsyncPinned</p>
<h3><a href="http://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-36-CLR-GC-Part-4" target="_blank">Defrag Tools: #36 - CLR GC - Part&nbsp;4</a></h3><br />
<iframe style="height: 540px; width: 960px;" src="http://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-36-CLR-GC-Part-4/player?h=540&amp;w=960" height="240" width="320" allowfullscreen="" frameborder="0" scrolling="no"></iframe></p>
<p>Timeline:<br />
[00:38] - PerfView overview<br />
[02:52] - (Basic) Collection<br />
[04:39] - GCStats<br />
[10:10] - GC Rollup By Generation<br />
[11:22] - GC Events By Time (>200ms)<br />
[11:31] - LOH Allocation (>200ms)<br />
[12:34] - Gen2<br />
[12:48] - GC Events By Time<br />
[28:40] - Best Approach to Performance Analysis<br />
[31:03] - GC Collect Only<br />
[32:10] - Channel 9 - PerfView Tutorial</p>
