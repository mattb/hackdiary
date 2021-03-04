---
title: The Chumpologica – an RSS feed combiner
author: Matt Biddulph
type: post
date: 2003-06-30T21:15:13+00:00
excerpt: \n
url: /2003/06/30/the-chumpologica-an-rss-feed-combiner/
categories:
  - foaf
  - python
  - rss

---
Today we relaunched [The Daily Chump][1], a multi-author IRC-based blog, with a shiny new look and a new feature: the [chumpologica][2]. This is a webpage (and [RSS 1.0 feed][3]) that aggregates entries from blogs written by regular contributors to the Chump. It&#8217;s built using about 150 lines of python and takes its configuration from a [FOAF file][4].

_Update:_ I&#8217;ve now packaged and released this project as a [proper distribution][5].

<!--more-->

  
[FOAF][6] has a predicate in its vocabulary for indicating that a person has a weblog. [bloginfo.py][7] uses the [Redland RDF framework][8] to read the FOAF file and find the details of each weblog. It uses the very latest version of Redland&#8217;s python support (which contains support for iterators, allowing nice syntax such as: `for statement in model: print statement.subject`) which is only available in the [nightly source snapshots][9] at the time of writing.

[chumpologica.py][10] is the program start point. It uses [Mark Pilgrim&#8217;s RSS parser][11] to read in the RSS feeds, and puts the entries into a listed sorted by date. The date is taken from the entry&#8217;s Dublin Core date property, unless that&#8217;s missing in which case the time of retrieval is used. A hash is kept of entries seen on previous runs so that we don&#8217;t get duplicate entries. After a run, the entries and hashes are pickled (serialised) into a file for reuse on the next run.

If new entries were found, [Mark Nottingham&#8217;s RSS.py][12] is invoked to output a new RSS 1.0 file using the newest 30 items. Weblog information taken from the FOAF file is stored along with each entry using standard Dublin Core tags such as _relation_ to point to the original blog and _creator_ to give the name of the writer. The resulting RSS file is sufficient to be transformed using XSLT into the final webpage.

 [1]: https://pants.heddley.com
 [2]: https://pants.heddley.com/logica/
 [3]: https://pants.heddley.com/chumpologica.rdf
 [4]: https://pants.heddley.com/logica/blogsources.rdf
 [5]: https://www.hackdiary.com/projects/chumpologica/
 [6]: https://xmlns.com/foaf/0.1/
 [7]: /src/bloginfo.py
 [8]: https://www.redland.opensource.ac.uk
 [9]: https://www.redland.opensource.ac.uk/dist/snapshots/source/
 [10]: /src/chumpologica.py
 [11]: https://www.diveintomark.org/projects/rss_parser/
 [12]: https://www.mnot.net/python/RSS.py