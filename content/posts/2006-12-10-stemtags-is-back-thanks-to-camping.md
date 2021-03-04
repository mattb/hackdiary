---
title: Stemtags is back, thanks to Camping
author: Matt Biddulph
type: post
date: 2006-12-10T17:08:46+00:00
excerpt: \n
url: /2006/12/10/stemtags-is-back-thanks-to-camping/
categories:
  - Uncategorized

---
Nearly two years ago, I wrote a utility to [check your del.icio.us tags for duplication using Porter stemming][1]. Until today, the application had stopped working completely due to the fragility of the screenscraping code it was using. For fun, I&#8217;ve done a rewrite using Ruby <strike>and [Hpricot][2]</strike>, with all-new <strike>fragile screenscraping</strike> code based on [the del.icio.us JSON feeds][3] (thanks to [Lenny Domnitser][4] for pointer those out to me). I web-enabled it using [Camping][5], a nice mini-framework for when webapps don&#8217;t need all the bells and whistles of Rails.

[Here&#8217;s the result][6].

<!--more-->

  
Thanks to camping, the code is compact &#8211; only <strike>105</strike> 98 lines including templates:

<div style='width:600px'>
  <textarea name="code" class="ruby" id='source' rows="10" cols="60" style="display:none"><br /> </textarea>
</div>

<link type="text/css" rel="stylesheet" href="/style/SyntaxHighlighter.css" />
</link> 
  
  
  
</p> 

If you want to run it yourself, you&#8217;ll also need [stemmable.rb][7].

 [1]: https://www.hackdiary.com/archives/000067.html
 [2]: https://code.whytheluckystiff.net/hpricot/
 [3]: https://del.icio.us/help/json/tags
 [4]: https://domnit.org/tagstem.html
 [5]: https://redhanded.hobix.com/bits/campingAMicroframework.html
 [6]: https://www.hackdiary.com/stemtags
 [7]: https://www.tartarus.org/martin/PorterStemmer/ruby.txt