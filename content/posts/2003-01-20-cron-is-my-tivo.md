---
title: Cron is my TiVo
author: Matt Biddulph
type: post
date: 2003-01-20T17:09:24+00:00
excerpt: \n
url: /2003/01/20/cron-is-my-tivo/
categories:
  - hardware
  - linux

---
One thing I&#8217;d like to do with a [silent PC][1] is make a homebrew TiVo-alike. Well, I would if I watched any TV. Which I don&#8217;t. But still, the idea interests me beyond any use I&#8217;d actually make of it. Anyway&#8230;

In the past, this idea has been beyond my means since recording analogue TV to MPEG on a hard disk in realtime requires a great deal of CPU (or dedicated encoder hardware). The general availability of digital TV in the UK now means that the MPEG encoding is already done for you by the broadcasters; you just need a way to get it out of the airwaves or cables and into a PC. Happily, there&#8217;s now a range of cheap digital WinTV cards for cable, terrestrial and satellite. I&#8217;ve been checking out a [NOVA-t][2] (terrestrial) card on a linux box this week.

<!--more-->

  
The wonderful thing about the drivers and utilities that have been written so far is that they are simple commandline tools, easily pipeable and cronable. There are just two key commands &#8211; dvbtune to tune into a multiplex and dump the &#8216;table of contents&#8217; listing all the channel available, and dvbstream to extract an audio+video mpeg stream or an entire transport stream (the data stream containing all the audio, video and data from all the channels on a mux) and stream it to stdout or multicast it.

Getting the drivers set up is the fiddly bit; this took me a day or two until I stumbled across the right combination of driver, dvbstream and dvbtune versions. [A post][3] on the linux-dvb list helped me a lot there. Basically you should use the latest CVS version of everything. There are [nightly CVS snapshots][4] of the drivers, but the rest will probably have to be dragged direct out of the relevant CVS.

To tune into the 16QAM 506Mhz multiplex containing BBC2 at Crystal Palace and output the service information as XML ([looks like this][5]):

_dvbtune -f 506000000 -i -qam 16 -cr 3_4_

To capture 10 seconds of audio/video mpeg stream direct from BBC2 (video PID 610, audio PID 611):

_dvbstream -n 10 -ps -c 0 610 611 -o > out.mpg_

or pipe it into mplayer to play it directly:

_dvbstream -n 10 -ps -c 0 610 611 -o | mplayer -cache 2048 &#8211;_

To re-scale and re-encode the video as MPEG4 and the audio as VBR MP3 to save diskspace (but retain quality comparable to the original MPEG):

_mencoder -o out.avi -vop scale=512:288 -ovc lavc -lavcopts vcodec=mpeg4:vbitrate=1500 -oac mp3lame -lameopts fast:preset=medium out.mpg_

This results in a [2 megabyte AVI file][6]. At this bitrate, a complete hour can be recorded in about 700meg, which would fit on a CDR. Since digital terrestrial TV carries a programme guide in the datastream on PID 0x12, it should be possible to extract that, parse it and use it to trigger recordings based on programme names. I haven&#8217;t found anything about how to do so yet.

_UPDATE:_ It seems there is more than one variant of card being sold with the WinTV Nova-T PCI name. Someone I know recently bought a card and the chipset used was completely different from the one I have, and wasn&#8217;t supported by the linux-dvb drivers. Unfortunately we haven&#8217;t worked out a way to distinguish supported from unsupported cards without opening the retail pack and inspecting the card itself.

_FURTHER UPDATE:_ The linux-dvb drivers now support the new chipset (using the tda1004x driver added earlier this year). The driver requires a copy of a DLL from the Windows driver, as detailed in the [README][7].

 [1]: /archives/000016.html
 [2]: https://www.hauppauge.co.uk/html/digitaltv_prod.htm#novatpci
 [3]: https://www.linuxtv.org/mailinglists/linux-dvb/2003/01-2003/msg00331.html
 [4]: https://www.linuxdvb.tv/download/
 [5]: /misc/service_information.xml
 [6]: /misc/sample.avi
 [7]: https://www.linuxtv.org/cgi-bin/cvsweb.cgi/DVB/driver/frontends/README.tda1004x?rev=1.2&content-type=text/x-cvsweb-markup