---
title: Simple dumb RDF parser script for perl
author: Matt Biddulph
type: post
date: 2002-09-29T17:45:00+00:00
excerpt: \n
url: /2002/09/29/simple-dumb-rdf-parser-script-for-perl/
categories:
  - perl
  - rdf
  - sql

---
As with the [ruby rdf parser][1], this runs XSLT over your RDF/XML to make ntriples then parses those. It spits out mysql insert statements ready for querying with my [rdf sql query stuff][2].

[rdfparse-perl.tar.gz][3]

<!--more-->

  
The XSLT is taken from the [rubyrdf distribution][4]. The perl code uses XML::LibXML and XML::LibXSLT.

 [1]: https://www.w3.org/2001/12/rubyrdf/intro.html
 [2]: https://www.picdiary.com/triplequerying/
 [3]: https://www.picdiary.com/~mattb/rdf/rdfparse-perl.tar.gz
 [4]: https://www.w3.org/2001/12/rubyrdf/xsltrdf/