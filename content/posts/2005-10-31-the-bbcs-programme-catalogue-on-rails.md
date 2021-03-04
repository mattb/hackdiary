---
title: The BBC’s programme catalogue (on Rails)
author: Matt Biddulph
type: post
date: 2005-10-31T19:00:00+00:00
excerpt: \n
url: /2005/10/31/the-bbcs-programme-catalogue-on-rails/
categories:
  - rails

---
**UPDATE: The BBC Programme Catalogue has launched at <https://open.bbc.co.uk/catalogue/infax>**

_&#8220;The BBC plans to open up its archive to make a treasure trove of material available to everyone.&#8221;_ &#8211; [BBC Press Release, August 2003][1]

Ever wondered what&#8217;s in that archive? Who looks after it? It turns out there&#8217;s a huge database that&#8217;s been carefully tended by a gang of crack BBC librarians for decades. Nearly a million programmes are catalogued, with descriptions, contributor details and annotations drawn from a wonderfully detailed controlled vocabulary.

I&#8217;m the lucky developer who gets to turn this hidden treasure into a public website. No programme downloads yet, but a massive searchable programme catalogue.

<!--more-->

  
In the early part of next year, you can look forward to a public beta with extensive programme details and broadcast histories. There are &#8220;On This Day&#8221; schedules that go back to 1933. It&#8217;s got full contributor histories, and Really Good Search. I can&#8217;t begin to describe the depth of this dataset &#8211; it had an entry for the one time in the 1990s when my dad was on local TV news as a spokesman for Oxfordshire County Council. The cataloguers have worked hard on this stuff for years, and it deserves a wide audience.

Here are some early screenshots: [searching for John Peel][2]; [John Peel&#8217;s contributor page][3]. The design&#8217;s not finished yet, but they give you a flavour of the data.

Oh yes, there&#8217;s also plenty of web 2.0 goodness: Ajax, feeds for everything, tags, full read-only REST API including FOAF for all contributors, and it&#8217;s all run with Ruby on Rails. Yes, the BBC have allowed me (after some persuasion) to rapidly prototype and deploy this 7,000,000-row database-backed site in everyone&#8217;s new favourite web framework. This first version is really just a prototype; wisely, the BBC have decided to get it out there quick and see the public reaction.

We&#8217;ve got [Ben Hammersley][4] on board working on layout, CSS and feed design. [Murray Walker][5] is our BBC developer on the inside. This is the most fun I&#8217;ve had on a project for a long time. If you want to hear more about it, come and see me talk on Rails at the [London Web Frameworks Night][6] in November. If you&#8217;ve got ideas on how you&#8217;d want to track down an obscure sci-fi drama from the 80s or a radio play from 1962, [drop me a mail][7].

 [1]: https://www.bbc.co.uk/pressoffice/pressreleases/stories/2003/08_august/24/dyke_dunn_lecture.shtml
 [2]: https://www.hackdiary.com/images/peel-search.png
 [3]: https://www.hackdiary.com/images/peel-contrib.png
 [4]: https://www.benhammersley.com/weblog/2005/10/31/hot_bbc_archive_action.html
 [5]: https://www.minty.org/
 [6]: https://blog.unixdaemon.net/cgi-bin/blosxom.pl/events/frameworks_night_short.html
 [7]: mailto:matt@hackdiary.com