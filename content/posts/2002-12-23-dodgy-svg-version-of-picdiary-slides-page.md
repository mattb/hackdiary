---
title: Dodgy SVG version of picdiary slides page
author: Matt Biddulph
type: post
date: 2002-12-23T13:32:00+00:00
excerpt: \n
url: /2002/12/23/dodgy-svg-version-of-picdiary-slides-page/
categories:
  - foaf
  - javascript
  - photos
  - svg
  - wordnet

---
I felt it was time to learn a bit more about SVG and do some concrete work with it. I made a fairly simple SVG document that renders picdiary feeds. It parses the RSS and builds the page on the client-side using Jim Ley&#8217;s lovely [javascript rdf parser][1].

Compare the [HTML version][2] to the [SVG version][3]. There&#8217;s nothing in the SVG version that couldn&#8217;t be rendered in HTML; the interest was in doing the job entirely client-side.

<!--more-->

  
The system builds links into [foafnaut][4] and my wordnet picture hierarchy when it finds appropriate metadata about a picture.

Jim&#8217;s parser page says the RDF parser needs at least version 5.5 to run under IE. Javascript in SVG is a pain to debug in mozilla; you don&#8217;t seem to be able to use mozilla&#8217;s javascript console or debugger.

 [1]: https://jibbering.com/rdf-parser/
 [2]: https://www.picdiary.com/new/xcom
 [3]: https://www.picdiary.com/svg/pics.svg?rss=xcom.rss
 [4]: https://www.foafnaut.org