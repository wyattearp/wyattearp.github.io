---
id: 416
title: Stupid iPhone and Stupid Tethering
author: Wyatt
excerpt: "The last time I installed the tethering packages from Cydia, I lost access to voicemail for 2 weeks, couldn't get them to uninstall, yada-yada-yada, annoying experience. But today, I actually had time to think about how to solve this issue and then it hit me: I'm a moron; I should have seen this last year. Five minutes later, I was on the net."
layout: post
guid: http://blog.hackerforhire.org/?p=416
permalink: /2010/07/17/stupid-iphone-and-stupid-tethering/
categories:
  - General
  - Technology
  - Tips from a Hack
tags:
  - iphone
  - ssh
  - tether
  - tethering
---
I was sitting at a coffee shop today I was disappointed I forgot to ask for the wifi key. Now I could totally sit here and crack the WEP key, but that takes precious CPU and battery life and well, I just wasn&#8217;t that interested in getting the tools to compile for my Mac. This led me to wax poetic about the days I used to have a tether to my iPhone 3G and I thought &#8230; &#8220;Man, I would sure like to be able to tether again;&#8221; but the last time, that didn&#8217;t go over so well. The last time I installed the tethering packages from Cydia, I lost access to voicemail for 2 weeks, couldn&#8217;t get them to uninstall, yada-yada-yada, annoying experience. But today, I actually had time to think about how to solve this issue and then it hit me: I&#8217;m a moron, I should have seen this last year. Five minutes later, I was on the net.  
<!--more-->

  
At the very basic level, tethering is nothing more than providing a way to share your phone&#8217;s connection to the internet. I&#8217;ve been using a similar tool for years to do the same sort of thing, **ssh**. So why not just use that again? For all you hackers out there, he&#8217;s the quick and dirty in 10 easy steps:

  1. Jail-break your iPhone.  I recommend any of the following the procedures <a href="http://gizmodo.com/tag/iphone-jailbreak/" target="_blank">here</a>
  2. Install SSH using Cydia
  3. Setup a computer-to-computer network in whatever capacity you like (yea Mac!)
  4. Join your iPhone to the computer-to-computer network
  5. Open up a terminal and ping the broadcast address to find you iPhone (or whatever other method you want to find the IP address of the Iphone)
  6. SSH over to your iPhone and change your password and install a public-private key pair
  7. SSH back over to your iPhone using a command like this \`ssh root@<iphone_ip> -D8080\` to setup a SOCKS proxy tunnel
  8. Setup your web browser to use a SOCKS proxy using any way you like (<a href="http://www.google.com/search?q=use+SSH+proxy" target="_blank">examples here</a>)
  9. Open your iPhone and go to some web-page to get a 3G data IP address
 10. Start surfing the web on your &#8220;tethered&#8221; iphone

That&#8217;s all there is to it.  Now you can &#8220;tether&#8221; your iPhone, share the connection, whatever you want.  Oh, and AT&T can&#8217;t actually &#8220;tell&#8221; you&#8217;re tethering without some effort.  Now there are obviously more things you can do to make life easier like:

  * Installing the SSH reconnection tool
  * Disabling SSH timeouts with
  * Automatically connecting the Data IP address when you SSH

However, those are left as an exercise to the reader.  Don&#8217;t you hate it when people do that?  I know I do.  Friggen jerks.