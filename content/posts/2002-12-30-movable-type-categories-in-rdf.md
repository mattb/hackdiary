---
title: Movable Type categories in RDF
author: Matt Biddulph
type: post
date: 2002-12-30T02:28:52+00:00
excerpt: \n
url: /2002/12/30/movable-type-categories-in-rdf/
categories:
  - java
  - rdf

---
I&#8217;m collating writings about my various hacks and projects in a Movable Type system, but hopefully without actually creating a blog as such. I&#8217;d rather generate ad-hoc navigation based on the categories of the items, so creating RDF-based sitemaps seems like a good idea.

<!--more-->

  
Step 1 is a [template][1] that generates RDF for each entry (eg [the metadata for this entry][2]).  
Step 2 is a simple RDF widget ([src][3]) that builds an [aggregate model][4] of the metadata for each entry.  
Step 3 will be to build navigation based on that. To get a flavour of the possibilities, [browse the aggregate model using BrownSauce][5].

There&#8217;s an [extra mode][6] in the aggregate model system that adds an _inSubject_ reverse triple for each _dc:subject_ triple. Automatic inferencing of that sort might be handy for simplifying query code, and it&#8217;s something I&#8217;d like to play with, particularly if based on DAML rules.

Perhaps the aggregator could add other inferred metadata based on automatic analysis of the text, or other toys.

 [1]: /src/metadata.tmpl
 [2]: /archives/000004.rdf
 [3]: /src/com/picdiary/rdf/servlet/Posts.java
 [4]: https://www.picdiary.com:8180/rss/servlet/com.picdiary.rdf.servlet.Posts
 [5]: https://bender.ilrt.bris.ac.uk:1234/brownsauce/browse?source=http%3A%2F%2Fwww.picdiary.com%3A8180%2Frss%2Fservlet%2Fcom.picdiary.rdf.servlet.Posts%3Fcachedfoo&resource=http%3A%2F%2Fwww.hackdiary.com%2Farchives%2F000004.html
 [6]: https://www.picdiary.com:8180/rss/servlet/com.picdiary.rdf.servlet.Posts?augment=1