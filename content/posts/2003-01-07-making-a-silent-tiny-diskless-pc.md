---
title: Making a silent, tiny, diskless PC
author: Matt Biddulph
type: post
date: 2003-01-07T10:48:32+00:00
excerpt: \n
url: /2003/01/07/making-a-silent-tiny-diskless-pc/
categories:
  - hardware
  - linux
tags:
  - ""

---
For a while I&#8217;ve wanted a home PC that I can leave on all the time without the noise bugging me &#8211; I&#8217;ve become quite sensitive to machine noise over years of working with computers. I&#8217;d use it to play MP3s off my network, then I&#8217;d think up other projects. It wouldn&#8217;t need a monitor or a keyboard. It would just sit attached to the network, appliance-style, in the manner of a [slimp3][1] but with the flexibility of a full linux system. Now the off-the-shelf hardware I need to make such a thing is available.

<!--more-->

  
The [Via Eden ME6000][2] motherboard is full of integrated components (TV output, network, firewire, 5.1 sound with digital out, etc) and has a fairly powerful processor that needs no fan on its heatsink. Combined with a stick of memory and a [Morex 55W fanless external power supply][3], and booted diskless off the network, this system has no moving parts.

The bits arrived yesterday and after a bit of setup I got it booting Debian off the network and playing its first MP3 by the end of the evening. It&#8217;s all-but-silent; the DC-DC converter makes a very slight high-pitched noise, a little like the noise a TV makes with the sound off. It&#8217;ll be easily muffled inside some sort of box. The motherboard makes no noise at all. Playing MP3s with mpg123 takes about 7% CPU according to top.

Here&#8217;s a picture:

[![][4]][5]

 [1]: https://www.slimdevices.com
 [2]: https://www.viavpsd.com/product/epia_m_spec.jsp?motherboardId=81
 [3]: https://www.mini-itx.com/store/default.asp?c=9#p67
 [4]: https://www.hackdiary.com/pics/via1_small.jpg
 [5]: https://www.hackdiary.com/pics/via1.jpg