---
title: The PL2303 serial-USB adapter and Linux
author: Matt Biddulph
type: post
date: 2003-09-21T18:47:11+00:00
excerpt: \n
url: /2003/09/21/the-pl2303-serial-usb-adapter-and-linux/
categories:
  - hardware
  - linux

---
A short note to fill in for something I couldn&#8217;t find via google on getting a PL2303-based serial-USB adapter to work with linux&#8230;

<!--more-->

  
Recently I was trying to connect a [Garmin Geko 201][1] GPS unit to [my laptop][2] on a 2.4 series linux kernel using a no-brand generic USB serial port cable bought from Maplin.

I encountered the problem described in this [post to linux-kernel][3]: the device would work once after boot, then oops the kernel when it was closed. To use it again, I&#8217;d have to reboot.

The solution, in my case, was to recompile my kernel (or change my choice of loaded kernel modules) to use the usb-uhci.o module as my UHCI controller, instead of the &#8220;alternative (JE)&#8221; driver that I had been using.

 [1]: https://www.garmin.com/products/geko201/
 [2]: /archives/000025.html
 [3]: https://www.google.com/url?sa=U&start=1&q=https://www.uwsg.iu.edu/hypermail/linux/kernel/0307.1/0438.html&e=747