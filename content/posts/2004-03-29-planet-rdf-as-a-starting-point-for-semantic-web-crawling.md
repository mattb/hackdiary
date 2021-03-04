---
title: Planet RDF as a starting-point for semantic web crawling
author: Matt Biddulph
type: post
date: 2004-03-29T02:58:16+00:00
excerpt: \n
url: /2004/03/29/planet-rdf-as-a-starting-point-for-semantic-web-crawling/
categories:
  - rdf

---
I was thinking about [scuttering][1] and useful ways to gather information. It occurred to me that as well as following `rdfs:seeAlso` links as usual, it was worth scanning associated HTML for semantic links (eg [FOAF autodiscovery metadata][2]). I decided to use the [blogroll][3] at [Planet RDF][4] as a testing ground, on the assumption that if anyone was going to embed useful metadata in their HTML, it would be the hackers listed there.

<!--more-->

  
I should note that when [Dave][5] puts together the blogroll, he generally insists that the RSS we point to is parseable RDF, and not just [tag soup][6] that carries no meaning to a semantic web-aware client. This is well in keeping with the theme of the site and gives us a useful starting point for scuttering.

I hacked up [some rough code][7] pretty quickly (cribbing and adapting from [some Mark Pilgrim code][8] where necessary). It visits each RSS file in the blogroll with an RDF parser and finds the channel link. It downloads the HTML from there and looks for link tags pointing to rdf/xml. Finally, it outputs a new blogroll augmented with extra `rdfs:seeAlso` links, and combines all the discovered RDF into a single model.

I ran the code ([full log text][9]), and it gathered a [big bundle of information about the bloggers][10] and an [augmented blogroll][11].

I discovered that in the 33 weblogs listed:

  * 11 publish some sort of RDF link in their HTML (but one was a 404).
  * 9 of these RDF links were to FOAF files.
  * 2 didn&#8217;t publish parseable XML in their RSS due to Unicode or character encoding issues.
  * 2 had moved their RSS feeds to a new location pointed to by a 302.
  * One is publishing RSS 2.0 under an RDF link.
  * One of the links in the blogroll points to an RDF file that isn&#8217;t RSS (but there is an RSS file available on another URL).

When I&#8217;ve got some more hacking time, I&#8217;ll get back to this dataset and do some more analysis. Smushing the blogroll against the gathered data (via the weblog property, an IFP), it&#8217;ll be possible to build a little visualisation of who knows who on the Planet RDF planet, and gather some extra info to put on the site itself (thumbnail author images, for example). It&#8217;d be great to see more people put a link to their FOAF in their blog HTML.

 [1]: https://www.hackdiary.com/archives/000045.html
 [2]: https://rdfweb.org/topic/Autodiscovery
 [3]: https://journal.dajobe.org/journal/2003/07/semblogs/bloggers.rdf
 [4]: https://www.planetrdf.com
 [5]: https://journal.dajobe.org
 [6]: https://blogs.law.harvard.edu/tech/rss
 [7]: https://www.hackdiary.com/src/foafscan.py
 [8]: https://diveintomark.org/projects/misc/autorss/autorss.py.txt
 [9]: https://www.hackdiary.com/misc/foafscan.log.txt
 [10]: https://www.hackdiary.com/misc/gathered.rdf
 [11]: https://www.hackdiary.com/misc/augmented-blogroll.rdf