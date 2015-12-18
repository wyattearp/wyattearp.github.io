---
id: 62
title: Cisco Shut It Down
author: Wyatt
excerpt: At least I got to school the goober in Halo (15 to 6, 15 to 7, and 15 to 5).
layout: post
guid: http://blog.hackerforhire.org/?p=62
permalink: /2006/02/04/shut-it-down/
categories:
  - Rants
  - Technology
---
My boss is absolutely nuts about anything that Cisco dreams up. Sometimes it&#8217;s really annoying having him blow a Cisco-ey load all over the office every time he looks at a stupid PowerPoint they send out. The most recent one is Cisco Incident Control System. It&#8217;s basically a really pretty interface Cisco stole from TrendMicro and slapped their label on. The concept is that when:

  * An IPS pickups an malicious worm/virus/trojan
  * TrendMicro sends an emergency alert out
  * An administrator specifies a action

The system will automatically distribute IPS signatures to your IPS enabled routers, distribute access control list to your non-IPS devices to block ports, and sics something called Damage Control Server on any system that is reporting like it has something malicious. This of course takes action for X number of hours, minutes, seconds that the user delegates. I&#8217;ll admit, it&#8217;s pretty cool technology, even though it&#8217;s a glorified Perl script. I also find it kind of freaky that if we had another RPC worm come out, that it would just magically send out an access list that would block all Microsoft RPC traffic on the network &#8230; essentially crippling many services on an Active Directory domain.

It just annoys the crap out of me when I&#8217;m supposed to test and verify that this &#8220;amazing&#8221; system works without the IPS devices to actually trigger it. Because I share this frustration with my boss, to him it sounds like this endeavor is a waste of my time. **Newsflash!** It is a waste of my time! How in the hell am I supposed to give you a valid evaluation of a system that I cannot thoroughly test the capabilities of? I mean, I guess I could just make it up and say the thing works (which it does by the way, if you know how to convince the system that it is under attack.) At least I got to school the goober in Halo (15 to 6, 15 to 7, and 15 to 5).