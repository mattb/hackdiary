---
title: Stemming tags, and one website to the tune of another
author: Matt Biddulph
type: post
date: 2005-01-30T23:42:14+00:00
excerpt: \n
url: /2005/01/30/stemming-tags-and-one-website-to-the-tune-of-another/
categories:
  - web

---
del.icio.us is still giving me food for thought. Here are two toys I&#8217;ve made recently: a [tag stemming tool][1] that helps you tidy up your tagging using the Porter algorithm, and a (Flash) screen-recorded demo of [del.icio.us seamlessly embedded in the BBC Radio 3 website][2].

(Maximize your browser window! Apologies for the slow playback speed of the movie; although you&#8217;re welcome to [browse the javascript][3], it&#8217;s something of a pain to get it running on your own browser. I&#8217;m looking at how I can turn it into a reusable and configurable Firefox extension, but for now it&#8217;s just a demo built with [Greasemonkey][4].)

_UPDATE: I had to demo this to a mixed audience at the BBC this afternoon, so I put together [some quick slides][5] to help me explain the step-by-step process that goes on behind the scenes. Perhaps someone else will find them useful too._

<!--more-->

  
So, what are you seeing in this movie? It&#8217;s nothing more than a bit of DHTML trickery that imports a subset of del.icio.us functionality into an existing website. I chose BBC Radio 3 because it has a wealth of content with plenty of potential for horizontal navigation, and because it has a clearly-defined [canonical URL per programme][6] and thereby gains the maximum benefit from being tagged. By creating a symbiotic relationship between the two sites in your browser, you gain an overlaid cross-site navigation that doesn&#8217;t exist in the site as it currently stands, and del.icio.us users see [your tagging of Radio 3 pages][7] in the [wider context][8].

There are several things that I enjoy in this demo. In no particular order:

  * I like the immediate feedback that you can get from adding a tag to a programme. Decide that &#8216;cello&#8217; is relevant, and within seconds you see a bunch of other cello programmes. It&#8217;s common for content management systems to demand &#8216;metadata&#8217; or &#8216;keywords&#8217; of you when you file content, but rare that there&#8217;s an easy way to get a feel for what value you&#8217;ve added by doing so.
  * This was my first real attempt to wrangle the XMLHTTPRequest system, and it was a satisfying one. I did learn one or two things, including some problems with [asynchronous and synchronous modes of operation][9].
  * Looking beyond the specific application (tagging) used here, notice the two-way benefit that came from the mashup of one site&#8217;s service with another&#8217;s content. I like the idea that domain-specific use on Radio 3 leads to general usefulness on del.icio.us.

There are many more possibilities to explore. The demo uses a single user on del.icio.us for all tagging. Imagine instead being able to select between different tag sets to overlay &#8211; one to guide newcomers to classical music, another designed for experts and old hands, a third to explore the history of a particular instrument or musical movement.

 [1]: https://www.hackdiary.com/stemtags/
 [2]: https://www.hackdiary.com/misc/firefox-delicious-demo.html
 [3]: https://www.hackdiary.com/src/pips.user.js
 [4]: https://greasemonkey.mozdev.org/
 [5]: https://www.hackdiary.com/slides/pips-deli/
 [6]: https://www.plasticbag.org/archives/2004/06/developing_a_url_structure_for_broadcast_radio_sites.shtml
 [7]: https://del.icio.us/sekrit/
 [8]: https://del.icio.us/tag/bach
 [9]: https://jpspan.sourceforge.net/wiki/doku.php?id=tutorials:asynchronouscalls