---
title: Extracting a social graph from Wikipedia people pages
author: Matt Biddulph
type: post
date: 2012-04-05T00:27:58+00:00
url: /2012/04/05/extracting-a-social-graph-from-wikipedia-people-pages/
categories:
  - data
  - graphs

---
I&#8217;ve been in San Francisco this week giving a workshop at the Where Conference called [Prototyping Location Apps With Big Data][1]. You can read the full slides for the workshop [on Slideshare][2] and get the full code and sample data [on Github][3].

The key message of the workshop is that there are plenty of open datasets available on the web which can be used to prototype new applications by acting as proxies for the kind of data you expect to have later in the product lifecycle. You just have to do a bit of lateral thinking and some data-processing. For example, wouldn&#8217;t it be great if you were working on a social site and could test your designs, your algorithms and your scalability using a realistic social graph of 300,000 people with over 2 million connections between them? It&#8217;d be much better than entering a test dataset by hand using just a few examples from people you know or your family, and it&#8217;d make for a much better demo if you took it to an investor or a product board. No more [lorem ipsum!][4]

We can generate such a dataset using Wikipedia. Consider the [Wikipedia page for Bill Clinton][5]. In just the first three paragraphs there are mentions of people highly related to the former US President: Hillary Clinton, George H.W. Bush and Franklin D. Roosevelt. If we were to consider these intra-wiki links as connections in the social graph (&#8220;Bill Clinton knows Hillary Clinton&#8221;) and perform this extraction over all of Wikipedia then we&#8217;d have a pretty convincing graph. It would have lots of connections, a good mix of communities (politicians, historical figures, television personalities) and a nice mix of well-connected and less-connected people.

Raw Wikipedia text is [openly available for download][6] but parsing it is difficult, and doesn&#8217;t give us the kind of structured and typed data that we&#8217;re looking for. Luckily [the DBpedia project][7] has already tackled this problem. They have extracted page types, images, geocoded coordinates, intra-wiki links and many other things, and made them all [downloadable][8]. For this hack we&#8217;ll need the &#8220;[Ontology Infobox Types][9]&#8221; and the &#8220;[Wikipedia Pagelinks][10]&#8221; datasets.

The types file has one or more lines for each Wikipedia page. For example, the page for [Autism][11] is listed as a [Thing][12] and a [Disease][13]. We&#8217;ll filter this file down to just the [Person][14] pages. Then we&#8217;ll take the links file and filter it down to just the links that are from a Person to another Person (by using the filtered types file we just made). We can do all of this with [18 lines of Apache Pig code][15] then run it through a Hadoop cluster. You can see [sample results][16] in the Github project. If we convert it to GraphML format with a [JRuby script][17] (using the [JUNG library][18]) and load it into [Gephi][19] to detect the communities and create a force-directed layout, we get a pleasant and interesting social graph with all the kinds of clusters we&#8217;d expect:

[<img title="Social Graph of Wikipedia" src="https://farm8.staticflickr.com/7100/7046439385_b83413587a_b.jpg" alt="" width="500" height="500" />][20]

You can also explore a [simplified version of this graph][21] in PDF format for your zooming pleasure.

 [1]: https://whereconf.com/where2012/public/schedule/detail/23080
 [2]: www.slideshare.net/mattb/where-2012-prototyping-workshop
 [3]: https://github.com/mattb/where2012-workshop
 [4]: https://en.wikipedia.org/wiki/Lorem_ipsum
 [5]: https://en.wikipedia.org/wiki/Bill_Clinton
 [6]: https://en.wikipedia.org/wiki/Wikipedia:Database_download
 [7]: https://dbpedia.org/About
 [8]: https://wiki.dbpedia.org/Downloads37
 [9]: https://wiki.dbpedia.org/Downloads37#ontologyinfoboxtypes
 [10]: https://wiki.dbpedia.org/Downloads37#wikipediapagelinks
 [11]: https://en.wikipedia.org/wiki/Autism
 [12]: https://www.w3.org/TR/owl-guide/#DefiningSimpleClasses
 [13]: https://dbpedia.org/ontology/Disease
 [14]: https://xmlns.com/foaf/spec/#term_Person
 [15]: https://github.com/mattb/where2012-workshop/blob/master/wikipedia-graph/peoples.pig
 [16]: https://raw.github.com/mattb/where2012-workshop/master/wikipedia-graph/sample-data/sample-10000.txt
 [17]: https://github.com/mattb/where2012-workshop/blob/master/wikipedia-graph/graphml.rb
 [18]: https://jung.sourceforge.net/
 [19]: https://gephi.org/
 [20]: https://www.flickr.com/photos/mbiddulph/7046439385/
 [21]: https://biddul.ph/wikipedia-graph