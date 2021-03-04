---
title: del.icio.us experiments
author: Matt Biddulph
type: post
date: 2004-09-09T22:45:22+00:00
excerpt: \n
url: /2004/09/09/delicious-experiments/
categories:
  - web

---
Maybe you&#8217;re a python programmer. Maybe you think [del.icio.us][1] is kinda cool. Maybe you&#8217;d like to be able to do this:

<pre class="codeblock">&gt;&gt;&gt; print len(delicious.Href("https://www.vim.org/").posts())
8</pre>

or:

<pre class="codeblock">&gt;&gt;&gt; for post in delicious.users.mattb(delicious.tags.hackney):
...   print post.description,post.href
&nbsp;
Phil Gyford selling his flat https://www.gyford.com/strandbuilding/
POGO https://www.pogocafe.co.uk/
hackneycentral https://www.hackneycentral.org/
Armadillo https://www.armadillorestaurant.co.uk/
</pre>

or perhaps do something much, much cooler. [delicious.py][2] is for you.

_UPDATE:_ Since I published this code, Joshua Schachter has made the [rules around use of del.icio.us APIs][3] clearer. So that you can stay within these limits, you should be aware that no call to a method in delicious.py will cause more than one HTTP request to del.icio.us. This means that it&#8217;s left up to you to time your requests appropriately and politely, but at least you know that the code won&#8217;t spam del.icio.us of its own accord.

<!--more-->

  
As with [audioscrobbler a few months back][4], [del.icio.us][1] has been around for a while but last week really started to show up on [the radar][5]. I&#8217;ve been poking it with bits of code in the hope of achieving enlightenment.

I started by posting a few things: doing some [linklogging][6], scripting an extraction of my items from [The Daily Chump][7] into [a tag of their own][8], and extracting and posting pictures from [my photo site][9] under [a username of their own][10] with simple tags derived from the foaf and wordnet RDF annotations in that site&#8217;s [RSS][11]. I [pointed][12] to the picdiary experiment on the Semantic Web Interest Group IRC channel, and got some [interesting discussion][13] out of it.

The python wrapper that I used for most of this is fairly simple in structure. It uses a combination of [Redland][14]&#8216;s RDF parsing (for the pleasantly fulsome [RSS][15] bits) and [libxml2][16]&#8216;s HTML parser for the bits I needed to screenscrape. Href, User and Tag objects are used throughout, and can be used in combination. You can ask a User for all the posts from the user, or restrict it by passing one or more Tags into its post() method, and the converse for the Tags. It&#8217;s got some nice python automagic, creating Tag and User objects when you use syntax like &#8220;`delicious.tags.foo`&#8221; or &#8220;`delicious.users.bar`&#8221; and providing `__iter__` methods that allow the &#8220;`for post in delicious.tags.foo`&#8221; usage.

There&#8217;s a bit of an example in the module&#8217;s `__main__` code, which will take a username and find all the users that also posted two or more URLs posted by that user, and tell you what tags others used for the URLs posted by that user.

This code has evolved out of my own needs, rather than having a goal in particular. If you find it useful, I&#8217;d love to [hear from you][17].

 [1]: https://del.icio.us
 [2]: https://www.hackdiary.com/src/delicious.py
 [3]: https://lists.burri.to/pipermail/delicious-dev/2004-September/000058.html
 [4]: https://www.hackdiary.com/archives/000052.html
 [5]: https://bloglines.com/public/mbiddulph
 [6]: https://del.icio.us/mattb
 [7]: https://pants.heddley.com
 [8]: https://del.icio.us/mattb/dailychump
 [9]: https://www.picdiary.com
 [10]: https://del.icio.us/picdiary
 [11]: https://www.picdiary.com/rss/www2004.rss
 [12]: https://rdfig.xmlhack.com/2004/09/08/2004-09-08.html#1094679301.837777
 [13]: https://www.ilrt.bris.ac.uk/discovery/chatlogs/rdfig/2004-09-08.html#T21-35-01
 [14]: https://www.redland.opensource.ac.uk
 [15]: https://del.icio.us/rss/mattb
 [16]: https://www.xmlsoft.org
 [17]: mailto:mb@hackdiary.com