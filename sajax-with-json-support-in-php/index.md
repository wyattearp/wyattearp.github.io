---
id: 178
title: Sajax With JSON Support In PHP
author: Wyatt
layout: page
guid: http://blog.hackerforhire.org/sajax-with-json-support-in-php/
autometa:
  - 
---
A while ago, I wanted to recreate the cool functionality you get with DWR in PHP. There are a ton of frameworks out there that come close, but miss completely. Thus, I finally caved and created my own solution that is nothing more than patching the existing software into my desired hack. From the simple ingredients of:

  * [SAJAX][1]
  * [PHP 5.2.2+ (stupid JSON bugs)][2]
  * [JSON by Crockford][3]

Hacked-SAJAX was born.

  * **UPDATE: **It appears that someone decided to **finally** update [SAJAX][4] to support JSON, PHP, Perl, ColdFusion, UTF-8, etc. I&#8217;ll keep this on up, but I&#8217;d recommend going to the original developer from now on. We&#8217;ll have to see if they actually keep on their every 3.5yr release schedule <img src="http://blog.hackerforhire.org/wp-includes/images/smilies/simple-smile.png" alt=":smile:" class="wp-smiley" style="height: 1em; max-height: 1em;" /> Personally, I&#8217;d recommend to the developer (assuming he / she visits this page) to put up a project on [github.com][5] because it seems like a lot of people really like this project and would like to keep it alive / contribute.
  * <del datetime="2009-09-04T04:26:53+00:00">Download <a href="http://hackerforhire.org/hacked-sajax.zip">here</a></del>.

Example code is included and it can be used as follows:

  * Create your PHP function
  * Export your PHP function
  * Call sajax_init()
  * Call your PHP function from Javascript just like any other asynchronous function

<div class="codesnip-container" >
  <div class="php codesnip">
    <span class="kw2">function</span> addNameToObject<span class="br0">&#40;</span><span class="re0">$obj</span><span class="br0">&#41;</span> <span class="br0">&#123;</span><br /> &nbsp; &nbsp;<span class="re0">$obj</span><span class="sy0">-></span><span class="me1">name</span> <span class="sy0">=</span> <span class="st0">"wyatt "</span> <span class="sy0">.</span> <span class="re0">$obj</span><span class="sy0">-></span><span class="me1">name</span><span class="sy0">;</span><br /> &nbsp; &nbsp;<span class="kw1">return</span> <span class="re0">$obj</span><span class="sy0">;</span><br /> <span class="br0">&#125;</span></p> 
    
    <p>
      sajax_export<span class="br0">&#40;</span><span class="st0">"addNameToObject"</span><span class="br0">&#41;</span><span class="sy0">;</span>
    </p>
    
    <p>
      sajax_init<span class="br0">&#40;</span><span class="br0">&#41;</span><span class="sy0">;</span></div> </div> 
      
      <div class="codesnip-container" >
        <div class="javascript codesnip">
          <span class="kw2">var</span> myObj <span class="sy0">=</span> <span class="br0">&#123;</span> <span class="kw3">name</span><span class="sy0">:</span> <span class="st0">"neal"</span><span class="sy0">,</span> height<span class="sy0">:</span> <span class="nu0">6</span> <span class="br0">&#125;</span><span class="sy0">;</span></p> 
          
          <p>
            x_addNameToObject<span class="br0">&#40;</span>myObj<span class="sy0">,</span> <span class="kw2">function</span> <span class="br0">&#40;</span>obj2<span class="br0">&#41;</span> <span class="br0">&#123;</span>console.<span class="me1">log</span><span class="br0">&#40;</span>obj2<span class="br0">&#41;</span><span class="sy0">;</span> <span class="br0">&#125;</span> <span class="br0">&#41;</span><span class="sy0">;</span></div> </div> 
            
            <p>
              This is of course released under the GPL or whatever means that I&#8217;m giving away my modifications, please cite everyone who had a part in it. My changes to the code base are as follows
            </p>
            
            <div class="codesnip-container" >
              <div class="php codesnip">
                <span class="sy0">:</span><span class="nu0">119</span><br /> <span class="co1">//parse out the args array</span><br /> <span class="re0">$newArgArray</span> <span class="sy0">=</span> <a href="http://www.php.net/array"><span class="kw3">array</span></a><span class="br0">&#40;</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> <span class="re0">$arraySize</span> <span class="sy0">=</span> <a href="http://www.php.net/sizeof"><span class="kw3">sizeof</span></a><span class="br0">&#40;</span><span class="re0">$args</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> <span class="kw1">for</span><span class="br0">&#40;</span><span class="re0">$i</span> <span class="sy0">=</span> <span class="nu0"></span><span class="sy0">;</span> <span class="re0">$i</span> <span class="sy0"><</span> <span class="re0">$arraySize</span><span class="sy0">;</span> <span class="re0">$i</span><span class="sy0">++</span><span class="br0">&#41;</span> <span class="br0">&#123;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="co1">//decode the JSON object</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="re0">$tmpArg</span> <span class="sy0">=</span> <a href="http://www.php.net/json_decode"><span class="kw3">json_decode</span></a><span class="br0">&#40;</span><a href="http://www.php.net/stripslashes"><span class="kw3">stripslashes</span></a><span class="br0">&#40;</span><span class="re0">$args</span><span class="br0">&#91;</span><span class="re0">$i</span><span class="br0">&#93;</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <a href="http://www.php.net/array_push"><span class="kw3">array_push</span></a><span class="br0">&#40;</span><span class="re0">$newArgArray</span><span class="sy0">,</span> <span class="re0">$tmpArg</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> <span class="br0">&#125;</span></p> 
                
                <p>
                  <span class="re0">$result</span> <span class="sy0">=</span> <a href="http://www.php.net/call_user_func_array"><span class="kw3">call_user_func_array</span></a><span class="br0">&#40;</span><span class="re0">$func_name</span><span class="sy0">,</span> <span class="re0">$newArgArray</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> <span class="co1">//encode the result in to JSON</span><br /> <span class="re0">$retString</span> <span class="sy0">=</span> <a href="http://www.php.net/json_encode"><span class="kw3">json_encode</span></a><span class="br0">&#40;</span><span class="re0">$result</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> <span class="co1">//echo "var res = " . trim(sajax_get_js_repr($result)) . "; res;";</span><br /> <span class="kw1">echo</span> <span class="st0">"var res = "</span> <span class="sy0">.</span> <span class="re0">$retString</span> <span class="sy0">.</span> <span class="st0">"; res;"</span>
                </p>
                
                <p>
                  <span class="sy0">:</span><span class="nu0">215</span><br /> <span class="kw1">for</span> <span class="br0">&#40;</span>i <span class="sy0">=</span> <span class="nu0"></span><span class="sy0">;</span> i <span class="sy0"><</span> args<span class="sy0">.</span>length<span class="sy0">&#8211;</span><span class="nu0">1</span><span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">&#41;</span> <span class="br0">&#123;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="co1">//uri += "&rsargs[]=" + escape(args[i]);</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; uri <span class="sy0">+=</span> <span class="st0">"&rsargs[]="</span> <span class="sy0">+</span> escape<span class="br0">&#40;</span>args<span class="br0">&#91;</span>i<span class="br0">&#93;</span><span class="sy0">.</span>toJSONString<span class="br0">&#40;</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="sy0">;</span><br /> <span class="br0">&#125;</span>
                </p>
                
                <p>
                  <span class="sy0">:</span><span class="nu0">227</span><br /> <span class="kw1">for</span> <span class="br0">&#40;</span>i <span class="sy0">=</span> <span class="nu0"></span><span class="sy0">;</span> i <span class="sy0"><</span> args<span class="sy0">.</span>length<span class="sy0">&#8211;</span><span class="nu0">1</span><span class="sy0">;</span> i<span class="sy0">++</span><span class="br0">&#41;</span> <span class="br0">&#123;</span><br /> &nbsp; &nbsp; &nbsp; &nbsp; <span class="co1">//post_data = post_data + "&rsargs=" + esscape(args[i]);</span><br /> post_data <span class="sy0">=</span> post_data <span class="sy0">+</span> <span class="st0">"&rsargs[]="</span> <span class="sy0">+</span> escape<span class="br0">&#40;</span>args<span class="br0">&#91;</span>i<span class="br0">&#93;</span><span class="sy0">.</span>toJSONString<span class="br0">&#40;</span><span class="br0">&#41;</span><span class="br0">&#41;</span><span class="sy0">;</span>
                </p>
                
                <p>
                  <span class="br0">&#125;</span></div> </div> 
                  
                  <p>
                    The original rant is here:
                  </p>
                  
                  <p>
                    I have been scouring the Internet for two days for looking for a suitable <a href="http://www.php.net">PHP alternative to <a href="http://getahead.org/dwr/overview/dwr">DWR</a>(read the previous post for more information) and haven&#8217;t found a single one so I&#8217;ve hacked out my own.</p> 
                    
                    <p>
                      I had been looking at <a href="http://www.xajaxproject.org/">xajax</a> in the hopes that it would get me what I was looking for, but it didn&#8217;t. So the next one I found was <a href="http://www.modernmethod.com/sajax/">SAJAX</a>. This project appears to be less active than <a href="http://www.xajaxproject.org">xajax</a>; however, disappointment strikes again. <a href="http://www.modernmethod.com/sajax/">SAJAX</a> does not support JavaScript objects, only basic variables. While that&#8217;s all well and good, when I need to pass larger objects, that&#8217;s extremely fricken annoying!!!
                    </p>
                    
                    <p>
                      But wait &#8230; a glimmer of hope on the horizon &#8230; <a href="http://sanjer.berlios.de/">Sanjer</a> promises to combine <a href="http://www.modernmethod.com/sajax/">SAJAX</a> and <a href="http://www.json.org">JSON</a>. Only one major problem, it&#8217;s not actively maintained and it&#8217;s based on the 0.10 version of <a href="http://www.modernmethod.com/sajax/">SAJAX</a> which had some serialization bugs.
                    </p>
                    
                    <p>
                      So to end the frustration for me and anyone else on the Internet who would ever want to do something this stupid (it apparently has to be stupid since no one else is willing to pull this off), I present my solution to the problem &#8230; hacking <a href="http://www.modernmethod.com/sajax/">SAJAX</a>. Before I delve into what changed, I&#8217;m going to give you the files so you can just run with it in the event that you aren&#8217;t interested in that crap. <a href='http://blog.hackerforhire.org/wp-content/uploads/2007/03/hacked-sajax.zip' title='Sajax Hacked'>This zip includes everything you need to pull this off</a>: Crockford&#8217;s <strong>json.js</strong> from <a href="http://www.json.org/">http://www.json.org/</a>, hacked up version of <strong>Sajax.php</strong> from me, and a simple <strong>index.php</strong> file that gives a super simple example of how it works. Oh yeah, since this is all based on GPL/Open source code, my derivation falls under the same licensing and comes with absolutely no warranty. Now, on to the other stuff that most people don&#8217;t really care about.
                    </p>
                    
                    <p>
                      Fortunately, the people who wrote the SAJAX framework did a really good job a keeping a very nice code separation. All that had to happen to tweak this was:
                    </p>
                    
                    <ul>
                      <li>
                        JSON Encode the arguments before they are passed to the proxied PHP code
                      </li>
                      <li>
                        Create a new argument array of decoded JSON objects
                      </li>
                      <li>
                        Pass in the new argument array
                      </li>
                      <li>
                        JSON Encode the function result
                      </li>
                    </ul>
                    
                    <p>
                      Now I know that I could put this encode and decode inside every <a href="http://www.php.net">PHP</a> function; however, I&#8217;m lazy and I don&#8217;t want to do that, especially if it&#8217;s a framework and it should do it for me.
                    </p>
                    
                    <p>
                      Well, that&#8217;s it. Really fricken hard, eh? Yeah, didn&#8217;t think so. I&#8217;m sure that this version will work for most uses; however, if you do find a bug, feel free to leave a comment or send it to me at wyatt neal on my GMail account and I&#8217;ll do my best to help you out. Hopefully this will inspire someone else with more time to come up with a better PHP framework that is a lot closer to the coolness you get from DWR.
                    </p>
                    
                    <p>
                      If you have one that does what DWR does, drop a comment and let me know. SAJAX, PAJAX, and XAJAX don&#8217;t count because I&#8217;ve looked at them and I know they don&#8217;t provide the same level of use. The only one that comes close is PAJAX but it fails because it does synchronous instead of asynchronous calls by default (what where you thinking people?!?).
                    </p>

 [1]: http://www.modernmethod.com/sajax/
 [2]: http://www.php.net
 [3]: http://www.json.org/
 [4]: http://sajax.info
 [5]: http://github.com