---
title: A Semantic Web shoebox – annotating photos with RSS and RDF
author: Matt Biddulph
type: post
date: 2003-01-31T12:52:17+00:00
excerpt: \n
url: /2003/01/31/a-semantic-web-shoebox-annotating-photos-with-rss-and-rdf/
categories:
  - photos
  - rdf
  - wordnet
  - xml

---
I&#8217;ve had a proposal for a paper on RDF and annotating photos accepted for [XML Europe 2003][1]. Yay! Here&#8217;s what I submitted:

<!--more-->

  
[RSS 1.0][2] (RDF Site Summary) is a well-known XML format commonly used for syndicating news headlines. By design it is an extensible format in which metadata expressed using any RDF vocabulary can be linked to its component items, while still maintaining compatibility with applications such as newsreaders that may be unaware of such vocabularies. This paper will discuss some interesting applications that can be built with RSS as a base. The annotation of collections of photographs is used as a case study.

Using an [RDF representation of Wordnet][3], the lexical database of English, we attach keywords to photographs to indicate what they objects they depict. With simple inference logic, we create improved search engines over this data. For example, using the hypernym information in Wordnet to extrapolate from keywords, a search for buildings can find hotels, churches, houses and other related photographs. We can automatically build a Yahoo-like hierarchical web site of photographs organised by the meaning of their keywords.

Using the [Friend Of A Friend][4] (FOAF) vocabulary, we can record which photographs show particular people. Applications can then display related information with the photograph by using information gathered by spidering the existing network of FOAF information on the web.

Dynamically-built RSS channels are an ideal format for expressing search results; hence people who are interested could use newsreaders to subscribe to new pictures of any Wordnet noun, particular person or other metadeta criteria. This RSS is easily turned into web pages using templating tools. A Blogger-like front page can be built by building an RSS &#8216;meta-channel&#8217; summary of the 10 newest photo collections.

Processing toolkits for RDF are available in many languages, and RDF&#8217;s natural integration with the web&#8217;s URI system makes it easy to build applications in a loosely-coupled style. Tools for this project built using the [Redland][5] API in Perl and the [Jena][6] toolkit in Java easily interoperate, using the RDF output of one as the input of another. New applications can be built by others using any language or environment with RDF and HTTP support (even Mozilla), without needing to be granted any special database access or other privileges.

_Update: slides from this and other talks are [available][7]_.

 [1]: https://www.xmleurope.com/2003/
 [2]: https://www.purl.org/rss/1.0/
 [3]: https://xmlns.com/2001/08/wordnet/
 [4]: https://www.rdfweb.org/foaf/
 [5]: https://www.redland.opensource.ac.uk/
 [6]: https://www.hpl.hp.com/semweb/jena-top.html
 [7]: /cats.html#talks