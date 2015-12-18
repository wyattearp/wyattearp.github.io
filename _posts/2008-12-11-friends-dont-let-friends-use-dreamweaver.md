---
id: 254
title: 'Friends Don&#8217;t Let friends Use Dreamweaver'
author: Wyatt
excerpt: Two of my friends and I have spent nearly 2 days fixing 5 pages that were "generated" by Dreamweaver
layout: post
guid: http://blog.hackerforhire.org/?p=254
permalink: /2008/12/11/friends-dont-let-friends-use-dreamweaver/
categories:
  - Rants
  - Technology
tags:
  - code
  - editors
  - web
---
Really .. they don&#8217;t. No one should every be allowed to &#8220;generate,&#8221; and I use that term so loosely, a website from what they create in [Dreamweaver][1]. Two of my friends and I have spent nearly 2 days fixing 5 pages that were &#8220;generated&#8221; by Dreamweaver. Has any one ever looked at the crap HTML it generates??? It&#8217;s absolutely nuts. The cramming of all the style sheets in to anonymous names and stuffed at the top of each HTML is beyond ridiculous. And don&#8217;t even get me started on the static layout of all the pages it trys to render by default. I took at page that was &#8220;generated&#8221; by Dreamweaver and ran it though the [W3C Markup Validation Service][2] &#8230; 138 errors. And not hard to catch errors &#8230; they obvious really stupid errors. Missing tags, improper style declarations, style declarations to absolutely nothing on the page; the list goes on.

So moral of the story &#8230; don&#8217;t let anyone use Dreamweaver to PRODUCE the live version of a website. Build it in a REAL editor like Notepad, [Vim][3], [The Programmer&#8217;s Notepad][4], or [TextMate][5]. Hell, build it in Visual Studio&#8217;s text editor &#8230; just don&#8217;t trust some bloated, crappy tool to produce something functional for you.

 [1]: http://www.adobe.com/products/dreamweaver/
 [2]: http://validator.w3.org/
 [3]: http://www.vim.org
 [4]: http://www.pnotepad.org/
 [5]: http://macromates.com/