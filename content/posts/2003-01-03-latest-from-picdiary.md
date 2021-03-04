---
title: Latest from Picdiary
author: Matt Biddulph
type: post
date: 2003-01-03T15:27:33+00:00
excerpt: \n
url: /2003/01/03/latest-from-picdiary/
categories:
  - perl
  - photos
  - rdf
  - rss

---
New in the right-hand sidebar on the [site front page][1] is a little lineup of the 3 latest pictures from [picdiary][2], my photos website. This is created by parsing the RDF in the [latest photo collection RSS feed][3] and extracting rss:title, dc:date and foaf:thumbnail information via an MT plugin ([src][4]).

<!--more-->

  
The code uses RDF::Core::Parser from CPAN, which is a nice simple RDF parser that works much like SAX does for XML. You register an Assert callback with the parser which gets called once for each RDF statement found in the RDF it parses.

A very satisfying hack. RDF and HTTP makes this stuff so easy.

 [1]: /
 [2]: https://www.picdiary.com
 [3]: https://www.picdiary.com/cgi-bin/latest.pl
 [4]: /src/picdiarylatest.txt