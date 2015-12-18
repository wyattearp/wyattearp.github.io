---
id: 458
title: 'Python Zlib &#8230; Son I Am Disapoint'
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=458
permalink: /2013/08/19/python-zlib-son-i-am-disapoint/
categories:
  - Rants
---
Every now and then, I find myself digging through some arbitrarily compressed binary and in IDA, when you have to keep doing it over and over again, you should write a script or a loader to handle that (as any good programmer would). So I started wiring up a loader in python and thought that I&#8217;d use the zlib library to decompress things &#8230; boy was I wrong.  Not only did zlib fail to actually work correctly (because it can&#8217;t actually handle ZIP files, more on that in a moment), but the error messages were basically the same low-level messages you got out of zlib&#8217;s internal functions. Really? This is the best we can do right now? What I tried:

<div class="codesnip-container" >
  [wyatt@lazarus:~/Downloads]$ zip derp.zip Untitled\ drawing.png<br /> [wyatt@lazarus:~/Downloads]$ cat Whatsnew.txt derp.zip > file.out<br /> [wyatt@lazarus:~/Downloads]$ python<br /> Python 2.7.3 (default, Apr 10 2013, 06:20:15)<br /> [GCC 4.6.3] on linux2<br /> Type &#8220;help&#8221;, &#8220;copyright&#8221;, &#8220;credits&#8221; or &#8220;license&#8221; for more information.
</div>

<div class="codesnip-container" >
  <div class="python codesnip">
    <span class="kw1">import</span> <span class="kw3">struct</span><br /> <span class="kw1">import</span> <span class="kw3">zlib</span><br /> f = <span class="kw2">open</span><span class="br0">&#40;</span><span class="st0">&#8216;file.out&#8217;</span>,<span class="st0">&#8216;rb&#8217;</span><span class="br0">&#41;</span><br /> c = f.<span class="me1">read</span><span class="br0">&#40;</span><span class="br0">&#41;</span><br /> f.<span class="me1">close</span><span class="br0">&#40;</span><span class="br0">&#41;</span><br /> offset = c.<span class="me1">find</span><span class="br0">&#40;</span><span class="st0">&#8216;PK&#8217;</span><span class="br0">&#41;</span><br /> uncmp_size = <span class="kw3">struct</span>.<span class="me1">unpack</span><span class="br0">&#40;</span><span class="st0">"<l"</span>,c<span class="br0">&#91;</span>offset+<span class="nu0">22</span>:offset+<span class="nu0">22</span>+<span class="nu0">4</span><span class="br0">&#93;</span><span class="br0">&#41;</span><br /> z = <span class="kw3">zlib</span>.<span class="me1">decompressobj</span><span class="br0">&#40;</span><span class="br0">&#41;</span><br /> out = z.<span class="me1">decompress</span><span class="br0">&#40;</span>c<span class="br0">&#91;</span>offset:<span class="br0">&#93;</span>,<span class="kw2">int</span><span class="br0">&#40;</span>uncmp_size<span class="br0">&#91;</span><span class="nu0"></span><span class="br0">&#93;</span><span class="br0">&#41;</span><span class="br0">&#41;</span><br /> Traceback <span class="br0">&#40;</span>most recent call last<span class="br0">&#41;</span>:<br /> File <span class="st0">""</span>, line <span class="nu0">1</span>, <span class="kw1">in</span><br /> <span class="kw3">zlib</span>.<span class="me1">error</span>: Error &#8211;<span class="nu0">3</span> <span class="kw1">while</span> decompressing: incorrect header check
  </div>
</div>

This of course fails because zlib doesn&#8217;t actually work right with zip files (you&#8217;ll find a vauge note to such things in the ) and of course &#8230; I should have really known that ZIP isn&#8217;t actually zlib. Instead of trying to be clever, I decided to give up and be lazy. What actually worked:

<div class="codesnip-container" >
  <div class="python codesnip">
    <span class="kw1">import</span> <span class="kw3">subprocess</span><br /> <span class="kw3">subprocess</span>.<span class="me1">call</span><span class="br0">&#40;</span><span class="br0">&#91;</span><span class="st0">&#8216;7z&#8217;</span>,<span class="st0">&#8216;e&#8217;</span>,<span class="st0">&#8216;file.out&#8217;</span><span class="br0">&#93;</span><span class="br0">&#41;</span>
  </div>
</div>

<div class="codesnip-container" >
  7-Zip [64] 9.20 Copyright (c) 1999-2010 Igor Pavlov 2010-11-18<br /> p7zip Version 9.20 (locale=en_US.UTF-8,Utf16=on,HugeFiles=on,8 CPUs)</p> 
  
  <p>
    Processing archive: file.out
  </p>
  
  <p>
    Extracting Untitled drawing.png
  </p>
  
  <p>
    Everything is Ok
  </p>
  
  <p>
    Size: 24513<br /> Compressed: 22290
  </p>
</div>

So yes &#8230; apparently this is the best we can do with the zlib library.