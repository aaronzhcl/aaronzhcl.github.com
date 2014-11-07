---
layout: post
status: publish
published: true
title: WinInet connection limit
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 168
wordpress_url: http://www.webdebug.net:80/?p=168
date: '2013-01-04 15:02:55 +0800'
date_gmt: '2013-01-04 15:02:55 +0800'
categories:
- browser
- Troubleshooting
tags:
- browser
- WinINET
- connection limit
comments: []
---
<p><a href="http://support.microsoft.com/kb/183110" target="_blank"><strong>WinInet limits connections per server</strong></a></p>
<p>WinInet limits connections to a single HTTP 1.0 server to four simultaneous connections. Connections to a single HTTP 1.1 server are limited to two simultaneous connections. <a href="http://www.w3.org/Protocols/rfc2616/rfc2616.html" target="_blank">The HTTP 1.1 specification (RFC2616)</a> mandates the two-connection limit. The four-connection limit for HTTP 1.0 is a self-imposed restriction that coincides with the standard that is used by a number of popular Web browsers.</p>
<p>The only evidence of this limitation to your application is that calls such as HttpSendRequest and InternetOpenURL appear to take longer to complete because they wait for previous connections to be freed up before their requests are sent.</p>
<p>You can configure WinInet to exceed this limit by creating and setting the following registry entries:</p>
<p>Note By changing these settings, you cause WinInet to go against the HTTP protocol specification recommendation. You should only do this if absolutely necessary and then you should avoid doing standard Web browsing while these settings are in effect:</p>
<p><code>HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings</code><br />
MaxConnectionsPerServer REG_DWORD<br />
(Default 2)<br />
Sets the number of simultaneous requests to a single HTTP 1.1 Server, this value can be set from 2 to 128.</p>
<p>MaxConnectionsPer1_0Server REG_DWORD<br />
(Default 4)<br />
Sets the number of simultaneous requests to a single HTTP 1.0 Server</p>
<p>These settings are made for a particular user and will have no affect on other users who log on to the computer.</p>
<p>Below is a sample code to simulate the scenario, open up 10 connections using wininet.</p>
<p>[cpp]<br />
#include <windows.h><br />
#include <wininet.h><br />
#include
<process.h>
#include <stdio.h></p>
<p>const int kBufferLength = 2048;<br />
const int kThreadNumber = 10;<br />
const int kSleepInterval = 10;</p>
<p>#pragma comment(lib, "wininet.lib")</p>
<p>unsigned __stdcall ThreadFunc( void* pArguments ){<br />
	TCHAR response_buffer[kBufferLength];<br />
	HINTERNET session, connection, file;<br />
	SYSTEMTIME local_time;<br />
	DWORD thread_id = GetCurrentThreadId();</p>
<p>	/*GetLocalTime(&amp;local_time);<br />
	printf("%02d:%02d.%03d\tThread %d opening connection...\n",<br />
		local_time.wMinute,<br />
		local_time.wSecond,<br />
		local_time.wMilliseconds,<br />
		thread_id);*/</p>
<p>	session = InternetOpen(TEXT("WinInet demo"), 0, NULL, NULL, 0);<br />
	connection = InternetConnect(<br />
		session, TEXT("msdn.microsoft.com"),<br />
		INTERNET_DEFAULT_HTTP_PORT, NULL,<br />
		NULL, INTERNET_SERVICE_HTTP,<br />
		0, 0);<br />
	file = HttpOpenRequest(<br />
		connection, NULL,<br />
		TEXT("/en-us/library/aa384247(v=vs.85).aspx"), NULL,<br />
		NULL, NULL,<br />
		0, 0);</p>
<p>	GetLocalTime(&amp;local_time);<br />
	printf("%02d:%02d.%03d\tThread %d starting request...\n",<br />
		local_time.wMinute,<br />
		local_time.wSecond,<br />
		local_time.wMilliseconds,<br />
		thread_id);</p>
<p>	DWORD num_bytes;<br />
	//memset(response_buffer, '&#92;&#48;', sizeof(response_buffer));<br />
	if(HttpSendRequest(file, NULL, 0, NULL, 0)){<br />
		while(InternetReadFile(<br />
			file, &amp;response_buffer,_countof(response_buffer), &amp;num_bytes)){<br />
				if(num_bytes == 0)<br />
					break;<br />
				//printf("%s",response_buffer);<br />
				//memset(response_buffer, '&#92;&#48;', sizeof(response_buffer));<br />
		}<br />
	}<br />
	GetLocalTime(&amp;local_time);<br />
	printf("%02d:%02d.%03d\tThread %d ending request...\n",<br />
		local_time.wMinute,<br />
		local_time.wSecond,<br />
		local_time.wMilliseconds,<br />
		thread_id);</p>
<p>	InternetCloseHandle(file);<br />
	InternetCloseHandle(connection);<br />
	InternetCloseHandle(session);<br />
	return 0;<br />
} </p>
<p>int main(){<br />
	HANDLE threads[kThreadNumber];<br />
	unsigned thread_id;</p>
<p>	printf( "Creating threads...\n" );<br />
	for(int i = 0; i < kThreadNumber; i++){<br />
		threads[i] = (HANDLE)_beginthreadex(<br />
			NULL, 0, &amp;ThreadFunc, NULL, 0, &amp;thread_id );<br />
		//printf("Thread %d is created...\n",thread_id);<br />
		Sleep(kSleepInterval);<br />
	}</p>
<p>	WaitForMultipleObjects(kThreadNumber, threads, true, INFINITE);<br />
	printf("Downloading finished...\n");</p>
<p>	for(int i = 0; i< kThreadNumber; i++)<br />
		CloseHandle( threads[i] );<br />
}</p>
<p>[/cpp]</p>
<p>If you want to set the connection by InternetSetOption API, it may not working for you on IE 8.</p>
<p><a href="http://social.microsoft.com/Forums/en/Offtopic/thread/e744dec8-7854-482a-bc71-13fca32d24d2" target="_blank">Bug in WinInet+IE8: ignores max connections setting</a></p>
