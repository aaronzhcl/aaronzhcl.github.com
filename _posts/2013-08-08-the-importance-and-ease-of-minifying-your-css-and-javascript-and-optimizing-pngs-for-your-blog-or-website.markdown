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
<p>It's important (and useful!) to send as few bytes of CSS and JS and HTML markup down the wire as possible. It's not <strong>just <&#47;strong>about size, though, it's also about the <strong>number of requests to get the bits<&#47;strong>. In fact, that's often more of a problem then file size.</p>
<h3>First, go run <a href="http:&#47;&#47;developer.yahoo.com&#47;yslow&#47;">YSlow<&#47;a> on your site.<&#47;h3><br />
YSlow such a wonderful tool and it will totally ruin your day and make you feel horrible about yourself and your site. ;) But you can work through that. Eek. First, my images are huge. I've also <strong>got 184k of JS, 21k of CSS and 30k of markup. <&#47;strong>Note my favicon is small. It was&nbsp; LOT bigger before and <a href="http:&#47;&#47;www.hanselman.com&#47;blog&#47;FavIconicoCanBeABandwidthHog.aspx">even sucked up gigabytes of bandwidth a few years back<&#47;a>. YSlow also tells me that I am making folks make too many HTTP requests:</p>
<blockquote><p><em>This page has 33 external JavaScript scripts. Try combining them into one. This page has 5 external stylesheets. Try combining them into one.<&#47;em><&#47;blockquote><br />
Seems that speeding things up is not just about making things smaller, but also asking for fewer things and getting more for the asking. I want to make fewer request that may have larger payloads, but then those payloads will be minified and then compressed with GZip.</p>
<h3>Optimize, Minify, Squish and GZip your CSS and JavaScript<&#47;h3><br />
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
[&#47;css]</p>
<p>Or like this, and it still works.</p>
<p>[css]<br />
body{line-height:1}ol,ul{list-style:none}blockquote,q{quotes:none}<br />
[&#47;css]</p>
<p>There's lots of ways to "minify" CSS and JavaScript, and fortunately you don't need to care! <strong>Think about CSS&#47;JS minifying kind of like the Great Zip File Wars of the early nineties. There's a lot of different choices, they are all within a few percentage points of each other, and everyone thinks theirs is the best one ever.<&#47;strong> There are JavaScript specific compressors. You run your code through these before you put your site live.</p>
<ul>
<li><a href="http:&#47;&#47;dean.edwards.name&#47;packer&#47;">Packer<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;crockford.com&#47;javascript&#47;jsmin">JSMin<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;code.google.com&#47;intl&#47;pl&#47;closure&#47;compiler&#47;">Closure compiler<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;developer.yahoo.com&#47;yui&#47;compressor&#47;">YUICompressor<&#47;a> (also does CSS)<&#47;li>
<li><a href="http:&#47;&#47;ajaxmin.codeplex.com&#47;">AjaxMin<&#47;a> (also does CSS)<&#47;li><br />
<&#47;ul><br />
And there are CSS compressors:</p>
<ul>
<li><a href="http:&#47;&#47;csstidy.sourceforge.net&#47;">CSSTidy<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;code.google.com&#47;p&#47;minify&#47;">Minify<&#47;a><&#47;li>
<li><a href="http:&#47;&#47;developer.yahoo.com&#47;yui&#47;compressor&#47;">YUICompressor<&#47;a> (also does JS)<&#47;li>
<li><a href="http:&#47;&#47;ajaxmin.codeplex.com&#47;">AjaxMin<&#47;a> (also does JS)<&#47;li>
<li><a href="http:&#47;&#47;www.csscompressor.com&#47;">CSSCompressor<&#47;a><&#47;li><br />
<&#47;ul><br />
And some of these integrate nicely into your development workflow. You can put them in your build files, or minify things on the fly.</p>
<ul>
<li><a title="http:&#47;&#47;yuicompressor.codeplex.com&#47;" href="http:&#47;&#47;yuicompressor.codeplex.com&#47;">YUICompressor<&#47;a> - .NET Port that can compress on the fly or at build time. Also <a href="http:&#47;&#47;nuget.org&#47;List&#47;Packages&#47;YUICompressor.NET">on NuGet<&#47;a>.<&#47;li>
<li><a href="http:&#47;&#47;ajaxmin.codeplex.com&#47;">AjaxMin<&#47;a>&nbsp; - Has MSBuild tasks and can be integrated into your project's build.<&#47;li>
<li><a href="http:&#47;&#47;www.codethinked.com&#47;squishit-the-friendly-aspnet-javascript-and-css-squisher">SquishIt<&#47;a> - Used at runtime in your ASP.NET applications' views and does magic at runtime.<&#47;li>
<li><strong>UPDATE:<&#47;strong> <a href="http:&#47;&#47;chirpy.codeplex.com&#47;">Chirpy<&#47;a> - "Mashes, minifies, and validates your javascript, stylesheet, and dotless files."<&#47;li>
<li><strong>UPDATE:<&#47;strong> <a href="http:&#47;&#47;combres.codeplex.com&#47;">Combres<&#47;a> - ".NET library which enables minification, compression, combination, and caching of JavaScript and CSS resources for ASP.NET and ASP.NET MVC web applications."<&#47;li>
<li><strong>UPDATE: <&#47;strong><a href="https:&#47;&#47;github.com&#47;andrewdavey&#47;cassette&#47;">Cassette by Andrew Davey<&#47;a> - Does it all, compiles CoffeeScript, script combining, <a href="https:&#47;&#47;github.com&#47;andrewdavey&#47;cassette&#47;wiki&#47;Getting-Started">smart about debug- and release-time<&#47;a>.<&#47;li><br />
<&#47;ul><br />
There's <a href="http:&#47;&#47;www.phpied.com&#47;css-minifiers-comparison&#47;">plenty of comparisons out there<&#47;a> looking at the different choices. Ultimately when compression percentages don't matter much, you should focus on two things:</p>
<ul>
<li>compatibility - does it break your CSS? It should never do this<&#47;li>
<li>workflow - does it fit into your life and how you work?<&#47;li><br />
<&#47;ul><br />
For me, I have a template language in my blog and I need to compress my CSS and JS when I deploy my new template. A batch file and command line utility works nicely so I used <a href="http:&#47;&#47;ajaxmin.codeplex.com&#47;">AjaxMin<&#47;a> (yes, it's made by Microsoft, but it did exactly what I needed.) I created a simple batch file that took the pile of JS from the top of my blog and the pile from the bottom and created a .header.js and a .footer.js. I also squished all the CSS, including my plugins that needed CSS, and put them in one file while being sure to maintain file order. I've split these lines up for readability only.</p>
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
    themes&#47;Hanselman&#47;scripts&#47;activatePlaceholders.js<br />
    themes&#47;Hanselman&#47;scripts&#47;convertListToSelect.js<br />
    scripts&#47;fancybox&#47;jquery.fancybox-1.3.4.pack.js<br />
    -o scripts\hanselman.header.v4.min.js</p>
<p>ajaxmin -clobber<br />
    scripts&#47;omni_external_blogs_v2.js<br />
    scripts&#47;syntaxhighlighter_3.0.83&#47;scripts&#47;shCore.js<br />
    scripts&#47;syntaxhighlighter_3.0.83&#47;scripts&#47;shLegacy.js<br />
    scripts&#47;syntaxhighlighter_3.0.83&#47;scripts&#47;shBrushCSharp.js<br />
    scripts&#47;syntaxhighlighter_3.0.83&#47;scripts&#47;shBrushPowershell.js<br />
    scripts&#47;syntaxhighlighter_3.0.83&#47;scripts&#47;shBrushXml.js<br />
    scripts&#47;syntaxhighlighter_3.0.83&#47;scripts&#47;shBrushCpp.js<br />
    scripts&#47;syntaxhighlighter_3.0.83&#47;scripts&#47;shBrushJScript.js<br />
    scripts&#47;syntaxhighlighter_3.0.83&#47;scripts&#47;shBrushCss.js<br />
    scripts&#47;syntaxhighlighter_3.0.83&#47;scripts&#47;shBrushRuby.js<br />
    scripts&#47;syntaxhighlighter_3.0.83&#47;scripts&#47;shBrushVb.js<br />
    scripts&#47;syntaxhighlighter_3.0.83&#47;scripts&#47;shBrushPython.js<br />
    scripts&#47;twitterbloggerv2.js scripts&#47;ga_social_tracker.js<br />
    -o scripts\hanselman.footer.v4.min.js</p>
<p>pause<br />
[&#47;code]</p>
<p>All those ones at the bottom support my code highlighter. This looks complex ,but it's just making three files, two JS and a CSS out of all my mess of required JS files. This squished all my CSS down to 26k, and here's the output:</p>
<blockquote><p><strong>CSS <&#47;strong>Original Size: 35667 bytes; reduced size: 26537 bytes (25.6% minification) Gzip of output approximately 5823 bytes (78.1% compression) <strong>JS <&#47;strong>Original Size: 83505 bytes; reduced size: 64515 bytes (22.7% minification) Gzip of output approximately 34415 bytes (46.7% compression)<&#47;blockquote><br />
That also turned 22 HTTP requests into 3.</p>
<h3>Optimize your Images (particularly PNGs)<&#47;h3><br />
Looks like my 1600k cold (machine not cached) home page is mostly images, about 1300k. That's because I put a lot of articles on the home page but I also use PNGs for images most of my blog posts. I could be more thoughtful and:</p>
<ul>
<li>Use JPEGs for photos of people, things that are visually "busy"<&#47;li>
<li>Use PNGs for charts, screenshots, things that must be "crystal clear"<&#47;li><br />
<&#47;ul><br />
I can also <a href="http:&#47;&#47;www.hanselman.com&#47;blog&#47;AddingPNGOUTToTheExplorerRightClickContextMenu.aspx">optimize the size of my PNGs (did you know you can do that!) before I upload them with PNGOUT<&#47;a>. For bloggers and for ease I recommend <a href="http:&#47;&#47;pnggauntlet.com&#47;">PNGGauntlet, which is a Windows app that calls PNGOut for you<&#47;a>.&nbsp; Easier than <a href="http:&#47;&#47;www.hanselman.com&#47;blog&#47;AddingPNGOUTToTheExplorerRightClickContextMenu.aspx">PowerShell, although I do that also<&#47;a>. If you use Visual Studio 2010, you can use <a href="http:&#47;&#47;madskristensen.net&#47;post&#47;Image-Optimizer-%28beta%29-VS2010-extension.aspx">Mad's Beta Image Optimizer Extension<&#47;a> that will let you optimize images directly from Visual Studio. To show you how useful this is, I downloaded the images from the last month or so of posts on this blog totaling 7.29MB and then ran them through PNGOut via PNGGauntlet. <a href="http:&#47;&#47;www.hanselman.com&#47;blog&#47;content&#47;binary&#47;Windows-Live-Writer&#47;d266a7394287_9A85&#47;PNGGauntlet%20%28131%29_2.png"><img title="All my PNGs getting in line to be optimzed inside of PNGGauntlet" alt="All my PNGs getting in line to be optimzed inside of PNGGauntlet" src="http:&#47;&#47;www.hanselman.com&#47;blog&#47;content&#47;binary&#47;Windows-Live-Writer&#47;d266a7394287_9A85&#47;PNGGauntlet%20%28131%29_thumb.png" width="691" height="525" border="0" &#47;><&#47;a> Then I took a few of the PNGs that were too large and saved them as JPGs. All in all, I saved 1359k (that's almost a meg and a half or almost 20%) for minimal extra work. If you think this kind of optimization is a bad idea, or boring or a waste of time, think about the multipliers. You're saving (or I am) a meg and a half of image downloads, <strong>thousands of times<&#47;strong>. When you're dead and gone your blog will still be saving bytes for your readers! ;) This is important not just because saving bandwidth is nice, but because <strong>perception of speed is important<&#47;strong>. Give the browser less work to do, especially if, like me, almost 10% of your users are mobile. Don't make these little phones work harder than they need to and remember that not everyone has an unlimited data plan.</p>
<h3>Let your browser cache everything, forever<&#47;h3><br />
<a href="http:&#47;&#47;madskristensen.net&#47;post&#47;Add-expires-header-for-images.aspx">Mads reminded me about this great tip for IIS7<&#47;a> that tells the webserver to set the "Expires" header to a far future date, effectively telling the browser to cache things forever. What's nice about this is that if you or your host is using IIS7, you can change this setting yourself from web.config and don't need to touch IIS settings.</p>
<div>
<div id="highlighter_207302">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td>
<div>1<&#47;div></p>
<div>2<&#47;div></p>
<div>3<&#47;div><&#47;td></p>
<td>
<div>
<div><code><<&#47;code><code>staticContent<&#47;code><code>><&#47;code><&#47;div></p>
<div><code>&nbsp;<&#47;code><code><<&#47;code><code>clientCache<&#47;code> <code>httpExpires<&#47;code><code>=<&#47;code><code>"Sun, 29 Mar 2020 00:00:00 GMT"<&#47;code> <code>cacheControlMode<&#47;code><code>=<&#47;code><code>"UseExpires"<&#47;code> <code>&#47;><&#47;code><&#47;div></p>
<div><code><&#47;<&#47;code><code>staticContent<&#47;code><code>><&#47;code><&#47;div><br />
<&#47;div><&#47;td><br />
<&#47;tr><br />
<&#47;tbody><br />
<&#47;table><br />
<&#47;div><br />
<&#47;div><br />
You might think this is insane. This is, in fact, insane. Insane like a fox. I built the website so I want control. I version my CSS and JS files in the filename. Others use QueryStrings with versions and some use hashes. The point is are YOU in control or are you just letting caching happen? Even if you don't use this tip, know <strong>how and why <&#47;strong>things are cached and how you can control it.</p>
<h3>Compress everything<&#47;h3><br />
Make sure everything is GZip'ed as it goes out of your Web Server. This is also easy with IIS7 and allowed me to get rid of some old 3rd party libraries. All these settings are in system.webServer.</p>
<div>
<div id="highlighter_853072">
<table border="0" cellspacing="0" cellpadding="0">
<tbody>
<tr>
<td>
<div>1<&#47;div><&#47;td></p>
<td>
<div>
<div><code><<&#47;code><code>urlCompression<&#47;code> <code>doDynamicCompression<&#47;code><code>=<&#47;code><code>"true"<&#47;code> <code>doStaticCompression<&#47;code><code>=<&#47;code><code>"true"<&#47;code> <code>dynamicCompressionBeforeCache<&#47;code><code>=<&#47;code><code>"true"<&#47;code><code>&#47;><&#47;code><&#47;div><br />
<&#47;div><&#47;td><br />
<&#47;tr><br />
<&#47;tbody><br />
<&#47;table><br />
<&#47;div><br />
<&#47;div><br />
If there is one thing you can do to your website, it's turning on HTTP compression. For average pages, like my 100k of HTML, it can turn into 20k. It downloads faster and the perception of speed by the user from "click to render" will increase. Certainly this post just scratches the surface of REAL performance optimization and only goes up to the point where the bits hit the browser. You can go nuts trying to get an "A" grade in YSlow, optimizing for # of DOM objects, DNS Lookups, JavaScript ordering, and on and on. That said, you can get 80% of the benefit for 5% of the effort by these tips. It'll take you no time and you'll reap the benefits hourly:</p>
<ul>
<li>Minifying your JS and CSS<&#47;li>
<li>Combining CSS and JS into single files to minimize HTTP requests<&#47;li>
<li>Turning on Gzip Compression for as much as you can<&#47;li>
<li>Set Expires Headers on everything you can<&#47;li>
<li>Compress your PNGs and JPEGs (but definitely your PNGs)<&#47;li>
<li><a href="http:&#47;&#47;www.hanselman.com&#47;blog&#47;NuGetPackageOfTheWeek1ASPNETSpriteAndImageOptimization.aspx">Use CSS Sprites if you have lots of tiny images<&#47;a><&#47;li><br />
<&#47;ul><br />
I still have a "D" on YSlow, but a D is a passing grade. ;) Enjoy, and leave your tips, and your "duh!" in the comments, Dear Reader. Also, read anything by <a href="http:&#47;&#47;stevesouders.com&#47;">Steve Souders<&#47;a>. He wrote YSlow.</p>
<p><a href="http:&#47;&#47;www.hanselman.com&#47;blog&#47;TheImportanceAndEaseOfMinifyingYourCSSAndJavaScriptAndOptimizingPNGsForYourBlogOrWebsite.aspx" target="_blank">http:&#47;&#47;www.hanselman.com&#47;blog&#47;TheImportanceAndEaseOfMinifyingYourCSSAndJavaScriptAndOptimizingPNGsForYourBlogOrWebsite.aspx<&#47;a> </p>
