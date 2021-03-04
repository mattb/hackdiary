---
title: Screenscraping HTML with TagSoup and XPath
author: Matt Biddulph
type: post
date: 2003-04-13T14:40:18+00:00
excerpt: \n
url: /2003/04/13/screenscraping-html-with-tagsoup-and-xpath/
categories:
  - java
  - xml

---
Often I find I need to pull out a bit of information from a webpage to reuse inside some code. I&#8217;ve always done this from the commandline using a combination of [wget][1], [HTML TIDY][2] and [xsltproc][3]. Recently I&#8217;ve been doing the same thing in program code using some very handy tools written in Java.

_Note: the example code below has been [updated][4]._

<!--more-->

  
The commandline version looks like this:

`wget -O - https://example.com | tidy -asxml - | xsltproc somexsl.xsl -`

where somexsl.xsl looks something like this:

`<?xml version='1.0'?><br />
<xsl:stylesheet xmlns:xsl="https://www.w3.org/1999/XSL/Transform" version='1.0'><br />
<xsl:output method="text" /><br />
<xsl:template match="/"><br />
<xsl:value-of select="/html/head/title" /><br />
</xsl:template><br />
</xsl:stylesheet>`

It&#8217;s also possible to do the same thing entirely in Java. John Cowan wrote a wonderful HTML parser called [TagSoup][5] that outputs SAX events using a do-the-best-I-can approach (&#8220;Just Keep On Truckin'&#8221; as he describes it) that attempts to make the best job of even the nastiest badly-written HTML. It produces output in cases when HTML TIDY gives up and tells you that errors in the input must be corrected before it can continue.

Because the SAX events just look like XML to any downstream code, it can be plugged into an XPath processor such as [Jaxen][6]. XPath processors need DOM trees to work with (because of the backwards-and-forwards-looking nature of the language which makes streaming processing difficult). [JDOM][7] contains a nice class called SAXBuilder that can do this SAX-to-DOM conversion, and handily Jaxen can work with JDOM trees directly. So, the Java equivalent of the commandline above is:

`URL url = new URL("https://example.com");<br />
SAXBuilder builder = new SAXBuilder("org.ccil.cowan.tagsoup.Parser"); // build a JDOM tree from a SAX stream provided by tagsoup<br />
Document doc = builder.build(url);<br />
JDOMXPath titlePath = new JDOMXPath("/h:html/h:head/h:title");<br />
titlePath.addNamespace("h","https://www.w3.org/1999/xhtml");<br />
String title = ((Element)titlePath.selectSingleNode(doc)).getText();<br />
System.out.println("Title is "+title);`

 [1]: https://www.gnu.org/software/wget/wget.html
 [2]: https://www.w3.org/People/Raggett/tidy/
 [3]: https://xmlsoft.org/XSLT/xsltproc2.html
 [4]: /archives/000041.html
 [5]: https://mercury.ccil.org/~cowan/XML/tagsoup/
 [6]: https://jaxen.sf.net/
 [7]: https://www.jdom.org