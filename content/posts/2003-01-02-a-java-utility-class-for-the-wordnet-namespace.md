---
title: A Java utility class for the Wordnet namespace
author: Matt Biddulph
type: post
date: 2003-01-02T23:32:14+00:00
excerpt: \n
url: /2003/01/02/a-java-utility-class-for-the-wordnet-namespace/
categories:
  - java
  - rdf
  - wordnet

---
To support the work I&#8217;ve been doing with Wordnet and RDF, I wrote a [utility Java class][1] to handle URIs from the [Wordnet ontology for RDF][2] devised by [Dan Brickley][3].

<!--more-->

  
The class is implemented using the [Java Wordnet Library][4] package, which means it requires JDK 1.4.

The major methods are:

  * public Synset lookup(String uri)
Takes a URI string such as <https://xmlns.com/wordnet/1.6/Dog> and returns a JWNL Synset object representing the wordnet synset of that URI.

  * public String uri(Synset synset)
Takes a JWNL Synset object and returns its canonical URI string from the wordnet namespace. </ul> 

The constructor takes a filename of a JWNL config file from which to configure the JWNL system.

 [1]: /src/WordnetNamespace.java
 [2]: https://xmlns.com/wordnet/1.6/
 [3]: https://www.w3.org/People/DanBri/
 [4]: https://sourceforge.net/projects/jwordnet