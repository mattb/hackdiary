---
title: Google map of London with Flickr shape data overlaid
author: Matt Biddulph
type: post
date: 2008-11-16T16:18:53+00:00
url: /2008/11/16/google-map-of-london-with-flickr-shape-data-overlaid/
categories:
  - javascript
tags:
  - dopplr
  - Flickr

---
<div style="padding: 3px; text-align: left;">
  <a title="photo sharing" href="https://www.flickr.com/photos/mbiddulph/3034389047/"><img style="border: 2px solid rgb(0, 0, 0);" src="https://farm4.static.flickr.com/3062/3034389047_2996e08e29.jpg" alt="" /></a>
</div>

<a class="zem_slink" title="Flickr" rel="homepage" href="https://www.flickr.com/">Flickr</a> place info now includes shape data for many places. See [the Flickr code blog][1] for more.

We&#8217;ve correlated most of Dopplr&#8217;s places with Yahoo WOE IDs using Flickr&#8217;s reverse geocoder, so we can use this data too. As an experiment, I wrote some clientside code to overlay this shape data onto the maps we use on Dopplr. Help yourself to the code if you want it: [gist.github.com/25502][2]

 [1]: https://code.flickr.com/blog/2008/10/30/the-shape-of-alpha/
 [2]: https://gist.github.com/25502