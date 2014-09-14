---
layout: post
status: publish
published: true
title: How Browsers Work
author:
  display_name: aaronzh
  login: wdadmin
  email: webdebug.net@gmail.com
  url: ''
author_login: wdadmin
author_email: webdebug.net@gmail.com
wordpress_id: 426
wordpress_url: http://www.webdebug.net/?p=426
date: '2013-12-21 10:35:45 +0800'
date_gmt: '2013-12-21 10:35:45 +0800'
categories:
- browser
tags:
- browser
- design
- architecture
comments:
- id: 1956
  author: Dan
  author_email: danculpin@gmail.com
  author_url: http://www.adobe.com/
  date: '2014-04-02 13:04:19 +0800'
  date_gmt: '2014-04-02 13:04:19 +0800'
  content: "If you wish for to obtain much from this piece of writing then \r\nyou
    have to apply these techniques to your won weblog.\r\n\r\n\r\n\r\nmy blog post
    :: adobe (<a href=\"http:&#47;&#47;www.adobe.com&#47;\" rel=\"nofollow\">Dan<&#47;a>)"
- id: 9896
  author: www.palurd.com
  author_email: klaudiaburger@gawab.com
  author_url: ''
  date: '2014-06-06 10:28:26 +0800'
  date_gmt: '2014-06-06 10:28:26 +0800'
  content: "Appreciate this post. Will try it out.\r\n\r\nMy webpage ... <a href=\"http:&#47;&#47;www.palurd.com&#47;ortho6&#47;forum&#47;extremely-short-layered-bob-hairstyles-back-again-rear-check-out&#47;11411\"
    rel=\"nofollow\">www.palurd.com<&#47;a>"
- id: 10549
  author: Sanford
  author_email: sanfordwimmer@gmail.com
  author_url: ''
  date: '2014-06-10 02:53:49 +0800'
  date_gmt: '2014-06-10 02:53:49 +0800'
  content: "Good post. I learn something totally new and challenging on websites I
    stumbleupon on a daily basis.\r\n\r\nIt's always exciting to read through content
    from other writers and practice something from their sites."
- id: 21440
  author: Www.Zavodpm.ru
  author_email: jeseniadesrochers@gmail.com
  author_url: http://Www.Zavodpm.ru/blogs/titusbrownellkunwo/17686-have-shed-some-pounds-use-these-suggestions
  date: '2014-08-25 13:21:22 +0800'
  date_gmt: '2014-08-25 13:21:22 +0800'
  content: "Hey! This is my 1st comment here so I just wanted to give \r\na quick
    shout out and tell you I genuinely enjoy reading your posts.\r\n\r\nCan you suggest
    any other blogs&#47;websites&#47;forums that go over the \r\nsame topics? Thanks!\r\n\r\nFeel
    free to visit my weblog :: <a href=\"http:&#47;&#47;Www.Zavodpm.ru&#47;blogs&#47;titusbrownellkunwo&#47;17686-have-shed-some-pounds-use-these-suggestions\"
    rel=\"nofollow\">Www.Zavodpm.ru<&#47;a>"
---
<div>
<h2>Preface<&#47;h2><br />
This comprehensive primer on the internal operations of WebKit and Gecko is the result of much research done by Israeli developer Tali Garsiel. Over a few years, she reviewed all the published data about browser internals <small>(see <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#Resources">Resources<&#47;a>)<&#47;small> and spent a lot of time reading web browser source code. She wrote:</p>
<blockquote><p>In the years of IE 90% dominance there was nothing much to do but regard the browser as a "black box", but now, with open source browsers having <a href="http:&#47;&#47;techcrunch.com&#47;2011&#47;08&#47;01&#47;open-web-browsers&#47;">more than half of the usage share<&#47;a>, it's a good time to take a peek under the engine's hood and see what's inside a web browser. Well, what's inside are millions of C++ lines...<&#47;blockquote><br />
Tali published her research on <a href="http:&#47;&#47;taligarsiel.com&#47;">her site<&#47;a>, but we knew it deserved a larger audience, so we've cleaned it up and republished it here.As a web developer, <strong>learning the internals of browser operations helps you make better decisions and know the justifications behind development best practices<&#47;strong>. While this is a rather lengthy document, we recommend you spend some time digging in; we guarantee you'll be glad you did. <cite>Paul Irish, Chrome Developer Relations<&#47;cite></p>
<div>
<p>This article has been <a href="http:&#47;&#47;helloworld.naver.com&#47;helloworld&#47;59361">translated into Korean<&#47;a> by the community. HTML5 Rocks hosts the <a href="http:&#47;&#47;www.html5rocks.com&#47;de&#47;tutorials&#47;internals&#47;howbrowserswork&#47;">German<&#47;a>, <a href="http:&#47;&#47;www.html5rocks.com&#47;es&#47;tutorials&#47;internals&#47;howbrowserswork&#47;">Spanish<&#47;a>, <a href="http:&#47;&#47;www.html5rocks.com&#47;ja&#47;tutorials&#47;internals&#47;howbrowserswork&#47;">Japanese<&#47;a>, <a href="http:&#47;&#47;www.html5rocks.com&#47;pt&#47;tutorials&#47;internals&#47;howbrowserswork&#47;">Portuguese<&#47;a>, <a href="http:&#47;&#47;www.html5rocks.com&#47;ru&#47;tutorials&#47;internals&#47;howbrowserswork&#47;">Russian<&#47;a> and <a href="http:&#47;&#47;www.html5rocks.com&#47;zh&#47;tutorials&#47;internals&#47;howbrowserswork&#47;">Simplified Chinese<&#47;a> versions.</p>
<p>You can also watch <a href="http:&#47;&#47;vimeo.com&#47;44182484">Tali Garsiel give a talk on this topic<&#47;a> on Vimeo.</p>
<p><&#47;div><br />
<&#47;div></p>
<hr &#47;>
<h2 id="Introduction">Introduction<&#47;h2><br />
Web browsers are the most widely used software. In this primer, I will explain how they work behind the scenes. We will see what happens when you type <code>google.com<&#47;code> in the address bar until you see the Google page on the browser screen.</p>
<h3>Table of Contents<&#47;h3></p>
<ol>
<li><a href="#Introduction">Introduction<&#47;a>
<ol>
<li><a href="#The_browsers_we_will_talk_about">The browsers we will talk about<&#47;a><&#47;li>
<li><a href="#The_browser_main_functionality">The browser's main functionality<&#47;a><&#47;li>
<li><a href="#The_browser_high_level_structure">The browser's high level structure<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#The_rendering_engine">The rendering engine<&#47;a>
<ol>
<li><a href="#Rendering_engines">Rendering engines<&#47;a><&#47;li>
<li><a href="#The_main_flow">The main flow<&#47;a><&#47;li>
<li><a href="#Main_flow_examples">Main flow examples<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#Parsing_general">Parsing and DOM tree construction<&#47;a>
<ol>
<li><a href="#Parsing_general">Parsing: general<&#47;a>
<ol>
<li><a href="#Grammars">Grammars<&#47;a><&#47;li>
<li><a href="#Parser_Lexer_combination">Parser&ndash;Lexer combination<&#47;a><&#47;li>
<li><a href="#Translation">Translation<&#47;a><&#47;li>
<li><a href="#Parsing_example">Parsing example<&#47;a><&#47;li>
<li><a href="#Formal_definitions_for_vocabulary_and_syntax">Formal definitions for vocabulary and syntax<&#47;a><&#47;li>
<li><a href="#Types_of_parsers">Types of parsers<&#47;a><&#47;li>
<li><a href="#Generating_parsers_automatically">Generating parsers automatically<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#HTML_Parser">HTML Parser<&#47;a>
<ol>
<li><a href="#The_HTML_grammar_definition">The HTML grammar definition<&#47;a><&#47;li>
<li><a href="#Not_a_context_free_grammar">Not a context free grammar<&#47;a><&#47;li>
<li><a href="#HTML_DTD">HTML DTD<&#47;a><&#47;li>
<li><a href="#DOM">DOM<&#47;a><&#47;li>
<li><a href="#The_parsing_algorithm">The parsing algorithm<&#47;a><&#47;li>
<li><a href="#The_tokenization_algorithm">The tokenization algorithm<&#47;a><&#47;li>
<li><a href="#Tree_construction_algorithm">Tree construction algorithm<&#47;a><&#47;li>
<li><a href="#Actions_when_the_parsing_is_finished">Actions when parsing is finished<&#47;a><&#47;li>
<li><a href="#Browsers_error_tolerance">Browser error tolerance<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#CSS_parsing">CSS parsing<&#47;a>
<ol>
<li><a href="#WebKit_CSS_parser">WebKit CSS parser<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#The_order_of_processing_scripts_and_style_sheets">The order of processing scripts and style sheets<&#47;a>
<ol>
<li><a href="#Scripts">Scripts<&#47;a><&#47;li>
<li><a href="#Speculative_parsing">Speculative parsing<&#47;a><&#47;li>
<li><a href="#Style_sheets">Style sheets<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#Render_tree_construction">Render tree construction<&#47;a>
<ol>
<li><a href="#The_render_tree_relation_to_the_DOM_tree">The render tree relation to the DOM tree<&#47;a><&#47;li>
<li><a href="#The_flow_of_constructing_the_tree">The flow of constructing the tree<&#47;a><&#47;li>
<li><a href="#Style_Computation">Style Computation<&#47;a>
<ol>
<li><a href="#Sharing_style_data">Sharing style data<&#47;a><&#47;li>
<li><a href="#Firefox_rule_tree">Firefox rule tree<&#47;a>
<ol>
<li><a href="#Division_into_structs">Division into structs<&#47;a><&#47;li>
<li><a href="#Computing_the_style_contexts_using_the_rule_tree">Computing the style contexts using the rule tree<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#Manipulating_the_rules_for_an_easy_match">Manipulating the rules for an easy match<&#47;a><&#47;li>
<li><a href="#Applying_the_rules_in_the_correct_cascade_order">Applying the rules in the correct cascade order<&#47;a>
<ol>
<li><a href="#Style_sheet_cascade_order">Style sheet cascade order<&#47;a><&#47;li>
<li><a href="#Specificity">Specificity<&#47;a><&#47;li>
<li><a href="#Sorting_the_rules">Sorting the rules<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#Gradual_process">Gradual process<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#Layout">Layout<&#47;a>
<ol>
<li><a href="#Dirty_bit_system">Dirty bit system<&#47;a><&#47;li>
<li><a href="#Global_and_incremental_layout">Global and incremental layout<&#47;a><&#47;li>
<li><a href="#Asynchronous_and_Synchronous_layout">Asynchronous and synchronous layout<&#47;a><&#47;li>
<li><a href="#Optimizations">Optimizations<&#47;a><&#47;li>
<li><a href="#The_layout_process">The layout process<&#47;a><&#47;li>
<li><a href="#Width_calculation">Width calculation<&#47;a><&#47;li>
<li><a href="#Line_Breaking">Line breaking<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#Painting">Painting<&#47;a>
<ol>
<li><a href="#Global_and_Incremental">Global and incremental<&#47;a><&#47;li>
<li><a href="#The_painting_order">The painting order<&#47;a><&#47;li>
<li><a href="#Firefox_display_list">Firefox display list<&#47;a><&#47;li>
<li><a href="#WebKit_rectangle_storage">WebKit rectangle storage<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#Dynamic_changes">Dynamic changes<&#47;a><&#47;li>
<li><a href="#The_rendering_engines_threads">The rendering engine's threads<&#47;a>
<ol>
<li><a href="#Event_loop">Event loop<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#css">CSS2 visual model<&#47;a>
<ol>
<li><a href="#The_canvas">The canvas<&#47;a><&#47;li>
<li><a href="#CSS_Box_model">CSS box model<&#47;a><&#47;li>
<li><a href="#Positioning_scheme">Positioning scheme<&#47;a><&#47;li>
<li><a href="#Box_types">Box types<&#47;a><&#47;li>
<li><a href="#Positioning">Positioning<&#47;a>
<ol>
<li><a href="#Relative">Relative<&#47;a><&#47;li>
<li><a href="#Floats">Floats<&#47;a><&#47;li>
<li><a href="#Absolute_and_fixed">Absolute and fixed<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#Layered_representation">Layered representation<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li><a href="#Resources">Resources<&#47;a><&#47;li><br />
<&#47;ol></p>
<div>
<h2 id="The_browsers_we_will_talk_about">The browsers we will talk about<&#47;h2><br />
There are five major browsers used on desktop today: Chrome, Internet Explorer, Firefox, Safari and Opera. On mobile, the main browsers are Android Browser, iPhone, Opera Mini and Opera Mobile, UC Browser, the Nokia S40&#47;S60 browsers and Chrome&ndash;all of which, except for the Opera browsers, are based on WebKit. I will give examples from the open source browsers Firefox and Chrome, and Safari (which is partly open source). According to <a href="http:&#47;&#47;gs.statcounter.com&#47;">StatCounter statistics<&#47;a> (as of June 2013) Chrome, Firefox and Safari make up around 71% of global desktop browser usage. On mobile, Android Browser, iPhone and Chrome constitute around 54% of usage.</p>
<h2 id="The_browser_main_functionality">The browser's main functionality<&#47;h2><br />
The main function of a browser is to present the web resource you choose, by requesting it from the server and displaying it in the browser window. The resource is usually an HTML document, but may also be a PDF, image, or some other type of content. The location of the resource is specified by the user using a URI (Uniform Resource Identifier).</p>
<p>The way the browser interprets and displays HTML files is specified in the HTML and CSS specifications. These specifications are maintained by the <a id="w3c"><&#47;a>W3C (World Wide Web Consortium) organization, which is the standards organization for the web. For years browsers conformed to only a part of the specifications and developed their own extensions. That caused serious compatibility issues for web authors. Today most of the browsers more or less conform to the specifications.</p>
<p>Browser user interfaces have a lot in common with each other. Among the common user interface elements are:</p>
<ul>
<li>Address bar for inserting a URI<&#47;li>
<li>Back and forward buttons<&#47;li>
<li>Bookmarking options<&#47;li>
<li>Refresh and stop buttons for refreshing or stopping the loading of current documents<&#47;li>
<li>Home button that takes you to your home page<&#47;li><br />
<&#47;ul><br />
Strangely enough, the browser's user interface is not specified in any formal specification, it just comes from good practices shaped over years of experience and by browsers imitating each other. The HTML5 specification doesn't define UI elements a browser must have, but lists some common elements. Among those are the address bar, status bar and tool bar. There are, of course, features unique to a specific browser like Firefox's downloads manager.</p>
<h2 id="The_browser_high_level_structure">The browser's high level structure<&#47;h2><br />
The browser's main components are (<a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#1_1">1.1<&#47;a>):</p>
<ol>
<li><strong>The user interface<&#47;strong>: this includes the address bar, back&#47;forward button, bookmarking menu, etc. Every part of the browser display except the window where you see the requested page.<&#47;li>
<li><strong>The browser engine<&#47;strong>: marshals actions between the UI and the rendering engine.<&#47;li>
<li><strong>The rendering engine <&#47;strong>: responsible for displaying requested content. For example if the requested content is HTML, the rendering engine parses HTML and CSS, and displays the parsed content on the screen.<&#47;li>
<li><strong>Networking<&#47;strong>: for network calls such as HTTP requests, using different implementations for different platform behind a platform-independent interface.<&#47;li>
<li><strong>UI backend<&#47;strong>: used for drawing basic widgets like combo boxes and windows. This backend exposes a generic interface that is not platform specific. Underneath it uses operating system user interface methods.<&#47;li>
<li><strong>JavaScript interpreter<&#47;strong>. Used to parse and execute JavaScript code.<&#47;li>
<li><strong>Data storage<&#47;strong>. This is a persistence layer. The browser may need to save all sorts of data locally, such as cookies. Browsers also support storage mechanisms such as localStorage, IndexedDB, WebSQL and FileSystem.<&#47;li><br />
<&#47;ol></p>
<figure><img title="" alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;layers.png" width="500" height="339" &#47;><br />
<figcaption>Figure : Browser components<&#47;figcaption><&#47;figure>It is important to note that browsers such as Chrome run multiple instances of the rendering engine: one for each tab. Each tab runs in a separate process.</p>
<h2 id="The_rendering_engine">The rendering engine<&#47;h2><br />
The responsibility of the rendering engine is well... Rendering, that is display of the requested contents on the browser screen.</p>
<p>By default the rendering engine can display HTML and XML documents and images. It can display other types of data via plug-ins or extension; for example, displaying PDF documents using a PDF viewer plug-in. However, in this chapter we will focus on the main use case: displaying HTML and images that are formatted using CSS.</p>
<h2 id="Rendering_engines">Rendering engines<&#47;h2><br />
Different browsers use different rendering engines: Internet Explorer uses Trident, Firefox uses Gecko, Safari uses WebKit. Chrome and Opera (from version 15) use Blink, a fork of WebKit.</p>
<p>WebKit is an open source rendering engine which started as an engine for the Linux platform and was modified by Apple to support Mac and Windows. See <a href="http:&#47;&#47;webkit.org&#47;">webkit.org<&#47;a> for more details.</p>
<h2 id="The_main_flow">The main flow<&#47;h2><br />
The rendering engine will start getting the contents of the requested document from the networking layer. This will usually be done in 8kB chunks.</p>
<p>After that, this is the basic flow of the rendering engine:</p>
<figure><img title="" alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;flow.png" width="600" height="66" &#47;><br />
<figcaption>Figure : Rendering engine basic flow<&#47;figcaption><&#47;figure>The rendering engine will start parsing the HTML document and convert elements to <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#DOM">DOM<&#47;a> nodes in a tree called the "content tree". The engine will parse the style data, both in external CSS files and in style elements. Styling information together with visual instructions in the HTML will be used to create another tree: the <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#Render_tree_construction">render tree<&#47;a>.</p>
<p>The render tree contains rectangles with visual attributes like color and dimensions. The rectangles are in the right order to be displayed on the screen.</p>
<p>After the construction of the render tree it goes through a "<a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#layout">layout<&#47;a>" process. This means giving each node the exact coordinates where it should appear on the screen. The next stage is <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#Painting">painting<&#47;a>&ndash;the render tree will be traversed and each node will be painted using the UI backend layer.</p>
<p>It's important to understand that this is a gradual process. For better user experience, the rendering engine will try to display contents on the screen as soon as possible. It will not wait until all HTML is parsed before starting to build and layout the render tree. Parts of the content will be parsed and displayed, while the process continues with the rest of the contents that keeps coming from the network.</p>
<h3 id="Main_flow_examples">Main flow examples<&#47;h3></p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;webkitflow.png" width="624" height="289" &#47;><br />
<figcaption>Figure : WebKit main flow<&#47;figcaption><&#47;figure><br />
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image008.jpg" width="624" height="290" &#47;><br />
<figcaption>Figure : Mozilla's Gecko rendering engine main flow (<a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#3_6">3.6<&#47;a>)<&#47;figcaption><&#47;figure>From figures 3 and 4 you can see that although WebKit and Gecko use slightly different terminology, the flow is basically the same.</p>
<p>Gecko calls the tree of visually formatted elements a "Frame tree". Each element is a frame. WebKit uses the term "Render Tree" and it consists of "Render Objects". WebKit uses the term "layout" for the placing of elements, while Gecko calls it "Reflow". "Attachment" is WebKit's term for connecting DOM nodes and visual information to create the render tree. A minor non-semantic difference is that Gecko has an extra layer between the HTML and the DOM tree. It is called the "content sink" and is a factory for making DOM elements. We will talk about each part of the flow:</p>
<h3 id="Parsing_general">Parsing&ndash;general<&#47;h3><br />
Since parsing is a very significant process within the rendering engine, we will go into it a little more deeply. Let's begin with a little introduction about parsing.</p>
<p>Parsing a document means translating it to a structure the code can use. The result of parsing is usually a tree of nodes that represent the structure of the document. This is called a parse tree or a syntax tree.</p>
<p>For example, parsing the expression <samp>2 + 3 - 1<&#47;samp> could return this tree:</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image009.png" width="400" height="155" &#47;><br />
<figcaption> Figure : mathematical expression tree node<&#47;figcaption><&#47;figure></p>
<h3 id="Grammars">Grammars<&#47;h3><br />
Parsing is based on the syntax rules the document obeys: the language or format it was written in. Every format you can parse must have deterministic grammar consisting of vocabulary and syntax rules. It is called a <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#context_free_grammar">context free grammar<&#47;a>. Human languages are not such languages and therefore cannot be parsed with conventional parsing techniques.</p>
<h3 id="Parser_Lexer_combination">Parser&ndash;Lexer combination<&#47;h3><br />
Parsing can be separated into two sub processes: lexical analysis and syntax analysis.</p>
<p>Lexical analysis is the process of breaking the input into tokens. Tokens are the language vocabulary: the collection of valid building blocks. In human language it will consist of all the words that appear in the dictionary for that language.</p>
<p>Syntax analysis is the applying of the language syntax rules.</p>
<p>Parsers usually divide the work between two components: the <b>lexer<&#47;b> (sometimes called tokenizer) that is responsible for breaking the input into valid tokens, and the <b>parser<&#47;b> that is responsible for constructing the parse tree by analyzing the document structure according to the language syntax rules. The lexer knows how to strip irrelevant characters like white spaces and line breaks.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image011.png" width="101" height="300" &#47;><br />
<figcaption> Figure : from source document to parse trees<&#47;figcaption><&#47;figure>The parsing process is iterative. The parser will usually ask the lexer for a new token and try to match the token with one of the syntax rules. If a rule is matched, a node corresponding to the token will be added to the parse tree and the parser will ask for another token.</p>
<p>If no rule matches, the parser will store the token internally, and keep asking for tokens until a rule matching all the internally stored tokens is found. If no rule is found then the parser will raise an exception. This means the document was not valid and contained syntax errors.</p>
<h3 id="Translation">Translation<&#47;h3><br />
In many cases the parse tree is not the final product. Parsing is often used in translation: transforming the input document to another format. An example is compilation. The compiler that compiles source code into machine code first parses it into a parse tree and then translates the tree into a machine code document.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image013.png" width="104" height="400" &#47;><br />
<figcaption>Figure : compilation flow<&#47;figcaption><&#47;figure></p>
<h3 id="Parsing_example">Parsing example<&#47;h3><br />
In figure 5 we built a parse tree from a mathematical expression. Let's try to define a simple mathematical language and see the parse process.</p>
<p>Vocabulary: Our language can include integers, plus signs and minus signs.</p>
<p>Syntax:</p>
<ol>
<li>The language syntax building blocks are expressions, terms and operations.<&#47;li>
<li>Our language can include any number of expressions.<&#47;li>
<li>An expression is defined as a "term" followed by an "operation" followed by another term<&#47;li>
<li>An operation is a plus token or a minus token<&#47;li>
<li>A term is an integer token or an expression<&#47;li><br />
<&#47;ol><br />
Let's analyze the input <samp>2 + 3 - 1<&#47;samp>.<br />
The first substring that matches a rule is <samp>2<&#47;samp>: according to rule #5 it is a term. The second match is <samp>2 + 3<&#47;samp>: this matches the third rule: a term followed by an operation followed by another term. The next match will only be hit at the end of the input. <samp>2 + 3 - 1<&#47;samp> is an expression because we already know that <samp>2 + 3<&#47;samp> is a term, so we have a term followed by an operation followed by another term. <samp>2 + + <&#47;samp>will not match any rule and therefore is an invalid input.</p>
<h3 id="Formal_definitions_for_vocabulary_and_syntax">Formal definitions for vocabulary and syntax<&#47;h3><br />
Vocabulary is usually expressed by <a href="http:&#47;&#47;www.regular-expressions.info&#47;">regular expressions<&#47;a>.</p>
<p>For example our language will be defined as:</p>
<pre>INTEGER: 0|[1-9][0-9]*<br />
PLUS: +<br />
MINUS: -<&#47;pre><br />
As you see, integers are defined by a regular expression.Syntax is usually defined in a format called <a href="http:&#47;&#47;en.wikipedia.org&#47;wiki&#47;Backus%E2%80%93Naur_Form">BNF<&#47;a>. Our language will be defined as:</p>
<pre>expression :=  term  operation  term<br />
operation :=  PLUS | MINUS<br />
term := INTEGER | expression<&#47;pre><br />
We said that a language can be parsed by regular parsers if its grammar is a <a id="context_free_grammar"><&#47;a>context free grammar. An intuitive definition of a context free grammar is a grammar that can be entirely expressed in BNF. For a formal definition see <a href="http:&#47;&#47;en.wikipedia.org&#47;wiki&#47;Context-free_grammar">Wikipedia's article on Context-free grammar<&#47;a></p>
<h3 id="Types_of_parsers">Types of parsers<&#47;h3><br />
There are two types of parsers: top down parsers and bottom up parsers. An intuitive explanation is that top down parsers examine the high level structure of the syntax and try to find a rule match. Bottom up parsers start with the input and gradually transform it into the syntax rules, starting from the low level rules until high level rules are met.</p>
<p>Let's see how the two types of parsers will parse our example.</p>
<p>The top down parser will start from the higher level rule: it will identify <samp>2 + 3<&#47;samp> as an expression. It will then identify <samp>2 + 3 - 1<&#47;samp> as an expression (the process of identifying the expression evolves, matching the other rules, but the start point is the highest level rule).</p>
<p>The bottom up parser will scan the input until a rule is matched. It will then replace the matching input with the rule. This will go on until the end of the input. The partly matched expression is placed on the parser's stack.</p>
<table id="stack">
<tbody>
<tr>
<th>Stack<&#47;th></p>
<th>Input<&#47;th><br />
<&#47;tr></p>
<tr>
<td><&#47;td></p>
<td><samp>2 + 3 - 1 <&#47;samp><&#47;td><br />
<&#47;tr></p>
<tr>
<td>term<&#47;td></p>
<td><samp> + 3 - 1 <&#47;samp><&#47;td><br />
<&#47;tr></p>
<tr>
<td>term operation<&#47;td></p>
<td><samp> 3 - 1 <&#47;samp><&#47;td><br />
<&#47;tr></p>
<tr>
<td>expression<&#47;td></p>
<td><samp>- 1 <&#47;samp><&#47;td><br />
<&#47;tr></p>
<tr>
<td>expression operation<&#47;td></p>
<td><samp>1 <&#47;samp><&#47;td><br />
<&#47;tr></p>
<tr>
<td>expression<&#47;td></p>
<td><samp> - <&#47;samp><&#47;td><br />
<&#47;tr><br />
<&#47;tbody><br />
<&#47;table><br />
This type of bottom up parser is called a shift-reduce parser, because the input is shifted to the right (imagine a pointer pointing first at the input start and moving to the right) and is gradually reduced to syntax rules.</p>
<h3 id="Generating_parsers_automatically">Generating parsers automatically<&#47;h3><br />
There are tools that can generate a parser. You feed them the grammar of your language&ndash;its vocabulary and syntax rules&ndash;and they generate a working parser. Creating a parser requires a deep understanding of parsing and it's not easy to create an optimized parser by hand, so parser generators can be very useful.</p>
<p><a id="parser_generators"><&#47;a>WebKit uses two well known parser generators: <a href="http:&#47;&#47;en.wikipedia.org&#47;wiki&#47;Flex_lexical_analyser">Flex<&#47;a> for creating a lexer and <a href="http:&#47;&#47;www.gnu.org&#47;software&#47;bison&#47;">Bison<&#47;a> for creating a parser (you might run into them with the names Lex and Yacc). Flex input is a file containing regular expression definitions of the tokens. Bison's input is the language syntax rules in BNF format.</p>
<h2 id="HTML_Parser">HTML Parser<&#47;h2><br />
The job of the HTML parser is to parse the HTML markup into a parse tree.</p>
<h3 id="The_HTML_grammar_definition">The HTML grammar definition<&#47;h3><br />
The vocabulary and syntax of HTML are defined in <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#w3c">specifications<&#47;a> created by the W3C organization.</p>
<h3 id="Not_a_context_free_grammar">Not a context free grammar<&#47;h3><br />
As we have seen in the parsing introduction, grammar syntax can be defined formally using formats like BNF.</p>
<p>Unfortunately all the conventional parser topics do not apply to HTML (I didn't bring them up just for fun&ndash;they will be used in parsing CSS and JavaScript). HTML cannot easily be defined by a context free grammar that parsers need.</p>
<p>There is a formal format for defining HTML&ndash;DTD (Document Type Definition)&ndash;but it is not a context free grammar.</p>
<p>This appears strange at first sight; HTML is rather close to XML. There are lots of available XML parsers. There is an XML variation of HTML&ndash;XHTML&ndash;so what's the big difference?</p>
<p>The difference is that the HTML approach is more "forgiving": it lets you omit certain tags (which are then added implicitly), or sometimes omit start or end tags, and so on. On the whole it's a "soft" syntax, as opposed to XML's stiff and demanding syntax.</p>
<p>This seemingly small detail makes a world of a difference. On one hand this is the main reason why HTML is so popular: it forgives your mistakes and makes life easy for the web author. On the other hand, it makes it difficult to write a formal grammar. So to summarize, HTML cannot be parsed easily by conventional parsers, since its grammar is not context free. HTML cannot be parsed by XML parsers.</p>
<h3 id="HTML_DTD">HTML DTD<&#47;h3><br />
HTML definition is in a DTD format. This format is used to define languages of the <a href="http:&#47;&#47;en.wikipedia.org&#47;wiki&#47;Standard_Generalized_Markup_Language">SGML<&#47;a> family. The format contains definitions for all allowed elements, their attributes and hierarchy. As we saw earlier, the HTML DTD doesn't form a context free grammar.</p>
<p>There are a few variations of the DTD. The strict mode conforms solely to the specifications but other modes contain support for markup used by browsers in the past. The purpose is backwards compatibility with older content. The current strict DTD is here: <a href="http:&#47;&#47;www.w3.org&#47;TR&#47;html4&#47;strict.dtd">www.w3.org&#47;TR&#47;html4&#47;strict.dtd<&#47;a></p>
<h3 id="DOM">DOM<&#47;h3><br />
The output tree (the "parse tree") is a tree of DOM element and attribute nodes. DOM is short for Document Object Model. It is the object presentation of the HTML document and the interface of HTML elements to the outside world like JavaScript.<br />
The root of the tree is the "<a href="http:&#47;&#47;www.w3.org&#47;TR&#47;1998&#47;REC-DOM-Level-1-19981001&#47;level-one-core.html#i-Document">Document<&#47;a>" object.</p>
<p>The DOM has an almost one-to-one relation to the markup. For example:</p>
<pre><html><br />
  <body></p>
<p>
      Hello World<br />
    <&#47;p></p>
<div> <img src="example.png"&#47;><&#47;div><br />
  <&#47;body><br />
<&#47;html><&#47;pre><br />
This markup would be translated to the following DOM tree:</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image015.png" width="400" height="219" &#47;><br />
<figcaption> Figure : DOM tree of the example markup<&#47;figcaption><&#47;figure>Like HTML, DOM is specified by the W3C organization. See <a href="http:&#47;&#47;www.w3.org&#47;DOM&#47;DOMTR">www.w3.org&#47;DOM&#47;DOMTR<&#47;a>. It is a generic specification for manipulating documents. A specific module describes HTML specific elements. The HTML definitions can be found here: <a href="http:&#47;&#47;www.w3.org&#47;TR&#47;2003&#47;REC-DOM-Level-2-HTML-20030109&#47;idl-definitions.html">www.w3.org&#47;TR&#47;2003&#47;REC-DOM-Level-2-HTML-20030109&#47;idl-definitions.html<&#47;a>.</p>
<p>When I say the tree contains DOM nodes, I mean the tree is constructed of elements that implement one of the DOM interfaces. Browsers use concrete implementations that have other attributes used by the browser internally.</p>
<h4 id="The_parsing_algorithm">The parsing algorithm<&#47;h4><br />
As we saw in the previous sections, HTML cannot be parsed using the regular top down or bottom up parsers.</p>
<p>The reasons are:</p>
<ol>
<li>The forgiving nature of the language.<&#47;li>
<li>The fact that browsers have traditional error tolerance to support well known cases of invalid HTML.<&#47;li>
<li>The parsing process is reentrant. For other languages, the source doesn't change during parsing, but in HTML, dynamic code (such as script elements containing <code>document.write()<&#47;code> calls) can add extra tokens, so the parsing process actually modifies the input.<&#47;li><br />
<&#47;ol><br />
Unable to use the regular parsing techniques, browsers create custom parsers for parsing HTML.</p>
<p>The <a href="http:&#47;&#47;www.whatwg.org&#47;specs&#47;web-apps&#47;current-work&#47;multipage&#47;parsing.html">parsing algorithm is described in detail by the HTML5 specification<&#47;a>. The algorithm consists of two stages: tokenization and tree construction.</p>
<p>Tokenization is the lexical analysis, parsing the input into tokens. Among HTML tokens are start tags, end tags, attribute names and attribute values.</p>
<p>The tokenizer recognizes the token, gives it to the tree constructor, and consumes the next character for recognizing the next token, and so on until the end of the input.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image017.png" width="308" height="400" &#47;><br />
<figcaption>Figure : HTML parsing flow (taken from HTML5 spec)<&#47;figcaption><&#47;figure></p>
<h3 id="The_tokenization_algorithm">The tokenization algorithm<&#47;h3><br />
The algorithm's output is an HTML token. The algorithm is expressed as a state machine. Each state consumes one or more characters of the input stream and updates the next state according to those characters. The decision is influenced by the current tokenization state and by the tree construction state. This means the same consumed character will yield different results for the correct next state, depending on the current state. The algorithm is too complex to describe fully, so let's see a simple example that will help us understand the principle.</p>
<p>Basic example&ndash;tokenizing the following HTML:</p>
<pre><html><br />
  <body><br />
    Hello world<br />
  <&#47;body><br />
<&#47;html><&#47;pre><br />
The initial state is the "Data state". When the <code><<&#47;code> character is encountered, the state is changed to <b>"Tag open state"<&#47;b>. Consuming an <code>a-z<&#47;code> character causes creation of a "Start tag token", the state is changed to <b>"Tag name state"<&#47;b>. We stay in this state until the <code>><&#47;code> character is consumed. Each character is appended to the new token name. In our case the created token is an <code>html<&#47;code> token.</p>
<p>When the <code>><&#47;code> tag is reached, the current token is emitted and the state changes back to the <b>"Data state"<&#47;b>. The <code><body><&#47;code> tag will be treated by the same steps. So far the <code>html<&#47;code> and <code>body<&#47;code> tags were emitted. We are now back at the <b>"Data state"<&#47;b>. Consuming the <code>H<&#47;code> character of <code>Hello world<&#47;code> will cause creation and emitting of a character token, this goes on until the <code><<&#47;code> of <code><&#47;body><&#47;code> is reached. We will emit a character token for each character of <code>Hello world<&#47;code>.</p>
<p>We are now back at the <b>"Tag open state"<&#47;b>. Consuming the next input <code>&#47;<&#47;code> will cause creation of an <code>end tag token<&#47;code> and a move to the <b>"Tag name state"<&#47;b>. Again we stay in this state until we reach <code>><&#47;code>.Then the new tag token will be emitted and we go back to the <b>"Data state"<&#47;b>. The <code><&#47;html><&#47;code> input will be treated like the previous case.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image019.png" width="627" height="387" &#47;><br />
<figcaption>Figure : Tokenizing the example input<&#47;figcaption><&#47;figure></p>
<h4 id="Tree_construction_algorithm">Tree construction algorithm<&#47;h4><br />
When the parser is created the Document object is created. During the tree construction stage the DOM tree with the Document in its root will be modified and elements will be added to it. Each node emitted by the tokenizer will be processed by the tree constructor. For each token the specification defines which DOM element is relevant to it and will be created for this token. The element is added to the DOM tree, and also the stack of open elements. This stack is used to correct nesting mismatches and unclosed tags. The algorithm is also described as a state machine. The states are called "insertion modes".</p>
<p>Let's see the tree construction process for the example input:</p>
<pre><html><br />
  <body><br />
    Hello world<br />
  <&#47;body><br />
<&#47;html><&#47;pre><br />
The input to the tree construction stage is a sequence of tokens from the tokenization stage. The first mode is the <b>"initial mode"<&#47;b>. Receiving the "html" token will cause a move to the <b>"before html"<&#47;b> mode and a reprocessing of the token in that mode. This will cause creation of the HTMLHtmlElement element, which will be appended to the root Document object.</p>
<p>The state will be changed to <b>"before head"<&#47;b>. The "body" token is then received. An HTMLHeadElement will be created implicitly although we don't have a "head" token and it will be added to the tree.</p>
<p>We now move to the <b>"in head"<&#47;b> mode and then to <b>"after head"<&#47;b>. The body token is reprocessed, an HTMLBodyElement is created and inserted and the mode is transferred to <b>"in body"<&#47;b>.</p>
<p>The character tokens of the "Hello world" string are now received. The first one will cause creation and insertion of a "Text" node and the other characters will be appended to that node.</p>
<p>The receiving of the body end token will cause a transfer to <b>"after body"<&#47;b> mode. We will now receive the html end tag which will move us to <b>"after after body"<&#47;b> mode. Receiving the end of file token will end the parsing.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image022.gif" width="532" height="769" &#47;><br />
<figcaption>Figure : tree construction of example html<&#47;figcaption><&#47;figure></p>
<h3 id="Actions_when_the_parsing_is_finished">Actions when the parsing is finished<&#47;h3><br />
At this stage the browser will mark the document as interactive and start parsing scripts that are in "deferred" mode: those that should be executed after the document is parsed. The document state will be then set to "complete" and a "load" event will be fired.</p>
<p>You can see <a href="http:&#47;&#47;www.w3.org&#47;TR&#47;html5&#47;syntax.html#html-parser">the full algorithms for tokenization and tree construction in the HTML5 specification<&#47;a></p>
<h3 id="Browsers_error_tolerance">Browsers' error tolerance<&#47;h3><br />
You never get an "Invalid Syntax" error on an HTML page. Browsers fix any invalid content and go on.</p>
<p>Take this HTML for example:</p>
<pre><html><br />
  <mytag><br />
  <&#47;mytag></p>
<div>
<p>
  <&#47;div><br />
    Really lousy HTML<br />
  <&#47;p><br />
<&#47;html><&#47;pre><br />
I must have violated about a million rules ("mytag" is not a standard tag, wrong nesting of the "p" and "div" elements and more) but the browser still shows it correctly and doesn't complain. So a lot of the parser code is fixing the HTML author mistakes.</p>
<p>Error handling is quite consistent in browsers, but amazingly enough it hasn't been part of HTML specifications. Like bookmarking and back&#47;forward buttons it's just something that developed in browsers over the years. There are known invalid HTML constructs repeated on many sites, and the browsers try to fix them in a way conformant with other browsers.</p>
<p>The HTML5 specification does define some of these requirements. (WebKit summarizes this nicely in the comment at the beginning of the HTML parser class.)</p>
<blockquote><p>The parser parses tokenized input into the document, building up the document tree. If the document is well-formed, parsing it is straightforward.</p>
<p>Unfortunately, we have to handle many HTML documents that are not well-formed, so the parser has to be tolerant about errors.</p>
<p>We have to take care of at least the following error conditions:</p>
<ol>
<li>The element being added is explicitly forbidden inside some outer tag. In this case we should close all tags up to the one which forbids the element, and add it afterwards.<&#47;li>
<li>We are not allowed to add the element directly. It could be that the person writing the document forgot some tag in between (or that the tag in between is optional). This could be the case with the following tags: HTML HEAD BODY TBODY TR TD LI (did I forget any?).<&#47;li>
<li>We want to add a block element inside an inline element. Close all inline elements up to the next higher block element.<&#47;li>
<li>If this doesn't help, close elements until we are allowed to add the element&ndash;or ignore the tag.<&#47;li><br />
<&#47;ol><br />
<&#47;blockquote><br />
Let's see some WebKit error tolerance examples:</p>
<h4><&#47;br> instead of <br><&#47;h4><br />
Some sites use <&#47;br> instead of <br>. In order to be compatible with IE and Firefox, WebKit treats this like <br>.<br />
The code:</p>
<pre>if (t->isCloseTag(brTag) &amp;&amp; m_document->inCompatMode()) {<br />
     reportError(MalformedBRError);<br />
     t->beginTag = true;<br />
}<&#47;pre><br />
Note that the error handling is internal: it won't be presented to the user.</p>
<h4>A stray table<&#47;h4><br />
A stray table is a table inside another table, but not inside a table cell.</p>
<p>For example:</p>
<pre>
<table>
<table>
<tr>
<td>inner table<&#47;td><&#47;tr><br />
    <&#47;table></p>
<tr>
<td>outer table<&#47;td><&#47;tr><br />
<&#47;table><&#47;pre><br />
WebKit will change the hierarchy to two sibling tables:</p>
<pre>
<table>
<tr>
<td>outer table<&#47;td><&#47;tr><br />
<&#47;table></p>
<table>
<tr>
<td>inner table<&#47;td><&#47;tr><br />
<&#47;table><&#47;pre><br />
The code:</p>
<pre>if (m_inStrayTableContent &amp;&amp; localName == tableTag)<br />
        popBlock(tableTag);<&#47;pre><br />
WebKit uses a stack for the current element contents: it will pop the inner table out of the outer table stack. The tables will now be siblings.</p>
<h4>Nested form elements<&#47;h4><br />
In case the user puts a form inside another form, the second form is ignored.<br />
The code:</p>
<pre>if (!m_currentFormElement) {<br />
        m_currentFormElement = new HTMLFormElement(formTag,    m_document);<br />
}<&#47;pre></p>
<h4>A too deep tag hierarchy<&#47;h4><br />
The comment speaks for itself.</p>
<div>
<blockquote><p>www.liceo.edu.mx is an example of a site that achieves a level of nesting of about 1500 tags, all from a bunch of <b>s. We will only allow at most 20 nested tags of the same type before just ignoring them all together.<&#47;blockquote><br />
<&#47;div></p>
<pre>bool HTMLParser::allowNestedRedundantTag(const AtomicString&amp; tagName)<br />
{</p>
<p>unsigned i = 0;<br />
for (HTMLStackElem* curr = m_blockStack;<br />
         i < cMaxRedundantTagDepth &amp;&amp; curr &amp;&amp; curr->tagName == tagName;<br />
     curr = curr->next, i++) { }<br />
return i != cMaxRedundantTagDepth;<br />
}<&#47;pre></p>
<h4>Misplaced html or body end tags<&#47;h4><br />
Again&ndash;the comment speaks for itself.</p>
<blockquote><p>Support for really broken HTML. We never close the body tag, since some stupid web pages close it before the actual end of the doc. Let's rely on the end() call to close things.<&#47;blockquote></p>
<pre>if (t->tagName == htmlTag || t->tagName == bodyTag )<br />
        return;<&#47;pre><br />
So web authors beware&ndash;unless you want to appear as an example in a WebKit error tolerance code snippet&ndash;write well formed HTML.</p>
<h2 id="CSS_parsing">CSS parsing<&#47;h2><br />
Remember the parsing concepts in the introduction? Well, unlike HTML, CSS is a context free grammar and can be parsed using the types of parsers described in the introduction. In fact <a href="http:&#47;&#47;www.w3.org&#47;TR&#47;CSS2&#47;grammar.html">the CSS specification defines CSS lexical and syntax grammar<&#47;a>.</p>
<p>Let's see some examples:<br />
The lexical grammar (vocabulary) is defined by regular expressions for each token:</p>
<pre>comment   \&#47;\*[^*]*\*+([^&#47;*][^*]*\*+)*\&#47;<br />
num   [0-9]+|[0-9]*"."[0-9]+<br />
nonascii  [\200-\377]<br />
nmstart   [_a-z]|{nonascii}|{escape}<br />
nmchar    [_a-z0-9-]|{nonascii}|{escape}<br />
name    {nmchar}+<br />
ident   {nmstart}{nmchar}*<&#47;pre><br />
"ident" is short for identifier, like a class name. "name" is an element id (that is referred by "#" )</p>
<p>The syntax grammar is described in BNF.</p>
<pre>ruleset<br />
  : selector [ ',' S* selector ]*<br />
    '{' S* declaration [ ';' S* declaration ]* '}' S*<br />
  ;<br />
selector<br />
  : simple_selector [ combinator selector | S+ [ combinator? selector ]? ]?<br />
  ;<br />
simple_selector<br />
  : element_name [ HASH | class | attrib | pseudo ]*<br />
  | [ HASH | class | attrib | pseudo ]+<br />
  ;<br />
class<br />
  : '.' IDENT<br />
  ;<br />
element_name<br />
  : IDENT | '*'<br />
  ;<br />
attrib<br />
  : '[' S* IDENT S* [ [ '=' | INCLUDES | DASHMATCH ] S*<br />
    [ IDENT | STRING ] S* ] ']'<br />
  ;<br />
pseudo<br />
  : ':' [ IDENT | FUNCTION S* [IDENT S*] ')' ]<br />
  ;<&#47;pre><br />
Explanation: A ruleset is this structure:</p>
<pre>div.error, a.error {<br />
  color:red;<br />
  font-weight:bold;<br />
}<&#47;pre><br />
div.error and a.error are selectors. The part inside the curly braces contains the rules that are applied by this ruleset. This structure is defined formally in this definition:</p>
<pre>ruleset<br />
  : selector [ ',' S* selector ]*<br />
    '{' S* declaration [ ';' S* declaration ]* '}' S*<br />
  ;<&#47;pre><br />
This means a ruleset is a selector or optionally a number of selectors separated by a comma and spaces (S stands for white space). A ruleset contains curly braces and inside them a declaration or optionally a number of declarations separated by a semicolon. "declaration" and "selector" will be defined in the following BNF definitions.</p>
<h3 id="WebKit_CSS_parser">WebKit CSS parser<&#47;h3><br />
WebKit uses <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#parser_generators">Flex and Bison<&#47;a> parser generators to create parsers automatically from the CSS grammar files. As you recall from the parser introduction, Bison creates a bottom up shift-reduce parser. Firefox uses a top down parser written manually. In both cases each CSS file is parsed into a StyleSheet object. Each object contains CSS rules. The CSS rule objects contain selector and declaration objects and other objects corresponding to CSS grammar.</p>
<figure><img title="" alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image023.png" width="500" height="393" align="" border="0" &#47;><br />
<figcaption>Figure : parsing CSS<&#47;figcaption><&#47;figure></p>
<h2 id="The_order_of_processing_scripts_and_style_sheets">The order of processing scripts and style sheets<&#47;h2></p>
<h4 id="Scripts">Scripts<&#47;h4><br />
The model of the web is synchronous. Authors expect scripts to be parsed and executed immediately when the parser reaches a <script> tag. The parsing of the document halts until the script has been executed. If the script is external then the resource must first be fetched from the network&ndash;this is also done synchronously, and parsing halts until the resource is fetched. This was the model for many years and is also specified in HTML4 and 5 specifications. Authors can add the "defer" attribute to a script, in which case it will not halt document parsing and will execute after the document is parsed. HTML5 adds an option to mark the script as asynchronous so it will be parsed and executed by a different thread.</p>
<h3 id="Speculative_parsing">Speculative parsing<&#47;h3><br />
Both WebKit and Firefox do this optimization. While executing scripts, another thread parses the rest of the document and finds out what other resources need to be loaded from the network and loads them. In this way, resources can be loaded on parallel connections and overall speed is improved. Note: the speculative parser only parses references to external resources like external scripts, style sheets and images: it doesn't modify the DOM tree&ndash;that is left to the main parser.</p>
<h3 id="Style_sheets">Style sheets<&#47;h3><br />
Style sheets on the other hand have a different model. Conceptually it seems that since style sheets don't change the DOM tree, there is no reason to wait for them and stop the document parsing. There is an issue, though, of scripts asking for style information during the document parsing stage. If the style is not loaded and parsed yet, the script will get wrong answers and apparently this caused lots of problems. It seems to be an edge case but is quite common. Firefox blocks all scripts when there is a style sheet that is still being loaded and parsed. WebKit blocks scripts only when they try to access certain style properties that may be affected by unloaded style sheets.</p>
<h2 id="Render_tree_construction">Render tree construction<&#47;h2><br />
While the DOM tree is being constructed, the browser constructs another tree, the render tree. This tree is of visual elements in the order in which they will be displayed. It is the visual representation of the document. The purpose of this tree is to enable painting the contents in their correct order.</p>
<p>Firefox calls the elements in the render tree "frames". WebKit uses the term renderer or render object.<br />
A renderer knows how to lay out and paint itself and its children.<br />
WebKit's RenderObject class, the base class of the renderers, has the following definition:</p>
<pre>class RenderObject{<br />
  virtual void layout();<br />
  virtual void paint(PaintInfo);<br />
  virtual void rect repaintRect();<br />
  Node* node;  &#47;&#47;the DOM node<br />
  RenderStyle* style;  &#47;&#47; the computed style<br />
  RenderLayer* containgLayer; &#47;&#47;the containing z-index layer<br />
}<&#47;pre><br />
Each renderer represents a rectangular area usually corresponding to a node's CSS box, as described by the CSS2 spec. It includes geometric information like width, height and position.<br />
The box type is affected by the "display" value of the style attribute that is relevant to the node (see the <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#style_computation">style computation<&#47;a> section). Here is WebKit code for deciding what type of renderer should be created for a DOM node, according to the display attribute:</p>
<pre>RenderObject* RenderObject::createObject(Node* node, RenderStyle* style)<br />
{<br />
    Document* doc = node->document();<br />
    RenderArena* arena = doc->renderArena();<br />
    ...<br />
    RenderObject* o = 0;</p>
<p>    switch (style->display()) {<br />
        case NONE:<br />
            break;<br />
        case INLINE:<br />
            o = new (arena) RenderInline(node);<br />
            break;<br />
        case BLOCK:<br />
            o = new (arena) RenderBlock(node);<br />
            break;<br />
        case INLINE_BLOCK:<br />
            o = new (arena) RenderBlock(node);<br />
            break;<br />
        case LIST_ITEM:<br />
            o = new (arena) RenderListItem(node);<br />
            break;<br />
       ...<br />
    }</p>
<p>    return o;<br />
}<&#47;pre><br />
The element type is also considered: for example, form controls and tables have special frames.<br />
In WebKit if an element wants to create a special renderer, it will override the <code>createRenderer()<&#47;code> method. The renderers point to style objects that contains non geometric information.</p>
<h3 id="The_render_tree_relation_to_the_DOM_tree">The render tree relation to the DOM tree<&#47;h3><br />
The renderers correspond to DOM elements, but the relation is not one to one. Non-visual DOM elements will not be inserted in the render tree. An example is the "head" element. Also elements whose display value was assigned to "none" will not appear in the tree (whereas elements with "hidden" visibility will appear in the tree).There are DOM elements which correspond to several visual objects. These are usually elements with complex structure that cannot be described by a single rectangle. For example, the "select" element has three renderers: one for the display area, one for the drop down list box and one for the button. Also when text is broken into multiple lines because the width is not sufficient for one line, the new lines will be added as extra renderers.<br />
Another example of multiple renderers is broken HTML. According to the CSS spec an inline element must contain either only block elements or only inline elements. In the case of mixed content, anonymous block renderers will be created to wrap the inline elements.</p>
<p>Some render objects correspond to a DOM node but not in the same place in the tree. Floats and absolutely positioned elements are out of flow, placed in a different part of the tree, and mapped to the real frame. A placeholder frame is where they should have been.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image025.png" width="731" height="396" &#47;><br />
<figcaption>Figure : The render tree and the corresponding DOM tree (<a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#3_1">3.1<&#47;a>). The "Viewport" is the initial containing block. In WebKit it will be the "RenderView" object<&#47;figcaption><&#47;figure></p>
<h4 id="The_flow_of_constructing_the_tree">The flow of constructing the tree<&#47;h4><br />
In Firefox, the presentation is registered as a listener for DOM updates. The presentation delegates frame creation to the <code>FrameConstructor<&#47;code> and the constructor resolves style (see <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#style">style computation<&#47;a>) and creates a frame.</p>
<p>In WebKit the process of resolving the style and creating a renderer is called "attachment". Every DOM node has an "attach" method. Attachment is synchronous, node insertion to the DOM tree calls the new node "attach" method.</p>
<p>Processing the html and body tags results in the construction of the render tree root. The root render object corresponds to what the CSS spec calls the containing block: the top most block that contains all other blocks. Its dimensions are the viewport: the browser window display area dimensions. Firefox calls it <code>ViewPortFrame<&#47;code> and WebKit calls it <code>RenderView<&#47;code>. This is the render object that the document points to. The rest of the tree is constructed as a DOM nodes insertion.</p>
<p>See <a href="http:&#47;&#47;www.w3.org&#47;TR&#47;CSS21&#47;intro.html#processing-model">the CSS2 spec on the processing model<&#47;a>.</p>
<h3 id="Style_Computation">Style Computation<&#47;h3><br />
Building the render tree requires calculating the visual properties of each render object. This is done by calculating the style properties of each element.</p>
<p>The style includes style sheets of various origins, inline style elements and visual properties in the HTML (like the "bgcolor" property).The later is translated to matching CSS style properties.</p>
<p>The origins of style sheets are the browser's default style sheets, the style sheets provided by the page author and user style sheets&ndash;these are style sheets provided by the browser user (browsers let you define your favorite styles. In Firefox, for instance, this is done by placing a style sheet in the "Firefox Profile" folder).</p>
<p>Style computation brings up a few difficulties:</p>
<ol>
<li><a id="issue1"><&#47;a>Style data is a very large construct, holding the numerous style properties, this can cause memory problems.<&#47;li>
<li><a id="issue2"><&#47;a>Finding the matching rules for each element can cause performance issues if it's not optimized. Traversing the entire rule list for each element to find matches is a heavy task. Selectors can have complex structure that can cause the matching process to start on a seemingly promising path that is proven to be futile and another path has to be tried.For example&ndash;this compound selector:
<pre>div div div div{<br />
  ...<br />
}<&#47;pre><br />
Means the rules apply to a <code>
<div><&#47;code> who is the descendant of 3 divs. Suppose you want to check if the rule applies for a given <code>
<div><&#47;code> element. You choose a certain path up the tree for checking. You may need to traverse the node tree up just to find out there are only two divs and the rule does not apply. You then need to try other paths in the tree.<&#47;li></p>
<li><a id="issue3"><&#47;a>Applying the rules involves quite complex cascade rules that define the hierarchy of the rules.<&#47;li><br />
<&#47;ol><br />
Let's see how the browsers face these issues:</p>
<h3 id="Sharing_style_data">Sharing style data<&#47;h3><br />
WebKit nodes references style objects (RenderStyle) These objects can be shared by nodes in some conditions. The nodes are siblings or cousins and:</p>
<ol>
<li>The elements must be in the same mouse state (e.g., one can't be in :hover while the other isn't)<&#47;li>
<li>Neither element should have an id<&#47;li>
<li>The tag names should match<&#47;li>
<li>The class attributes should match<&#47;li>
<li>The set of mapped attributes must be identical<&#47;li>
<li>The link states must match<&#47;li>
<li>The focus states must match<&#47;li>
<li>Neither element should be affected by attribute selectors, where affected is defined as having any selector match that uses an attribute selector in any position within the selector at all<&#47;li>
<li>There must be no inline style attribute on the elements<&#47;li>
<li>There must be no sibling selectors in use at all. WebCore simply throws a global switch when any sibling selector is encountered and disables style sharing for the entire document when they are present. This includes the + selector and selectors like :first-child and :last-child.<&#47;li><br />
<&#47;ol></p>
<h3 id="Firefox_rule_tree">Firefox rule tree<&#47;h3><br />
Firefox has two extra trees for easier style computation: the rule tree and style context tree. WebKit also has style objects but they are not stored in a tree like the style context tree, only the DOM node points to its relevant style.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image035.png" width="640" height="407" &#47;><br />
<figcaption>Figure : Firefox style context tree(<a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#2_2">2.2<&#47;a>)<&#47;figcaption><&#47;figure>The style contexts contain end values. The values are computed by applying all the matching rules in the correct order and performing manipulations that transform them from logical to concrete values. For example, if the logical value is a percentage of the screen it will be calculated and transformed to absolute units. The rule tree idea is really clever. It enables sharing these values between nodes to avoid computing them again. This also saves space.</p>
<p>All the matched rules are stored in a tree. The bottom nodes in a path have higher priority. The tree contains all the paths for rule matches that were found. Storing the rules is done lazily. The tree isn't calculated at the beginning for every node, but whenever a node style needs to be computed the computed paths are added to the tree.</p>
<p>The idea is to see the tree paths as words in a lexicon. Lets say we already computed this rule tree:</p>
<figure><img title="" alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;tree.png" width="400" height="261" align="" border="0" &#47;><&#47;figure>Suppose we need to match rules for another element in the content tree, and find out the matched rules (in the correct order) are B-E-I. We already have this path in the tree because we already computed path A-B-E-I-L. We will now have less work to do.Let's see how the tree saves us work.</p>
<h3 id="Division_into_structs">Division into structs<&#47;h3><br />
The style contexts are divided into structs. Those structs contain style information for a certain category like border or color. All the properties in a struct are either inherited or non inherited. Inherited properties are properties that unless defined by the element, are inherited from its parent. Non inherited properties (called "reset" properties) use default values if not defined.</p>
<p>The tree helps us by caching entire structs (containing the computed end values) in the tree. The idea is that if the bottom node didn't supply a definition for a struct, a cached struct in an upper node can be used.</p>
<h3 id="Computing_the_style_contexts_using_the_rule_tree">Computing the style contexts using the rule tree<&#47;h3><br />
When computing the style context for a certain element, we first compute a path in the rule tree or use an existing one. We then begin to apply the rules in the path to fill the structs in our new style context. We start at the bottom node of the path&ndash;the one with the highest precedence (usually the most specific selector) and traverse the tree up until our struct is full. If there is no specification for the struct in that rule node, then we can greatly optimize&ndash;we go up the tree until we find a node that specifies it fully and simply point to it&ndash;that's the best optimization&ndash;the entire struct is shared. This saves computation of end values and memory.<br />
If we find partial definitions we go up the tree until the struct is filled.</p>
<p>If we didn't find any definitions for our struct then, in case the struct is an "inherited" type, we point to the struct of our parent in the <b>context tree<&#47;b>. In this case we also succeeded in sharing structs. If it's a reset struct then default values will be used.</p>
<p>If the most specific node does add values then we need to do some extra calculations for transforming it to actual values. We then cache the result in the tree node so it can be used by children.</p>
<p>In case an element has a sibling or a brother that points to the same tree node then the <b>entire style context<&#47;b> can be shared between them.</p>
<p>Lets see an example: Suppose we have this HTML</p>
<pre><html><br />
  <body></p>
<div class="err" id="div1">
<p>
        this is a <span class="big"> big error <&#47;span><br />
        this is also a<br />
        <span class="big"> very  big  error<&#47;span> error<br />
      <&#47;p><br />
    <&#47;div></p>
<div class="err" id="div2">another error<&#47;div><br />
  <&#47;body><br />
<&#47;html><&#47;pre><br />
And the following rules:</p>
<ol>
<li>div {margin:5px;color:black}<&#47;li>
<li>.err {color:red}<&#47;li>
<li>.big {margin-top:3px}<&#47;li>
<li>div span {margin-bottom:4px}<&#47;li>
<li>#div1 {color:blue}<&#47;li>
<li>#div2 {color:green}<&#47;li><br />
<&#47;ol><br />
To simplify things let's say we need to fill out only two structs: the color struct and the margin struct. The color struct contains only one member: the color The margin struct contains the four sides.<br />
The resulting rule tree will look like this (the nodes are marked with the node name: the number of the rule they point at):</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image027.png" width="500" height="294" &#47;><br />
<figcaption>Figure : The rule tree<&#47;figcaption><&#47;figure>The context tree will look like this (node name: rule node they point to):</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image029.png" width="400" height="305" &#47;><br />
<figcaption> Figure : The context tree<&#47;figcaption><&#47;figure>Suppose we parse the HTML and get to the second
<div> tag. We need to create a style context for this node and fill its style structs.<br />
We will match the rules and discover that the matching rules for the
<div> are 1, 2 and 6. This means there is already an existing path in the tree that our element can use and we just need to add another node to it for rule 6 (node F in the rule tree).<br />
We will create a style context and put it in the context tree. The new style context will point to node F in the rule tree.</p>
<p>We now need to fill the style structs. We will begin by filling out the margin struct. Since the last rule node (F) doesn't add to the margin struct, we can go up the tree until we find a cached struct computed in a previous node insertion and use it. We will find it on node B, which is the uppermost node that specified margin rules.</p>
<p>We do have a definition for the color struct, so we can't use a cached struct. Since color has one attribute we don't need to go up the tree to fill other attributes. We will compute the end value (convert string to RGB etc) and cache the computed struct on this node.</p>
<p>The work on the second <span> element is even easier. We will match the rules and come to the conclusion that it points to rule G, like the previous span. Since we have siblings that point to the same node, we can share the entire style context and just point to the context of the previous span.</p>
<p>For structs that contain rules that are inherited from the parent, caching is done on the context tree (the color property is actually inherited, but Firefox treats it as reset and caches it on the rule tree).<br />
For instance if we added rules for fonts in a paragraph:</p>
<pre>p {font-family: Verdana; font size: 10px; font-weight: bold}<&#47;pre><br />
Then the paragraph element, which is a child of the div in the context tree, could have shared the same font struct as his parent. This is if no font rules where specified for the paragraph.In WebKit, who does not have a rule tree, the matched declarations are traversed four times. First non-important high priority properties are applied (properties that should be applied first because others depend on them, such as display), then high priority important, then normal priority non-important, then normal priority important rules. This means that properties that appear multiple times will be resolved according to the correct cascade order. The last wins.</p>
<p>So to summarize: sharing the style objects (entirely or some of the structs inside them) solves issues <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#issue1">1<&#47;a> and <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#issue3">3<&#47;a>. The Firefox rule tree also helps in applying the properties in the correct order.</p>
<h3 id="Manipulating_the_rules_for_an_easy_match">Manipulating the rules for an easy match<&#47;h3><br />
There are several sources for style rules:</p>
<ul>
<li>CSS rules, either in external style sheets or in style elements.
<pre>p {color: blue}<&#47;pre><br />
<&#47;li></p>
<li>Inline style attributes like
<pre>
<p style="color: blue" &#47;><&#47;pre><br />
<&#47;li></p>
<li>HTML visual attributes (which are mapped to relevant style rules)
<pre>
<p bgcolor="blue" &#47;><&#47;pre><br />
<&#47;li><br />
<&#47;ul><br />
The last two are easily matched to the element since he owns the style attributes and HTML attributes can be mapped using the element as the key.</p>
<p>As noted previously in <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#issue2">issue #2<&#47;a>, the CSS rule matching can be trickier. To solve the difficulty, the rules are manipulated for easier access.</p>
<p>After parsing the style sheet, the rules are added to one of several hash maps, according to the selector. There are maps by id, by class name, by tag name and a general map for anything that doesn't fit into those categories. If the selector is an id, the rule will be added to the id map, if it's a class it will be added to the class map etc.<br />
This manipulation makes it much easier to match rules. There is no need to look in every declaration: we can extract the relevant rules for an element from the maps. This optimization eliminates 95+% of the rules, so that they need not even be considered during the matching process(<a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#4_1">4.1<&#47;a>).</p>
<p>Let's see for example the following style rules:</p>
<pre>p.error {color: red}<br />
#messageDiv {height: 50px}<br />
div {margin: 5px}<&#47;pre><br />
The first rule will be inserted into the class map. The second into the id map and the third into the tag map.<br />
For the following HTML fragment;</p>
<pre>
<p class="error">an error occurred <&#47;p></p>
<div id=" messageDiv">this is a message<&#47;div><&#47;pre><br />
We will first try to find rules for the p element. The class map will contain an "error" key under which the rule for "p.error" is found. The div element will have relevant rules in the id map (the key is the id) and the tag map. So the only work left is finding out which of the rules that were extracted by the keys really match.<br />
For example if the rule for the div was</p>
<pre>table div {margin: 5px}<&#47;pre><br />
it will still be extracted from the tag map, because the key is the rightmost selector, but it would not match our div element, who does not have a table ancestor.Both WebKit and Firefox do this manipulation.</p>
<h3 id="Applying_the_rules_in_the_correct_cascade_order">Applying the rules in the correct cascade order<&#47;h3><br />
The style object has properties corresponding to every visual attribute (all CSS attributes but more generic). If the property is not defined by any of the matched rules, then some properties can be inherited by the parent element style object. Other properties have default values.</p>
<p>The problem begins when there is more than one definition&ndash;here comes the cascade order to solve the issue.</p>
<h3 id="Style_sheet_cascade_order">Style sheet cascade order<&#47;h3><br />
A declaration for a style property can appear in several style sheets, and several times inside a style sheet. This means the order of applying the rules is very important. This is called the "cascade" order. According to CSS2 spec, the cascade order is (from low to high):</p>
<ol>
<li>Browser declarations<&#47;li>
<li>User normal declarations<&#47;li>
<li>Author normal declarations<&#47;li>
<li>Author important declarations<&#47;li>
<li>User important declarations<&#47;li><br />
<&#47;ol><br />
The browser declarations are least important and the user overrides the author only if the declaration was marked as important. Declarations with the same order will be sorted by <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#Specificity">specificity<&#47;a> and then the order they are specified. The HTML visual attributes are translated to matching CSS declarations . They are treated as author rules with low priority.</p>
<h3 id="Specificity">Specificity<&#47;h3><br />
The selector specificity is defined by the <a href="http:&#47;&#47;www.w3.org&#47;TR&#47;CSS2&#47;cascade.html#specificity">CSS2 specification<&#47;a> as follows:</p>
<ul>
<li>count 1 if the declaration it is from is a 'style' attribute rather than a rule with a selector, 0 otherwise (= a)<&#47;li>
<li>count the number of ID attributes in the selector (= b)<&#47;li>
<li>count the number of other attributes and pseudo-classes in the selector (= c)<&#47;li>
<li>count the number of element names and pseudo-elements in the selector (= d)<&#47;li><br />
<&#47;ul><br />
Concatenating the four numbers a-b-c-d (in a number system with a large base) gives the specificity.The number base you need to use is defined by the highest count you have in one of the categories.<br />
For example, if a=14 you can use hexadecimal base. In the unlikely case where a=17 you will need a 17 digits number base. The later situation can happen with a selector like this: html body div div p ... (17 tags in your selector.. not very likely).</p>
<p>Some examples:</p>
<pre> *             {}  &#47;* a=0 b=0 c=0 d=0 -> specificity = 0,0,0,0 *&#47;<br />
 li            {}  &#47;* a=0 b=0 c=0 d=1 -> specificity = 0,0,0,1 *&#47;<br />
 li:first-line {}  &#47;* a=0 b=0 c=0 d=2 -> specificity = 0,0,0,2 *&#47;<br />
 ul li         {}  &#47;* a=0 b=0 c=0 d=2 -> specificity = 0,0,0,2 *&#47;<br />
 ul ol+li      {}  &#47;* a=0 b=0 c=0 d=3 -> specificity = 0,0,0,3 *&#47;<br />
 h1 + *[rel=up]{}  &#47;* a=0 b=0 c=1 d=1 -> specificity = 0,0,1,1 *&#47;<br />
 ul ol li.red  {}  &#47;* a=0 b=0 c=1 d=3 -> specificity = 0,0,1,3 *&#47;<br />
 li.red.level  {}  &#47;* a=0 b=0 c=2 d=1 -> specificity = 0,0,2,1 *&#47;<br />
 #x34y         {}  &#47;* a=0 b=1 c=0 d=0 -> specificity = 0,1,0,0 *&#47;<br />
 style=""          &#47;* a=1 b=0 c=0 d=0 -> specificity = 1,0,0,0 *&#47;<&#47;pre></p>
<h3 id="Sorting_the_rules">Sorting the rules<&#47;h3><br />
After the rules are matched, they are sorted according to the cascade rules. WebKit uses bubble sort for small lists and merge sort for big ones. WebKit implements sorting by overriding the ">" operator for the rules:</p>
<pre>static bool operator >(CSSRuleData&amp; r1, CSSRuleData&amp; r2)<br />
{<br />
    int spec1 = r1.selector()->specificity();<br />
    int spec2 = r2.selector()->specificity();<br />
    return (spec1 == spec2) : r1.position() > r2.position() : spec1 > spec2;<br />
}<&#47;pre></p>
<h3 id="Gradual_process">Gradual process<&#47;h3><br />
WebKit uses a flag that marks if all top level style sheets (including @imports) have been loaded. If the style is not fully loaded when attaching, place holders are used and it is marked in the document, and they will be recalculated once the style sheets were loaded.</p>
<h2 id="Layout">Layout<&#47;h2><br />
When the renderer is created and added to the tree, it does not have a position and size. Calculating these values is called layout or reflow.</p>
<p>HTML uses a flow based layout model, meaning that most of the time it is possible to compute the geometry in a single pass. Elements later ``in the flow'' typically do not affect the geometry of elements that are earlier ``in the flow'', so layout can proceed left-to-right, top-to-bottom through the document. There are exceptions: for example, HTML tables may require more than one pass (<a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#3_5">3.5<&#47;a>).</p>
<p>The coordinate system is relative to the root frame. Top and left coordinates are used.</p>
<p>Layout is a recursive process. It begins at the root renderer, which corresponds to the <code><html><&#47;code> element of the HTML document. Layout continues recursively through some or all of the frame hierarchy, computing geometric information for each renderer that requires it.</p>
<p>The position of the root renderer is 0,0 and its dimensions are the viewport&ndash;the visible part of the browser window.All renderers have a "layout" or "reflow" method, each renderer invokes the layout method of its children that need layout.</p>
<h3 id="Dirty_bit_system">Dirty bit system<&#47;h3><br />
In order not to do a full layout for every small change, browsers use a "dirty bit" system. A renderer that is changed or added marks itself and its children as "dirty": needing layout.</p>
<p>There are two flags: "dirty", and "children are dirty" which means that although the renderer itself may be OK, it has at least one child that needs a layout.</p>
<h3 id="Global_and_incremental_layout">Global and incremental layout<&#47;h3><br />
Layout can be triggered on the entire render tree&ndash;this is "global" layout. This can happen as a result of:</p>
<ol>
<li>A global style change that affects all renderers, like a font size change.<&#47;li>
<li>As a result of a screen being resized<&#47;li><br />
<&#47;ol><br />
Layout can be incremental, only the dirty renderers will be laid out (this can cause some damage which will require extra layouts).<br />
Incremental layout is triggered (asynchronously) when renderers are dirty. For example when new renderers are appended to the render tree after extra content came from the network and was added to the DOM tree.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;reflow.png" width="326" height="341" &#47;><br />
<figcaption> Figure : Incremental layout&ndash;only dirty renderers and their children are laid out (<a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#3_6">3.6<&#47;a>)<&#47;figcaption><&#47;figure></p>
<h3 id="Asynchronous_and_Synchronous_layout">Asynchronous and Synchronous layout<&#47;h3><br />
Incremental layout is done asynchronously. Firefox queues "reflow commands" for incremental layouts and a scheduler triggers batch execution of these commands. WebKit also has a timer that executes an incremental layout&ndash;the tree is traversed and "dirty" renderers are layout out.<br />
Scripts asking for style information, like "offsetHeight" can trigger incremental layout synchronously.<br />
Global layout will usually be triggered synchronously.<br />
Sometimes layout is triggered as a callback after an initial layout because some attributes, like the scrolling position changed.</p>
<h3 id="Optimizations">Optimizations<&#47;h3><br />
When a layout is triggered by a "resize" or a change in the renderer position(and not size), the renders sizes are taken from a cache and not recalculated..<br />
In some cases only a sub tree is modified and layout does not start from the root. This can happen in cases where the change is local and does not affect its surroundings&ndash;like text inserted into text fields (otherwise every keystroke would trigger a layout starting from the root).</p>
<h3 id="The_layout_process">The layout process<&#47;h3><br />
The layout usually has the following pattern:</p>
<ol>
<li>Parent renderer determines its own width.<&#47;li>
<li>Parent goes over children and:
<ol>
<li>Place the child renderer (sets its x and y).<&#47;li>
<li>Calls child layout if needed&ndash;they are dirty or we are in a global layout, or for some other reason&ndash;which calculates the child's height.<&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li>Parent uses children's accumulative heights and the heights of margins and padding to set its own height&ndash;this will be used by the parent renderer's parent.<&#47;li>
<li>Sets its dirty bit to false.<&#47;li><br />
<&#47;ol><br />
Firefox uses a "state" object(nsHTMLReflowState) as a parameter to layout (termed "reflow"). Among others the state includes the parents width.<br />
The output of the Firefox layout is a "metrics" object(nsHTMLReflowMetrics). It will contain the renderer computed height.</p>
<h3 id="Width_calculation">Width calculation<&#47;h3><br />
The renderer's width is calculated using the container block's width, the renderer's style "width" property, the margins and borders.<br />
For example the width of the following div:</p>
<pre>
<div style="width: 30%"&#47;><&#47;pre><br />
Would be calculated by WebKit as the following(class RenderBox method calcWidth):</p>
<ul>
<li>The container width is the maximum of the containers availableWidth and 0. The availableWidth in this case is the contentWidth which is calculated as:
<pre>clientWidth() - paddingLeft() - paddingRight()<&#47;pre><br />
clientWidth and clientHeight represent the interior of an object excluding border and scrollbar.<&#47;li></p>
<li>The elements width is the "width" style attribute. It will be calculated as an absolute value by computing the percentage of the container width.<&#47;li>
<li>The horizontal borders and paddings are now added.<&#47;li><br />
<&#47;ul><br />
So far this was the calculation of the "preferred width". Now the minimum and maximum widths will be calculated.<br />
If the preferred width is greater then the maximum width, the maximum width is used. If it is less then the minimum width (the smallest unbreakable unit) then the minimum width is used.The values are cached in case a layout is needed, but the width does not change.</p>
<h3 id="Line_Breaking">Line Breaking<&#47;h3><br />
When a renderer in the middle of a layout decides that it needs to break, the renderer stops and propagates to the layout's parent that it needs to be broken. The parent creates the extra renderers and calls layout on them.</p>
<h2 id="Painting">Painting<&#47;h2><br />
In the painting stage, the render tree is traversed and the renderer's "paint()" method is called to display content on the screen. Painting uses the UI infrastructure component.</p>
<h3 id="Global_and_Incremental">Global and Incremental<&#47;h3><br />
Like layout, painting can also be global&ndash;the entire tree is painted&ndash;or incremental. In incremental painting, some of the renderers change in a way that does not affect the entire tree. The changed renderer invalidates its rectangle on the screen. This causes the OS to see it as a "dirty region" and generate a "paint" event. The OS does it cleverly and coalesces several regions into one. In Chrome it is more complicated because the renderer is in a different process then the main process. Chrome simulates the OS behavior to some extent. The presentation listens to these events and delegates the message to the render root. The tree is traversed until the relevant renderer is reached. It will repaint itself (and usually its children).</p>
<h3 id="The_painting_order">The painting order<&#47;h3><br />
<a href="http:&#47;&#47;www.w3.org&#47;TR&#47;CSS21&#47;zindex.html">CSS2 defines the order of the painting process<&#47;a>. This is actually the order in which the elements are stacked in the <a href="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;#stackingcontext">stacking contexts<&#47;a>. This order affects painting since the stacks are painted from back to front. The stacking order of a block renderer is:</p>
<ol>
<li>background color<&#47;li>
<li>background image<&#47;li>
<li>border<&#47;li>
<li>children<&#47;li>
<li>outline<&#47;li><br />
<&#47;ol></p>
<h3 id="Firefox_display_list">Firefox display list<&#47;h3><br />
Firefox goes over the render tree and builds a display list for the painted rectangular. It contains the renderers relevant for the rectangular, in the right painting order (backgrounds of the renderers, then borders etc). That way the tree needs to be traversed only once for a repaint instead of several times&ndash;painting all backgrounds, then all images, then all borders etc.Firefox optimizes the process by not adding elements that will be hidden, like elements completely beneath other opaque elements.</p>
<h4 id="WebKit_rectangle_storage">WebKit rectangle storage<&#47;h4><br />
Before repainting, WebKit saves the old rectangle as a bitmap. It then paints only the delta between the new and old rectangles.</p>
<h3 id="Dynamic_changes">Dynamic changes<&#47;h3><br />
The browsers try to do the minimal possible actions in response to a change. So changes to an elements color will cause only repaint of the element. Changes to the element position will cause layout and repaint of the element, its children and possibly siblings. Adding a DOM node will cause layout and repaint of the node. Major changes, like increasing font size of the "html" element, will cause invalidation of caches, relayout and repaint of the entire tree.</p>
<h3 id="The_rendering_engines_threads">The rendering engine's threads<&#47;h3><br />
The rendering engine is single threaded. Almost everything, except network operations, happens in a single thread. In Firefox and Safari this is the main thread of the browser. In Chrome it's the tab process main thread.<br />
Network operations can be performed by several parallel threads. The number of parallel connections is limited (usually 2&ndash;6 connections).</p>
<h3 id="Event_loop">Event loop<&#47;h3><br />
The browser main thread is an event loop. It's an infinite loop that keeps the process alive. It waits for events (like layout and paint events) and processes them. This is Firefox code for the main event loop:</p>
<pre>while (!mExiting)<br />
    NS_ProcessNextEvent(thread);<&#47;pre></p>
<h2 id="css">CSS2 visual model<&#47;h2></p>
<h3 id="The_canvas">The canvas<&#47;h3><br />
According to the <a href="http:&#47;&#47;www.w3.org&#47;TR&#47;CSS21&#47;intro.html#processing-model">CSS2 specification<&#47;a>, the term canvas describes "the space where the formatting structure is rendered": where the browser paints the content. The canvas is infinite for each dimension of the space but browsers choose an initial width based on the dimensions of the viewport.</p>
<p>According to <a href="http:&#47;&#47;www.w3.org&#47;TR&#47;CSS2&#47;zindex.html">www.w3.org&#47;TR&#47;CSS2&#47;zindex.html<&#47;a>, the canvas is transparent if contained within another, and given a browser defined color if it is not.</p>
<h3 id="CSS_Box_model">CSS Box model<&#47;h3><br />
The <a href="http:&#47;&#47;www.w3.org&#47;TR&#47;CSS2&#47;box.html">CSS box model<&#47;a> describes the rectangular boxes that are generated for elements in the document tree and laid out according to the visual formatting model.<br />
Each box has a content area (e.g. text, an image, etc.) and optional surrounding padding, border, and margin areas.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image046.jpg" width="509" height="348" &#47;><br />
<figcaption> Figure : CSS2 box model<&#47;figcaption><&#47;figure>Each node generates 0..n such boxes.<br />
All elements have a "display" property that determines the type of box that will be generated. Examples:</p>
<pre>block: generates a block box.<br />
inline: generates one or more inline boxes.<br />
none: no box is generated.<&#47;pre><br />
The default is inline but the browser style sheet may set other defaults. For example: the default display for the "div" element is block.<br />
You can find a default style sheet example here: <a href="http:&#47;&#47;www.w3.org&#47;TR&#47;CSS2&#47;sample.html">www.w3.org&#47;TR&#47;CSS2&#47;sample.html<&#47;a></p>
<h3 id="Positioning_scheme">Positioning scheme<&#47;h3><br />
There are three schemes:</p>
<ol>
<li>Normal: the object is positioned according to its place in the document. This means its place in the render tree is like its place in the DOM tree and laid out according to its box type and dimensions<&#47;li>
<li>Float: the object is first laid out like normal flow, then moved as far left or right as possible<&#47;li>
<li>Absolute: the object is put in the render tree in a different place than in the DOM tree<&#47;li><br />
<&#47;ol><br />
The positioning scheme is set by the "position" property and the "float" attribute.</p>
<ul>
<li>static and relative cause a normal flow<&#47;li>
<li>absolute and fixed cause absolute positioning<&#47;li><br />
<&#47;ul><br />
In static positioning no position is defined and the default positioning is used. In the other schemes, the author specifies the position: top, bottom, left, right.The way the box is laid out is determined by:</p>
<ul>
<li>Box type<&#47;li>
<li>Box dimensions<&#47;li>
<li>Positioning scheme<&#47;li>
<li>External information such as image size and the size of the screen<&#47;li><br />
<&#47;ul></p>
<h3 id="Box_types">Box types<&#47;h3><br />
Block box: forms a block&ndash;has its own rectangle in the browser window.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image057.png" width="150" height="127" &#47;><br />
<figcaption> Figure : Block box<&#47;figcaption><&#47;figure>Inline box: does not have its own block, but is inside a containing block.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image059.png" width="300" height="233" &#47;><br />
<figcaption>Figure : Inline boxes<&#47;figcaption><&#47;figure>Blocks are formatted vertically one after the other. Inlines are formatted horizontally.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image061.png" width="350" height="324" &#47;><br />
<figcaption>Figure : Block and Inline formatting<&#47;figcaption><&#47;figure>Inline boxes are put inside lines or "line boxes". The lines are at least as tall as the tallest box but can be taller, when the boxes are aligned "baseline"&ndash;meaning the bottom part of an element is aligned at a point of another box other then the bottom. If the container width is not enough, the inlines will be put on several lines. This is usually what happens in a paragraph.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image063.png" width="400" height="277" &#47;><br />
<figcaption>Figure: Lines<&#47;figcaption><&#47;figure></p>
<h3 id="Positioning">Positioning<&#47;h3></p>
<h4 id="Relative">Relative<&#47;h4><br />
Relative positioning&ndash;positioned like usual and then moved by the required delta.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image065.png" width="500" height="261" &#47;><br />
<figcaption>Figure: Relative positioning<&#47;figcaption><&#47;figure></p>
<h4 id="Floats">Floats<&#47;h4><br />
A float box is shifted to the left or right of a line. The interesting feature is that the other boxes flow around it The HTML:</p>
<pre>
<p>
  <img style="float: right" src="images&#47;image.gif" width="100" height="100"><br />
  Lorem ipsum dolor sit amet, consectetuer...<br />
<&#47;p><&#47;pre><br />
Will look like:</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image067.png" width="444" height="203" &#47;><br />
<figcaption>Figure : Float<&#47;figcaption><&#47;figure></p>
<h4 id="Absolute_and_fixed">Absolute and fixed<&#47;h4><br />
The layout is defined exactly regardless of the normal flow. The element does not participate in the normal flow. The dimensions are relative to the container. In fixed, the container is the viewport.</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image069.png" width="500" height="343" &#47;><br />
<figcaption>Figure : Fixed positioning<&#47;figcaption><&#47;figure>Note: the fixed box will not move even when the document is scrolled!</p>
<h3 id="Layered_representation">Layered representation<&#47;h3><br />
This is specified by the z-index CSS property. It represents the third dimension of the box: its position along the "z axis".</p>
<p>The boxes are divided into <a id="stackingcontext"><&#47;a>stacks (called stacking contexts). In each stack the back elements will be painted first and the forward elements on top, closer to the user. In case of overlap the foremost element will hide the former element.<br />
The stacks are ordered according to the z-index property. Boxes with "z-index" property form a local stack. The viewport has the outer stack.</p>
<p>Example:</p>
<pre>
<style type="text&#47;css">
      div {<br />
        position: absolute;<br />
        left: 2in;<br />
        top: 2in;<br />
      }<br />
<&#47;style></p>
<p><div<br />
         style="z-index: 3;background-color:red; width: 1in; height: 1in; "><br />
    <&#47;div></p>
<div<br />
         style="z-index: 1;background-color:green;width: 2in; height: 2in;"><br />
    <&#47;div><br />
 <&#47;p><&#47;pre><br />
The result will be this:</p>
<figure><img alt="" src="http:&#47;&#47;www.html5rocks.com&#47;en&#47;tutorials&#47;internals&#47;howbrowserswork&#47;image071.png" width="254" height="227" &#47;><br />
<figcaption>Figure : Fixed positioning<&#47;figcaption><&#47;figure>Although the red div precedes the green one in the markup, and would have been painted before in the regular flow, the z-index property is higher, so it is more forward in the stack held by the root box.</p>
<h2 id="Resources">Resources<&#47;h2></p>
<div>
<ol>
<li id="1">Browser architecture
<ol>
<li id="1_1">Grosskurth, Alan. <a href="http:&#47;&#47;grosskurth.ca&#47;papers&#47;browser-refarch.pdf">A Reference Architecture for Web Browsers (pdf)<&#47;a><&#47;li>
<li id="1_2">Gupta, Vineet. <a href="http:&#47;&#47;www.vineetgupta.com&#47;2010&#47;11&#47;how-browsers-work-part-1-architecture&#47;">How Browsers Work&ndash;Part 1&ndash;Architecture<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li id="2">Parsing
<ol>
<li id="2_1">Aho, Sethi, Ullman, Compilers: Principles, Techniques, and Tools (aka the "Dragon book"), Addison-Wesley, 1986<&#47;li>
<li id="2_2">Rick Jelliffe. <a href="http:&#47;&#47;broadcast.oreilly.com&#47;2009&#47;05&#47;the-bold-and-the-beautiful-two.html">The Bold and the Beautiful: two new drafts for HTML 5.<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li id="3">Firefox
<ol>
<li id="3_1">L. David Baron, <a href="http:&#47;&#47;dbaron.org&#47;talks&#47;2008-11-12-faster-html-and-css&#47;slide-6.xhtml">Faster HTML and CSS: Layout Engine Internals for Web Developers.<&#47;a><&#47;li>
<li id="3_2">L. David Baron, <a href="http:&#47;&#47;www.youtube.com&#47;watch?v=a2_6bGNZ7bA">Faster HTML and CSS: Layout Engine Internals for Web Developers (Google tech talk video)<&#47;a><&#47;li>
<li id="3_3">L. David Baron, <a href="http:&#47;&#47;www.mozilla.org&#47;newlayout&#47;doc&#47;layout-2006-07-12&#47;slide-6.xhtml">Mozilla's Layout Engine<&#47;a><&#47;li>
<li id="3_4">L. David Baron, <a href="http:&#47;&#47;www.mozilla.org&#47;newlayout&#47;doc&#47;style-system.html">Mozilla Style System Documentation<&#47;a><&#47;li>
<li id="3_5">Chris Waterson, <a href="http:&#47;&#47;www.mozilla.org&#47;newlayout&#47;doc&#47;reflow.html">Notes on HTML Reflow<&#47;a><&#47;li>
<li id="3_6">Chris Waterson, <a href="http:&#47;&#47;www.mozilla.org&#47;newlayout&#47;doc&#47;gecko-overview.htm">Gecko Overview<&#47;a><&#47;li>
<li id="3_7">Alexander Larsson, <a href="https:&#47;&#47;developer.mozilla.org&#47;en&#47;The_life_of_an_HTML_HTTP_request">The life of an HTML HTTP request<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li id="4">WebKit
<ol>
<li id="4_1">David Hyatt, <a href="http:&#47;&#47;weblogs.mozillazine.org&#47;hyatt&#47;archives&#47;cat_safari.html">Implementing CSS(part 1)<&#47;a><&#47;li>
<li id="4_2">David Hyatt, <a href="http:&#47;&#47;weblogs.mozillazine.org&#47;hyatt&#47;WebCore&#47;chapter2.html">An Overview of WebCore<&#47;a><&#47;li>
<li id="4_3">David Hyatt, <a href="http:&#47;&#47;webkit.org&#47;blog&#47;114&#47;">WebCore Rendering<&#47;a><&#47;li>
<li id="4_5">David Hyatt, <a href="http:&#47;&#47;webkit.org&#47;blog&#47;66&#47;the-fouc-problem&#47;">The FOUC Problem<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li id="5">W3C Specifications
<ol>
<li id="5_1"><a href="http:&#47;&#47;www.w3.org&#47;TR&#47;html4&#47;">HTML 4.01 Specification<&#47;a><&#47;li>
<li id="5_2"><a href="http:&#47;&#47;dev.w3.org&#47;html5&#47;spec&#47;Overview.html">W3C HTML5 Specification<&#47;a><&#47;li>
<li id="5_3"><a href="http:&#47;&#47;www.w3.org&#47;TR&#47;CSS2&#47;">Cascading Style Sheets Level 2 Revision 1 (CSS 2.1) Specification<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li></p>
<li>Browsers build instructions
<ol>
<li>Firefox. <a href="https:&#47;&#47;developer.mozilla.org&#47;en&#47;Build_Documentation">https:&#47;&#47;developer.mozilla.org&#47;en&#47;Build_Documentation<&#47;a><&#47;li>
<li>WebKit. <a href="http:&#47;&#47;webkit.org&#47;building&#47;build.html">http:&#47;&#47;webkit.org&#47;building&#47;build.html<&#47;a><&#47;li><br />
<&#47;ol><br />
<&#47;li><br />
<&#47;ol><br />
<&#47;div><br />
<&#47;div></p>
<aside><a href="http:&#47;&#47;taligarsiel.com&#47;">Tali Garsiel<&#47;a> is a developer in Israel. She started as a web developer in 2000, and became aquainted with Netscape's "evil" layer model. Just like Richard Feynmann, she had a fascination for figuring out how things work so she began digging into browser internals and documenting what she found. Tali also has published a short <a href="http:&#47;&#47;taligarsiel.com&#47;ClientSidePerformance.html">guide on client-side performance<&#47;a>.<&#47;aside></p>
