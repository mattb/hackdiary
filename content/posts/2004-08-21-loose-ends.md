---
title: Loose ends
author: Matt Biddulph
type: post
date: 2004-08-21T22:26:10+00:00
excerpt: \n
url: /2004/08/21/loose-ends/
categories:
  - rdf

---
This weekend I&#8217;m at [EuroFoo][1], and I&#8217;ve managed to find some happy hacking time. [Jim Ley][2] and [Dan Brickley][3] are around, and they&#8217;ve been nudging me into fixing up and releasing some old code.

<!--more-->

  
Firstly, I have [a bunch of old RDF photo annotation demos][4] that had bitrotted quite badly due to new releases of Wordnet in debian. All but one of those are now working again. This will make Jim happy.

Secondly, I&#8217;ve been trying for ages to finish a rewrite of my [RDF crawler][5] in Python. It&#8217;s got a much nicer architecture than the old one, being based on a pipeline of optional processors implementing smushing, FOAF mbox normalisation and interfaces to Joseki and various other storage mechanisms. I&#8217;ve stalled, so [here&#8217;s the work in progress][6]. It requires python 2.3, [Redland][7] and [Twisted][8]. It will start from one or more URLs passed on the command line, and follow seeAlsos until it can find no more. This will make Dan happy.

 [1]: https://wiki.oreillynet.com/eurofoo/index.cgi
 [2]: https://jibbering.com
 [3]: https://danbri.org/
 [4]: https://www.hackdiary.com/archives/000034.html
 [5]: https://www.hackdiary.com/archives/000030.html
 [6]: https://www.hackdiary.com/src/scutter.py
 [7]: https://www.redland.opensource.ac.uk/
 [8]: https://www.twistedmatrix.com/