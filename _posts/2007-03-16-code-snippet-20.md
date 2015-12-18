---
id: 165
title: Code Snippet 2.0
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/2007/03/16/code-snippet-20/
permalink: /2007/03/16/code-snippet-20/
autometa:
  - plugin snippet code lang argc argv languages actionscript
categories:
  - Technology
---
First off, Code Snippet 2.0 is not mine. I didn&#8217;t make it, I won&#8217;t take any credit for it. The original creator was the person who hosted a blog at http://blog.enargi.com/codesnippet/ (which no longer works and is apparently down for good; however, it is GPL.). I came across the plugin awhile ago and and I&#8217;ve decided that I couldn&#8217;t just let it be lost to the ages and I&#8217;ll let it live here as long as I&#8217;m able.

Straight from the readme.txt, Code Snippet 2.0 is is a WordPress plugin for displaying code with highlighting in blog posts. The plugin uses GeSHi syntax highlighter engine. I&#8217;ve seen others, but they&#8217;ve gone the way of the dodo and most of them didn&#8217;t have as many supported languages at Code Snippet 2.0. I also think that Code Snippet does a better job than the Code Auto-escape plugin.

**Install**

  * Download the plugin [here][1].
  * Copy archive to wp-content/plugins directory
  * Extract the zip file
  * When extracted properly you should have following directory structure: /wp-content/plugins/codesnippet
  * Since I&#8217;ve not tore through the code, the plugin will probably not work if extracted/copied in diffrenet directory.
  * Enable the Plugin

**Usage**  
The original author recommended always wrapping your code in a **<pre>** tag; however, I&#8217;ve found that you generally don&#8217;t need to. To use it, simply surround your code with as such and specify your language type:

<div class="codesnip-container" >
  &#91;code lang="c"&#93;<br /> int main(int argc, char** argv) { return 0; }<br /> &#91;/code&#93;
</div>

And you get this:

<div class="codesnip-container" >
  <div class="c codesnip">
    <span class="kw4">int</span> main<span class="br0">&#40;</span><span class="kw4">int</span> argc<span class="sy0">,</span> <span class="kw4">char</span><span class="sy0">**</span> argv<span class="br0">&#41;</span> <span class="br0">&#123;</span> <span class="kw1">return</span> <span class="nu0"></span><span class="sy0">;</span> <span class="br0">&#125;</span>
  </div>
</div>

Or you could do something like:

<div class="codesnip-container" >
  &#91;code lang="php"&#93;<br /> <?php<br /> echo &#8220;Hello World!&#8221;;<br /> ?><br /> &#91;/code&#93
</div>

<div class="codesnip-container" >
  <div class="php codesnip">
    <span class="kw2"><?php</span><br /> &nbsp; &nbsp; &nbsp;<span class="kw1">echo</span> <span class="st0">"Hello World!"</span><span class="sy0">;</span><br /> <span class="sy1">?></span>
  </div>
</div>

If you find a bug in it, drop a comment or an email to wyatt dot neal at gmail and I&#8217;ll try my best to fix it for you.

Also, if you have find that your language isn&#8217;t here and you write your own GeSHi hack to work with it, let me know and I&#8217;ll drop a link on this page so that people can find you. Heck, I&#8217;ll even put it in the archive so the world can share it if you want. Here&#8217;s the list of supported languages:<!--more-->

  
  
<a href="#supportedLang" onclick="javascript: showHide();">Collapse Language List</a>

<div id="supportedLang">
  <ul>
    <li>
      actionscript-french
    </li>
    <li>
      actionscript
    </li>
    <li>
      ada
    </li>
    <li>
      apache
    </li>
    <li>
      applescript
    </li>
    <li>
      asm
    </li>
    <li>
      asp
    </li>
    <li>
      bash
    </li>
    <li>
      caddcl
    </li>
    <li>
      cadlisp
    </li>
    <li>
      c_mac
    </li>
    <li>
      c
    </li>
    <li>
      cpp
    </li>
    <li>
      csharp
    </li>
    <li>
      css-gen
    </li>
    <li>
      css
    </li>
    <li>
      delphi
    </li>
    <li>
      diff
    </li>
    <li>
      div
    </li>
    <li>
      dos
    </li>
    <li>
      d
    </li>
    <li>
      eiffel
    </li>
    <li>
      freebasic
    </li>
    <li>
      gml
    </li>
    <li>
      html4strict
    </li>
    <li>
      ini
    </li>
    <li>
      inno
    </li>
    <li>
      java
    </li>
    <li>
      javascript
    </li>
    <li>
      lisp
    </li>
    <li>
      lua
    </li>
    <li>
      matlab
    </li>
    <li>
      mpasm
    </li>
    <li>
      nsis
    </li>
    <li>
      objc
    </li>
    <li>
      oobas
    </li>
    <li>
      oracle8
    </li>
    <li>
      pascal
    </li>
    <li>
      perl
    </li>
    <li>
      php-brief
    </li>
    <li>
      php
    </li>
    <li>
      python
    </li>
    <li>
      qbasic
    </li>
    <li>
      sdlbasic
    </li>
    <li>
      smarty
    </li>
    <li>
      sql
    </li>
    <li>
      vbnet
    </li>
    <li>
      vb
    </li>
    <li>
      vhdl
    </li>
    <li>
      visualfoxpro
    </li>
    <li>
      xml
    </li>
  </ul>
</div>

 [1]: http://hackerforhire.org/codesnippet21.zip