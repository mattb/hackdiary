---
title: Moyles-proof code
author: Matt Biddulph
type: post
date: 2004-04-11T14:32:17+00:00
excerpt: \n
url: /2004/04/11/moyles-proof-code/
categories:
  - perl
  - python

---
While the rest of the UK was enjoying a Good Friday lie-in, I dragged myself into Yalding House (home of [BBC Radio 1][1]) at 7.30am. I was there to see our new text message system get its first live broadcast use on the Chris Moyles show in a preview of the [Ten Hour Takeover][2].

<!--more-->

  
_This is a long piece&#8230; [skip to the end][3] if you want to see how it went on the day._

#### The project

I work for the beeb at Radio and Music Interactive, in the software architecture team. We&#8217;re responsible for the behind-the-scenes plumbing, running the systems behind things like [LiveText][4], and providing toolkits for the guys on the apps team who build public services. When Radio 1 came up with the takeover day (ten hours of radio with music selected entirely by the listeners via text message and phone), they asked us to build them something to deal with the expected deluge of messages.

As you probably know, [text messaging is huge in the UK][5] and it&#8217;s been taken up enthusiastically by the BBC&#8217;s radio networks. Radio 1&#8217;s incoming SMS provider have a web console that&#8217;s used by the broadcast assistants and DJs in the studio. It works rather like an email inbox, and like most email clients the user interface treats the incoming messages as a chronological stream of text rather than a database to be mined for information. This works for running a regular radio show, but the takeover day needs special treatment.

Since the web console had been enough for the networks so far, this was our department&#8217;s first project based on machine-processing of SMS. Knowing how important text is to the radio networks, we wanted to build a foundation of components that would support future applications. As every software engineer knows, it&#8217;s hard to &#8220;[build one to throw away][6]&#8221; after the users have got their hands on it.

#### The build

In our team the language of choice is Python, whereas the apps team prefer Perl. Contrary to what some might expect, this mixed economy hasn&#8217;t yet given us any interop problems. We&#8217;re very keen on using abstractions such as [asynchronous messaging][7], [REST][8]ful web services and relational databases to act as language-agnostic intermediaries for our data flows.

My immediate thoughts about the architecture were that it should be built from a series of loosely-coupled layers. Even solving the simple problem of how to pull in a high-volume external XML feed of text messages and redistribute it to applications would show benefits later if it was simple to hook new code into. Further layers could process the data, with a web user interface layered on top of that. Working from a specification of the XML format used by the provider, Paul Clifford quickly built a gateway that collected messages and rebroadcast them over a message bus. Using asynchronous messaging as a transport gives us a good level of resilience and clusterability for free, while keeping the logic very simple. Building on this, he then started work on code to push messages sent to Radio 1 into a database and analyse their contents.

We wanted to provide simple, useful features to the users such as freetext search, but we thought we could do more given that the incoming texts would have a certain amount of implicit structure. The programme was going to ask people to text in &#8220;Artist &#8211; Track &#8211; Name &#8211; Dedication&#8221;, but we assumed that there would be a lot of variation in the accuracy of the texts and a lack of consistent punctuation to act as delimiters. We planned a system of &#8216;fuzzy matching&#8217; to group together texts using stopwords, sounds-alike phonetic matching and statistical analysis of text prefixes. If you see enough text strings beginning with words that sound like &#8220;Bob Dylan&#8221; then you can start to guess that Bob Dylan might be an artist, rather than a track called Dylan by a band named Bob. Paul did some great work on refining these techniques, and an on-air test a few weeks before the real broadcast showed that we could pretty accurately infer that &#8220;Weezer&#8221;, &#8220;Wheezer&#8221;, &#8220;Weazer&#8221; and &#8220;Wheeser&#8221; were all the creators of tracks called &#8220;Buddy Holly&#8221;, &#8220;Budy Holly&#8221; and &#8220;Buddy Holy&#8221;.

While Paul worked on the analysis, I created a Perl wrapper around the database so that the apps team could get to work on the user interface. At the same time, I passed on a few lines of sample client code to [Matt Webb][9] to see what he could do with it. When working on a toolkit or API, I always like to have more than one client using it, to make sure that the requirements of the main project haven&#8217;t kept the interface from being generic and useful in other contexts. He built a nice rolling graph of texts received per minute, tapping in at the message bus layer. As with any messaging system, adding a new message recipient affected neither the code providing the messages nor any other clients of the bus. Neil Slater and Conal Jones in the apps team did great work building a web interface with guidance from the Radio 1 team, and within a few weeks we were ready to go live.

#### On air {#on-air}

Chris Moyles likes to break things. He once managed to get listeners to send [14,000 texts at once][10]. When I arrived, [Aled the BA][11] asked me how many messages the new system could take, and told me that Chris was going to do his best to overload it. At 8.45am, Chris started trailing the feature, and the text messages started trickling in. Then flooding. I was impressed: on a UK Bank Holiday, thousands of people were not just listening but involved enough to get on their phones and interact with the programme.

Chris and his team did a great job of understanding our system. They caught onto the freetext search right away and used it to find interesting tracks, and messages to read out from people who requested them. We put a &#8216;quick stats&#8217; box on every screen of the app, which they used to goad on the listeners: &#8220;3000 text messages so far. That is simply not enough. I want that quadrupled!&#8221;. Once there were enough messages in the system for the pattern matching to kick in, they used it to navigate through the data and see which tracks by which artists were getting the most attention. As the listeners realised that the playlist had gone out the window and they could request anything, we got some great stuff coming in. Our system even got a little mention on air as Chris teased us for matching an Elvis Costello track to a bunch of requests for Elvis.

As the programme started I was sitting nervously next-door to the studio tailing logfiles and watching process tables, but as it went on and the code coped with everything they could throw at it, I relaxed and enjoyed the show. I don&#8217;t normally listen to the Radio 1 Breakfast Show but listening to this gave me new respect for the skills of a daytime DJ, sitting in a tiny room in a basement working a crowd of millions that they never see.

If you want to hear the show, there&#8217;s a [Listen Again][12] stream available from the BBC until April 16th. The request section is in the last hour. Tune into Radio 1 on Monday April 12th from 10am for the ten hour version.

 [1]: https://www.bbc.co.uk/radio1/
 [2]: https://www.bbc.co.uk/radio1/djs/tenhour/index.shtml
 [3]: #on-air
 [4]: https://www.bods.me.uk/rantnrave/2003/09/26/dab_text_on_bbci_radio_stations.live
 [5]: https://news.bbc.co.uk/1/hi/technology/3368815.stm
 [6]: https://www.amazon.co.uk/exec/obidos/ASIN/0201835959/
 [7]: https://www.spread.org
 [8]: https://internet.conveyor.com/RESTwiki/moin.cgi/FrontPage
 [9]: https://interconnected.org/home
 [10]: https://www.chrismoyles.net/mw/coranto/Radio_Reviews/Radio_Reviews-archive-8-2003.shtml#newsitemEpykpAuullxrucLuEy
 [11]: https://www.bbc.co.uk/radio1/chrismoyles/biography/#aled
 [12]: https://www.bbc.co.uk/radio/aod/rpms/r1moylesfri.rpm