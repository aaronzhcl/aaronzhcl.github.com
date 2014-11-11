---
layout: post
status: publish
published: true
title: ViewStateUserKey and ViewStateMac validation failure
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 589
wordpress_url: http://webdebug.net/?p=589
date: '2014-07-17 02:56:23 +0800'
date_gmt: '2014-07-17 02:56:23 +0800'
categories:
- ASP.NET
tags:
- viewstate
- validationKey
- ViewStateMAC
- ViewStateUserKey
comments: []
---
<p>Previously I have <a href="http://webdebug.net/2013/08/validation-of-viewstate-mac-failed/" target="_blank">posted on the validation of viewstate MAC failure</a>. We already know that the validationKey and validation algorithm need to be the same across all the servers in a load-balanced environment. But user still see viewState validation failures in event logs.</p>
<!--more-->
<h1>ViewStateUserKey</h1>
<p>There is another factor that could be playing in the middle. That is the <strong>ViewStateUserKey</strong>. Microsoft&reg; ASP.NET version 1.1 added an additional <code>Page</code> class property&mdash;<code>ViewStateUserKey</code>. This property, if used, must be assigned a string value in the initialization stage of the page life cycle (in the <code>Page_Init</code> event handler). The point of the property is to assign some user-specific key to the view state, such as a username. The <code>ViewStateUserKey</code>, if provided, is used as <a href="http://www.dotnetjunkies.com/Tutorial/77D4AFDC-585D-4539-A364-30028327FF14.dcik">a salt to the hash</a> during the MAC.</p>
<p>What the <code>ViewStateUserKey</code> property protects against is the case where a nefarious user visits a page, gathers the view state, and then entices a user to visit the same page, passing in their view state. </p>
<p><img title="ms972976.viewstate_fig10(en-us,MSDN.10).gif" alt="ms972976.viewstate_fig10(en-us,MSDN.10).gif" src="http://i.msdn.microsoft.com/dynimg/IC161589.gif"></p>
<p>&nbsp;</p><br />
<h1>ASP.NET Implementation</h1>
<p>If we reflect the System.Web.dll and look into the implementation, we will see the method below is taking ViewStateUserKey as a hash modifier which combines with validationKey to compute the hash for the viewstate.</p>
<pre class="brush:csharp">// System.Web.UI.ObjectStateFormatter<br />
private byte[] GetMacKeyModifier()<br />
{<br />
    if (this._macKeyBytes == null)<br />
    {<br />
        if (this._page == null)<br />
        {<br />
            return null;<br />
        }<br />
        uint clientStateIdentifier = this._page.GetClientStateIdentifier();<br />
        string viewStateUserKey = this._page.ViewStateUserKey;<br />
        if (viewStateUserKey != null)<br />
        {<br />
            int byteCount = Encoding.Unicode.GetByteCount(viewStateUserKey);<br />
            this._macKeyBytes = new byte[byteCount + 4];<br />
            Encoding.Unicode.GetBytes(viewStateUserKey, 0, viewStateUserKey.Length, this._macKeyBytes, 4);<br />
        }<br />
        else<br />
        {<br />
            this._macKeyBytes = new byte[4];<br />
        }<br />
        this._macKeyBytes[0] = (byte)clientStateIdentifier;<br />
        this._macKeyBytes[1] = (byte)(clientStateIdentifier >> 8);<br />
        this._macKeyBytes[2] = (byte)(clientStateIdentifier >> 16);<br />
        this._macKeyBytes[3] = (byte)(clientStateIdentifier >> 24);<br />
    }<br />
    return this._macKeyBytes;<br />
}</p>
<p>// System.Web.Configuration.MachineKeySection<br />
private static byte[] HashDataUsingNonKeyedAlgorithm(HashAlgorithm hashAlgo, byte[] buf, byte[] modifier, int start, int length, byte[] validationKey)<br />
{<br />
    int num = length + validationKey.Length + ((modifier != null) ? modifier.Length : 0);<br />
    byte[] array = new byte[num];<br />
    Buffer.BlockCopy(buf, start, array, 0, length);<br />
    if (modifier != null)<br />
    {<br />
        Buffer.BlockCopy(modifier, 0, array, length, modifier.Length);<br />
    }<br />
    Buffer.BlockCopy(validationKey, 0, array, length, validationKey.Length);<br />
    if (hashAlgo != null)<br />
    {<br />
        return hashAlgo.ComputeHash(array);<br />
    }<br />
    byte[] array2 = new byte[16];<br />
    int sHA1Hash = UnsafeNativeMethods.GetSHA1Hash(array, array.Length, array2, array2.Length);<br />
    Marshal.ThrowExceptionForHR(sHA1Hash);<br />
    return array2;<br />
}<br />
</pre></p>
<h1>Resolution</h1></p>
<p>Usually we would set the ViewStateUserKey are set to sessionID during the page_init stage, that works well in a single server, however in a load-balanced server environment, we need to make sure the sessionID for one user is consistent across all the servers,</p></p>
<ul>
<li>Make sure the servers are using the same state server
<li>Make sure not to cache the pages with cookies
<li>Make sure session expiration faster than the authentications</li></ul>
<p>Also we can use choose to use user name instead of sessionID when authenticated as the user is always consistent across all the servers.</p>
<pre class="brush:csharp">void Page_Init (Object sender, EventArgs e)<br />
{<br />
   if (User.Identity.IsAuthenticated)<br />
      ViewStateUserKey = User.Identity.Name;<br />
}<br />
</pre></p>
<p>&nbsp;</p></p>
<h1>Reference</h1></p>
<p><strong>Understanding ASP.NET View State</strong></p></p>
<p><a title="http://msdn.microsoft.com/library/ms972976.aspx" href="http://msdn.microsoft.com/library/ms972976.aspx" target="_blank">http://msdn.microsoft.com/library/ms972976.aspx</a></p></p>
<p><strong>Take Advantage of ASP.NET Built-in Features to Fend Off Web Attacks</strong></p></p>
<p><a title="http://msdn.microsoft.com/en-us/library/ms972969.aspx" href="http://msdn.microsoft.com/en-us/library/ms972969.aspx" target="_blank">http://msdn.microsoft.com/en-us/library/ms972969.aspx</a></p></p>
<p><strong>ViewStateUserKey makes ViewState more tamper-resistant</strong></p></p>
<p><a title="http://www.hanselman.com/blog/ViewStateUserKeyMakesViewStateMoreTamperresistant.aspx" href="http://www.hanselman.com/blog/ViewStateUserKeyMakesViewStateMoreTamperresistant.aspx" target="_blank">http://www.hanselman.com/blog/ViewStateUserKeyMakesViewStateMoreTamperresistant.aspx</a></p></p>
<p><strong>Cross-site request forgery</strong></p></p>
<p><a title="http://en.wikipedia.org/wiki/Cross-site_request_forgery" href="http://en.wikipedia.org/wiki/Cross-site_request_forgery" target="_blank">http://en.wikipedia.org/wiki/Cross-site_request_forgery</a></p></p>
