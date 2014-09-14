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
<p>1. Download and then install the <strong>DebugDiag<&#47;strong> from <a href="http:&#47;&#47;www.microsoft.com&#47;download&#47;en&#47;details.aspx?id=26798">http:&#47;&#47;www.microsoft.com&#47;download&#47;en&#47;details.aspx?id=26798<&#47;a><br />
2. Run <strong>DebugDiag Tool 1.2<&#47;strong> and click <strong>Add Rule<&#47;strong> button.<br />
4. Select <strong>Performance<&#47;strong> rule type and click <strong>Next<&#47;strong>.<br />
5. Select <strong>Performance Counters<&#47;strong> performance rule type and click <strong>Next.<&#47;strong><br />
6. Click <strong>Add Perf Triggers.<&#47;strong></p>
<ul>
<li>In <strong>Add Counters<&#47;strong> dialog select <strong>Process\%Processor Time<&#47;strong>, select <strong>w3wp<&#47;strong> instance, then click <strong>Add<&#47;strong> button then click <strong>OK<&#47;strong> button. (If there are multiple w3wp instances, you can add multiple counters for each.)<&#47;li>
<li>Select the counter just added and click <strong>Edit Thresholds<&#47;strong> button.<&#47;li>
<li>Take actions when this counter stays: <strong>Above<&#47;strong><&#47;li>
<li>This <strong>threshold<&#47;strong>: <strong>80<&#47;strong> (adjust this according to your CPU usage)<&#47;li>
<li>For this <strong>number of seconds<&#47;strong>: <strong>10<&#47;strong><&#47;li><br />
<&#47;ul><br />
7. Click <strong>OK<&#47;strong> and click <strong>Next<&#47;strong>.<br />
8. Select <strong>Add Dump Target<&#47;strong> and choose<strong> Web application pool<&#47;strong> as <strong>Target Type。<&#47;strong><br />
9. Select the application pool which costs high CPU usage and click <strong>OK<&#47;strong> and <strong>Next<&#47;strong>.<br />
10. Configure <strong>UserDump Series<&#47;strong></p>
<ul>
<li>Generate a UserDump every <strong>10<&#47;strong> seconds<&#47;li>
<li>Start the timer <strong>when writing the dump file completes<&#47;strong><&#47;li>
<li>Stop after generating <strong>3<&#47;strong> user dumps.<&#47;li>
<li>Collect <strong>Full UserDumps<&#47;strong><&#47;li><br />
<&#47;ul><br />
11. Click <strong>Next<&#47;strong> and name your rule and specify the <strong>UserDump locations<&#47;strong>.<br />
12. Click <strong>Next<&#47;strong> and <strong>Activate the Rule now<&#47;strong>.</p>
