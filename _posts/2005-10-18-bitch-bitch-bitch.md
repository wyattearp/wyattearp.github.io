---
id: 15
title: Bitch, Bitch, Bitch
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=15
permalink: /2005/10/18/bitch-bitch-bitch/
categories:
  - Rants
---
You know, I haven&#8217;t complained about work lately; probably because it&#8217;s not been as bad. But I do have something to gripe about. At the client I&#8217;m at, I&#8217;m the first contractor they&#8217;ve had in 4 years. Anyone else smell something? So far since I&#8217;ve been there, I&#8217;ve been fingered as causing 3 problems. First, they had a system just sporatically reboot. They looked to me because I was walking out of the data center at the time they got the page. After some asking around, they found out that I was back pulling cable (yeah, hell of a job for a Security/Software Engineer) and no where need the racks of servers that had the failure. The second one was that a Solaris box locked up and caused a backup failure. Naturally, I was working on a Solaris system. Again, the system that locked up was not the one that I was working on. Third time&#8217;s a charm right? Ha, I think not. Their core router was spiking in utiliazation due to the SNMP process getting into an infinite wait. Again, they came to me because I was working on the system that talks SNMP to all the network devices. Nevermind the fact that I was working on a totally unrelated component. So after they come to talk with me about it, and we walk through what was wrong, we come to find out that THEY were the ones that caused the problem when they upgraded the router and removed a command that causes a bug. And as me to have a smart ass verification, I showed them that their SNMP querying system didn&#8217;t even talk to that router. And another thing, who in their right mind would put SNMP on an Internet facing router??? Oh sure, that&#8217;s a great idea, let&#8217;s just allow everyone and their brother to determine/modify our router configuration and blow up our Internet connect. Morons.