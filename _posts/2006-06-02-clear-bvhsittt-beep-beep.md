---
id: 115
title: 'Clear! **BVHSITTT** &#8230;. Beep, Beep'
author: Wyatt
excerpt: Right ... so basically my drive had a seizure and Ext3, wonderful, faithful, I-Node truncating, recovery-journal destroying, Super-block mangaling, Backup-Super-block ramdomly hiding, Backup-Super-block overwriting Ext3 ground to a screeching halt.
layout: post
guid: http://blog.hackerforhire.org/?p=115
permalink: /2006/06/02/clear-bvhsittt-beep-beep/
autometa:
  - 
categories:
  - Rants
  - Technology
---
After I don&#8217;t know how many hours of surgery/disaster recovery/uncontrollable swearing/whatever you want to call it, MOST of hackerforhire.org is back up and running. Email is still flaky, but that&#8217;s of no concern to anyone other than me. That&#8217;s the short  
version of what happened &#8230; this is the long one.  
<!--more-->

  
On Friday of last week, Sara and I went to see X-men 3 (good movie, I highly recommend it). On our way back, we noticed that there were some pretty heavy storms &#8230; that or a ravenous 40&#8242; ogre with dysentery and a really bad mood disorder just went trouncing through the Reading area of Cincinnati laying waste to the land. Either way, the result was the same: Power out. The whole way back, every neighborhood had it&#8217;s power out. I was relieved to see that ours was still on being as some of our friends were going to be out for almost 2 days.

When we got in, Heather said the power had flickered but hadn&#8217;t gone out. For my server, that is possibly the worst thing that can happen. Why? Because my server is the only one in the world I know of that can be half-way rebooted. Yes, you read that correct, half-way rebooted. What&#8217;s halfway rebooted you ask? Basically, the system &#8220;reboots&#8221; the drive but the processor and video card stay functional. This leads to as what can only be described as a &#8220;bad thing.&#8221; Sorry to use harsh words, but it&#8217;s a very frustrating experience.

Right &#8230; so basically my drive had a seizure and Ext3, wonderful, faithful, I-Node truncating, recovery-journal destroying, Super-block mangling, Backup-super-block randomly hiding, Backup-super-block overwriting Ext3 ground to a screeching halt. The best part about Ext3 is that the &#8220;auto-fix&#8221; &#8230; and I use that term o-so lightly &#8230; basically truncates unknown I-nodes and them moves them to /lost+found and renames them with their I-node number so you have no frickin&#8217; idea what the file was before hand. Even better it does it with directories too! Now, I know that it&#8217;s my own damn fault for running the stupid file-system, but man &#8230; Windows seems to have it better.

Fortunately, the &#8220;good&#8221; part my design was keeping all of my data contained on another drive that doesn&#8217;t vomit on itself at the first sign of a power fluctuation; however, with Gentoo keeping a lot of it&#8217;s critical package information in one of those data directories &#8230; it makes stitching the OS back together pretty hard because it thinks that packages are or aren&#8217;t installed and with whatever options it may or may not have had &#8230; longer story short, not a fun time and someone needs to write a better DR paper for Gentoo because I&#8217;m not doing it.

Everything is backup and running now &#8230; all the critical stuff anyway (minus mailing lists) so feel free to resume your reading enjoyment at Hacker for Hire (all 2 or 5 of you:-)).

Oh yeah, and to that no talent ass clown in #gentoo &#8230; thanks for being an &#8220;expert&#8221; on disaster recovery and telling me how I could just use it the way it was and it would work. You frickin&#8217; lying bastard!!! It doesn&#8217;t work like that! I had errors flying out the ass trying to emerge my system because it &#8220;thought&#8221; libraries were installed when they weren&#8217;t as well as portage &#8220;uninstalling&#8221; packages that weren&#8217;t even installed. You can go to the seventh sub-cellar of Hell&#8217;s out house and chew a turd you damn jerk! Next time, tell people how much of a pain it is to merge their old config/world files and then rebuild everything on the system to get things back to a stable state! Oh yeah &#8230; I hate you &#8230; you seventh sub-cellar of Hell&#8217;s out house dwelling, turd chewing jerk!