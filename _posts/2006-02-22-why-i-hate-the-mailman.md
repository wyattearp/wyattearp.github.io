---
id: 75
title: Why I hate the MailMan
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=75
permalink: /2006/02/22/why-i-hate-the-mailman/
categories:
  - Rants
---
No, not the USPS guy, but that stupid ass little program that does email list management. All I did was flip the switch in postfix to say &#8220;hey, you now can host virtual domains&#8221; and BAM!!! Mailman instantly vomits all over itself like a bunch of wookies at a fur-ball contest. And of course, there are thousands of people on the net with my exact same problem:

Final-Recipient: rfc822; &#8212;&#8211;@freeplay.hackerforhire.org  
Original-Recipient: rfc822; &#8212;&#8211;@hackerforhire.org  
Action: failed  
Status: 5.0.0  
Diagnostic-Code: X-Postfix; Command died with status 2:  
&#8220;/usr/local/mailman/mail/mailman post &#8212;&#8211;&#8220;. Command output: Group mismatch  
error. Mailman expected the mail wrapper script to be executed as group  
&#8220;mailman&#8221;, but the system&#8217;s mail server executed the mail script as group  
&#8220;nobody&#8221;. Try tweaking the mail server to run the script as group  
&#8220;mailman&#8221;, or re-run configure, providing the command line option  
\`&#8211;with-mail-gid=nobody&#8217;.

Seems sort of obvious that I want the program to run with its own damn permissions. Well trying to find the solution to this is about as difficult as Micheal Jackson not using a daycare as a drive through. I tried every possible fix that I could and then I finally found something that seemed just so stupid it might be right. Apparently, if you have multiple aliases files (which I was unaware that I had) and one of them belongs to root, postfix will just star executing every damn thing it can as &#8216;nobody&#8217; because that&#8217;s who owns every fricken file on you damn hard drive &#8230; NOT!!!

Shesh &#8230; that took me 4 hours to find. I figured I&#8217;d post it here in case I ever needed to do it again.

>