---
title: Crawling the Semantic Web
author: Matt Biddulph
type: post
date: 2004-02-12T19:52:47+00:00
excerpt: \n
url: /2004/02/12/crawling-the-semantic-web/
categories:
  - rdf
  - talks
  - web

---
I&#8217;ve had a proposal for a paper accepted for [XML Europe 2004][1]. Yay! Looking forward to meeting lots of old friends and making new ones in Amsterdam in April. Let me know if you&#8217;re going to be there. Here&#8217;s what I submitted:

<!--more-->

  
This presentation examines the problem of semantic web crawling &#8211; following links from document to document and gathering the results for searching. Unlike centralised web search facilities, semantic web agents will be distributed, personalised and often highly domain-specific. How can we hold the entire world inside our laptops?

The W3C vision for the Semantic Web is &#8220;an extension of the current web in which information is given well-defined meaning, better enabling computers and people to work in cooperation&#8221;. It is &#8220;the representation of data on the World Wide Web&#8221;, expressed using the Resource Description Framework (RDF). Just as the web grew in usefulness as it was traversed, indexed and searched by systems such as Lycos, Altavista and Google, the semantic web requires technologies that can crawl, aggregate and query the RDF data.

This talk presents a modular semantic web crawler designed to explore the provision of services to applications. It highlights differences from and similarities to existing web search systems that gather their source data from the public web.

Rather than have web crawling and aggregation built into every semantic web application, agents will be able to call on aggregation services via webservices, be notified of new resources by publish-and-subscribe mechanisms, or simply receive a stream of RDF statements as they are found. A number of different RDF storage mechanisms are tested, including traditional relational databases and RDF toolkits such as Redland.

Applications will be discussed in the areas of social networks (using the Friend Of A Friend vocabulary) and personal publishing. Models for providing centralised services to lighter-weight agents (such as mobile applications) are explored, and important issues such as trust and attribution of information are covered.

 [1]: https://www.xmleurope.com/2004/