---
layout: post
status: publish
published: true
title: Proxy PAC File Tricks and Tips
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 450
wordpress_url: http://webdebug.net/?p=450
date: '2014-01-02 09:42:03 +0800'
date_gmt: '2014-01-02 09:42:03 +0800'
categories:
- browser
tags:
- IE
- pac
- proxy
comments:
- id: 8838
  author: Vpn Ipad
  author_email: TwyfordEastmond741@hotmail.com
  author_url: https://www.youtube.com/watch?v=Ewex9QB8WAg
  date: '2014-05-31 23:22:14 +0800'
  date_gmt: '2014-05-31 23:22:14 +0800'
  content: Hey there, I discovered your web site by means of Yahoo and google while
    doing so because hunting for a similar issue, your web site got here in place,
    it seems like very good. I've got added to my own favourites types|added to book
    marking.
- id: 18605
  author: Paulette
  author_email: paulettemedders@arcor.de
  author_url: http://whatculture.com/film/five-things-that-probably-will-happen-in-the-dark-knight-rises.php
  date: '2014-07-29 00:56:42 +0800'
  date_gmt: '2014-07-29 00:56:42 +0800'
  content: "I create a comment each time I appreciate a post on a website or if I
    have \r\nsomething to valuable to contribute to the conversation. It's a result
    of \r\nthe sincerness communicated in the post I browsed.\r\nAnd after this article
    Proxy PAC File Tricks and Tips | Web Debug.\r\nI was actually moved enough to
    drop a thought :-P I do have a few questions for \r\nyou if it's okay. Is it only
    me or does it give \r\nthe impression like a few of the responses look as if they
    are coming from brain dead \r\npeople? :-P And, if you are writing at additional
    online social \r\nsites, I would like to follow you. Would you list the complete
    urls of all your community pages like your linkedin profile, Facebook \r\npage
    or twitter feed?"
- id: 19364
  author: seedbox how to make pizza dough from scratch
  author_email: bertmcdavid@mailc.net
  author_url: http://www.ohiovotes.org/forum/blogs/sample_weblog/archive/2009/03/12/My-First-Post.aspx
  date: '2014-08-07 07:41:30 +0800'
  date_gmt: '2014-08-07 07:41:30 +0800'
  content: "It's very effortless to find out any topic on web as compared to textbooks,
    as I found \r\nthis piece of writing at this web page."
---
<h1><img class="alignright" alt="" src="http:&#47;&#47;blogs.msdn.com&#47;blogfiles&#47;askie&#47;WindowsLiveWriter&#47;AutomaticProxyConfigurationScriptfailing_C281&#47;clip_image002_2.jpg" width="384" height="332" &#47;>Dealing with Case Sensitivity<&#47;h1><br />
As mentioned above, PAC files are case sensitive. If you are seeing issues with upper&#47;lower case URL&rsquo;s it is relatively simple to convert everything to lower case at the top of the PAC file and not have to worry about case later on. To do so, simply put this section somewhere near the top of your PAC file:</p>
<pre class="brush:js">var lhost = host.toLowerCase();<br />
host = lhost;<&#47;pre></p>
<h1>Effective use of Indentations<&#47;h1><br />
Another fairly simple programming trick is to make sure you effectively use indentations. It makes your PAC file much easier to read and easier to troubleshoot. The very simple rule says "If you are putting something inside braces ( { } ), indent it one more tab stop. Your close brace should be at the same indent level as the item that opened the brace. The only exception to this rule is that you don&rsquo;t need to indent your entire PAC file that&rsquo;s between the "function FindProxyForURL(url, host) {" at the top and the very last closing brace at the bottom. It&rsquo;s safe to cheat here. Just be sure to indent your IF statements and make things line up nicely for readability. You (and your co-workers) will be happy about this later as they can more easily read through the PAC file.</p>
<p>For a good examples of indenting, see the sample PAC files in the menues to the left.</p>
<h1>Dealing with localhost and loopback addresses<&#47;h1><br />
Localhost and loopback should always bypass the proxy &ndash; Put this near the top of your PAC file.</p>
<pre class="brush:js">if ((host == "localhost") ||<br />
(shExpMatch(host, "localhost.*")) ||<br />
(host == "127.0.0.1")) {<br />
return "DIRECT";<&#47;pre></p>
<h1>Safely Blocking Sites at the Browser Instead of the Proxy<&#47;h1><br />
Blocking sites is also handy. This can be done for a number of reasons &ndash; Spyware&#47;malware sites are very good examples Blocking these sites can be done very easily &ndash; Simply return a proxy value somewhere on a loopback address so that the requests never actually leave the local machine to take up network bandwidth. The only caveat with this is to ensure that your selection of port number isn&rsquo;t actually listening on the PC which could odd behavior.</p>
<pre class="brush:js">if (dnsDomainIs(host, ".badspyware.com") ||<br />
dnsDomainIs(host, ".worsespyware2.com")) {<br />
return "PROXY 127.0.0.1:48890";<br />
}<&#47;pre></p>
<h1>Using alert() for Notifications and Troubleshooting<&#47;h1><br />
Alert() can be used very effectively to help troubleshooting browser issues, especially the one mentioned above where the browser occasionally picks the wrong IP for myIpAddress(). For this, pick a bogus hostname &ndash; proxyinfo.company.com would work fine. It doesn&rsquo;t have to be in DNS or registered anywhere &ndash; Just placing it in the PAC file is all you need. Be aware, however that the alert message is displayed with EVERY request that matches the condition. If you accidentally get an alert in the wrong place it can be very annoying and render the browser nearly useless. Used properly, however, it can be VERY handy.</p>
<pre class="brush:js">if ((host =="proxyinfo.company.com")) {<br />
alert("Local IP address is: " + myIpAddress());<br />
}<&#47;pre></p>
<h1>Using Variables<&#47;h1><br />
Using variables within a PAC file can be an extremely powerful way to simplify your PAC file. You can create variables to hold almost any value - A client's IP address, a proxy server address, a true&#47;false value, etc. This variable can be read and reset at any point in the PAC file.</p>
<p>To use a variable, all you need to do is set it to a value. For example, to set a variable called "myip", enter the following near the top of your PAC file.</p>
<pre class="brush:js">myip = myIpAddress();<&#47;pre><br />
When setting a variable, you can <em>optionally <&#47;em>insert the word "var" in front of it. I typically do not do this, however.</p>
<p>Once the variable has been set, you can the variable name at any further point in the PAC file. For example:</p>
<pre class="brush:js">if(isInNet(myip, "192.160.1.0","255.255.255.0")) { ....  }<&#47;pre><br />
Why would you do this? In this particular case, it's much "cheaper" computationally to call the function myIpAddress() once and put it into a variable rather than to call it multiple times.</p>
<p>One of most effective uses of varialbles is to set a variable to one piece of data and then change it as your PAC file progresses. I use this for setting a proxy variable and then adjusting it based on client IP address or other conditions. When I get to a RETURN statement I simply return the proxy variable. Here's an example of how that can be used:</p>
<pre class="brush:js">function FindProxyForURL(url, host) {<br />
&#47;&#47; Set the default proxy variable that users get if they don&rsquo;t match<br />
&#47;&#47; any more specific rule.<br />
proxy = "PROXY coreproxy.company.com:8000";</p>
<p>&#47;&#47; Los Angeles WAN subnets go to LA proxy<br />
if (isInNet(myIpAddress(), "10.100.0.0", "255.252.0.0")) {<br />
proxy = "PROXY la-proxy.company.com:8000";<br />
}</p>
<p>&#47;&#47; New York WAN subnets go to New York proxy<br />
if (isInNet(myIpAddress(), "10.200.0.0", "255.252.0.0")) {<br />
proxy = "PROXY ny-proxy.company.com:8000";<br />
}<&#47;pre><br />
When writing this kind of PAC file, remember to start with the most generic and get to the most specific. If you need to route a single &#47;24 to a specific proxy, do it AFTER you&rsquo;re done routing the &#47;16&rsquo;s. Pay attention to where the variable gets set and make sure it doesn&rsquo;t get overwritten later.</p>
<p>When you have reached a point in your PAC file that you need to return a proxy value, you just return the variable, as shown below.</p>
<p>return proxy;</p>
<h1>Safely using IsInNet(host, &hellip;)<&#47;h1><br />
It is very useful to use isInNet(host., &hellip;.), especially when the host is an IP address and you&rsquo;re trying to match it. For example, you might need to send all traffic in the 10.0.0.0&#47;8 and 192.168.0.0&#47;16 address spaces browser direct but all other direct IP&rsquo;s via the proxy. Unfortunately, just using IsInNet(host, &hellip;) alone causes problems, discussed the Lessons Learned article.</p>
<p>Fortunately, there is a way around it: Write an IF statement that uses a regex check to see if the host is an IP address then use IsInNet(host, &hellip;) to check to see if it&rsquo;s in a specific subnet. Example:</p>
<pre class="brush:js">reip = &#47;^\d+\.\d+\.\d+\.\d+$&#47;g;<br />
if (reip.test(host)) {<br />
if (isInNet(host, "10.0.0.0", "255.0.0.0") ||<br />
isInNet(host, "192.168.0.0", "255.255.0.0")) {<br />
return "DIRECT";<br />
}<br />
}<&#47;pre><br />
Some have reported issues with later versions of IE not working properly with this type of regex test, but that shExpMatch works properly.</p>
<pre class="brush:js">if (shExpMatch(host, "&#47;^\d+\.\d+\.\d+\.\d+$&#47;g")) {<br />
if (isInNet(host, "10.0.0.0", "255.0.0.0") ||<br />
isInNet(host, "192.168.0.0", "255.255.0.0")) {<br />
return "DIRECT";<br />
}<br />
}<&#47;pre><br />
You can also use simple regex matches for your IP space, but this is far more elegant and effective, especially if you&rsquo;re testing multiple subnets.</p>
<h1>Using Substrings<&#47;h1><br />
It is possible to check only a specified range of characters within the URL or within the host variable. This is referred to as a substring. It can be extremely handy for many things. One of the most common ways to use a substring is to check what protocol it is. This might be handy, for example, if you have a configuration where you have a separate proxy for different protocols &ndash; i.e. HTTP requests go to the main company proxy, ftp requests go to the FTP relay and MMS links go to the streaming infrastructure. One important note on substrings - Because of IE's Automatic Proxy Results Cache (See the Lessons Learned section for details) the browser only queries the PAC file once per host and caches that result. Be sure to consider this when using substrings.</p>
<p>Using substrings is fairly simple. The syntax is &ldquo;varname.substring(begin,end)&rdquo; where varname is the text-based variable (i.e. host or url) that you want to check, begin is where the substring starts and end is where it finishes. Keep in mind that the first character in a string is position #0, not #1 as you might expect.</p>
<p>Examples:</p>
<pre class="brush:js">if (url.substring(0,4) == "http") { return "PROXY http-proxy.company.com:8000"; }  &#47;&#47;matches HTTP and HTTPS URLs<br />
if (url.substring(0,3) == "ftp")  { return "PROXY ftp-proxy.company.com:8000"; }  &#47;&#47;matches FTP:&#47;&#47; links<br />
if (url.substring(0,3) == "mms") { return "PROXY http-proxy.company.com:8000"; }  &#47;&#47;matches MMS links<&#47;pre><br />
This is only one way to use substrings &ndash; If you can find a consistent character position within the URL you can split it out and look at it.</p>
<h1>Advanced JavaScript Ideas<&#47;h1><br />
This guide is focused on the things that I&rsquo;ve found are useful when writing PAC files. That isn&rsquo;t to say that it covers everything you might need to do. JavaScript is a complex language with a lot of very powerful features. You can use nearly all of them within a PAC file. Don&rsquo;t let this (or any other such guide) limit you to what you can try. Dig into a JavaScript reference and experiment a bit with some of the more advanced features. Think about some of the string manipulation features (length, used in combination with substring, for example), using arrays, writing your own reusable subroutines within the PAC file, etc.</p>
<p>Here&rsquo;s a non-real-world example to get you thinking about what you could do...</p>
<p>Let&rsquo;s say your company has fifty office buildings. Each one is assigned a &#47;16 in 10.x &ndash; 10.1.0.0&#47;16, 10.2.0.0&#47;16, etc. Each floor gets a range of ten &#47;24 subnets. Floor 1 is .10 -.19, floor 2 is .20-29, etc. In each building, the executives are placed on the 20th floor. So, their subnet range is .200 - .209. An executive in building #13 might be assigned an IP address of 10.13.202.84.</p>
<p>Your team has built a special proxy to be used only be executives, to ensure they get the fastest possible response time. Using basic PAC file functions described so far, you&rsquo;d have to put in 100+ isInNet(myIpAddress()) lines to match all of these. But there&rsquo;s a better way &ndash; Using the JavaScript split function and arrays. Here&rsquo;s how..</p>
<pre class="brush:js">var myip = myIpAddress();  &#47;&#47; Set a variable for the local IP address.<br />
var my-addr-array = myip.split(".");  &#47;&#47; Split that IP address var into an array.<br />
var mysubnet=parseInt(my-addr-array[2]);  &#47;&#47; Convert array element #2 into a number and store it in a new variable<br />
if ((mysubnet >= 200) &amp;&amp; (mysubnet < = 209)) {   &#47;&#47; If that number is between 200 and 209&#47;&#47;<br />
proxy = "PROXY execproxy.company.com:8000");   &#47;&#47; Assign it to the executive proxy<br />
}<br />
else {<br />
proxy = "PROXY proxy.company.com:8000";   &#47;&#47; Otherwise they get the standard proxy.<br />
}<&#47;pre><br />
Another very useful JavaScript idea is using split. This is a way to break out a string into chunks by splitting on a specific character. The result of this will be an array that you can use containing the split-apart text. A good example of this is to split the client IP address into chunks. For example..</p>
<pre class="brush:js">var myip=myIpAddress()<br />
var octects=myip.split(".")<&#47;pre><br />
You now have an array variable called "octects" that is the different octects of the IP address string split into an array. You can refer to "octects[0]" for the first octect, "octets[1]" for the second, etc.</p>
<p>One important item to keep in mind is that a string value and a number value are very different. The character "3" stored in text is just that - A string character. The number 3 is a real number that can be manipulated. In the above case, for a IP address of 192.168.103.93 you will have an array with four text strings. "192", "168", "103" and "93". These can be used for an exact match, but not to compare or run any math. You can, however, convert them to numbers using the ParseInt() function. Here's an example:</p>
<pre class="brush:js">firstoctet = ParseInt(octects[0]);<&#47;pre><br />
Now, the variable "firstoctet" will contain the number 192, not the string "192". This new variable can use any type of math function, greater&#47;less than compares, etc.<br />
These are just a few example &ndash; If you can think of something you need to do, it&rsquo;s probably possible to do it. Need to block all &ldquo;.pif&rdquo; files? Use the url.length-3 as the beginning of your url.substring and url.length as the end of it &ndash; Is the substring &ldquo;pif&rdquo;? If so, send it to a loopback address, like a spyware block. Don&rsquo;t be afraid to dig in and experiment.</p>
<p>It is, of course, important to add the standard caveat &ndash; Assume that you&rsquo;re going to get hit by a bus tomorrow. Make sure that someone else can support your PAC file. Document it, add appropriate comments, etc. and follow the golden rule - Keep It Simple and Supportable! A PAC file is not the place to be writing obfuscated JavaScript!</p>
<h1>Proxy Load Balancing within a PAC File<&#47;h1><br />
Many organizations have multiple proxy servers in the same location without a hardware load balancer to distribute traffic. This section provides a method to load balance traffic between two proxies by looking at the last octect of the users' IP address. Addresses with even numbers go to one proxy, addresses with odd numbers go to another. This includes failover, should one proxy become non-responsive. PAC-file based proxy failover can have it's challenges (as noted in the Lessons Learned section) but is perfectly acceptable to use here.</p>
<p>This section is based on a document by a Novell BorderManager guru named Shawn Pond and is used with his permission. It is simple, logical and easy to implement. His original document can be found at <a href="http:&#47;&#47;www.novell.com&#47;coolsolutions&#47;feature&#47;7949.html">www.novell.com&#47;coolsolutions&#47;feature&#47;7949.html<&#47;a>.</p>
<p>First, the PAC file code:</p>
<pre class="brush:js">&#47;&#47; Find the 4th octet<br />
var myip=myIpAddress()<br />
var ipbits=myip.split(".")<br />
var myseg=parseInt(ipbits[3])</p>
<p>&#47;&#47; Check to see if the 4th octect is even or odd<br />
if (myseg==Math.floor(myseg&#47;2)*2) {<br />
&#47;&#47; Even<br />
proxy = "PROXY p1.company.com:8080; PROXY p2.company.com:8080";<br />
}<br />
else {<br />
&#47;&#47; Odd<br />
proxy = "PROXY p2.company.com:8080; PROXY p1.company.com:8080";<br />
}<&#47;pre><br />
In this code, the first thign we do is to find the users IP address into a variable called "myip". We then split the address into an array called "ipbits", separating by the period character. We find convert the 4th octect (ipbits[3]) and convert it to a numeric value which is stored in the variable "myseg":</p>
<pre class="brush:js">var myip=myIpAddress()<br />
var ipbits=myip.split(".")<br />
var myseg=parseInt(ipbits[3])<&#47;pre><br />
To check of even&#47;odd we divide it by the last octect by two, discarding any remainder, then multiply that result by two. If the result is the same as the original 4th octet then it is even. If the number is different then the last octect is odd. If it's even, we set the variable called "proxy" to be the proper proxies to use - P1 first, then P2 as a failover. If it's odd, we set the "proxy" variable to the proper value for odd-number users - P2 as first and P1 as failover.</p>
<pre class="brush:js">&#47;&#47; Check to see if the 4th octect is even or odd<br />
if (myseg==Math.floor(myseg&#47;2)*2) {<br />
&#47;&#47; Even<br />
proxy = "PROXY p1.company.com:8080; PROXY p2.company.com:8080";<br />
}<br />
else {<br />
&#47;&#47; Odd<br />
proxy = "PROXY p2.company.com:8080; PROXY p1.company.com:8080";}<&#47;pre><br />
Add the rest of your PAC file code. When you have reached a point in your PAC file that you need to return a proxy value, you just use "return proxy;" to send back the proper proxy value for the user.</p>
<p><strong>Original link<&#47;strong></p>
<p><a href="http:&#47;&#47;www.proxypacfiles.com&#47;proxypac&#47;index.php?option=com_content&amp;view=article&amp;id=54&amp;Itemid=83" target="_blank">http:&#47;&#47;www.proxypacfiles.com&#47;proxypac&#47;index.php?option=com_content&amp;view=article&amp;id=54&amp;Itemid=83<&#47;a></p>
