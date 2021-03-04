---
title: Audioscrobbler meets the commandline
author: Matt Biddulph
type: post
date: 2004-05-03T22:50:14+00:00
excerpt: \n
url: /2004/05/03/audioscrobbler-meets-the-commandline/
categories:
  - python

---
It&#8217;s been around for a while, but suddenly [everyone&#8217;s][1] [talking][2] about [audioscrobbler][3] again. I got interested when I saw a talk about [last.fm][4] at [dorkbot][5] a few months back. It&#8217;s based on the simple idea of instrumenting your music player to send a ping to a central site every time you&#8217;re listening to a track. Going further than just a &#8216;now playing&#8217; on a sidebar on your website, this leads to a world of potential new music toys using collaborative filtering and the like.

At home I play all my music from the commandline: my mp3 jukebox has no fancy user interface, I just SSH into it. Audioscrobbler have several player plugins for [download][6], but no commandline interface. I wrote myself some [python code to play MP3s and talk to audioscrobbler][7] so that I could keep [my profile][8] up to date.

<!--more-->

  
Popping onto the [audioscrobbler IRC channel][9], I found [Russ][10] and [RJ][11], two key guys behind the system. They were very helpful, sorting me out with a client ID for testing and giving debugging tips.

As so often happens, the python community had already supplied all the libraries I need to make the guts of my system: [pymad][12] to decode MP3s, [pyao][13] for audio output, [pyid3lib][14] to read ID3 tags. Building the code was just a matter of following the protocol documentation and writing about 100 lines to stick it all together.

The [Audioscrobbler protocol][15] is very nice. Top marks for using the web the way it was designed, letting me GET the details I need to start a session (MD5 challenge, URL to submit to, etc) and then POST my information to affect my user profile. The protocol used within the transaction doesn&#8217;t use RDF or XML, which would be my choice, but it is nice and simple, reminiscent of traditional text-based internet protocols such as SMTP and POP3.

Now I&#8217;ve reached this simple goal (a commandline MP3 player with no controls that submits &#8216;now playing&#8217; information), I&#8217;d like to take it further. If I had a newer iPod, it&#8217;d be great to write a bit of code to submit tracks I&#8217;ve been playing on the move to my profile, but sadly my iPod is of too early a generation to have that feature. More interestingly, I look forward to being able to make use of audioscrobbler&#8217;s analysis to build my own playlists and discover new music. For now this is mostly only doable through the audioscrobbler site, but there are also [data dumps][16] available. It&#8217;d be great to have a combination of the two &#8211; an online REST query interface that gives machine-readable results.

Oh, and don&#8217;t forget&#8230; [donate to Audioscrobbler][17] and keep a great project online.

 [1]: https://cityofsound.typepad.com/
 [2]: https://www.gyford.com/phil/writing/2004/04/15/audioscrobbler.php
 [3]: https://www.audioscrobbler.com
 [4]: https://last.fm
 [5]: https://www.music.columbia.edu/pipermail/dorkbotlondon-blabber/2004-February/000277.html
 [6]: https://www.audioscrobbler.com/download.php
 [7]: https://www.hackdiary.com/src/scrobbler.py
 [8]: https://www.audioscrobbler.com/user/biddulph
 [9]: irc://irc.phasenet.co.uk/audioscrobbler
 [10]: https://www.audioscrobbler.com/user/Russ
 [11]: https://www.audioscrobbler.com/user/RJ
 [12]: https://spacepants.org/src/pymad/
 [13]: https://freshmeat.net/projects/pyao/
 [14]: https://pyid3lib.sourceforge.net/
 [15]: https://wiki.audioscrobbler.com/index.php/Protocol1.1
 [16]: https://www.audioscrobbler.com/development.php
 [17]: https://www.audioscrobbler.com/donate.php