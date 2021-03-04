---
title: An RDF crawler
author: Matt Biddulph
type: post
date: 2003-04-21T14:33:33+00:00
excerpt: \n
url: /2003/04/21/an-rdf-crawler/
categories:
  - java
  - rdf

---
I wrote an RDF crawler (aka [scutter][1]) using Java and the Jena RDF toolkit that spiders the web gathering up semantic web data and storing it in any of Jena&#8217;s backend stores (in-memory, Berkeley DB, mysql, etc). [Download it here][2].

<!--more-->

  
The system is multithreaded and so can simultaneously download from many sources while the aggregation thread does the processing. It builds a model that remembers the provenance of the RDF and takes care to delete and replace triples if it hits the same URL twice, so you can run it as often as you like to keep the data fresh without bloating the store with out-of-date information. As yet it doesn&#8217;t do anything with what it gathers; the information&#8217;s just sitting there waiting for interesting applications to be built on top of it.

To use it as distributed, set up a mysql database called &#8220;scutter&#8221; and set the username and password in the DBConnection setup in Scutter.java then recompile using &#8216;ant compile&#8217; (sorry, no handy config files in this 0.1 release). Run the script scutter.sh passing in as many starting-point URLs as you like. These will be added to the queue, and any rdfs:seeAlso pointers in the downloaded RDF will be recursively followed until no more unique URLs can be found. The biggest known issue at the moment is that it doesn&#8217;t do proper management to work out when it&#8217;s run out of URLs &#8211; it just stops. The standard log4j.properties file can be edited to change what gets logged &#8211; with full debugging information turned on, you get [quite a lot of output][3].

Plans for the future include tying [FOAF][4]-related processing into the aggregation such as [smushing and mbox_sha1sum normalising][5], and making a publish/subscribe-based system so that people who can&#8217;t run their own aggregators can subscribe to the RDF that&#8217;s gathered.

 [1]: https://rdfweb.org/topic/ScutterSpec
 [2]: /src/hackscutter-0.1.tar.gz
 [3]: /misc/scutter.log.txt
 [4]: https://rdfweb.org/foaf/
 [5]: https://www.hackdiary.com/archives/000021.html