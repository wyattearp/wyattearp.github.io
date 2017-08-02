---
layout: post
title: "Malduino Elite Expansion Pins"
description: ""
category: 
tags: [technology,malduino]
---
I finally got enough time to get to actually play with my [Malduino Elite](https://malduino.com/) which is a pretty sweet open source USB rubber duck. After dorking around with the base code as well as the [Hack A Day code](https://github.com/kripthor/malduino-elite), I wanted to know what else I could do with those expansion pins.

Here's the details ***I believe that I have correct*** - though I recommend you check before you burn out your own stuff, reference information pulled from the [ATmega32U4](https://www.arduino.cc/en/Hacking/PinMapping32u4):

{% highlight html %}

  +-----------------------------------+
  | TOP                               |
  |    +------------------------+   O | GND
  |    | ON                     |     |
  |    |   +-+  +-+  +-+  +-+   |   O | VCC+ (5V-USB)
  |    |   | |  | |  | |  | |   |     |
  |    |   | |  | |  | |  | |   |   O | PIN09 - SCLK
  |    |   | |  | |  | |  | |   |     |
  |    |   | |  | |  | |  | |   |   O | PIN10 - MOSI
  |    |   +-+  +-+  +-+  +-+   |     |
  |    |    1    2    3    4    |   O | PIN11 - MISO
  |    |                        |     |
  |    +------------------------+   O | RESET
  |                                   |
  +-----------------------------------+

{% endhighlight %}