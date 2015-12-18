---
id: 228
title: Too Good To Be True
author: Wyatt
excerpt: Some would think this is success, but I like to check again just to make sure ...
layout: post
guid: http://blog.hackerforhire.org/?p=228
permalink: /2008/08/28/too-good-to-be-true/
categories:
  - Rants
  - Tips from a Hack
tags:
  - scam
  - tips
---
**Update**: *In retrospect of writing this, I think I&#8217;m going to start a new section in the blog called &#8220;Tips from a Hack&#8221; to hopefully educate people and try to prevent issues like this in the future. If anyone else has suggestion on tips or things they would like to know about, email me.*

There are somethings I get asked to do quite frequently, most I won&#8217;t do because they are illegal or unethical or some combination of the two. Occasionally, I&#8217;ll have people ask me to recover password for them. Most times it&#8217;s easy and very doable; however, sometimes there isn&#8217;t much I can do due to the nature the request. The other day I got one from a lady that had fallen into a scam.

If you&#8217;re ever really bored sometime, find a software product you like and drop it into to Google. For example, Photoshop. You&#8217;ll notice one of the &#8220;sponsored&#8221; links is a site that offers you a download and all you have to do is complete several *small, stupid* tasks. We&#8217;ll after moving around from site to site, they provide you with a file to download, but you&#8217;ll need to provide a &#8220;password&#8221; found by going to another site and searching for some magic term. This is of course all done in an effort to get referrals and advertising and malarkey of that crap.

Most users would hope that after they finshed doing all of this, they would get their software &#8230; yea, right. Most times, these site provide corrupted files. Other times, they are password protected with passwords that would never appear on any site. So that&#8217;s where I came in. This lady had gone through probably 15 different sites and around $50 to get an update to Photoshop CS3 and just couldn&#8217;t seem to get anywhere.

Enter Hacker for Hire.

So I get the file she&#8217;s looking at and I can tell right away that things aren&#8217;t adding up. First off, I hear the story and I know that it&#8217;s just not going to end well. Second, when I get the file, it&#8217;s only 6mb. Now I&#8217;ve not used Photoshop recently, but I have downloaded other Adobe and it can only be described as bloatware. Don&#8217;t get me wrong, Photoshop is great and does and excellent job but it falls into that category where programmers have just given up on how bloated their code gets. Micro-rant asside, there is no way an update from CS2 to CS3 is going to be only 6mb.

So I start to crack the zip file (thank you [fcrackzip][1]!) and just let the crack run overnight. The result?

<div class="codesnip-container" >
  <div class="bash codesnip">
    wyatt<span class="sy0">@</span>hax0red:~<span class="sy0">/</span>Desktop$ fcrackzip <span class="re5">-b</span> <span class="re5">-p</span> aaaaaa <span class="re5">-u</span> <span class="nu0">2008</span>-Update.zip</p> 
    
    <p>
      PASSWORD FOUND<span class="sy0">!!!!</span>: pw == t5MbAQ</div> </div> 
      
      <p>
        Some would think this is success, but I like to check again just to make sure &#8230;
      </p>
      
      <div class="codesnip-container" >
        <div class="bash codesnip">
          wyatt<span class="sy0">@</span>hax0red:~<span class="sy0">/</span>Desktop$ <span class="kw2">unzip</span> <span class="re5">-P</span> t5MbAQ <span class="nu0">2008</span>-Update.zip<br /> Archive: &nbsp;<span class="nu0">2008</span>-Update.zip<br /> &nbsp; &nbsp;skipping: TheProduct<span class="sy0">/</span>product.zip &nbsp;incorrect password<br /> wyatt<span class="sy0">@</span>hax0red:~<span class="sy0">/</span>Desktop$
        </div>
      </div>
      
      <p>
        Anyone else see the problem? It&#8217;s the right password for the first file in the zip, the directory, but not for the actual content, which is probably another password protected zip file. I thought about taking the time to patch fcrackzip to deal with this, but I already knew the truth. This was a sham, plain and simple.
      </p>
      
      <p>
        So a lesson for everyone out there, think twice before you submit any information online. If it sounds to good to be true, it almost certainly is. Try to remember to buy from trusted sources, like <a href="http://amazon.com">Amazon.com</a> or something like that instead of these scam artists.
      </p>

 [1]: http://www.goof.com/pcg/marc/fcrackzip.html