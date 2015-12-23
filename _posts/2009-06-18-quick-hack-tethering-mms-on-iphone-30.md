---
id: 380
title: 'Quick Hack:  Tethering &#038; MMS on iPhone 3.0'
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=380
permalink: /2009/06/18/quick-hack-tethering-mms-on-iphone-30/
categories:
  - Rants
tags:
  - iphone
  - mms
  - quick hacks
  - tethering
---
Just because I spent so much time looking for this last night and found so many broken carrier data files, I figured I&#8217;d keep this around for me.

**Instructions**

  * Make a backup of your /Library/iTunes/iTunes Carrier Support/ATT_US.ipcc file.
  * Quit iTunes
  * Open Terminal and type &#8220;defaults write com.apple.iTunes carrier-testing -bool TRUE&#8221;
  * Open iTunes, select your phone and press &#8220;check for updates&#8221; while holding down the &#8216;Alt&#8217; key on your keyboard. You will be prompted to select a file. [This][1] is the one that worked for me after numerous other failures. (found in gizmodo&#8217;s cache somewhere)
  * After you load the file, make sure you restart the phone

Instructions for Windows are the same, but you&#8217;ll have to use the Windows Paths for stuff (C:\Program Files\iTunes\blah blah blah).

Right, and I&#8217;m not responsible for you running up a trillion dollar bill with AT&T or if your spine curves or if your teeth yellow or if you drink rat poison because you fell in love with a rough trick named Jim or anything else as a result of you trying to do something to your bejebus phone <img src="http://blog.hackerforhire.org/wp-includes/images/smilies/simple-smile.png" alt=":-)" class="wp-smiley" style="height: 1em; max-height: 1em;" />

 [1]: {{ site.baseurl }}/wp-content/uploads/2009/06/att_us.ipcc