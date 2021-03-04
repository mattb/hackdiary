---
title: Ericsson Bluetooth phone as remote control
author: Matt Biddulph
type: post
date: 2003-08-03T23:36:27+00:00
excerpt: \n
url: /2003/08/03/ericsson-bluetooth-phone-as-remote-control/
categories:
  - hardware
  - python

---
After seeing Richard Clamp&#8217;s excellent talk at a london.pm techmeet on [using Ericsson phones as remote controls][1] I went away to code something similar (but less fully-functioned) in python for my own use. My code plugs into the [Twisted][2] framework and listens for phone keypress events. It uses the AT commands defined in [an Ericsson PDF for the R320 phone][3], and it works with my T610.

<!--more-->

  
My main need for a remote was for controlling slides when doing presentations, so I looked into how to send fake keypresses to X applications. My presentation format of choice is PDFs, so I just needed to be able to send PgUp and PgDown events to Acrobat Reader.

X has a useful extension called XTEST that is designed to help automated testing of GUI apps. It has [a fairly simple API][4], and with the help of the source of the [X11::GUITest CPAN module][5] I created a python extension that lets me write code such as `keycontrol.tapkey('PGU')` to simulate tapping on the PgUp key.

The [resulting code][6] defines an `Ericsson` class that can be subclassed to receive events such as `cursor_left` and `camera` when the keys are pressed on the phone. It helps to have the keypad lock activated when using it so that you don&#8217;t end up triggering events on the phone itself.

Libby Miller took [a photo of me using it][7] at the [XML Summer School][8] Semantic Web forum, where it came in very handy. The phone is just visible in my right hand.

 [1]: https://unixbeard.net/~richardc/cgi/blog.cgi/dea.pod/
 [2]: https://www.twistedmatrix.com/
 [3]: https://www.ericsson.com/mobilityworld/developerszonedown/downloads/docs/r320/R320s_WP_R1A.pdf
 [4]: https://member.nifty.ne.jp/tsato/xvkbd/events.html
 [5]: https://search.cpan.org/author/CTRONDLP/X11-GUITest-0.16/
 [6]: /src/blueremote-1.0.tar.gz
 [7]: https://swordfish.rdfweb.org/photos/2003/07/30/2003-07-30-Pages/Image3.html
 [8]: https://www.xmlsummerschool.com