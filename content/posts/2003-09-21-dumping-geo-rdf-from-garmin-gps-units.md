---
title: Dumping Geo RDF from Garmin GPS units
author: Matt Biddulph
type: post
date: 2003-09-21T19:41:08+00:00
excerpt: \n
url: /2003/09/21/dumping-geo-rdf-from-garmin-gps-units/
categories:
  - python
  - rdf

---
Having [connected my GPS unit to my laptop][1], it was time to dump the data off into a usable RDF model.

<!--more-->

  
There&#8217;s a useful RDF Interest Group [Geo namespace][2] for describing simple lat/long/alt properties of points, so using  
[PyGarmin][3] I wrote [some code][4] to pull off the waypoints and tracklogs and produce a model like [this][5].

 [1]: /archives/000039.html
 [2]: https://www.w3.org/2003/01/geo/
 [3]: https://pygarmin.sourceforge.net/
 [4]: /src/garmin2rdf.py
 [5]: /rdf/tracks.rdf