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
<p>Previously I have <a href="http:&#47;&#47;webdebug.net&#47;2013&#47;08&#47;validation-of-viewstate-mac-failed&#47;" target="_blank">posted on the validation of viewstate MAC failure<&#47;a>. We already know that the validationKey and validation algorithm need to be the same across all the servers in a load-balanced environment. But user still see viewState validation failures in event logs.<&#47;p>
<p>&nbsp;<&#47;p><br />
<h1>ViewStateUserKey<&#47;h1>
<p>There is another factor that could be playing in the middle. That is the <strong>ViewStateUserKey<&#47;strong>. Microsoft&reg; ASP.NET version 1.1 added an additional <code>Page<&#47;code> class property&mdash;<code>ViewStateUserKey<&#47;code>. This property, if used, must be assigned a string value in the initialization stage of the page life cycle (in the <code>Page_Init<&#47;code> event handler). The point of the property is to assign some user-specific key to the view state, such as a username. The <code>ViewStateUserKey<&#47;code>, if provided, is used as <a href="http:&#47;&#47;www.dotnetjunkies.com&#47;Tutorial&#47;77D4AFDC-585D-4539-A364-30028327FF14.dcik">a salt to the hash<&#47;a> during the MAC.<&#47;p>
<p>What the <code>ViewStateUserKey<&#47;code> property protects against is the case where a nefarious user visits a page, gathers the view state, and then entices a user to visit the same page, passing in their view state. <&#47;p>
<p><img title="ms972976.viewstate_fig10(en-us,MSDN.10).gif" alt="ms972976.viewstate_fig10(en-us,MSDN.10).gif" src="http:&#47;&#47;i.msdn.microsoft.com&#47;dynimg&#47;IC161589.gif"><&#47;p>
<p>&nbsp;<&#47;p><br />
<h1>ASP.NET Implementation<&#47;h1>
<p>If we reflect the System.Web.dll and look into the implementation, we will see the method below is taking ViewStateUserKey as a hash modifier which combines with validationKey to compute the hash for the viewstate.<&#47;p>
<pre class="brush:csharp">&#47;&#47; System.Web.UI.ObjectStateFormatter<br />
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
<p>&#47;&#47; System.Web.Configuration.MachineKeySection<br />
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
<&#47;pre></p>
<h1>Resolution<&#47;h1></p>
<p>Usually we would set the ViewStateUserKey are set to sessionID during the page_init stage, that works well in a single server, however in a load-balanced server environment, we need to make sure the sessionID for one user is consistent across all the servers,<&#47;p></p>
<ul>
<li>Make sure the servers are using the same state server
<li>Make sure not to cache the pages with cookies
<li>Make sure session expiration faster than the authentications<&#47;li><&#47;ul>
<p>Also we can use choose to use user name instead of sessionID when authenticated as the user is always consistent across all the servers.<&#47;p>
<pre class="brush:csharp">void Page_Init (Object sender, EventArgs e)<br />
{<br />
   if (User.Identity.IsAuthenticated)<br />
      ViewStateUserKey = User.Identity.Name;<br />
}<br />
<&#47;pre></p>
<p>&nbsp;<&#47;p></p>
<h1>Reference<&#47;h1></p>
<p><strong>Understanding ASP.NET View State<&#47;strong><&#47;p></p>
<p><a title="http:&#47;&#47;msdn.microsoft.com&#47;library&#47;ms972976.aspx" href="http:&#47;&#47;msdn.microsoft.com&#47;library&#47;ms972976.aspx" target="_blank">http:&#47;&#47;msdn.microsoft.com&#47;library&#47;ms972976.aspx<&#47;a><&#47;p></p>
<p><strong>Take Advantage of ASP.NET Built-in Features to Fend Off Web Attacks<&#47;strong><&#47;p></p>
<p><a title="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ms972969.aspx" href="http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ms972969.aspx" target="_blank">http:&#47;&#47;msdn.microsoft.com&#47;en-us&#47;library&#47;ms972969.aspx<&#47;a><&#47;p></p>
<p><strong>ViewStateUserKey makes ViewState more tamper-resistant<&#47;strong><&#47;p></p>
<p><a title="http:&#47;&#47;www.hanselman.com&#47;blog&#47;ViewStateUserKeyMakesViewStateMoreTamperresistant.aspx" href="http:&#47;&#47;www.hanselman.com&#47;blog&#47;ViewStateUserKeyMakesViewStateMoreTamperresistant.aspx" target="_blank">http:&#47;&#47;www.hanselman.com&#47;blog&#47;ViewStateUserKeyMakesViewStateMoreTamperresistant.aspx<&#47;a><&#47;p></p>
<p><strong>Cross-site request forgery<&#47;strong><&#47;p></p>
<p><a title="http:&#47;&#47;en.wikipedia.org&#47;wiki&#47;Cross-site_request_forgery" href="http:&#47;&#47;en.wikipedia.org&#47;wiki&#47;Cross-site_request_forgery" target="_blank">http:&#47;&#47;en.wikipedia.org&#47;wiki&#47;Cross-site_request_forgery<&#47;a><&#47;p></p>
