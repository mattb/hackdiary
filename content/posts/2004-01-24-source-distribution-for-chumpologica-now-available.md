---
title: Source distribution for Chumpologica now available
author: Matt Biddulph
type: post
date: 2004-01-24T19:05:17+00:00
excerpt: \n
url: /2004/01/24/source-distribution-for-chumpologica-now-available/
categories:
  - foaf
  - python
  - rdf
  - rss

---
Now available: the first source distribution of [Chumpologica][1], the system behind [Planet RDF][2] and the [Daily Chump Chumpologica][3].

<!--more-->

  
Although source for an earlier version was [previously available][4], this new version 1.0 includes all the improvements made by myself and [Dave Beckett][5] for Planet RDF. I&#8217;ve also refactored the code to use an external configuration file, and packaged it up using python distutils with a simple control script. This means that a single global installation of the system can be used to run multiple clogica sites on a single machine. It&#8217;ll also make it easy to build distribution packages for Redhat and Debian.

 [1]: https://www.hackdiary.com/projects/chumpologica/
 [2]: https://www.planetrdf.com
 [3]: https://pants.heddley.com/logica/
 [4]: https://www.hackdiary.com/archives/000036.html
 [5]: https://journal.dajobe.org