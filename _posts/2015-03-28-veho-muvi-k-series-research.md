---
id: 474
title: veho Muvi K-Series Research
author: Wyatt
layout: post
guid: http://blog.hackerforhire.org/?p=474
permalink: /2015/03/28/veho-muvi-k-series-research/
categories:
  - Rants
---
I recently picked up a veho Muvi K-Series action camera &#8230; and the application on Android didn&#8217;t work for anything. So I started down my own path.

Rather than put all the details here, I decided that I was going to primarily work out of a git repo (after the jump) in the event that I decided anything worthwhile should be developed to work with the camera over wifi. What I found was a couple of key points:

  * The support from veho&#8217;s technical team was terrible; essentially every email I sent them was worse than chucking it into a blackhole because at least the blackhole wouldn&#8217;t respond with insane questions
  * The camera is linux based and runs a very simple configuration that is some how statically limited based on what&#8217;s been included
  * Muvi&#8217;s camera and application look to be blatently stolen from AEE Action Camera which appears to be blatently stolen from GoPro &#8230; but at each effort of &#8220;stealifying&#8221; they&#8217;ve made it suck just a little more

Due to the fact that the camera&#8217;s quality was kind of terrible (random blocks of video would just jump in and out) and the SD card that was shipped with it was broken and wouldn&#8217;t function in anything, I decided to send it back. But I&#8217;ve collected all of my comments, code, research, etc. into the <a title="Research into connecting to the VEHO Muvi K-Series action camera" href="https://github.com/wyattearp/muvi_kseries_research" target="_blank">muvi_kseries_research repository</a> for anyone else that would like to poke, prod, or build their own application for whatever reason. Enjoy and let me know if you found anything helpful.