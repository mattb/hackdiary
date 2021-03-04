---
title: To rss-dev about picdiary
author: Matt Biddulph
type: post
date: 2002-12-17T21:18:00+00:00
excerpt: \n
url: /2002/12/17/to-rss-dev-about-picdiary/
categories:
  - foaf
  - photos
  - rdf
  - rss
  - xml

---
A mail [sent to RSS-DEV][1] about work in progress on picdiary and its use of RSS for cataloguing photos.

<!--more-->

  
**Subject: Re: [RSS-DEV] RSS and Libraries**  
From: mb@p&#8230;  
Date: Tue Dec 17, 2002 9:18 pm

On Mon, Dec 16, 2002 at 05:14:33PM +0000, Libby Miller wrote:  
> On Mon, 16 Dec 2002, se teague wrote:  
> > I&#8217;m so happy to find this group! I&#8217;ve been developing an  
> > RSS/Perl/PHP/MySQL based rss program to generate news and events for the  
> > academic library I work for. i do have a question though; We haven&#8217;t  
> > tackled associating images with RSS items rather than channels. Has  
> > anyone done this before? Any best practices out there?  
>  
> I rather like what Matt Biddulph&#8217;s been doing, e.g.:  
> <https://www.picdiary.com/rss/barcelona_conf.rss>

Thanks Libby. To (over)elaborate:

My site (<https://www.picdiary.com>) is just a blog of collections of  
pictures. There&#8217;s not much text, the pictures are the main focus and  
just have a few lines of description. For a while it&#8217;s been lacking good  
search facilities, and was built out of static HTML.

I decided to use RSS 1.0 as the &#8216;container&#8217; format for each picture  
collection. RSS works just as well for pictures-as-items as it does for  
html-pages-as-items &#8211; they&#8217;re all just web links. So I wrote a bunch of  
simple perl scripts to read in RSS and display them as web pages. For  
example, The link Libby gave above can be viewed at  
[  
https://www.picdiary.com/new/barcelona\_conf?rss=barcelona\_conf.rss&page=1  
][2]  
or of course it can be viewed in a newsreader/aggregator.

If you look in the HTML source of that page, you&#8217;ll see a line like  
this:

<link rel=&#8221;alternate&#8221; type=&#8221;application/rss+xml&#8221; title=&#8221;RSS&#8221;  
href=&#8221;https://www.picdiary.com/rss/barcelona_conf.rss&#8221;>

This is following the rss autodiscovery standard so that spiders can  
find the RSS metadata from the webpage.

Using RSS 1.0&#8217;s RDF capability, I can add all sorts of metadata to  
channels and items with a few extra tags in the RSS. That particular  
feed uses FOAF to say that certain pictures are of people like Libby.  
Other (more recent) feeds such as  
<https://www.picdiary.com/rss/highwalk.rss> also use Dublin Core to give  
the creator and date of the channel, and Wordnet to list keywords  
associated with each picture (item).

There&#8217;s a (prerelease) search engine that indexes all the RSS and uses  
the Wordnet terms (and exploits Wordnet&#8217;s synonym and hypernym  
relationships between words to give better search results) at  
<https://www.picdiary.com/cgi-bin/search.pl?word=building>  
If you look &#8216;behind the scenes&#8217; of that search engine at  
<https://www.picdiary.com:8180/rss/search?word=building>  
then you&#8217;ll see that the search results themselves are returned as  
dynamically-built RSS channels then rendered into HTML by some perl. So  
you could subscribe to the search results if you wanted to.

Ramble ramble. There&#8217;s quite a lot to say, feel free to followup or mail  
me off-list for more information.

Cheers,  
Matt.

 [1]: https://groups.yahoo.com/group/rss-dev/message/4580
 [2]: https://www.picdiary.com/new/barcelona_conf?rss=barcelona_conf.rss&page=1