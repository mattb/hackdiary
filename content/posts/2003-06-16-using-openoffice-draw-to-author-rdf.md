---
title: Using OpenOffice Draw to author RDF
author: Matt Biddulph
type: post
date: 2003-06-16T21:38:30+00:00
excerpt: \n
url: /2003/06/16/using-openoffice-draw-to-author-rdf/
categories:
  - python
  - rdf
  - xml

---
OpenOffice&#8217;s vector-drawing app has a very nice Visio-like &#8216;connector&#8217; tool that can link objects together with lines. It&#8217;s very easy to put together labelled directed graph diagrams and have the lines re-flow as you move the nodes around. It also has a [well-documented XML file format][1], which got me thinking that graph drawings could be converted into RDF automatically. I wrote some [python code][2] to read in OO files and print out n-triples.

<!--more-->

  
A sample RDF graph drawn in OpenOffice looks like this:

![][3]  
([original file][4])

The output of the script run over this file is:

<pre class="codeblock">_:a11055796046 &lt;https://example.com#pred2&gt; &lt;https://example.com#1&gt; .
_:a11055796046 &lt;https://example.com#pred1&gt; "text" .
&lt;https://example.com#1&gt; &lt;https://example.com#foo&gt; &lt;https://example.com#bar&gt; .</pre>

Rectangles or ellipses with no text on them are taken to be bNodes. Those with text have URIs if they look like URIs (start with https:// or similar) and those with _&#8220;quoted text&#8221;_ are literals (the quotes are discarded). Predicate URIs are taken from the text on the connectors.

The code uses the xpath processor from [PyXML][5] and is written for python 2.2. It&#8217;s worth setting up the &#8216;Default&#8217; style in OpenOffice Draw so that it puts arrows on the end of each connector, otherwise it&#8217;s easy to get confused about which way round the connectors are.

 [1]: https://xml.openoffice.org
 [2]: /src/oo2ntriples.py
 [3]: /misc/oomodel.png
 [4]: /misc/oomodel.sxd
 [5]: https://pyxml.sourceforge.net/