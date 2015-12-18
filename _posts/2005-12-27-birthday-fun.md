---
id: 44
title: Birthday Fun
author: Wyatt
excerpt: "Working on your birthday is never a good idea, that's why you get it off.  What would you imagine denying someone that day off would cause?"
layout: post
guid: http://blog.hackerforhire.org/?p=44
permalink: /2005/12/27/birthday-fun/
categories:
  - Rants
---
My current company has a policy, you get your birthday off. Apparently, this policy can be waived when you are the only person who can do whatever job they need at that instant.  
<!--more-->

  
We got a call at about 4:00 P.M. on Thursday (my companies last working day due to the holiday schedule) to help with an ISP change over. They wanted it done Tuesday &#8230; my birthday. Initially it was set for 8:00 A.M. but then that got changed &#8230; wait, I&#8217;m getting ahead of myself. Reluctantly, I said that I would do it even though I had already made plans. The guy sends me the configuration an tells me that they need to now do their own NAT. This of course raises a concern because nearly everyone does their own NAT. For those of you who don&#8217;t know what NAT is, I&#8217;m sorry, I don&#8217;t have the space to explain it in this tirade. Moving along, I get the configuration settings of both routers &#8230; both? This is about the way the setup looks:

> Internal Network &#8212; Router1 &#8212; Private T1 &#8212; Router2 &#8212; Internet 

NAT was apparently happening for them somewhere around the &#8220;Internet&#8221; area. This design is horrid by any measurement, but that&#8217;s for another rant. So I figure out the changes that need to be made, write up the new configurations and say that I&#8217;m good to go. Tuesday rolls around, the swap is supposed to start at 8:00 &#8230; doesn&#8217;t start till 11:00. The new guy and I head over to the site and wait around for their &#8220;tech guy,&#8221; who I will refer to as &#8220;Big T,&#8221; to come and let us work on their stuff. About 15 minutes later, the &#8220;Big T&#8221; calls asking if I know what the IP addresses are over at the other location because he&#8217;s trying to get into the router over there. Some more time goes by and he calls back saying that he still can&#8217;t get into it. I break down and say that we will be coming over to help him out. Now 11:45, we are over at the new colocation facility where Big T is attempting to get into the router.

Enter problem 2.

Not only can he not get into the router, but they don&#8217;t have a connection to the T1 for him to plug in. Apparently, someone forgot to run a cable. So while Big T and the manager argue over who should have brought some CAT5 to the party, I go to work on the router, guess the password and find out that THIS is the location we needed to be at anyway. So I make my configuration changes, test stuff, it works &#8230; wait, no it doesn&#8217;t. Why not? Well, that&#8217;s because for some stupid reason they didn&#8217;t have anything doing NAT for their internal network. So now, the Router2 has to be tweaked to start NAT-ing addresses out to the Internet because of the horridly poor design. Four hours later this issue is resolved and everything is better so we go back to the office where the idiot project manager is still asking me if I&#8217;ve had the chance to look in on someone else&#8217;s IDS while I&#8217;ve been out trying to restore life to a company&#8217;s Internet connection. We already know how that conversation went, so we&#8217;ll just keep moving along.

I called up my realtor and ask if I can still go look at the houses that I had planned on looking at until work screwed it up, and I can so we go. Unfortunately, I found nothing special. All the houses sucked and to make it worse they made me late for Dave & Busters where I was meeting people for fun and merriment. That was the good part of the night though. It was an awesome time at D&B and I even got to see Marilynn argue over the bill (this is a long standing tradition, if we don&#8217;t get horrible service or something like that, the night is never complete at D&B).

And so ends the tale of my 24th birthday. Thanks again to everyone who went to D&B and got to hear me go through this rant live <img src="http://blog.hackerforhire.org/wp-includes/images/smilies/simple-smile.png" alt=":-)" class="wp-smiley" style="height: 1em; max-height: 1em;" />