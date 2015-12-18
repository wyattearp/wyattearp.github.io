---
id: 205
title: How to Make Developers Hate Your Platform
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=205
permalink: /2008/04/21/how-to-make-developers-hate-your-platform/
categories:
  - Rants
  - Technology
tags:
  - c++
  - carbide.c++
  - development
  - e61
  - nokia
  - s60
  - symbian
  - visual stuido
---
As a developer, I constantly use API&#8217;s and platforms created by others to develop software &#8230; just like every other developer in the world.

Well, I got it in my head that I wanted to write an application for the S60 3rd Ed. platform, the same one that runs on my Nokia E61. So first things first, I head over and download the SDK from Symbain, which requires registration, but I&#8217;m used to that so I don&#8217;t mind. Well, there are two downloads &#8230; the SDK files &#8230; and then the recommended IDE to build the application in without the SDK files. Which brings me to the first way to make developers hate your platform.

**1. Make the IDE not include the SDK files**

OK, I get that not everyone wants to use Carbide.c++ to develop their application in &#8230; especially since Nokia charges for it. And just so you know, Carbide.c++ is nothing more than Eclipse SDK with Nokia&#8217;s extra bells and whistles.

**2. Steal open source IDE&#8217;s and call them your own**

Screw that, I&#8217;ll use my copy of Visual Studio and run with it for free and not pay for your more than likely busted-ass Eclipse plug-in. I&#8217;m sure that if I *really* wanted, I could break apart your stupid Carbide.c++ plug-in to not require any registration for all your &#8220;features&#8221; in your stolen IDE. Whatever, I&#8217;ll start downloading the 400mb of SDK from Nokia and while that downloads and I&#8217;ll read some more on how to build a Symbian application instead of wasting my time (I like Visual Studio better for Windows style development anyway.)

Now if you&#8217;ve never played with a Nokia application, all of the applications have to be signed with a certificate &#8230; which is really, REALLY frustrating. You can&#8217;t install an application unless it has been signed, which brings about the question, &#8220;Why the frick can&#8217;t I choose what to install on my phone???&#8221; It&#8217;s my phone, if I want to melt it into a pile of goo after I write 0-s to the stupid flash module on it, I should be able to do that &#8230; especially if I&#8217;m a developer.

Well, alright, I&#8217;ll go get a certificate so I can test my application on my own phone. There are a ton of places that tell you how to do this. [Here][1], [here][2], or [here][3] &#8230; but they&#8217;ve all been replaced with go to [SymbianSigned.com][4] method. Fine, I&#8217;ll go here and get a certificate &#8230; oh wait, I can&#8217;t, I have to register to get a developer certificate. OK, I&#8217;ll register &#8230; again &#8230; CRAP!

> Your email has address has been rejected as we do not accept registrations from publicly available email domains (e.g. gmail, yahoo, hotmail etc).

Well, I&#8217;m glad I have another domain name in my pocket &#8230; not everyone does Symbian, you flippin&#8217; jackasses. Alright, now I&#8217;m registered at another site (that I couldn&#8217;t use my perfered email address at) so I can get a developer certificate just for my phone. Which brings me to my next way to make developers hate you:

**3. Make it so developers can&#8217;t test their applications without restrictions**

Trying to get a certificate results in a:

> Your request has failed. Reason:  
> -Developer Certificates will be ENABLED for users who have a Publisher ID ONLY  
> -ONLY if you used a Publisher ID to create a .csr file with the DevCertCreate tool will you be able to use Open Signed Offline to create a Developer Certificate.  
> -Developer Certificates are currently DISABLED for users without a Publisher ID. Users who DO NOT have a Publisher ID CANNOT request Developer Certificates or use Open Signed Offline.  
> -If you have recently obtained a Publisher ID and are unable to create a Developer Certificate using Open Signed Offline please request support through the Symbian Signed forum on the Symbian Developer Network. 

**4. Make the development process painful by requiring developers to send you their applications before usage.**

Well that&#8217;s just fricken great, I can&#8217;t even test my application on **MY PHONE THAT I BOUGHT WITH MY MONEY**. FINE, where do I get the stupid fricken Publisher ID? Oh wait, that&#8217;s **$200** per year to get a certificate (A.K.A Publisher ID) so you can take your stupid application, submit it to THEIR test center, so they can charge you **$20** for each submission that THEY HAVE TO TEST so that it can be Symbian signed so &#8220;normal&#8221; users can actually install your application.

<font size="+2">F &#8211; THAT!</font>

I&#8217;m not going to pay $200/year so I can give away an application for free. I&#8217;ll go write apps for Windows Mobile or the fricken iPhone or some other platform because of this crap. Screw you Symbian. Screw you.

 [1]: http://www.n91.us/nokia-n91-tips-tricks/howto-self-sign-symbian-sis-application-files-16.html
 [2]: http://symbianwebblog.wordpress.com/2007/11/27/8/
 [3]: http://then95blog.wordpress.com/2008/01/23/how-to-sign-symbian-applicationsagain-but-very-simple-this-time/
 [4]: http://www.symbiansigned.com