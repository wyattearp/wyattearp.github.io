---
id: 97
title: Not so S.M.A.R.T
author: Wyatt
excerpt: 'Powered it up ... got a nice big (\) on my screen.  Crapsticks.'
layout: post
guid: http://blog.hackerforhire.org/?p=97
permalink: /2006/04/19/not-so-smart/
autometa:
  - tray migrate smart disk utility diagnostic boot moved
categories:
  - Rants
  - Technology
---
I really like my X Server that Rick built for me. It&#8217;s fast, it&#8217;s 1u, and it&#8217;s got blue blinky LEDs on it. It had everything I wanted &#8230; everything but that pretty and cool OS X.

So I went on my war to get OS X on this system, and a long an arduous battle it was; however, I prevailed in the end. I&#8217;ve not booted my Mac since we moved into our new place. Mainly because I don&#8217;t have a place to put it other than in the server rack, but more so because it&#8217;s really loud. Last night, I decided that it had been dormant long enough and needed to be started (first mistake). I hauled all the crap I would need down to the basement, move the sever rack, ran a long Ethernet cable from upstairs, etc.

Powered it up &#8230; got a nice big **(\)** on my screen. Crapsticks.  
<!--more-->

  
That can only mean one thing &#8230; my computer is dead. Watching the diagnostic lights revealed that the drive was having an issue starting &#8230; maybe. A green light followed by an orange blink and then none. Watching in diagnostic mode &#8230; I get &#8220;Still waiting on root device &#8230;&#8221; Generally, this error occurs when the system can&#8217;t find which disk to boot. I know that this isn&#8217;t what is happening because I can see it detect the drive and then attempt the boot and just sit there.

Reluctantly, I pull out one of my 75,000 copies of the Tiger install CD (I have that many because of how much of a damned pain it was to get it) and fire it up. OS X does not see the drive being present; however, it sees another drive fine. Damn. Past the standard troubleshooting, the only thing left I can see possible wrong is the drive tray or the drive itself. Being as the tray is a circuit board with no &#8220;real&#8221; moving parts, I think it&#8217;s safe to say I&#8217;ve lost that drive and all the data on it.

Now for the part that pisses me off. That drive was not reporting any SMART failures at all. I know because I checked it and ran the equivalent of fsck or chkdsk on it before we moved and Apple shows you the SMART status in that same window. Mine said that it was fine &#8230; it obviously wasn&#8217;t or the drive just died horribly during transport. I have no idea. But what I do remember is that another drive I had in the system was reported as being in a failed SMART state by the disk utility. Apple&#8217;s utility suggested I migrate all the data of and replace it ASAP.

Only, they wouldn&#8217;t let me access it with their OS!!! WTF??? You want me to migrate the damn data &#8230; but I can&#8217;t touch it? Show me in the manual where that works. Now yes, I am aware that I can go into the command line and try to find the horridly long string that represents one of my 4 SATA translated IDE devices, but why the hell should I have to do that with an OS that is supposed to be the most user friendly in the world? Yes, this is the consumer version and not the server version of the product &#8230; so if I were Joe-moron-user (not you Joe Rocklin), and I got this big warning that said &#8220;Oh my dear transistors!!! You need to move your data!&#8221; I should be able to move my data in the same damn fashion I always have. \*Sigh\* &#8230; but maybe that&#8217;s why I don&#8217;t write operating systems and make lots of money.