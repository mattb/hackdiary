---
title: 'Update: Screenscraping HTML with TagSoup and XPath'
author: Matt Biddulph
type: post
date: 2003-12-28T20:14:41+00:00
excerpt: \n
url: /2003/12/28/update-screenscraping-html-with-tagsoup-and-xpath/
categories:
  - java

---
_UPDATE: [Oliver Roup][1] has published updated code that uses the builtin XPath processor in JDK 1.5_

Some emails and comments on [Screenscraping HTML with TagSoup and XPath][2] alerted me to the fact that the example I gave on that page has gone out of sync with the current release of JDOM and no longer works. I&#8217;ve reworked the example using [Xalan 2.5][3].

<!--more-->

  
The problem seems to be that JDOM is asking the TagSoup parser for full namespace support, which it&#8217;s not able to give. This new example uses Xalan&#8217;s SAX2DOM class to make a DOM tree out of the TagSoup SAX stream, then uses the simple XPathAPI wrapper to make the XPath call.

<pre class="codeblock">import java.net.URL;
import org.apache.xalan.xsltc.trax.SAX2DOM;
import org.apache.xpath.XPathAPI;
import org.apache.xpath.objects.XObject;
import org.ccil.cowan.tagsoup.Parser;
import org.w3c.dom.Node;
import org.xml.sax.InputSource;
&nbsp;
public class example {
&nbsp;public final static void main(String[] args) throws Exception {
&nbsp;&nbsp;URL url = new URL("https://example.com");
&nbsp;&nbsp;Parser p = new Parser();
&nbsp;&nbsp;p.setFeature("https://xml.org/sax/features/namespace-prefixes",true);
&nbsp;&nbsp;// to define the html: prefix (off by default)
&nbsp;&nbsp;SAX2DOM sax2dom = new SAX2DOM();
&nbsp;&nbsp;p.setContentHandler(sax2dom);
&nbsp;&nbsp;p.parse(new InputSource(url.openStream()));
&nbsp;&nbsp;Node doc = sax2dom.getDOM();
&nbsp;&nbsp;String titlePath = "/html:html/html:head/html:title";
&nbsp;&nbsp;XObject title = XPathAPI.eval(doc,titlePath);
&nbsp;&nbsp;System.out.println("Title is '"+title+"'");
&nbsp;}
}</pre>

This code example can be compiled and run with just the TagSoup classes and the Xalan 2.5 main jar on the classpath.

 [1]: https://blog.oroup.com/2006/11/05/the-joys-of-screenscraping/
 [2]: /archives/000029.html
 [3]: https://xml.apache.org/xalan-j