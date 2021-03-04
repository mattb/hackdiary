---
title: del.icio.us experiments redux
author: Matt Biddulph
type: post
date: 2004-10-06T22:26:08+00:00
excerpt: \n
url: /2004/10/06/delicious-experiments-redux/
categories:
  - web

---
About a month ago, I posted about some [del.icio.us experiments][1] I&#8217;d been doing, and published the python wrapper I&#8217;d been using. Of course, the post itself was another del.icio.us experiment.

<!--more-->

  
Guessing that the post would be perfect linkfodder, I was curious to see how the del.icio.us community would take the bait. It went down pretty well. To date, it&#8217;s been posted by 153 people.

I knocked up a bit of code to list the tags that the item got, something like this:

<pre class="codeblock">tags = {}
for post in d.Href("https://www.hackdiary.com/archives/000060.html"):
for tag in post.tags:
tags[tag.name] = tags.get(tag.name,0) + 1
</pre>

And what was the emergent categorisation of my piece? It was a pretty broad list, demonstrating several different styles of tagging strategy:

  * _97 times_ python
  * _64 times_ del.icio.us
  * _37 times_ delicious
  * _22 times_ programming
  * _10 times_ hacks
  * _7 times_ tools
  * _6 times_ web
  * _4 times_ software
  * _4 times_ dev
  * _3 times_ rdf
  * _3 times_ bookmarks
  * _2 times_ unread
  * _2 times_ social
  * _2 times_ semweb
  * _2 times_ library
  * _2 times_ hacking
  * _2 times_ hack
  * _2 times_ development
  * _2 times_ del
  * _2 times_ api
  * \***
  * *checkout
  * *touch
  * blog
  * blogentry
  * blognew
  * bookmark
  * booty
  * checkout
  * clipz
  * code
  * collaboration
  * collaborativefiltering
  * computer
  * cool
  * del.icio.us social
  * delic
  * delicios
  * devel
  * extensions
  * geek_stuff
  * generalreference
  * greatminds
  * icio.us
  * images
  * metabookmark
  * metadelicious
  * namespaces
  * newnet
  * news/articles
  * read
  * readlater
  * rss
  * ruby
  * semanticweb
  * socialsoftware
  * todo
  * viapopular
  * webdev
  * webservices/delicious
  * webtech
  * xml
  * yummy
  * z:active
  * z:del.icio.us_experiments

I was also curious about what the pattern of linking would be over time. Mostly I expected the standard power law curve, reflecting an initial flurry of attention followed by a swift drop-off. I put together a quick chart in openoffice:

<center>
  <img src="https://www.hackdiary.com/misc/delposts.jpg" />
</center>

My hypothesis appears to be largely borne out by the results, but there are some ripples in the tail of the curve where the post regains momentary popularity then tails off again. I&#8217;m guessing this happens when the link is discovered by a new del.icio.us sub-community (python programmers, etc) who read each other&#8217;s del.icio.us streams via rss or inbox.

A few more numbers: of 153 posts, only 19 used a title other than the page title I used in the post. Only 44 posts gave an extended description. Most users (64) assigned just two tags, with the rest distributed like this:

<center>
  <img src="https://www.hackdiary.com/misc/deltags.jpg" />
</center>

 [1]: https://www.hackdiary.com/archives/000060.html