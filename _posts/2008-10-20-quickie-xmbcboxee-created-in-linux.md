---
id: 247
title: 'Quickie: XMBC/Boxee Created in Linux'
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=247
permalink: /2008/10/20/quickie-xmbcboxee-created-in-linux/
categories:
  - Technology
  - Tips from a Hack
tags:
  - apple tv
  - patch stcik
  - xbmc
---
Alright, I&#8217;m sure this will be documented much more clearly elsewhere and in a hacker-ish manner, but here&#8217;s the basic steps to make the [atv-bootloader][1] in a Linux environment so you can install [Boxee][2] or [XBMC][3]. Make sure you install the HFS/HFS+ tools for your Linux distribution.

  1. Open up the shell and roll up your sleeves
  2. Get the latest from svn <div class="codesnip-container" >
      <div class="bash codesnip">
        wyatt<span class="sy0">@</span>hax0red:~<span class="sy0">/</span> <span class="kw2">svn</span> <span class="kw2">co</span> http:<span class="sy0">//</span>atvusb-creator.googlecode.com<span class="sy0">/</span>svn<span class="sy0">/</span>trunk<span class="sy0">/</span>atvusb-creator
      </div>
    </div>

  3. Change into the atv-usbcreator directory and launch the creator <div class="codesnip-container" >
      <div class="bash codesnip">
        wyatt<span class="sy0">@</span>hax0red:~<span class="sy0">/</span>atvusb-creator$ <span class="kw2">sudo</span> .<span class="sy0">/</span>atvusb-creator.py
      </div>
    </div>

  4. Plug in a partitioned USB drive and create the patch stick with Boxee/XBMC/whatever (which will do it wrong, but that&#8217;s ok!)
  5. Now, write the **real** image to the device using dd like a good linux user <div class="codesnip-container" >
      <div class="bash codesnip">
        wyatt<span class="sy0">@</span>hax0red:~<span class="sy0">/</span>atvusb-creator$ <span class="kw2">dd</span> <span class="re2">if</span>=staging<span class="sy0">/</span>atv_512MB.img <span class="re2">of</span>=<span class="sy0">/</span>dev<span class="sy0">/</span>sdb
      </div>
    </div>

  6. Once that&#8217;s done, pop out the USB drive and plug it back in
  7. You should now be prompted to automount 2 partitions on the drive, the second should be empty
  8. Copy everything from payloads into this mounted directory <div class="codesnip-container" >
      <div class="bash codesnip">
        wyatt<span class="sy0">@</span>hax0red:~<span class="sy0">/</span>atvusb-creator$ <span class="kw2">sudo</span> <span class="kw2">cp</span> <span class="re5">-r</span> payloads<span class="sy0">/</span>patchstick<span class="sy0">/*</span> <span class="sy0">/</span>media<span class="sy0">/</span>PATCHSTICK<span class="sy0">/</span>.
      </div>
    </div>

Hope it works for you! And if not, give it a few, they&#8217;ll have a Windows and Linux version working shortly.

 [1]: http://code.google.com/p/atv-bootloader/
 [2]: http://boxee.tv
 [3]: http://xbmc.org