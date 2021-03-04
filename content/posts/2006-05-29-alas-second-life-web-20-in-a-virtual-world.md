---
title: Alas, Second Life! Web 2.0 in a virtual world
author: Matt Biddulph
type: post
date: 2006-05-29T23:37:00+00:00
excerpt: \n
url: /2006/05/29/alas-second-life-web-20-in-a-virtual-world/
categories:
  - web

---
[Second Life][1] has been my new hacking obsession ever since I bought a laptop fast enough to run it. I don&#8217;t spend a lot of time socialising in the gameworld, but I am fascinated by the possibilities for makers of new user interfaces, useful virtual objects and playful toys. With every object being scriptable, aware and active, it&#8217;s a proving ground for [Everyware][2].

Version 1.10 was released last week, and hidden among the exciting new visual modeling possibilities of shiny rendering and flexible objects was Second Life&#8217;s own XMLHTTPRequest: [llHTTPRequest][3]. Using asynchronous callbacks, it gives the platform an important new capability: communication with the web on demand. A lot of what we are learning about AJAX makes sense here, in this world of Asynchronous Lindenscriptinglanguage And Some-sort-of-data (ALAS!)

I&#8217;ve spent a few hours hacking on some toy objects with this new capability, starting with the mashup de rigeur: [Flickr][4] integration. My home in SL now sports a simple picture frame. Touch it and it looks up your avatar name to see what your favourite Flickr tag is, picks a random picture with that tag from Flickr and displays it on its surface. If it hasn&#8217;t met you before, it asks you to tell it what tag to use.

Because Second Life is so wonderfully visual, here&#8217;s a little demo movie that I recorded with [Tom Coates][5]:



<!--more-->

## how it works

_UPDATE: [source code is available][6]_

LSL is a rather limited C-like scripting language with a couple of interesting features (like its native support for state-machines to respond to events). As far as I&#8217;ve been able to work out, it lacks the ability to parse XML or JSON, and has no native associative array type. Objects can store some state, but it is a little fragile in the face of resets. I decided not to try accessing the Flickr API directly, or using local storage. Instead, I created a stateful web companion for my new object with a bit of serverside Rails.

Strings and lists are the most useful datatypes available, and there&#8217;s a function similar to perl&#8217;s &#8216;split&#8217; for turning strings into lists. This makes pipe-delimited a reasonable format for simple data. I created the following web resources:

`/seen?user=SomeAvatar`: Records that the object has sensed the presence of SomeAvatar

`/touched?user=SomeAvatar`: In response to a &#8216;touch&#8217; event, consults the database for the user&#8217;s tag and asks the Flickr API for a random photo with that tag. Returns a string such as `https://flickr.com/some/photo.jpg|SomeAvatar|`, or `UNKNOWN`.

`/set_tag?user=SomeAvatar&tag=sausages`: Records SomeAvatar&#8217;s favourite tag

The HTTP system is nicely responsive: using the web as my object&#8217;s outboard brain added only a tiny bit of latency to the mix. The asynchronous model allowed other processing to continue while waiting for a response. With these URLs ready to respond, I wired up the appropriate Second Life events using [llSensorRepeat][7] and [sensor][8] for presence, [llListen][9] and [listen][10] to respond to spoken commands, and [touch_start][11] for the physical interface. The [llParcelMediaCommandList][12] features are confusing (and only work on land you own, with movie streaming enabled in the client), but I found the [source code for Freeview][13] to be a useful reference.

If you&#8217;re interested in this code, or would like to see a demo, you can find me from time to time in SL as Matt Basiat.

 [1]: https://www.secondlife.com/
 [2]: https://www.alistapart.com/articles/everyware
 [3]: https://secondlife.com/badgeo/wakka.php?wakka=llHTTPRequest
 [4]: https://flickr.com/
 [5]: https://plasticbag.org/
 [6]: https://www.hackdiary.com/archives/000087.html
 [7]: https://secondlife.com/badgeo/wakka.php?wakka=llSensorRepeat
 [8]: https://secondlife.com/badgeo/wakka.php?wakka=sensor
 [9]: https://secondlife.com/badgeo/wakka.php?wakka=llListen
 [10]: https://secondlife.com/badgeo/wakka.php?wakka=listen
 [11]: https://secondlife.com/badgeo/wakka.php?wakka=touch_start
 [12]: https://secondlife.com/badgeo/wakka.php?wakka=llParcelMediaCommandList
 [13]: https://www.simteach.com/wiki/index.php?title=SL_FreeView