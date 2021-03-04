---
title: Using Wikipedia and the Yahoo API to give structure to flat lists
author: Matt Biddulph
type: post
date: 2005-09-02T22:49:10+00:00
excerpt: \n
url: /2005/09/02/using-wikipedia-and-the-yahoo-api-to-give-structure-to-flat-lists/
categories:
  - metadata

---
Some of my recent (and [final][1]) work at the BBC has involved breathing life into old rolodex-style flat databases of content. With my colleague [Tom Coates][2], I&#8217;ve been puzzling over how to take a list of text strings like this:

`"AGNEW, Spiro", "ATTLEE, Clement", "BARBER, Anthony", "BEVAN, Aneurin", "BLAIR, Tony", "CALLAGHAN, James", "CHAMBERLAIN, Neville", "CHURCHILL, Winston", "COULTHARD, David", "DYALL, Valentine", "EDEN, Anthony", "FOOT, Michael", "GAITSKELL, Hugh", "HAGUE, William", "HEATH, Edward", "HESELTINE, Michael", "JENKINS, Roy", "KINNOCK, Neil", "MACLEOD, Iain", "MACMILLAN, Harold", "MARSHALL, David", "MILLIGAN, Spike", "NIXON, Richard", "REDWOOD, John", "THATCHER, Margaret", "WILSON, Harold"`

and turn it into a network of directed links [like this][3]. Hopefully anyone who has a passing knowledge of the history of the British government will agree that it&#8217;s a convincing little map, easily usable as a basis for navigation around the concepts attached to the text strings

We found a pretty neat automated solution, entirely based on public internet resources, that requires no input at our end apart from the text strings above.

<!--more-->

  
The first step is to turn our flat text strings into references to internet resources that we can use to gather judgements about them. For the politics domain (and for a vast variety of others), [Wikipedia][4] is an obvious choice. How do we turn &#8220;BLAIR, Tony&#8221; into <https://en.wikipedia.org/wiki/Tony_Blair>? The simplest approach, transforming the former string into the latter by regular expression, doesn&#8217;t work for all cases, even in this small data set. Note the URL for [Anthony Barber][5], for example. Thankfully, the solution is still simple: we use a search engine. Yahoo&#8217;s REST API is far preferable to Google&#8217;s SOAP, so we use it to formulate [a search for &#8220;margaret thatcher&#8221; restricted to wikipedia.org][6] and take the top result.

Straight away we&#8217;ve added value to our database. With a plausibily-canonical URL for Margaret Thatcher (certainly an [inverse functional property][7] in ontology terms), we can use a service like Bloglines Citation Search to gather [web zeitgeist around that particular politician][8].

Wikipedia gives us much more than just an identifier, however. There&#8217;s great human-readable information in that resource. Luckily, the Yahoo API has another service that can help machine-agents make sense of human prose. Its [Term Extraction service][9] will take a chunk of content and return a short list of &#8216;significant words or phrases&#8217; from it. Incidentally, you can play with some great visualisations based on this service at [tagcloud.com][10].

If we run the HTML from Thatcher&#8217;s wikipedia page through an html-to-text process (perhaps `lynx -dump`) and then hand the text to the Yahoo service, we get the following:

  * margaret thatcher
  * baroness thatcher
  * woman
  * political philosophy
  * james callaghan
  * figurehead
  * government spending
  * margaret hilda thatcher
  * conservative party
  * tony blair
  * wikipedia
  * wikimedia
  * free encyclopedia
  * thatcherism
  * order of the garter

What&#8217;s particularly interesting about this list? It contains some text strings we can relate directly back to members of our original list. So we judge that Margaret Thatcher links to James Callaghan and Tony Blair. Repeat this extraction and correlation process for each member of the list and you get [the map we are looking for][3]. While a political journalist might complain about its completeness, it&#8217;s an impressive result that comes at zero cost.

What are the implications of this method? Firstly, it shows yet again the value of using [existing well-designed URLs][11] as globally-unique and resolvable identifiers for concepts. Simply using a consensus URL as a proxy for a concept increases the chances of correlating your information with that of others on the web. As the method is applicable to any text strings, it could be used with a list of tags attached to a URL or photo on [flickr][12] or [del.icio.us][13]. While it certainly wouldn&#8217;t give results on the every single tag, any result at all is better than none.

Secondly, it&#8217;s a great method for adding value to your own data by using external information. It fits well with other emerging thinking on ad-hoc inferencing such as Tom&#8217;s [How To Build On Bubbleup Folksonomies][14]. Now that tagging and URL-linking are firmly established as viable and accessible tools for distributed correlation and consensus-forming, second-generation techniques such as these can start to take advantage of the resulting network effect. We can aggregate opinion and categorisation up the chain, and across the network, along any axis that makes sense for our problem domain. By using external resources, we can start somewhere in our data, hop up onto the web, take a few steps, and come back down in a different, yet relevant, part of our own database.

 [1]: https://www.hackdiary.com/archives/000068.html
 [2]: https://www.plasticbag.org
 [3]: https://www.hackdiary.com/misc/people.png
 [4]: https://www.wikipedia.org
 [5]: https://en.wikipedia.org/wiki/Lord_Barber
 [6]: https://api.search.yahoo.com/WebSearchService/V1/webSearch?appid=YahooDemo&query=%22margaret%20thatcher%22&site=wikipedia.org
 [7]: https://www.w3.org/TR/owl-ref/#InverseFunctionalProperty-def
 [8]: https://www.bloglines.com/citations?url=https://en.wikipedia.org/wiki/Margaret_Thatcher
 [9]: https://developer.yahoo.net/search/content/V1/termExtraction.html
 [10]: https://www.tagcloud.com/
 [11]: https://www.hackdiary.com/slides/xtech2005/
 [12]: https://www.flickr.com/
 [13]: https://del.icio.us/
 [14]: https://www.plasticbag.org/archives/2005/09/how_to_build_on_bubbleup_folksonomies.shtml