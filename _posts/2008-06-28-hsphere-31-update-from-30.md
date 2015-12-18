---
id: 215
title: 'Hsphere 3.1 Update From 3.0 &#8211; UPDATED'
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=215
permalink: /2008/06/28/hsphere-31-update-from-30/
categories:
  - Rants
tags:
  - code
  - hacks
  - hsphere
  - suckfactor5
---
OK, so this went painfully &#8230; very painfully. Let me reiterate &#8230; I flipping HATE H-Sphere and refused to pay $70+ for a service incident that shouldn&#8217;t happen because their crew didn&#8217;t do their homework with testing and didn&#8217;t provide a &#8220;here&#8217;s what to do if things go wrong&#8221; section.

Followed the instructions [here.][1]

Did a **cpupdate** and received this error:

<div class="codesnip-container" >
  > Temporary directory = [ /var/hsphere/update/U31.0.18078 ]<br /> > Current directory === [ /root ]<br /> > Extracting &#8230;<br /> =================================================================<br /> + UPDATE TO U31.0 2008-06-28.12:03<br /> =================================================================<br /> /var/hsphere/update/U31.0.18078<br /> + Executing &#8230;<br /> ########################################<br /> =================================================================<br /> + COMMAND=&#8217;cpupdate&#8217;<br /> =================================================================</p> 
  
  <p>
    __ Update physical boxes.<br /> |<br /> |&#8211; Current CP version: 3.0.828<br /> |&#8211; Current CP Postgres version: 7.4.19.<br /> |<br /> |&#8211; Update of CP box started.<br /> | |&#8211; Install local package updater.<br /> | |&#8211; Update cp box related software.<br /> | | |&#8211; Sat Jun 28 12:03:27 EDT 2008<br /> | | |&#8211; Downloading pkglist (64.131.90.141).<br /> | | | |&#8211; 100% 88,482 &#8211;.&#8211;K/s<br /> | | | `&#8211; Downloaded pkglist.<br /> | | |&#8211; Downloading subpkglist (64.131.90.141).<br /> | | | |&#8211; 100% 4,700 &#8211;.&#8211;K/s<br /> | | | `&#8211; Downloaded subpkglist.<br /> | | |<br /> | | |&#8211; Identifying required packages.<br /> | | |&#8211; OS: CentOS release 4.6 (Final).<br /> | | |&#8211; Perl version: 5.8.5.<br /> | | |&#8211; CP Postgres version: 7.4.19.<br /> | | |&#8211; Downloading hsphere-info-1-14.rpm (64.131.90.141).<br /> | | | |&#8211; 100% 93,483 334.84K/s<br /> | | | `&#8211; Downloaded hsphere-info-1-14.rpm.<br /> | | |&#8211; Installing hsphere-info-1-14 package.<br /> | | | |&#8211; Checked system configuration files.<br /> | | | |&#8211; Formed ips and interface files.<br /> | | | |&#8211; Additional MANPATH entries checked.<br /> | | | |&#8211; TimeZone files checked.<br /> | | | |&#8211; H-Sphere related cron tasks added.<br /> | | |&#8211; Downloading hsphere-utils-1-8.rpm (64.131.90.141).<br /> | | | |&#8211; 100% 2,163,621 3.48M/s<br /> | | | `&#8211; Downloaded hsphere-utils-1-8.rpm.<br /> | | |&#8211; Installing hsphere-utils-1-8 package.<br /> | | | `&#8211;Installing hsphere-utils-1-8 package.<br /> | | |<br /> | | |&#8211; Check whether logical servers are completely configured.<br /> | | | |&#8211; List of identified logical servers: dns, cp.<br /> | | | `&#8211; Check whether logical servers are completely configured.<br /> | | |<br /> | | |&#8211; Check required system packages.<br /> | | | `&#8211; Check required system packages.<br /> | | |<br /> | | |&#8211; Check/download pre-install hsphere core package list.<br /> | | | |&#8211; Downloading hsphere-sudo-1.6.9p14-1.rpm (64.131.90.141).<br /> | | | | |&#8211; 100% 131,287 &#8211;.&#8211;K/s<br /> | | | | `&#8211; Downloaded hsphere-sudo-1.6.9p14-1.rpm.<br /> | | | |&#8211; hsphere-script-runner-1-10.rpm with the same md5sum exist.<br /> | | | |&#8211; hsphere-oscommerce-2.2ms2-3.rpm with the same md5sum exist.<br /> | | | |&#8211; hsphere-phpBB-2.0.22-1.rpm with the same md5sum exist.<br /> | | | |&#8211; hsphere-jdk-1.5.0-13.rpm with the same md5sum exist.<br /> | | | |&#8211; Downloading hsphere-cpanel-javart-3.1-904.rpm (64.131.90.141).<br /> | | | | |&#8211; 100% 24,017,794 2.10M/s ETA 00:00<br /> | | | | `&#8211; Downloaded hsphere-cpanel-javart-3.1-904.rpm.<br /> | | | |&#8211; Downloading hsphere-jakarta-6.0.14-0.rpm (64.131.90.141).<br /> | | | | |&#8211; 100% 4,794,818 4.46M/s<br /> | | | | `&#8211; Downloaded hsphere-jakarta-6.0.14-0.rpm.<br /> | | | |&#8211; Downloading hsphere-cpanel-apache2-2.2.8-2.rpm (64.131.90.141).<br /> | | | | |&#8211; 100% 2,107,508 2.75M/s<br /> | | | | `&#8211; Downloaded hsphere-cpanel-apache2-2.2.8-2.rpm.<br /> | | | |&#8211; Downloading hsphere-core-3.1-904.rpm (64.131.90.141).<br /> | | | | |&#8211; 100% 12,229,070 3.62M/s ETA 00:00<br /> | | | | `&#8211; Downloaded hsphere-core-3.1-904.rpm.<br /> | | | |&#8211; hsphere-aspell-0.60.3-1.rpm with the same md5sum exist.<br /> | | | |&#8211; hsphere-oscommerce-2.2ms2-3.rpm with the same md5sum exist.<br /> | | | |&#8211; hsphere-phpBB-2.0.22-1.rpm with the same md5sum exist.<br /> | | | |&#8211; postgresql-libs-7.4.19-1.rpm with the same md5sum exist.<br /> | | | |&#8211; postgresql-7.4.19-1.rpm with the same md5sum exist.<br /> | | | |&#8211; postgresql-server-7.4.19-1.rpm with the same md5sum exist.<br /> | | | |&#8211; postgresql-contrib-7.4.19-1.rpm with the same md5sum exist.<br /> | | | |&#8211; Downloading hsphere-config-pgsql-1.1-5.rpm (64.131.90.141).<br /> | | | | |&#8211; 100% 10,185 &#8211;.&#8211;K/s<br /> | | | | `&#8211; Downloaded hsphere-config-pgsql-1.1-5.rpm.<br /> | | | |&#8211; hsphere-sudo-1.6.9p14-1.rpm with the same md5sum exist.<br /> | | | |&#8211; hsphere-script-runner-1-10.rpm with the same md5sum exist.<br /> | | | `&#8211; Check/download pre-install hsphere core package list.<br /> | | |<br /> | | |&#8211; Check presence of the deprecated hsphere packages.<br /> | | | `&#8211; Check presence of the deprecated hsphere packages.<br /> | | |<br /> | | |&#8211; Deleting deprecated hsphere packages.<br /> | | | |&#8211; Deleting hsphere-apache-1.3.37-6 package.<br /> | | | | `&#8211; hsphere-apache-1.3.37-6 package deleted.<br /> | | | |&#8211; Deleting hsphere-cpanel-apache-1.3.41-1 package.<br /> | | | | `&#8211; hsphere-cpanel-apache-1.3.41-1 package deleted.<br /> | | | |&#8211; Deleting hsphere-php4-4.4.4-2 package.<br /> | | | | `&#8211; hsphere-php4-4.4.4-2 package deleted (nodeps).<br /> | | | |&#8211; Deleting hsphere-php4-plugins-4.4.4-2 package.<br /> | | | | `&#8211; hsphere-php4-plugins-4.4.4-2 package deleted.<br /> | | | |&#8211; Deleting hsphere-php5-5.2.0-1 package.<br /> | | | | `&#8211; hsphere-php5-5.2.0-1 package deleted (nodeps).<br /> | | | |&#8211; Deleting hsphere-php5-plugins-5.2.0-1 package.<br /> | | | | `&#8211; hsphere-php5-plugins-5.2.0-1 package deleted.<br /> | | | `&#8211; Deleting deprecated hsphere packages.<br /> | | |<br /> | | |&#8211; Check/Installing pre-install hsphere core package list.<br /> | | | |&#8211; Deleting hsphere-sudo-1.6.9p6-1 package.<br /> | | | | `&#8211; hsphere-sudo-1.6.9p6-1 package deleted (nodeps).<br /> | | | |&#8211; Installing hsphere-sudo-1.6.9p14-1 package.<br /> | | | | `&#8211;Installing hsphere-sudo-1.6.9p14-1 package.<br /> | | | |&#8211; Deleting hsphere-cpanel-javart-3.0-828 package.<br /> | | | | `&#8211; hsphere-cpanel-javart-3.0-828 package deleted.<br /> | | | |&#8211; Installing hsphere-cpanel-javart-3.1-904 package.<br /> | | | | |&#8211; removing redundant jar files<br /> | | | | `&#8211;Installing hsphere-cpanel-javart-3.1-904 package.<br /> | | | |&#8211; Deleting hsphere-jakarta-5.5.16-0 package.<br /> | | | | `&#8211; hsphere-jakarta-5.5.16-0 package deleted (nodeps).<br /> | | | |&#8211; Installing hsphere-jakarta-6.0.14-0 package.<br /> | | | | |&#8211; Existing cpanel user changed.<br /> | | | | |&#8211; *** Conversion has not been done. ***<br /> | | | | `&#8211;Installing hsphere-jakarta-6.0.14-0 package.<br /> | | | |&#8211; Installing hsphere-cpanel-apache2-2.2.8-2 package.<br /> | | | | |&#8211; Temporary certificate assigned self-signed CA Certificate created.<br /> | | | | |&#8211; Cpanel apache started.<br /> | | | | `&#8211; hsphere-cpanel-apache2-2.2.8-2 package installed.<br /> | | | |&#8211; Deleting hsphere-core-3.0-828 package.<br /> | | | | `&#8211; hsphere-core-3.0-828 package deleted.<br /> | | | |&#8211; Installing hsphere-core-3.1-904 package.<br /> | | | | |&#8211; Existing cpanel user changed.<br /> | | | | |&#8211; Existing cpanel user changed.<br /> | | | | `&#8211;Installing hsphere-core-3.1-904 package.<br /> | | | |&#8211; Deleting postgresql-libs-7.4.19-1.el4_6.1 package.<br /> | | | | `&#8211; postgresql-libs-7.4.19-1.el4_6.1 package deleted (nodeps).<br /> | | | |&#8211; Deleting postgresql-7.4.19-1.el4_6.1 package.<br /> | | | | `&#8211; postgresql-7.4.19-1.el4_6.1 package deleted (nodeps).<br /> | | | |&#8211; Deleting postgresql-server-7.4.19-1.el4_6.1 package.<br /> | | | | `&#8211; postgresql-server-7.4.19-1.el4_6.1 package deleted (nodeps).<br /> | | | |&#8211; Deleting postgresql-contrib-7.4.19-1.el4_6.1 package.<br /> | | | | `&#8211; postgresql-contrib-7.4.19-1.el4_6.1 package deleted.<br /> | | | |&#8211; Deleting hsphere-config-pgsql-1.1-4 package.<br /> | | | | `&#8211; hsphere-config-pgsql-1.1-4 package deleted.<br /> | | | |&#8211; Installing hsphere-config-pgsql-1.1-5 package.<br /> | | | | |&#8211; **** Can not find startup file.<br /> | | | | `&#8211; hsphere-config-pgsql-1.1-5 package installed.<br /> | | | |&#8211; Deleting hsphere-sudo-1.6.9p6-1 package.<br /> | | | | `&#8211; *** hsphere-sudo-1.6.9p6-1 package deletion error! For more details see /hsphere/pkg/updates/U31.0//U31.0/update_28.06.08_12_03.log file (209.173.159.100) ***<br /> | | |<br /> | | |&#8211; Sat Jun 28 12:07:21 EDT 2008 (update time: 3 min, 54 sec)<br /> | | `&#8211; *** Update cp box related software problems ***.<br /> =================================================================<br /> + COMMAND=&#8217;cpupdate&#8217;<br /> =================================================================
  </p>
  
  <p>
    __ Update physical boxes.<br /> |<br /> |&#8211; Current CP version: 3.1.904<br /> `&#8211; *** CP Postgres version: authentication access problem! ***<br /> =================================================================<br /> + COMMAND=&#8217;x&#8217;<br /> =================================================================<br /> + Cleaning &#8230;<br /> + Finished
  </p>
</div>

Well, that didn&#8217;t work, so lets just try it again:

<div class="codesnip-container" >
  =================================================================<br /> + COMMAND=&#8217;cpupdate&#8217;<br /> =================================================================</p> 
  
  <p>
    __ Update physical boxes.<br /> |<br /> |&#8211; Current CP version: 3.1.904<br /> `&#8211; *** CP Postgres version: authentication access problem! ***<br /> =================================================================<br /> + COMMAND=&#8217;x&#8217;<br /> =================================================================<br /> + Cleaning &#8230;<br /> + Finished
  </p>
</div>

Unfortunately, searching the Internet and H-Sphere&#8217;s site turned up nothing helpful on the issue except this [thread][2] &#8230; which didn&#8217;t match my situation and didn&#8217;t have anything in it except telling me to buy a new support request.

So since I refuse to pay for something I&#8217;ve already paid for, here&#8217;s the solution to fix it for the rest of you:

<div class="codesnip-container" >
  <div class="bash codesnip">
    rpm <span class="re5">-qa</span> <span class="sy0">|</span><span class="kw2">grep</span> postgresql <span class="sy0">|</span><span class="kw2">xargs</span> rpm <span class="re5">-e</span> <span class="re5">&#8211;nodeps</span><br /> rpm <span class="re5">-Uvh</span> <span class="sy0">/</span>hsphere<span class="sy0">/</span>pkg<span class="sy0">/</span>postgresql<span class="sy0">*</span><span class="nu0">19</span><span class="sy0">*</span>.rpm<br /> rpm <span class="re5">-Uvh</span> <span class="re5">&#8211;force</span> <span class="sy0">/</span>hsphere<span class="sy0">/</span>pkg<span class="sy0">/</span>hsphere-config-pgsql-<span class="nu0">1.1</span>&#8211;<span class="nu0">5</span>.rpm
  </div>
</div>

Then back into the H-Sphere updater:

<div class="codesnip-container" >
  <div class="bash codesnip">
    <span class="kw2">sh</span> <span class="sy0">/</span>hsphere<span class="sy0">/</span>U31.0<br /> cpupdate
  </div>
</div>

And the peasants rejoice &#8230; until they try to SSH in. The stupid jaild package that&#8217;s provided is busted in so may ways. The easiest solution is to just edit /etc/passwd to a real shell location; however, you&#8217;ll give up security to make this happen so I&#8217;ll leave the choice to you.

**Update 07/12/2008:**  
Fixed the jaild issue. Apparently, when you do the update, if ANY user is logged in and has an actively running process (yes, I tried it multiple ways) &#8230; the jail setup fails oddly and doesn&#8217;t allow ANY user to log into the system. The solution? Boot all the users off the box:

> /etc/init.d/sshd stop  
> killall sshd 

Reconfig the jaild:

> /hsphere/local/config/jail/scripts/config_jail 

H-sphere&#8217;s attempt [here][3]

 [1]: http://www.parallels.com/en/psoft/release_notes_hsphere/
 [2]: http://www.forum.psoft.net/showthread.php?t=23299
 [3]: http://www.forum.psoft.net/showthread.php?t=26812