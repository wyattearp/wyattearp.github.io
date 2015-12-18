---
id: 120
title: 3gp And Other Oddities
author: Wyatt
excerpt: "Save it, resume the emerge, ignore the warnings ... trust me, the magic goat of sorrow won't come after you."
layout: post
guid: http://blog.hackerforhire.org/?p=120
permalink: /2006/06/17/3gp-and-other-oddities/
autometa:
  - 3gp ffmpeg mencoder
enclosure:
  - |
    |
        http://zerohour.sytes.net/stuff/thx.avi.3gp
        482687
        video/x-msvideo
        
categories:
  - Technology
---
As you may or may not know, I purchase a new phone and switched my service to T-Mobile. I found out that the Nokia e60 will actually play video (no, I didn&#8217;t pay attention to that, I was more concerned with the SIP coolness capabilities). So I stared doing some research into making/converting video for access by mobile devices.  
<!--more-->

  
Apparently this phone supports multiple compression codecs; however, it only recognizes one file type of extension, 3gp. 3gp is basically a really slimmed down MPEG4 codec for GSM devices (aka, mobile phones). Obviously, there are more specifics to it than that &#8230; I just decided I didn&#8217;t really need to know those to get Kill Bill Vol. 1 running on my cell phone. If you want more information on 3gp, head over to [3gpg.org][1].

First things first, I needed a way to get the DVD on to my hard drive in a format that would allow me to smash-ifie a 4.7 GB DVD into a very tiny 3gp of whatever size (in my case, less that 512 MB because that&#8217;s the maximum amount of flash my phone will hold &#8230; I had to contact Nokia for that because it wasn&#8217;t listed anywhere on the net/support site). So to get the DVD to something usable, I used mencoder (I love open source). Mencoder is, IMHO, not a tool for those with a weak constitution, but it will do whatever you could possibly want to said anything A/V related. After some searching, I found that for 3gp to work the best, a couple of things need to happen. First off, everyone recommends MPEG4 for the video at less than 160 kbits&#8230; no brain-er, 3gp is based off of that. Secondly, audio sampling only works at 8 kbits &#8230; that&#8217;s a little more tricky.

So lets start with the video. Being as we want a nice DVD style movie, we&#8217;re going to crop to 720&#215;480 and being as we are on a super tiny screen (mine is 352&#215;288), we&#8217;re going to scale things down a bit too; however, I&#8217;m going to also break the rules and make my movie with a variable bit rate of 256 kbits being as I like Kill Bill in non-pixilated glory. We also need the audio in it&#8217;s crappy 8kbit so we&#8217;ll take care of that as well. Here&#8217;s what my mencoder line looks like:

<div class="codesnip-container" >
  #!/bin/bash<br /> mencoder dvd://1 \<br /> -oac pcm \<br /> -af resample=8000,volume=+5db:sc \<br /> -ovc lavc \<br /> -lavcopts vcodec=mpeg4:vbitrate=256 \<br /> -vf crop=720:480,scale=352:288:0:0:1 \<br /> -vf-add eq2=1:1:0:1 \<br /> -o &#8220;Kill Bill Vol 1.avi&#8221;
</div>

Ok, I threw a couple of other things in there as well. In the scale, the 0:0:1 means give me some interlaced scaling goodness (for more info check out the mencoder man page). I also bumped up the volume because it tends to be kind of quiet when you get it over to your phone. The eq2 is messing with the gamma &#8230; I don&#8217;t know how it is, but I found that on someone else site that I can&#8217;t find and it made the picture look a lot better &#8230; so kudos to that gamma correcting genius wherever you are.

After about 30 minutes, I now have a 1.4 GB file &#8230; not quite cell phone size, but better than 4.7 GB. That and we don&#8217;t yet have it in 3gp format. Next tool up on the block, ffmpeg. To get ffmpeg to work right, you have to download the 3gp codec and rebuild ffmpeg in some weird ass way. Fortunately, I run Gentoo so all I had to do was add the amr flag to USE= in /etc/make.conf and re-emerge ffmpeg. Only one problem &#8230; apparently, the new kernel headers break ffmpeg so that this line of code doesn&#8217;t work:

<div class="codesnip-container" >
  /* XXX: add ISOC specific test to avoid specific BSD testing. */<br /> /* better than nothing implementation. */<br /> /* btw, rintf() is existing on fbsd too &#8212; alex */<br /> static always_inline long int lrintf(float x)
</div>

To &#8220;hack&#8221; around this until someone at Gentoo fixes it with a patch, start the ebuild &#8230; pause it during the part where ffmpeg is being configured, run off to /var/tmp/portage/ffmpeg-*/work, and edit common.h (yes, both of them), to look like this:

<div class="codesnip-container" >
  /* XXX: add ISOC specific test to avoid specific BSD testing. */<br /> /* better than nothing implementation. */<br /> /* btw, rintf() is existing on fbsd too &#8212; alex */<br /> static __inline__ long int lrintf(float x)
</div>

Save it, resume the emerge, ignore the warnings &#8230; trust me, the magic goat of sorrow won&#8217;t come after you. Yes, I know I could do the whole portage overlay and make my own patch, but I&#8217;m too busy writing down how I did this so I won&#8217;t forget later.

Now that we have a function ffmpeg, we take our recent AVI and liquefy it down into some 3gp gooeyness. This is what my ffmpeg command looks like:

<div class="codesnip-container" >
  ffmpeg -i &#8220;Kill Bill Vol 1.avi&#8221; \<br /> -b 160 \<br /> -r 24 \<br /> -ac 1 \<br /> -ab 12 \<br /> -ar 8000 \<br /> -acodec amr_nb \<br /> -vcodec h263 \<br /> &#8220;Kill Bill Vol 1.avi.3gp&#8221;
</div>

So now we set our video bit rate to 160, using 24 frames and reduced our audio down to that ugly 8 kbits. Why did I make it \*.avi.3gp instead of \*.3gp you ask? Well, because my phone doesn&#8217;t seem to understand the file it isn&#8217;t named that way. I&#8217;m sure your mileage will vary accordingly. Being as I can&#8217;t legally put up the Kill Bill movie, I decided I would produce another example &#8230; the THX intro. I figured if you are going to be sacrilegious and put video on a cell phone &#8230; you had might as well do it with THX sound, right? [Here it is][2].

 [1]: http://3gpp.org
 [2]: http://zerohour.sytes.net/stuff/thx.avi.3gp