---
id: 32
title: Not Cabling
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=32
permalink: /2005/11/17/not-cabling/
categories:
  - Rants
---
Finally, a post that&#8217;s not about cabling. Well, not entirely. I&#8217;m done with that client, for now, and my boss said that he would never ask me to do that again and if we were going to work with that client that I would not be involved in stuff as stupid as re-cabling a data center. I guess he got nervous when he realized that I was the last engineer.

But man o man, working with him is a nightmare. They sent me into deal with two issues, a new switch installation and an SQL latency issue. The first was not so bad, given one of the older switches wouldn&#8217;t play nice, but that&#8217;s any Cisco upgrade. Though I had to be a nice person and fix the silly cluster servers because some moron from hell with a thirst for stupid with an extra smattering of cracked out the ass set the servers that are supposed to come back up after a failure to NOT COME BACK UP!!! The other issue that arose from this was that the client was out of IP addresses.

Totally out.

So I try to resolve this the correct way but I keep running into management that keeps saying, &#8220;Our problem is that our wireless computers could create an ad-hoc network and attackers could access the internal network.&#8221; Did I miss something? Yes, making sure that the laptops are not on the wireless and the wired network would free up a few IP addresses but attackers trying to get in via ad-hoc networks? Give me a break. Have you ever tried to set that up? It requires setting up and ad-hoc network and then trying to make the wonderful XP system try to be an Internet gateway for anything else. This is something many of the techie people I know can&#8217;t even accomplish and we are worried about an end user setting it up? My ass, Microsoft does not write that functional of programs.

Well that was the &#8220;switch install,&#8221; but the SQL problem still had to be dealt with. I can only liken this situation to going to a car mechanic and say &#8220;My car is making a sound.&#8221; Needless to say, there was nothing I could do. Well, nothing I was willing to try and break. I&#8217;m not a DBA, I don&#8217;t pretend to be, I want nothing to do with that monstrosity that people call a database. Crackers. So I got to go home early and be bored and write this entry.