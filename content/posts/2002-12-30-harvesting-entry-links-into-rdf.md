---
title: Harvesting entry links into RDF
author: Matt Biddulph
type: post
date: 2002-12-30T15:42:13+00:00
excerpt: \n
url: /2002/12/30/harvesting-entry-links-into-rdf/
categories:
  - rdf

---
Continuing the [theme][1] of harvesting information from MT entries into RDF summaries, I wrote another MT plugin ([src][2]) that uses HTML::LinkExtor to extract **<a>** links.

<!--more-->

  
The [RDF for this entry][3] shows that we have xlink:href triples for each link in the entry. Not sure if that&#8217;s a reasonable use of the xlink vocabulary&#8230;

The idea of this extraction is to be able to build better &#8220;more like this&#8221; links between entries; two entries linking to the same URL are going to be related in some way and so should be linked together.

 [1]: /archives/000005.html
 [2]: /src/links2rdf.txt
 [3]: /archives/000008.rdf