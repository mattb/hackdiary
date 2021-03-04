---
title: Wordnet-based search engine for picdiary
author: Matt Biddulph
type: post
date: 2002-11-29T10:48:00+00:00
excerpt: \n
url: /2002/11/29/wordnet-based-search-engine-for-picdiary/
categories:
  - photos
  - rss
  - wordnet

---
This search engine uses [wordnet][1] to find synonyms of search terms, and hypernyms of marked-up keywords. So a search for [skyscraper][2] finds one picture and a search for [structure][3] finds the skyscraper and a load of other pictures too.

<!--more-->

  
The pics are marked up in the RSS-based picture collections using markup like this:

<item rdf:about=&#8221;https://www.picdiary.com/kensington/img_1926.jpg&#8221;>  
<foaf:depicts><wordnet:Telephone /></foaf:depicts>  
</item>

Search results are actually returned in RSS; the html search page is just a wrapper around that. So you can subscribe to [pictures of shops][4] if you really want to.

Next steps:

  * Add &#8220;more like this&#8221; links to picture pages that find pictures by navigating the wordnet space
  * make a dmoz-style directory of pictures arranged into the wordnet hierarchy
  * do similar things with FOAF person information
  * do location annotation using jo&#8217;s [geonet-based namespace][5]
  * tie it all together into some sort of coherent website

 [1]: https://www.cogsci.princeton.edu/~wn/
 [2]: https://www.picdiary.com/cgi-bin/search.pl?word=skyscraper
 [3]: https://www.picdiary.com/cgi-bin/search.pl?word=structure
 [4]: https://www.picdiary.com:8180/rss/servlet/search?word=shop
 [5]: https://space.frot.org/mudengland.html