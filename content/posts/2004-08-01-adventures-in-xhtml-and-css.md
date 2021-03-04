---
title: Adventures in XHTML and CSS
author: Matt Biddulph
type: post
date: 2004-08-01T19:34:08+00:00
excerpt: \n
url: /2004/08/01/adventures-in-xhtml-and-css/
categories:
  - web

---
For my dad&#8217;s 60th birthday, my family and I produced a print book of memories and photographs from his life. I typeset it using OpenOffice 1.1 and sent it to the printers as PDF, which worked just fine. Today I&#8217;ve been creating an [online version][1] from the original document.

<!--more-->

  
Although the layout was quite simple (two columns of text and images), the automatic HTML export was pretty bad &#8211; full of ugly FONT tags and with the images in all the wrong places. I ended up starting again from scratch, hand-producing XHTML and CSS with nothing but a text editor and pasting the text in from the original.

The resulting HTML is [valid][2] XHTML 1.1 strict, and degrades nicely in lynx. I&#8217;ve not yet been able to check it in many other browsers, but it seems to look OK in IE6 running under [win4lin][3] (I don&#8217;t have any machines natively running Windows).

I used to shy away from frontend web work, finding it awfully fiddly and dull. Over the last year or two I&#8217;ve discovered that making simple semantic HTML and styling it with CSS can be quite a satisfying activity.

 [1]: https://www.mikebiddulph.org/selectiveperception/
 [2]: https://validator.w3.org/check?uri=http%3A%2F%2Fwww.mikebiddulph.org%2Fselectiveperception%2Fjobs.html
 [3]: https://www.netraverse.com