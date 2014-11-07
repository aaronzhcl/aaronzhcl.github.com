---
layout: post
status: publish
published: true
title: Collect IIS high CPU dumps with DebugDiag
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 29
wordpress_url: http://localhost:19634/?p=29
date: '2012-12-23 14:45:35 +0800'
date_gmt: '2012-12-23 14:45:35 +0800'
categories:
- IIS
- Data Collection
tags:
- IIS
- dump
- DebugDiag
- high CPU
comments: []
---
<p>1. Download and then install the <strong>DebugDiag</strong> from <a href="http://www.microsoft.com/download/en/details.aspx?id=26798">http://www.microsoft.com/download/en/details.aspx?id=26798</a><br />
2. Run <strong>DebugDiag Tool 1.2</strong> and click <strong>Add Rule</strong> button.<br />
4. Select <strong>Performance</strong> rule type and click <strong>Next</strong>.<br />
5. Select <strong>Performance Counters</strong> performance rule type and click <strong>Next.</strong><br />
6. Click <strong>Add Perf Triggers.</strong></p>
<ul>
<li>In <strong>Add Counters</strong> dialog select <strong>Process\%Processor Time</strong>, select <strong>w3wp</strong> instance, then click <strong>Add</strong> button then click <strong>OK</strong> button. (If there are multiple w3wp instances, you can add multiple counters for each.)</li>
<li>Select the counter just added and click <strong>Edit Thresholds</strong> button.</li>
<li>Take actions when this counter stays: <strong>Above</strong></li>
<li>This <strong>threshold</strong>: <strong>80</strong> (adjust this according to your CPU usage)</li>
<li>For this <strong>number of seconds</strong>: <strong>10</strong></li><br />
</ul><br />
7. Click <strong>OK</strong> and click <strong>Next</strong>.<br />
8. Select <strong>Add Dump Target</strong> and choose<strong> Web application pool</strong> as <strong>Target Type。</strong><br />
9. Select the application pool which costs high CPU usage and click <strong>OK</strong> and <strong>Next</strong>.<br />
10. Configure <strong>UserDump Series</strong></p>
<ul>
<li>Generate a UserDump every <strong>10</strong> seconds</li>
<li>Start the timer <strong>when writing the dump file completes</strong></li>
<li>Stop after generating <strong>3</strong> user dumps.</li>
<li>Collect <strong>Full UserDumps</strong></li><br />
</ul><br />
11. Click <strong>Next</strong> and name your rule and specify the <strong>UserDump locations</strong>.<br />
12. Click <strong>Next</strong> and <strong>Activate the Rule now</strong>.</p>
