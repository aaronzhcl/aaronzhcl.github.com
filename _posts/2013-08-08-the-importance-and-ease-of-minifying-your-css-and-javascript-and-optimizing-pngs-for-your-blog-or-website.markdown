---
layout: post
status: publish
published: true
title: Minifying your CSS and JavaScript for your Website
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 319
wordpress_url: http://www.webdebug.net:80/?p=319
date: '2013-08-08 06:29:04 +0800'
date_gmt: '2013-08-08 06:29:04 +0800'
categories:
- Performance
tags:
- javascript
- css
- performance
- combine
- images
- yslow
comments:
- id: 808
  author: Sally
  author_email: donjuansjiz@gmail.com
  author_url: ''
  date: '2013-08-12 06:35:27 +0800'
  date_gmt: '2013-08-12 06:35:27 +0800'
  content: I prefer UglifyJS for minifying my JS files have had the best luck with
    it, and it not being to overly aggressive. I found an online tool that uses UglifyJS2
    and has become my lazy way of quickly minifying my JavaScript or combining all
    my files into one.
- id: 811
  author: aaronzh
  author_email: webdebug.net@gmail.com
  author_url: ''
  date: '2013-08-12 09:52:04 +0800'
  date_gmt: '2013-08-12 09:52:04 +0800'
  content: Nice tool Sally, it get really competive compression rate and time to other
    tools.
---
<p>It's important (and useful!) to send as few bytes of CSS and JS and HTML markup down the wire as possible. It's not <strong>just </strong>about size, though, it's also about the <strong>number of requests to get the bits</strong>. In fact, that's often more of a problem then file size.</p>
<h3>First, go run <a href="http://developer.yahoo.com/yslow/">YSlow</a> on your site.</h3><br />
YSlow such a wonderful tool and it will totally ruin your day and make you feel horrible about yourself and your site. ;) But you can work through that. Eek. First, my images are huge. I've also <strong>got 184k of JS, 21k of CSS and 30k of markup. </strong>Note my favicon is small. It was&nbsp; LOT bigger before and <a href="http://www.hanselman.com/blog/FavIconicoCanBeABandwidthHog.aspx">even sucked up gigabytes of bandwidth a few years back</a>. YSlow also tells me that I am making folks make too many HTTP requests:</p>
<blockquote><p><em>This page has 33 external JavaScript scripts. Try combining them into one. This page has 5 external stylesheets. Try combining them into one.</em></blockquote><br />
Seems that speeding things up is not just about making things smaller, but also asking for fewer things and getting more for the asking. I want to make fewer request that may have larger payloads, but then those payloads will be minified and then compressed with GZip.</p>
<h3>Optimize, Minify, Squish and GZip your CSS and JavaScript</h3><br />
CSS can look like this:</p>
<p>[css]<br />
body {<br />
    line-height: 1;<br />
}<br />
ol, ul {<br />
    list-style: none;<br />
}<br />
blockquote, q {<br />
    quotes: none;<br />
}<br />
[/css]</p>
<p>Or like this, and it still works.</p>
<p>[css]<br />
body{line-height:1}ol,ul{list-style:none}blockquote,q{quotes:none}<br />
[/css]</p>
<p>There's lots of ways to "minify" CSS and JavaScript, and fortunately you don't need to care! <strong>Think about CSS/JS minifying kind of like the Great Zip File Wars of the early nineties. There's a lot of different choices, they are all within a few percentage points of each other, and everyone thinks theirs is the best one ever.</strong> There are JavaScript specific compressors. You run your code through these before you put your site live.</p>
<ul>
<li><a href="http://dean.edwards.name/packer/">Packer</a></li>
<li><a href="http://crockford.com/javascript/jsmin">JSMin</a></li>
<li><a href="http://code.google.com/intl/pl/closure/compiler/">Closure compiler</a></li>
<li><a href="http://developer.yahoo.com/yui/compressor/">YUICompressor</a> (also does CSS)</li>
<li><a href="http://ajaxmin.codeplex.com/">AjaxMin</a> (also does CSS)</li><br />
</ul><br />
And there are CSS compressors:</p>
<ul>
<li><a href="http://csstidy.sourceforge.net/">CSSTidy</a></li>
<li><a href="http://code.google.com/p/minify/">Minify</a></li>
<li><a href="http://developer.yahoo.com/yui/compressor/">YUICompressor</a> (also does JS)</li>
<li><a href="http://ajaxmin.codeplex.com/">AjaxMin</a> (also does JS)</li>
<li><a href="http://www.csscompressor.com/">CSSCompressor</a></li><br />
</ul><br />
And some of these integrate nicely into your development workflow. You can put them in your build files, or minify things on the fly.</p>
<ul>
<li><a title="http://yuicompressor.codeplex.com/" href="http://yuicompressor.codeplex.com/">YUICompressor</a> - .NET Port that can compress on the fly or at build time. Also <a href="http://nuget.org/List/Packages/YUICompressor.NET">on NuGet</a>.</li>
<li><a href="http://ajaxmin.codeplex.com/">AjaxMin</a>&nbsp; - Has MSBuild tasks and can be integrated into your project's build.</li>
<li><a href="http://www.codethinked.com/squishit-the-friendly-aspnet-javascript-and-css-squisher">SquishIt</a> - Used at runtime in your ASP.NET applications' views and does magic at runtime.</li>
<li><strong>UPDATE:</strong> <a href="http://chirpy.codeplex.com/">Chirpy</a> - "Mashes, minifies, and validates your javascript, stylesheet, and dotless files."</li>
<li><strong>UPDATE:</strong> <a href="http://combres.codeplex.com/">Combres</a> - ".NET library which enables minification, compression, combination, and caching of JavaScript and CSS resources for ASP.NET and ASP.NET MVC web applications."</li>
<li><strong>UPDATE: </strong><a href="https://github.com/andrewdavey/cassette/">Cassette by Andrew Davey</a> - Does it all, compiles CoffeeScript, script combining, <a href="https://github.com/andrewdavey/cassette/wiki/Getting-Started">smart about debug- and release-time</a>.</li><br />
</ul><br />
There's <a href="http://www.phpied.com/css-minifiers-comparison/">plenty of comparisons out there</a> looking at the different choices. Ultimately when compression percentages don't matter much, you should focus on two things:</p>
<ul>
<li>compatibility - does it break your CSS? It should never do this</li>
<li>workflow - does it fit into your life and how you work?</li><br />
</ul><br />
For me, I have a template language in my blog and I need to compress my CSS and JS when I deploy my new template. A batch file and command line utility works nicely so I used <a href="http://ajaxmin.codeplex.com/">AjaxMin</a> (yes, it's made by Microsoft, but it did exactly what I needed.) I created a simple batch file that took the pile of JS from the top of my blog and the pile from the bottom and created a .header.js and a .footer.js. I also squished all the CSS, including my plugins that needed CSS, and put them in one file while being sure to maintain file order. I've split these lines up for readability only.</p>
<p>[code]<br />
set PATH=%~dp0;"C:\Program Files (x86)\Microsoft\Microsoft Ajax Minifier\"</p>
<p>ajaxmin -clobber<br />
    scripts\openid.css<br />
    scripts\syntaxhighlighter_3.0.83\styles\shCore.css<br />
    scripts\syntaxhighlighter_3.0.83\styles\shThemeDefault.css<br />
    scripts\fancybox\jquery.fancybox-1.3.4.css<br />
    themes\Hanselman\css\screenv5.css<br />
    -o css\hanselman.v5.min.css</p>
<p>ajaxmin -clobber<br />
    themes/Hanselman/scripts/activatePlaceholders.js<br />
    themes/Hanselman/scripts/convertListToSelect.js<br />
    scripts/fancybox/jquery.fancybox-1.3.4.pack.js<br />
    -o scripts\hanselman.header.v4.min.js</p>
<p>ajaxmin -clobber<br />
    scripts/omni_external_blogs_v2.js<br />
    scripts/syntaxhighlighter_3.0.83/scripts/shCore.js<br />
    scripts/syntaxhighlighter_3.0.83/scripts/shLegacy.js<br />
    scripts/syntaxhighlighter_3.0.83/scripts/shBrushCSharp.js<br />
    scripts/syntaxhighlighter_3.0.83/scripts/shBrushPowershell.js<br />
    scripts/syntaxhighlighter_3.0.83/scripts/shBrushXml.js<br />
    scripts/syntaxhighlighter_3.0.83/scripts/shBrushCpp.js<br />
    scripts/syntaxhighlighter_3.0.83/scripts/shBrushJScript.js<br />
    scripts/syntaxhighlighter_3.0.83/scripts/shBrushCss.js<br />
    scripts/syntaxhighlighter_3.0.83/scripts/shBrushRuby.js<br />
    scripts/syntaxhighlighter_3.0.83/scripts/shBrushVb.js<br />
    scripts/syntaxhighlighter_3.0.83/scripts/shBrushPython.js<br />
    scripts/twitterbloggerv2.js scripts/ga_social_tracker.js<br />
    -o scripts\hanselman.footer.v4.min.js</p>
<p>pause<br />
[/code]</p>
<p>All those ones at the bottom support my code highlighter. This looks complex ,but it's just making three files, two JS and a CSS out of all my mess of required JS files. This squished all my CSS down to 26k, and here's the output:</p>
<blockquote><p><strong>CSS </strong>Original Size: 35667 bytes; reduced size: 26537 bytes (25.6% minification) Gzip of output approximately 5823 bytes (78.1% compression) <strong>JS </strong>Original Size: 83505 bytes; reduced size: 64515 bytes (22.7% minification) Gzip of output approximately 34415 bytes (46.7% compression)</blockquote><br />
That also turned 22 HTTP requests into 3.</p>
<h3>Optimize your Images (particularly PNGs)</h3><br />
Looks like my 1600k cold (machine not cached) home page is mostly images, about 1300k. That's because I put a lot of articles on the home page but I also use PNGs for images most of my blog posts. I could be more thoughtful and:</p>
<ul>
<li>Use JPEGs for photos of people, things that are visually "busy"</li>
<li>Use PNGs for charts, screenshots, things that must be "crystal clear"</li><br />
</ul><br />
I can also <a href="http://www.hanselman.com/blog/AddingPNGOUTToTheExplorerRightClickContextMenu.aspx">optimize the size of my PNGs (did you know you can do that!) before I upload them with PNGOUT</a>. For bloggers and for ease I recommend <a href="http://pnggauntlet.com/">PNGGauntlet, which is a Windows app that calls PNGOut for you</a>.&nbsp; Easier than <a href="http://www.hanselman.com/blog/AddingPNGOUTToTheExplorerRightClickContextMenu.aspx">PowerShell, although I do that also</a>. If you use Visual Studio 2010, you can use <a href="http://madskristensen.net/post/Image-Optimizer-%28beta%29-VS2010-extension.aspx">Mad's Beta Image Optimizer Extension</a> that will let you optimize images directly from Visual Studio. To show you how useful this is, I downloaded the images from the last month or so of posts on this blog totaling 7.29MB and then ran them through PNGOut via PNGGauntlet. <a href="http://www.hanselman.com/blog/content/binary/Windows-Live-Writer/d266a7394287_9A85/PNGGauntlet%20%28131%29_2.png"><img title="All my PNGs getting in line to be optimzed inside of PNGGauntlet" alt="All my PNGs getting in line to be optimzed inside of PNGGauntlet" src="http://www.hanselman.com/blog/content/binary/Windows-Live-Writer/d266a7394287_9A85/PNGGauntlet%20%28131%29_thumb.png" width="691" height="525" border="0" /></a> Then I took a few of the PNGs that were too large and saved them as JPGs. All in all, I saved 1359k (that's almost a meg and a half or almost 20%) for minimal extra work. If you think this kind of optimization is a bad idea, or boring or a waste of time, think about the multipliers. You're saving (or I am) a meg and a half of image downloads, <strong>thousands of times</strong>. When you're dead and gone your blog will still be saving bytes for your readers! ;) This is important not just because saving bandwidth is nice, but because <strong>perception of speed is important</strong>. Give the browser less work to do, especially if, like me, almost 10% of your users are mobile. Don't make these little phones work harder than they need to and remember that not everyone has an unlimited data plan.</p>
<h3>Let your browser cache everything, forever</h3><br />
<a href="http://madskristensen.net/post/Add-expires-header-for-images.aspx">Mads reminded me about this great tip for IIS7</a> that tells the webserver to set the "Expires" header to a far future date, effectively telling the browser to cache things forever. What's nice about this is that if you or your host is using IIS7, you can change this setting yourself from web.config and don't need to touch IIS settings.</p>
<div>
<div id="highlighter_207302">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td>
<div>1</div></p>
<div>2</div></p>
<div>3</div></td></p>
<td>
<div>
<div><code><</code><code>staticContent</code><code>></code></div></p>
<div><code>&nbsp;</code><code><</code><code>clientCache</code> <code>httpExpires</code><code>=</code><code>"Sun, 29 Mar 2020 00:00:00 GMT"</code> <code>cacheControlMode</code><code>=</code><code>"UseExpires"</code> <code>/></code></div></p>
<div><code></</code><code>staticContent</code><code>></code></div><br />
</div></td><br />
</tr><br />
</tbody><br />
</table><br />
</div><br />
</div><br />
You might think this is insane. This is, in fact, insane. Insane like a fox. I built the website so I want control. I version my CSS and JS files in the filename. Others use QueryStrings with versions and some use hashes. The point is are YOU in control or are you just letting caching happen? Even if you don't use this tip, know <strong>how and why </strong>things are cached and how you can control it.</p>
<h3>Compress everything</h3><br />
Make sure everything is GZip'ed as it goes out of your Web Server. This is also easy with IIS7 and allowed me to get rid of some old 3rd party libraries. All these settings are in system.webServer.</p>
<div>
<div id="highlighter_853072">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td>
<div>1</div></td></p>
<td>
<div>
<div><code><</code><code>urlCompression</code> <code>doDynamicCompression</code><code>=</code><code>"true"</code> <code>doStaticCompression</code><code>=</code><code>"true"</code> <code>dynamicCompressionBeforeCache</code><code>=</code><code>"true"</code><code>/></code></div><br />
</div></td><br />
</tr><br />
</tbody><br />
</table><br />
</div><br />
</div><br />
If there is one thing you can do to your website, it's turning on HTTP compression. For average pages, like my 100k of HTML, it can turn into 20k. It downloads faster and the perception of speed by the user from "click to render" will increase. Certainly this post just scratches the surface of REAL performance optimization and only goes up to the point where the bits hit the browser. You can go nuts trying to get an "A" grade in YSlow, optimizing for # of DOM objects, DNS Lookups, JavaScript ordering, and on and on. That said, you can get 80% of the benefit for 5% of the effort by these tips. It'll take you no time and you'll reap the benefits hourly:</p>
<ul>
<li>Minifying your JS and CSS</li>
<li>Combining CSS and JS into single files to minimize HTTP requests</li>
<li>Turning on Gzip Compression for as much as you can</li>
<li>Set Expires Headers on everything you can</li>
<li>Compress your PNGs and JPEGs (but definitely your PNGs)</li>
<li><a href="http://www.hanselman.com/blog/NuGetPackageOfTheWeek1ASPNETSpriteAndImageOptimization.aspx">Use CSS Sprites if you have lots of tiny images</a></li><br />
</ul><br />
I still have a "D" on YSlow, but a D is a passing grade. ;) Enjoy, and leave your tips, and your "duh!" in the comments, Dear Reader. Also, read anything by <a href="http://stevesouders.com/">Steve Souders</a>. He wrote YSlow.</p>
<p><a href="http://www.hanselman.com/blog/TheImportanceAndEaseOfMinifyingYourCSSAndJavaScriptAndOptimizingPNGsForYourBlogOrWebsite.aspx" target="_blank">http://www.hanselman.com/blog/TheImportanceAndEaseOfMinifyingYourCSSAndJavaScriptAndOptimizingPNGsForYourBlogOrWebsite.aspx</a> </p>
