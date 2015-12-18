---
id: 7
title: Killing Native American Web Servers
author: Wyatt
excerpt: I would like to take a moment to note that this, of course, is never a good idea for someone with an engineering mind like myself because it allows for the opportunity for "improvement."
layout: post
guid: http://blog.hackerforhire.org/?p=7
permalink: /2005/10/11/killing-native-american-web-servers/
categories:
  - Rants
---
In the business world of today, many things change at a very rapid pace. To keep a handle on these changes, there is a process called &#8220;Change Control&#8221; or &#8220;Change Management&#8221; or whatever buzz word your company/slum likes to refer to it as. So for those of you who are unfamiliar, the process goes something like this.

P1: I would like to make a change, here is what I want to do  
P2: How will it inconvenience me?  
P1: It won&#8217;t  
P2: OK, go ahead and do it  
P1: It&#8217;s done  
P2: My hair is on fire!!!

Basically, the whole principle is to notify people that there are going to be significant changes that may affect the way that business operates. So usually, you are given a notice and have X number of days/weeks/minutes to resolve your end of the bargain. Why would I rant about a system like this? Good question. The answer is I&#8217;m ranting about the system, I&#8217;m ranting about the lack of use of the system. My web server needed to be beat all to hell and dragged through a gutter before it would tell me what was wrong. After I found out that the geniuses at Gentoo had decided to un-organize the configuration for the web server and somehow magically delete my configuration, I got spend my morning recreating it.

I would like to take a moment to note that this, of course, is never a good idea for someone with an engineering mind like myself because it allows for the opportunity for &#8220;improvement.&#8221;

So I tinkered and tweaked and got the server back up to speed, but then I got it in my head to do one more thing. I decided I had to be cool like everyone else on the Internet and have my blog site be at http://blog.mystupiddomain.com instead of blah.com/blogeriffic. You wouldn&#8217;t think that it would be that hard to set something like that up&#8230;you would be right&#8230;unless you are battling through trying to remember your server configuration from a year ago. Well, obviously I got it working, but I am still not pleased with the actual file location on the server. The stupid thing had the right permissions but it still did not want to let me access the page and gave me a big fat 403 error. So it&#8217;s been hacked into functionality, but it will eventually change to be done correctly. Not that any of you will see the change.