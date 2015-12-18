---
id: 48
title: DenyHosts
author: Wyatt
excerpt: "... you can get the fsckers on the first attempt."
layout: post
guid: http://blog.hackerforhire.org/?p=48
permalink: /2006/01/08/denyhosts/
categories:
  - Technology
---
If you read the last post you know the my machine is under heavy on a daily basis. Quite frankly, I&#8217;m impressed that it holds up and doesn&#8217;t die from DoS attacks that hit it every day. I used to run and IDS/IPS on it at one point in time but I couldn&#8217;t handle looking at 1,000,000 alerts per day (yes, I did tune it and only select the signatures that I wanted, but as a human, you can only take so much). I suppose that part of it is due to being on a residential Road Runner connection and a lot of it dealing with the domain name being an &#8220;Oh I&#8217;ll show that bastard&#8221; type of thing. Being as such, I am always on the look out for new tools to make my life simpler. [DenyHosts][1] does exactly that.

DenyHosts is a really awesome script that basically keeps track of invalid logins and failures that on your system and after a specified threshold, blocks them. You can daemonize the script and have it run in the background keeping track of all the little miscreants that are constantly hammering you system. You can specify that you want hosts blocked for anywhere from 1 second to some ungodly number of years. It also has the ability to block sooner or later for attempted root logins. That&#8217;s just awesome because if you are like me and specify that root is never allowed to SSH in, you can get the fsckers on the first attempt. Best off, Gentoo has a package for it so installation for me was one command.

As with any tool, it will maim and disfigure you horribly if you don&#8217;t use it right, but I doubt that most competent people would have to worry about that. I&#8217;m not going to go through a configuration or installation here because the website has way better documentation that what I would care to write here. My only gripe is that it took a long time to go through my authorization log the first time because I don&#8217;t normally rotate my logs, but I can live with that.

Last words &#8230; if you have a *nix server with SSH access, you should probably use this tool.  
<http://denyhosts.sourceforge.net/>

 [1]: http://denyhosts.sourceforge.net/