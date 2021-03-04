---
title: XML TV Listings in RDF
author: Matt Biddulph
type: post
date: 2003-09-07T17:18:33+00:00
excerpt: \n
url: /2003/09/07/xml-tv-listings-in-rdf/
categories:
  - bots
  - python
  - xml

---
In preparation for a TiVoBot that I&#8217;m planning to write as a wrapper for scheduling [digital WinTV recordings][1], I&#8217;ve been looking at TV listings data produced by tools from the [XMLTV][2] project. I started out using the XML directly and storing it using [Berkeley DB XML][3] but soon found (like most of my projects) that I&#8217;d be happier if the data was expressed as an RDF model.

<!--more-->

  
The current [XMLTV DTD][4] turns out to be pretty [RDF-friendly][5] in its structure. This [XML example][6] looks very similar [as RDF][7] ([graph][8]). The major changes I made in the translation were in assigning URIs to channels and programme categories, using identifiers such as `https://xmlns.com/2003/rdftv/channel#bbc3.bbc.co.uk` and `https://xmlns.com/2003/rdftv/category/ananova#News/CurrentAffair`, and giving the tv data a namespace under <https://xmlns.com>. The conversion is performed by [some XSLT][9].

Taking a [complete TV feed as RDF][10], I can now write [query code][11] using [Redland][12] and Python to print out details of all films on TV this week.

 [1]: /archives/000018.html
 [2]: https://membled.com/work/apps/xmltv/
 [3]: https://www.sleepycat.com/xml
 [4]: https://cvs.sourceforge.net/cgi-bin/viewcvs.cgi/*checkout*/xmltv/xmltv/xmltv.dtd?rev=1.27
 [5]: https://www.xml.com/pub/a/2002/10/30/rdf-friendly.html
 [6]: /rdf/xmltv.xml
 [7]: /rdf/rdftv.rdf
 [8]: /rdf/rdftv.png
 [9]: /rdf/xmltv2rdf.xsl
 [10]: /rdf/rdftv_complete.rdf
 [11]: /src/tv.py
 [12]: https://www.redland.opensource.ac.uk