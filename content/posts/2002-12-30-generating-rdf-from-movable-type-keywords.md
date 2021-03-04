---
title: Generating RDF from Movable Type keywords
author: Matt Biddulph
type: post
date: 2002-12-30T03:11:21+00:00
excerpt: \n
url: /2002/12/30/generating-rdf-from-movable-type-keywords/
categories:
  - perl
  - rdf
tags:
  - |
    "some unique id" .
    .

---
Having created RDF summaries for each Movable Type entry, I wanted a way to add extra triples to that RDF. For a first go, it seems reasonable to make any triple that can be added to an entry have that entry as its subject, so I used a shorthand (no subject, namespace-abbreviated) syntax inspired by [N-Triples][1] and wrote an MT global filter plugin ([src][2]) to transform it into RDF/XML.

<!--more-->

  
As an example, in this entry, I put this in my keywords:

`<dc:identifier> "some unique id" .`  
`<rdfs:seeAlso> <https://www.movabletype.org> .`

and two extra triples get created in the [RDF for this entry][3].

It&#8217;s used in the MT RDF template by putting `<$MTEntryKeywords ntriples="1"$>`. Of course any namespace prefix used in the Keywords field must be declared in the RDF template beforehand. Apart from that it should be pretty resilient against breaking because it ignores any line that doesn&#8217;t match the syntax exactly.

 [1]: https://www.w3.org/TR/rdf-testcases/#ntriples
 [2]: /src/ntriples.txt
 [3]: /archives/000005.rdf