---
title: Taking automated webpage screenshots with embedded Mozilla
author: Matt Biddulph
type: post
date: 2004-06-13T14:35:11+00:00
excerpt: \n
url: /2004/06/13/taking-automated-webpage-screenshots-with-embedded-mozilla/
categories:
  - python

---
The other day I discovered [Hotlinks][1], a rather nice link aggregator. It collects links from sites (including those of a couple of my [respected][2] [colleagues][3]) and combines them into a good-looking summary page. I particularly like the automatic webpage thumbnails it makes, which are created using [khtml2png][4]. I couldn&#8217;t get khtml2png to compile on my machine. After finding that there are now [python wrappers for GtkMozEmbed][5], I made my own screenshotter-and-thumbnailer by embedding the Mozilla browser component using a little [python script][6].

_UPDATE:_ Ross Burton picked up the script and [made a couple of enhancements][7]. Miguel de Icaza posted a [C# version][8].

<!--more-->

  
To run, you&#8217;ll need PyGtkMoz, Gtk and the Python Imaging Library. Because it&#8217;s a GTK app, it needs an X server. To run headless, it&#8217;ll need an X server like Xnest or VNC. VNC&#8217;s working well for me.

The way it works is very simple:

Starting with the example.py shipped with PyGtkMoz, I created a stripped-down browser window app that loads a URL given on the commandline. By connecting the `net_stop` signal to a method, you can tell when network activity has finished. I couldn&#8217;t find a way to be notified when rendering has finished (images decompressed, etc) so I put in a 3 second pause here.

Following clues in  [a GTK mailing list post][9], I wrote these lines to save a PNG of my widget&#8217;s window:

    `window = self.widget.window`  
    `(x,y,width,height,depth) = window.get_geometry()`  
    `pixbuf = gtk.gdk.Pixbuf(gtk.gdk.COLORSPACE_RGB,False,8,width,height)`  
    `pixbuf.get_from_drawable(window,self.widget.get_colormap(),0,0,0,0,width,height)`  
    `pixbuf.save("<a href="https://www.hackdiary.com/misc/screenshot-hackdiary.png">screenshot.png</a>","png")`

After that, producing a thumbnail just takes a few more lines of PIL code to open, thumbnail and save the PNG under a new name:

[![][10]][11]

 [1]: https://dev.upian.com/hotlinks/
 [2]: https://www.paranoidfish.org
 [3]: https://www.plasticbag.org
 [4]: https://www.babysimon.co.uk/khtml2png/
 [5]: https://sourceforge.net/projects/pygtkmoz
 [6]: https://www.hackdiary.com/src/screenshot.py
 [7]: https://www.burtonini.com/blog/computers/mozilla-thumbnail-20040614.xhtml
 [8]: https://primates.ximian.com/~miguel/all.html#6%2f14%2f2004%201%3a55%3a00%20PM
 [9]: https://mail.gnome.org/archives/gtk-app-devel-list/2003-December/msg00382.html
 [10]: https://www.hackdiary.com/misc/thumbnail-hackdiary.png
 [11]: https://www.hackdiary.com/misc/screenshot-hackdiary.png