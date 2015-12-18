---
id: 160
title: 'PHP Alternative to DWR:  Hacker For Hire&#8217;s Solution'
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=160
permalink: /2007/03/06/php-alternative-to-dwr-hacker-for-hires-solution/
autometa:
  - PHP DWR SAJAX JavaScript JSON
categories:
  - Rants
  - Technology
---
I have been scouring the Internet for two days for looking for a suitable [PHP][1] alternative to [DWR][2](read the previous post for more information) and haven&#8217;t found a single one so I&#8217;ve hacked out my own.

I had been looking at [xajax][3] in the hopes that it would get me what I was looking for, but it didn&#8217;t. So the next one I found was [SAJAX][4]. This project appears to be less active than [xajax][5]; however, disappointment strikes again. [SAJAX][4] does not support JavaScript objects, only basic variables. While that&#8217;s all well and good, when I need to pass larger objects, that&#8217;s extremely fricken annoying!!!

But wait &#8230; a glimmer of hope on the horizon &#8230; [Sanjer][6] promises to combine [SAJAX][4] and [JSON][7]. Only one major problem, it&#8217;s not actively maintained and it&#8217;s based on the 0.10 version of [SAJAX][4] which had some serialization bugs.

So to end the frustration for me and anyone else on the Internet who would ever want to do something this stupid (it apparently has to be stupid since no one else is willing to pull this off), I present my solution to the problem &#8230; hacking [SAJAX][4]. Before I delve into what changed, I&#8217;m going to give you the files so you can just run with it in the event that you aren&#8217;t interested in that crap. [This zip includes everything you need to pull this off][8]: Crockford&#8217;s **json.js** from <http://www.json.org/>, hacked up version of **Sajax.php** from me, and a simple **index.php** file that gives a super simple example of how it works. Oh yeah, since this is all based on GPL/Open source code, my derivation falls under the same licensing and comes with absolutely no warranty. Now, on to the other stuff that most people don&#8217;t really care about.

Fortunately, the people who wrote the SAJAX framework did a really good job a keeping a very nice code separation. All that had to happen to tweak this was:

  * JSON Encode the arguments before they are passed to the proxied PHP code
  * Create a new argument array of decoded JSON objects
  * Pass in the new argument array
  * JSON Encode the function result

Now I know that I could put this encode and decode inside every [PHP][1] function; however, I&#8217;m lazy and I don&#8217;t want to do that, especially if it&#8217;s a framework and it should do it for me. Here&#8217;s a snip-it of changes I made to the file:

<div class="codesnip-container" >
  <div class="php codesnip">
    <span class="sy0">:</span><span class="nu0">119</span><br /> <span class="co1">//parse out the args array</span><br /> <span class="re0">$newArgArray</span> <span class="sy0">=</span> <a href="http://www.php.net/array"><span class="kw3">array</span></a><span class="br0">&#40;</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> <span class="re0">$arraySize</span> <span class="sy0">=</span> <a href="http://www.php.net/sizeof"><span class="kw3">sizeof</span></a><span class="br0">&#40;</span><span class="re0">$args</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> <span class="kw1">for</span><span class="br0">&#40;</span><span class="re0">$i</span> <span class="sy0">=</span> <span class="nu0"></span><span class="sy0">;</span> <span class="re0">$i</span> <span class="sy0"><</span> <span class="re0">$arraySize</span><span class="sy0">;</span> <span class="re0">$i</span><span class="sy0">++</span><span class="br0">&#41;</span> <span class="br0">&#123;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="co1">//decode the JSON object</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="re0">$tmpArg</span> <span class="sy0">=</span> <a href="http://www.php.net/json_decode"><span class="kw3">json_decode</span></a><span class="br0">&#40;</span><span class="re0">$args</span><span class="br0">&#91;</span><span class="re0">$i</span><span class="br0">&#93;</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <a href="http://www.php.net/array_push"><span class="kw3">array_push</span></a><span class="br0">&#40;</span><span class="re0">$newArgArray</span><span class="sy0">,</span> <span class="re0">$tmpArg</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> <span class="br0">&#125;</span></p> 
    
    <p>
      <span class="re0">$result</span> <span class="sy0">=</span> <a href="http://www.php.net/call_user_func_array"><span class="kw3">call_user_func_array</span></a><span class="br0">&#40;</span><span class="re0">$func_name</span><span class="sy0">,</span> <span class="re0">$newArgArray</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> <span class="co1">//encode the result in to JSON</span><br /> <span class="re0">$retString</span> <span class="sy0">=</span> <a href="http://www.php.net/json_encode"><span class="kw3">json_encode</span></a><span class="br0">&#40;</span><span class="re0">$result</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> <span class="co1">//echo "var res = " . trim(sajax_get_js_repr($result)) . "; res;";</span><br /> <span class="kw1">echo</span> <span class="st0">"var res = "</span> <span class="sy0">.</span> <span class="re0">$retString</span> <span class="sy0">.</span> <span class="st0">"; res;"</span>
    </p>
    
    <p>
      <span class="sy0">:</span><span class="nu0">215</span><br /> <span class="kw1">for</span> <span class="br0">&#40;</span>i <span class="sy0">=</span> <span class="nu0"></span><span class="sy0">;</span> i <span class="sy0"><</span> args<span class="sy0">.</span>length<span class="sy0">&#8211;</span><span class="nu0">1</span><span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">&#41;</span> <span class="br0">&#123;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="co1">//uri += "&rsargs[]=" + escape(args[i]);</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; uri <span class="sy0">+=</span> <span class="st0">"&rsargs[]="</span> <span class="sy0">+</span> escape<span class="br0">&#40;</span>args<span class="br0">&#91;</span>i<span class="br0">&#93;</span><span class="sy0">.</span>toJSONString<span class="br0">&#40;</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> <span class="br0">&#125;</span>
    </p>
    
    <p>
      <span class="sy0">:</span><span class="nu0">227</span><br /> <span class="kw1">for</span> <span class="br0">&#40;</span>i <span class="sy0">=</span> <span class="nu0"></span><span class="sy0">;</span> i <span class="sy0"><</span> args<span class="sy0">.</span>length<span class="sy0">&#8211;</span><span class="nu0">1</span><span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">&#41;</span> <span class="br0">&#123;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="co1">//post_data = post_data + "&rsargs[]=" + escape(args[i]);</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; post_data <span class="sy0">=</span> post_data <span class="sy0">+</span> <span class="st0">"&rsargs[]="</span> <span class="sy0">+</span> escape<span class="br0">&#40;</span>args<span class="br0">&#91;</span>i<span class="br0">&#93;</span><span class="sy0">.</span>toJSONString<span class="br0">&#40;</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> <span class="br0">&#125;</span></div> </div> 
      
      <p>
        Well, that&#8217;s it. Really fricken hard, eh? Yeah, didn&#8217;t think so. I&#8217;m sure that this version will work for most uses; however, if you do find a bug, feel free to leave a comment or send it to me at wyatt neal on my GMail account and I&#8217;ll do my best to help you out. Hopefully this will inspire someone else with more time to come up with a better PHP framework that is a lot closer to the coolness you get from DWR.
      </p>
      
      <p>
        If you have one that does what DWR does, drop a comment and let me know. SAJAX, PAJAX, and XAJAX don&#8217;t count because I&#8217;ve looked at them and I know they don&#8217;t provide the same level of use. The only one that comes close is PAJAX but it fails because it does synchronous instead of asynchronous calls by default (what where you thinking people?!?).
      </p>

 [1]: http://www.php.net
 [2]: http://getahead.org/dwr/overview/dwr
 [3]: http://www.xajaxproject.org/
 [4]: http://www.modernmethod.com/sajax/
 [5]: http://www.xajaxproject.org
 [6]: http://sanjer.berlios.de/
 [7]: http://www.json.org
 [8]: http://blog.hackerforhire.org/wp-content/uploads/2007/03/hacked-sajax.zip "Sajax Hacked"