---
id: 14
title: AJAX Webmail
author: Wyatt
excerpt: "When I say installed, I mean I unpacked it, attempted to do a base configuration, futzed with it a bit, and didn't read the documentation...like a true engineer."
layout: post
guid: http://blog.hackerforhire.org/?p=14
permalink: /2005/10/18/ajax-webmail/
autometa:
  - 
categories:
  - Technology
---
I got my first email account back in 1996. Back then, Juno and AOL were the big boys on the block and Microsoft was just being a pest by offering free email at Hotmail. Since then, I&#8217;ve become an email-account junkie. I have an account at Yahoo, Gmail, UC, work, and two at Hotmail. Since I&#8217;ve gotten this domain, I&#8217;ve added my wyatt at hackerforhire dot org account. Now of course, this requires having some sort of access to the email, either a client like Outlook or use a web mail solution. I&#8217;d have to say the best way to go is web mail access. For us open source folk, there aren&#8217;t that many \*good\* options for web mail. I know, I&#8217;ve looked. When I installed the server, I went through all 2 that Gentoo had builds for and the other 20 on Freshmeat that looked like they had some sort of potential. They were all pretty much sub-par. So I stuck with Squirrel Mail. It wasn&#8217;t the best looking or the most user-friendly interface, but at least I could check my mail without it exploding and dying horribly. Then I found this new one that I&#8217;m liking a lot. It&#8217;s called [RoundCube Mail][1]. It was posted on slashdot about a week and a half ago and it reminded me that I still had it &#8220;installed.&#8221;  
<!--more-->

  
When I say installed, I mean I unpacked it, attempted to do a base configuration, futzed with it a bit, and didn&#8217;t read the documentation&#8230;like a true engineer. Of course, I had my issues with it. I couldn&#8217;t get it to connect to my IMAP daemon properly, the system couldn&#8217;t see itself as a server, and just other general BS. But seeing the article reminded me about my hacked install, and I figured I would give it a second shot. So I went back through the install, this time reading the&#8230;um&#8230;&#8221;documentation.&#8221; Still had the same problems that I did last time. So I got the crazy idea, why not try to use just plain IMAP instead of SSL IMAP, I mean, the worst is that someone on my server could look at the traffic I&#8217;m sending to myself over the loopback interface. So a tweak here and a tweak there, shazam! It works! And I have to say, this is how you should write a web mail client. The interface is relatively intuitive (could use some really tiny font), and the actual way the application flow is pretty slick too. I think I&#8217;m going to have to dig into it a little more to try and figure out why the SSL doesn&#8217;t work right. It will be a good opportunity to give back to the community, though not on the scope that Tim [mentioned][2] last week.

 [1]: http://www.roundcube.net/
 [2]: http://blog.mecklem.com/2005-10-11/technological-burnout