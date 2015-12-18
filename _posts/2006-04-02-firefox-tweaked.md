---
id: 91
title: Firefox Tweaked
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=91
permalink: /2006/04/02/firefox-tweaked/
categories:
  - Rants
  - Technology
---
OK, first off, I love Firefox. It&#8217;s great; however, there are several things that just annoy the hell out of me. For example:

  1. No &#8220;X&#8221; on each tab
  2. Google Search not maintained per tab
  3. Default loading of links in background
  4. Crashes loose my tabs

However my friends, I have found the tweakers delight :-). Now, I know it&#8217;s been documented other places; however, I&#8217;m just going to put it here in the event that I blow something up and loose my stuff &#8230; it&#8217;s also for your benefit if you want to use it. Three of the above can be fixed in the magical &#8220;about:config&#8221; tab. The remaining has an extension to fix it. Ready to tweak? Great. Here comes the meat:  
<!--more-->

  
**1. No &#8220;X&#8221; on each tab**  
This is an easy fix. Open about:config in a new tab or window and put **extensions.tabprefs.showTabButton** in the filter area. Right click the value and choose toggle. Restart Firefox to complete the changes.

**2. Google Search not maintained per tab**  
Again, another easy fix, just not documented well. Fire up about:config again and this time find the value **extensions.tabprefs.searchbar**. Right click and toggle and you&#8217;re in business. Restart if the changes don&#8217;t take occur when you fire up a new tab.

**3. Default loading of links in background**

Don&#8217;t recognize this one? Well, here&#8217;s the skinny. Apparently the default behavior of Firefox is to start caching links on a page in the background &#8230; a trick from back in the dial up days to make browsing better. Since I live in the world of high speed &#8230; this is damned annoying to me. Again, fire up about:config and search for **browser.sessionhistory.max\_total\_viewers**. Change this value to 0 and restart Firefox to make the change.

**4. Crashes loose my tabs**  
This one requires an extension to fix. Head on over to [the SessionSaver][1] and do the download and install thing. Restart and tweak the changes to your delight and now crashes and accidental tab closures are no longer a bother.

While you&#8217;re in about:config, you may want to poke around and see if there is anything else cool you can convince the beast to do :twisted:. Let me know if you find anything spiffy.

 [1]: https://addons.mozilla.org/extensions/moreinfo.php?id=436&application=firefox