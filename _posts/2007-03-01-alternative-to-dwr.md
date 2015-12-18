---
id: 158
title: Alternative to DWR
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=158
permalink: /2007/03/01/alternative-to-dwr/
autometa:
  - DWR JavaScript PHP apps applications
categories:
  - Technology
---
So at [HTG][1], we build web applications. Hosted web apps to be precise. For one of our big ones, we choose to go the route of [DWR][2]. If you don&#8217;t know what [DWR ][2]is, it&#8217;s basically a way of getting a nice JavaScript interface to a back end Java server. That&#8217;s all well and good; however, only 2 of our 3 developers liked the idea of going with Java. The third has what can only be described as reverent animosity towards Java &#8230; especially after some classes we took in the Engineering college <img src="http://blog.hackerforhire.org/wp-includes/images/smilies/simple-smile.png" alt=":-)" class="wp-smiley" style="height: 1em; max-height: 1em;" /> .

Anyway, I think the best part of DWR is that you get this JavaScript, or files, that give you objects that have functions equivalent to your exposed Java interfaces on the server. The beauty of this is that you can just make calls to something like this in the JavaScript:

<div class="codesnip-container" >
  <script type=&#8217;text/javascript&#8217;<br /> src=&#8217;/project/remoteSecurityManager.js&#8217;> </script><br /> <script><br /> if (remoteSecurityManager.loginUser(&#8216;username&#8217;, &#8216;password&#8217;)) {<br /> &#8230;<br /> } else {<br /> &#8230;<br /> }<br /> </script>
</div>

Now of course, that code is completely bogus and won&#8217;t work for crap (bonus points if you can see why it would never work); however, it&#8217;s really nice because it gives you a way to have some people hammer on the server-side and some people work on the UI side without needing to really jump bank and forth from server to client. Well, Java&#8217;s all well and good; however, if you remember from earlier, we have one person that &#8220;hates&#8221; Java. So putting on the pseudo PM hat, I started looking around for some other ways to get that same sort of functionality in PHP &#8230; low and behold, such a thing does exist. It&#8217;s called [xajax][3] and it seems like it gets me the same sort of thing that DWR does. I&#8217;ve not read a ton on it, but I&#8217;m going to delve into it a little more and let you know what I think.

 [1]: http://htglimited.com
 [2]: http://getahead.ltd.uk/dwr/overview/dwr
 [3]: http://www.xajaxproject.org/