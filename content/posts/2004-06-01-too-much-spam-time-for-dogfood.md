---
title: Too much spam, time for dogfood
author: Matt Biddulph
type: post
date: 2004-06-01T00:28:21+00:00
excerpt: \n
url: /2004/06/01/too-much-spam-time-for-dogfood/
categories:
  - rdf

---
Over the weekend I was hit by over 200 MT comment spams, from a range of IP addresses. Using MT-blacklist I was able to clean up the damage, but wasted at least half an hour. In temporary despair, I&#8217;ve removed the comment forms from individual entries and disabled the comments cgi. For now, if you want to write something about one of my entries, go get your own website or something.

<!--more-->

  
I&#8217;ve been feeling like I want to move away from movabletype for some time now. My [other personal site][1] has been running on an RDF-based homebrew system for a couple of years now, and it looks like it&#8217;s time to make hackdiary an RDF dogfood site too.

I&#8217;ve restarted a coding project that tailed off last year when I lost a laptop: to create my own graph-oriented content wrangler. [Redland][2], my toolkit of choice, has moved on quite a bit over the last year, and has now gained a parser for [&#8220;scribbleable&#8221; non-XML syntax][3] and an [RDQL query engine][4] (for which I&#8217;ve just contributed python wrappers). These are expressive tools.

My intention is to keep it simple and avoid building Yet Another Generic CMS. So far I&#8217;ve got a simple templating engine that reads a [config file][5] and gathers RDF from internal and external sources for rendering in [Cheetah][6] templates. I plan to add proper [two-way web][7] features to it, and hopefully demonstrate (to myself at least) the value of treating the information relevant to my site as one big directed labelled graph.

 [1]: https://www.picdiary.com
 [2]: https://www.redland.opensource.ac.uk
 [3]: https://www.ilrt.bris.ac.uk/discovery/2004/01/turtle/
 [4]: https://www.redland.opensource.ac.uk/rasqal/
 [5]: https://www.hackdiary.com/misc/config.ttl
 [6]: https://cheetahtemplate.org
 [7]: https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm