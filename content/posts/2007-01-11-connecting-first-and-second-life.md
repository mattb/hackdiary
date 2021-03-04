---
title: Connecting First and Second Life
author: Matt Biddulph
type: post
date: 2007-01-11T22:40:00+00:00
excerpt: \n
url: /2007/01/11/connecting-first-and-second-life/
categories:
  - hardware

---
I&#8217;ve been interested for some time in the possibilities offered by [bringing external data into virtual environments like Second Life][1]. This data might [come from the web][2], but it could also come from the real world &#8211; from physical sensors and interfaces.

Over the last couple of weeks I&#8217;ve [enjoyed][3] [playing][4] with the [Arduino][5] hardware prototyping board. This week&#8217;s [open-sourcing of the Second Life client][6] came at exactly the right time for a new experiment.

Here&#8217;s a video demonstration (people reading the feed, start your web browsers). On the left you&#8217;ll see an Arduino reading analogue values from a potentiometer and feeding the results in via the USB-serial interface to my Mac. On the right, you&#8217;ll see a modified version of Second Life that is feeding those values in via my avatar&#8217;s chat channel. An object in the Second Life world is reacting, with perhaps a half-second lag.



<!--more-->

  
How does this work? All it takes is a few small code fragments in the right places. The Arduino code is trivial:

<pre class="codeblock">void setup() {
Serial.begin(9600);
pinMode(0,INPUT);
}
void loop() {
delay(100);
Serial.println(analogRead(0));
}
</pre>

The in-world LSL code is trivial:

<pre class="codeblock">vector pos;
default
{
state_entry()
{
llListen(42,"Matt Basiat",NULL_KEY,"");
pos = llGetPos();
}
listen(integer channel, string name, key id, string message) {
float val = (float)message;
llSetPos(pos + &lt;0,0,(val/100.0)>);
}
}
</pre>

The clever bit, such as it is, involves adding a bit of good old-fashioned Unix file-descriptor code to the SL client&#8217;s idle loop (located in `viewer.cpp` in the source) that polls the Arduino. Once I&#8217;ve got the reading, all it takes to make my avatar speak to the server is the line:

<pre class="codeblock">gChatBar->sendChatFromViewer(reading, CHAT_TYPE_NORMAL, FALSE);
</pre>

In total, I added about 150 lines of code to a single file to achieve this. Obviously this is just a concept demo, and there are plenty of places to take it from here, but I&#8217;m encouraged by the progress.

If you&#8217;re curious about the details, here&#8217;s [the patch][7] against `viewer.cpp` in the `newview` directory of the source. It&#8217;s definitely not The Right Way To Do It &#8211; just the fastest route I could find into the heart of the code. It has hardcoded device names and other bad practice. I release it under the GPL, and must thank Tod Kurt for the use of his [arduino-serial.c][8] code and [Massimo Banzi][9] for everything he taught me about Arduino over the holiday season.

 [1]: https://www.hackdiary.com/archives/000098.html
 [2]: https://www.hackdiary.com/archives/000085.html
 [3]: https://www.flickr.com/photos/mbiddulph/353389659/
 [4]: https://www.flickr.com/photos/alexandra666/341328079/
 [5]: https://www.arduino.cc/
 [6]: https://secondlife.com/developers/opensource/
 [7]: https://www.hackdiary.com/misc/secondlife-arduino-demo.patch
 [8]: https://todbot.com/blog/2006/12/06/arduino-serial-c-code-to-talk-to-arduino/
 [9]: https://www.potemkin.org/