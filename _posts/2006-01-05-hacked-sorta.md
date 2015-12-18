---
id: 47
title: Hacked, Sorta
author: Wyatt
excerpt: Great, just what I need after working on hardening an IIS box for 16 hrs, my own server that is so often neglected gets taken (you system administrators know exactly where I am coming from).
layout: post
guid: http://blog.hackerforhire.org/?p=47
permalink: /2006/01/05/hacked-sorta/
categories:
  - Rants
---
Well, if you don&#8217;t know it already, Hacker For Hire was &#8220;hacked&#8221; in the loosest sense of the term. What does that mean you ask? I&#8217;ll tell you in a moment, don&#8217;t interrupt me. Because knowing how to find out what a hacker did is just as important as knowing how to be a hacker, we&#8217;ll just follow along his path.  
<!--more-->

  
It&#8217;s been a long day being as I haven&#8217;t really slept, and I get an email about my site being a phishing scam for PayPal. Great, just what I need after working on hardening an IIS box for 16 hrs, my own server that is so often neglected gets taken (you system administrators know exactly where I am coming from). Here is the &#8220;attack&#8221; if you can even call it that:

Jan 4 16:56:35 freeplay sshd[29816]: Accepted password for mythtv from 85.186.190.23 port 2381 ssh2

Boy, that was hard &#8230; especially considering this is my MythTV box and the password is &#8216;mythtv&#8217;

This is followed by an SFTP request to send files 

Jan 4 20:16:33 freeplay sshd[30352]: subsystem request for sftp

I&#8217;ve got the sftp log somewhere, but I don&#8217;t think that I really need it because I&#8217;m fairly certain that he/she just pulled the files from the previous IP address.

Next, a public_html was setup under the mythtv user, and the email address judgebeng@yahoo.com was specified as the person to send the personal information to. There were some other miscellaneous commands, but being as the mythtv user is relatively locked down, there weren&#8217;t many places they could go.

Finally, a [post][1] to my blog about how I host sites that extort money from people. This could have been someone completely different being as the IP address was now coming from Amsterdan instead of Romania, but the post time is only minutes after the last login by &#8216;mythtv&#8217; on January 5.

Being the responsible system administrator that I try to be, I brought down the server, hashed the log files with MD5 and SHA-1 to provide some integrity, backed up the logs, traced down the IP addresses, email addresses, and other fun information and put them in a nice report. I sent a report to the FBI, Yahoo, PayPal, and Bank of America. I figure that I could care less about my MythTV box being hacked, but maybe they can use it to pin down some jerk who is making the world a less fun place to live.

And not to forget the final step, &#8220;Lessons Learned.&#8221; SSH was modified so that logging was increased, only specified users are allowed to use SSH to access the system. All passwords for all users have been changed and I&#8217;m experimenting with ssdfilter, Fail2Ban, and DenyHosts to help me combat this ever grown number of attempts to break into my system.

Just a couple of quick stats for fun:

Number of invalid login attempts in the past 3 months &#8211; **97456**  
Number of SSH exploit attempts in the past 3 months &#8211; **1346**  
Number of unique IP addresses blocked in the past 3 months &#8211; **486**  
Number of hours I&#8217;ve spent in system administration in the past 3 months &#8211; **4**

 [1]: http://blog.hackerforhire.org/?p=46#comments