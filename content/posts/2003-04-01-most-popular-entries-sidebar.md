---
title: “Most Popular Entries” sidebar
author: Matt Biddulph
type: post
date: 2003-04-01T18:23:07+00:00
excerpt: \n
url: /2003/04/01/most-popular-entries-sidebar/
categories:
  - perl
  - rss

---
Noticing the variety in popularity amongst the different topics that the pieces on this site cover, I added a &#8220;Most Popular Entries&#8221; sidebar to keep track of what people are reading. This is done with a simple application of [Apache::ParseLog][1], [XML::RSS][2], movabletype&#8217;s XML-RPC interface and a movabletype plugin.

<!--more-->

  
Every night after midnight, [hits.pl][3] runs and inspects the previous day&#8217;s Apache access log. Every entry has a predictable URL of the form `https://www.hackdiary.com/archive/000articleID.html`, so the code looks for hits on those URLs and parses out the article ID. It updates a dbm file, adding the day&#8217;s hits to hits already recorded for each item.

After that&#8217;s finished, [hits2rss.pl][4] is run and translates the dbm file into an [RSS file][5] by looking up the article titles via the MT XML-RPC interface. An MT [plugin][6] parses that file when the index page is rebuilt and makes the sidebar.

Fun hacks like this make me wish that MT had a [license][7] that allowed distribution of modifications to its core. Although the plugin interface is flexible, it&#8217;s a dead-end in the long run without the ability to dig in and change things under the skin.

 [1]: https://search.cpan.org/author/AKIRA/Apache-ParseLog-1.02/
 [2]: https://search.cpan.org/author/KELLAN/XML-RSS-1.02/
 [3]: /src/hits.txt
 [4]: /src/hits2rss.txt
 [5]: https://www.picdiary.com/~mattb/misc/hackdiary_hits.rss
 [6]: /src/tophits.txt
 [7]: https://www.movabletype.org/license.shtml