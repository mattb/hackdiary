---
title: Sha1ing, smushing and aggregating FOAF
author: Matt Biddulph
type: post
date: 2003-02-03T00:02:38+00:00
excerpt: \n
url: /2003/02/03/sha1ing-smushing-and-aggregating-foaf/
categories:
  - foaf
  - java
  - rdf

---
To normalise and aggregate FOAF metadata related to photographs, I needed some new code to:

  * convert foaf:mbox entries to privacy-protected foaf:mbox_sha1sum entries.
  * normalise statements of the form &#8220;PICTURE depicts PERSON&#8221; to &#8220;PERSON depiction PICTURE&#8221;.
  * smush disparate references to the same person into references to a single definition of that person.
  * extract depiction triples from a model and copy just the bare minimum of information related to those depictions

So I wrote [foaftool][1], a Java class that uses [Jena][2]. The tarball also contains a couple of servlets that can be used to transform existing content on the web.

<!--more-->

  
The first servlet will transform foaf:mbox triples in FOAF data into appropriately-encoded foaf:mbox_sha1sum triples. This makes [Edd&#8217;s FOAF file][3] look [like this][4]. Using an extra querystring parameter, it optionally [converts foaf:depicts triples to foaf:depiction][5]. foaf:depicts isn&#8217;t actually in the official [FOAF schema][6] at the time of writing, although it is in informal use in many places as it sometimes makes for more elegant modeling. Normalising to foaf:depictions makes working with large amounts of FOAF data simpler.

Writing the [smushing][7] code was an entertaining diversion. Smushing is important when merging multiple RDF sources. Say you have two sources, [edd1.rdf][8] and [edd2.rdf][9], showing where to find photos of Edd. When merged, the graph structure looks like this:

[<img class="noborder" width="500" height="166" alt="edd1.rdf" src="/images/edd1_small.png" />][10]  
[<img class="noborder" width="468" height="166" alt="edd1.rdf" src="/images/edd2_small.png" />][11]

This is because without smushing, the anonymous nodes that both have Edd&#8217;s email address are not equated. The [smushed version][12] (smushed on mbox_sha1sum using a foaftool servlet) looks like this:

[<img class="noborder" width="502" height="209" alt="edd1.rdf" src="/images/eddsmush_small.png" />][13]

With the data in normalised and merged form, I want to extract just the triples of the form &#8220;X foaf:depiction [picture uri]&#8221; and the related foaf:name and foaf:mbox_sha1sum triples. With the foaftool code, I can now [merge and extract depictions][14] from any number of RDF sources.

Comments and bugfixes are very welcome; the code has only been tested as far as the junit tests included in the tarball.

 [1]: https://www.hackdiary.com/src/foaftool-0.2.tar.gz
 [2]: https://www.hpl.hp.com/semweb/jena.htm
 [3]: https://heddley.com/edd/foaf.rdf
 [4]: https://www.hackdiary.com/foaf/apps/foafToSha1?foaf=https://heddley.com/edd/foaf.rdf
 [5]: https://www.hackdiary.com/foaf/apps/foafToSha1?foaf=https://heddley.com/edd/foaf.rdf&convertDepicts=1
 [6]: https://xmlns.com/foaf/0.1/
 [7]: https://rdfweb.org/2001/01/design/smush.html
 [8]: https://www.hackdiary.com/misc/edd1.rdf
 [9]: https://www.hackdiary.com/misc/edd2.rdf
 [10]: /images/edd1.png
 [11]: /images/edd2.png
 [12]: https://www.hackdiary.com/foaf/apps/aggregateDepictions?rdf=https://www.hackdiary.com/misc/edd1.rdf&rdf=https://www.hackdiary.com/misc/edd2.rdf
 [13]: /images/eddsmush.png
 [14]: https://www.hackdiary.com/foaf/apps/aggregateDepictions?rdf=https://www.picdiary.com/rss/xcom.rss&rdf=https://www.picdiary.com/rss/foafmeet.rss&rdf=https://www.picdiary.com/rss/barcelona_conf.rss&rdf=https://www.picdiary.com/rss/pantsconkeevil.rss