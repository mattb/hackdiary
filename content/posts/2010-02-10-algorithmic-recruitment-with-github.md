---
title: Algorithmic recruitment with GitHub
author: Matt Biddulph
type: post
date: 2010-02-10T13:34:58+00:00
url: /2010/02/10/algorithmic-recruitment-with-github/
categories:
  - web

---
In my [new job in Berlin][1] I&#8217;ve been asked to hire some people to help prototype new, secret projects. Berlin has a superb tech scene but as I&#8217;m new in town it&#8217;s taking me a little time to get to know everyone. While that&#8217;s going on, I wrote some code to help me explore Berlin&#8217;s developer community.

When I&#8217;m hiring, one of the things I always want to see is evidence of personal projects. Over the last two years, [GitHub][2] has become an amazing treasure trove of code, with the best social infrastructure I&#8217;ve ever seen on a developer site. GitHub profiles let the user set their location, so I started with a few [web searches][3] for Berlin developers. This finds hundreds of interesting people, but how do I prioritise them?

Another thing that I look for when building a good team is someone&#8217;s personal network. I&#8217;ve always believed strongly in spending lots of time at conferences meeting passionate people who are smarter than me. A good developer can make themselves even more productive by knowing who to email, IM or DM to answer a question when they&#8217;re stuck.

[<img style="float:right; margin-left: 20px;" src="https://upload.wikimedia.org/wikipedia/commons/thumb/6/60/Graph_betweenness.svg/200px-Graph_betweenness.svg.png" width="200" height="200" />][4] A recent [article by Stowe Boyd on centrality and influence in social networks][5] reminded me of some of the network analysis we use behind the scenes calculating recommendations for the [Dopplr Social Atlas][6]. So I wrote some code to query the [GitHub API][7] and analyse the social graph of the Berlin subset of their users.

The JRuby code uses Yahoo BOSS to do the web search. After querying the GitHub API for [each user&#8217;s followers][8] it builds an in-memory graph using the  [Java Universal Network/Graph Framework][9]. Then it ranks each user node in the graph using the [Betweenness Centrality algorithm][10]. You can see the simple [source code on my github][11].

To sanity-check the results I ran it for a couple of cities I already know well: London and San Francisco. Here are the top 5 for each, which seem quite plausible to me:

### [San Francisco][12]

  1. [Chris Wanstrath, GitHub][13]
  2.  [Tatsuhiko Miyagawa, Six Apart][14]
  3. [Leah Culver, Six Apart][15]
  4. [Square Inc][16]
  5. [Aman Gupta, ruby eventmachine maintainer][17]

### [London][18]

  1. [James Darling][19]
  2. [London Ruby User Group][20]
  3. [Mark Norman Francis][21]
  4. [Dan Webb (recently moved to Twitter in SF)][22]
  5.  [Carlos Villela, Thoughtworks][23]

My choice of metric biases these lists towards connectedness and influence &#8212; it can&#8217;t measure ability. It&#8217;s only measuring GitHub users, and they are biased towards [Ruby, Perl and Javascript][24]. But seeing names there that I trust gives me confidence that it&#8217;ll help me find interesting people in Berlin.

Hopefully some of those people are reading this blog post right now. Others outside Berlin might be interested to know that Nokia does a superb job of relocating people, with everything taken care of by shipping companies and local agents. If you love the web, Javascript, mobile, user experience, social networks, location, enormous datasets and currywurst, you should [get in touch][25].

 [1]: https://www.nokia.com/press/press-releases/showpressrelease?newsid=1344044
 [2]: https://github.com
 [3]: https://www.google.com/search?hl=en&q=site:github.com+location+berlin+%22profile+-+github%22
 [4]: https://en.wikipedia.org/wiki/Centrality
 [5]: https://www.stoweboyd.com/message/its-betweenness-that-matters-not-your-eigenvalue-the-dark-ma.html
 [6]: https://www.dopplr.com/socialatlas
 [7]: https://develop.github.com/
 [8]: https://develop.github.com/p/users.html
 [9]: https://jung.sourceforge.net/
 [10]: https://jung.sourceforge.net/doc/api/edu/uci/ics/jung/algorithms/importance/BetweennessCentrality.html
 [11]: https://github.com/mattb/flotsam/tree/master/github-recruitment/
 [12]: https://github.com/mattb/flotsam/blob/master/github-recruitment/sf.txt
 [13]: https://github.com/defunkt
 [14]: https://github.com/miyagawa
 [15]: https://github.com/leah
 [16]: https://github.com/square
 [17]: https://github.com/tmm1
 [18]: https://github.com/mattb/flotsam/blob/master/github-recruitment/london.txt
 [19]: https://github.com/james
 [20]: https://github.com/lrug
 [21]: https://github.com/norm
 [22]: https://github.com/danwrong
 [23]: https://github.com/cv
 [24]: https://github.com/languages
 [25]: mailto:mb@hackdiary.com