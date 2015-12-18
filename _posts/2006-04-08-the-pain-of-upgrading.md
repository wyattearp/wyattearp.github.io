---
id: 93
title: The Pain of Upgrading
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=93
permalink: /2006/04/08/the-pain-of-upgrading/
categories:
  - Rants
---
For the most part, I love my Gentoo server; however, as with anything cool, there must always come one horrible drawback. This one appears to be upgrading MySQL. Right now I&#8217;m running MySQL 4.0.25 &#8230; the current version is 4.1.x. I&#8217;ve put off upgrading because generally upgrading something like a database requires upgrading everything that builds against the libraries it provides.  
<!--more-->

  
Before I go on, I&#8217;m going hit on a point that annoys the ever living crap out of me that deals with all source/binary Linux distributions alike. I can understand taking a couple of weeks or even a few months to move to the latest stable release of an important package like MySQL; however, to have the &#8220;Latest Stable&#8221; version of a package be the version that the package developer calls deprecated &#8230; that&#8217;s a little stupid. And this has happened on every version of Linux I&#8217;ve ever used (with various packages). I believe the issue even came up on Digg that what Linux really needed was a common installer environment. I agree, but I think they need more than that. I think first and foremost, a damned root folder structure should be selected and all versions adhere to it (which of course blows up the whole &#8220;I can do whatever i want with my Linux distro&#8221; mentality). But this is a remedial similarity for all systems that I think would make things much smoother for new distro development, etc. OK, side rant aside, back to the original rant.

So I&#8217;ve attempted to upgrade MySQL to 4.1. Gentoo gives this really nasty message about how upgrading is horrible and bad and all sorts of mean nasty ugly and isn&#8217;t supported unless you go do it how they say in the forum. So the way I look at it, there are 3 options:

1. Upgrade the supported Gentoo way &#8230; possibility  
2. Upgrade the scary Gentoo way &#8230; not likely  
3. Upgrade the MySQL way &#8230; more likely than the previous

Well, initially, I took the supported Gentoo way &#8230; which was painful and best off unsuccessful. It blew up horribly. Trying do a restore of the backup yielded more than 4,000 separate errors as well as crippled the starting of mysqld (because some how the PID directory was wantonly destroyed). Well after 4 attempts of failure the Gentoo Way &#8230; I&#8217;ve decided to take matters into my own hands. I&#8217;m even composing this in [Writely][1] at the moment because everything on my site &#8230; email, blog, quote page &#8230; everything is down thanks to this piss poor documentation.

Heading on over the the MySQL site reveals their migration requires two servers &#8230; I don&#8217;t have two servers to play with and I&#8217;m not about to setup a new VM just to do an upgrade so that idea is scrapped. Since I&#8217;ve been told I have a blatant disregard for the safety of myself and others &#8230; bring on the unsupported method.

This is really stupid how this works too. Basically, one environmental variable is set and then portage will ignore everything it&#8217;s ever been told and just bulldoze over everything. Following the documentation for this method worked pretty well &#8230; except for one small problem. MySQL wouldn&#8217;t start when the process was over. That&#8217;s because the old package remove again kills the /var/run/mysqld directory. Recreating the directory, running mysql\_fix\_privilege\_tables, and ignoring the random step about inserting the /tmp/new\_pieces.sql resolved the issues. And of course the rebuilding of all the packages that depended on the 4.0 client (46 of them).

Needless to say, I&#8217;m still pissed. Why? BECAUSE IT&#8217;S ONLY VERSION 4.1!!! The stupid bastards at Gentoo haven&#8217;t upgraded to 5.0 yet so I can&#8217;t benefit from any portion of it. Oh, and one more thing. The Wildfire Jabber on hackerforhire.org was upgraded to version 2.6.0 for security reasons and will be upgraded again later this week to 2.6.1 to fix a performance issue and the morons at Wildfire didn&#8217;t provide a nice way to update the database &#8230; it was just conveniently exploded. So if you had a username on my server, you&#8217;ll need to re-register.

 [1]: http://www.writely.com