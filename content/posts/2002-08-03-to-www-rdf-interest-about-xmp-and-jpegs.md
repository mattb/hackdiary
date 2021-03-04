---
title: To www-rdf-interest about XMP and JPEGs
author: Matt Biddulph
type: post
date: 2002-08-03T19:18:39+00:00
excerpt: \n
url: /2002/08/03/to-www-rdf-interest-about-xmp-and-jpegs/
categories:
  - photos
  - rdf

---
A mail [sent to www-rdf-interest][1] after attempting to embed XMP metadata in JPEGs.

(It turns out my code doesn&#8217;t do the jpeg embedding quite right. It looks like the [JPEG-XMP][2] package will do it correctly.)

<!--more-->

  
**Subject: Adobe XMP and jpeg embedding**  
To: www-rdf-interest@w3.org  
Date: 03 Aug 2002 19:18:39 +0100

I was discussing picture metadata with some people this morning and  
decided to have a play with the Adobe XMP toolkit [1]. Here are my  
notes, in case they are of use or interest to anyone.

job 1: compile under linux, which is unsupported  
* the code compiles with warnings if you apply these small  
changes across the .c, .cpp and .h files:  
* s/xap\_xpdomconf.h/XAP\_XPDOMConf.h/g  
* s/XPDom.h/XPDOM.h/g  
* s/XAPTkinternals.h/XAPTkInternals.h/g  
* tsk tsk to adobe for developing on a case-insensitive OS but  
putting mixed-case filenames in their zipfiles  
* also, some files use FREE, REALLOC, CALLOC and MALLOC macros  
which presumably would get correctly resolved via a chain of ifdefs  
and stuff if i were on windows, but for now just #define them to  
regular libc free, realloc, calloc and malloc  
* then compile everything with gcc/g++ version 3  
* i should make a Makefile really, but i&#8217;m too dumb so I just  
muck about on the cmdline  
* the sample XAPDumper also needs the PacketScanner utility to  
compile, but that&#8217;s also in the distribution and compiles OK  
(perhaps with similar case-changes for include files)  
* having done this, i end up with a bunch of apparently  
working code, but I am getting some segfaults on exit  
* i shall run a memory profiler when i get a round tuit

job 2: try the dumper  
* as you&#8217;d hope, the PDF files that document the XMP toolkit  
themselves have XMP embedded  
* so I ran the dumper on XMPEmbedding.pdf and got this dump [2]  
* and here&#8217;s a nice w3c rdf validator visualisation of the  
metadata [3]

job 3: insert XMP into JPEG as described in XMPEmbedding.pdf  
* now, time to write some C++ using the toolkit  
* I used the MetaXAP object to create a new chunk of rdf  
describing a jpeg as having dc:creator David Brophy  
* that gets rendered to RDF/XML and the UtilityXAP object  
creates an &#8216;xml packet&#8217; wrapper around the metadata  
* i now have a string ready to insert into a jpeg  
* i use libexif5 and something named &#8216;libjpeg&#8217; extracted from  
the source distribution of the &#8216;exif&#8217; command to add data to the  
existing jpeg file  
* this goes in an APP1 segment that starts with a length value  
and the null-terminated string &#8216;<a HREF="https://ns.adobe.com/xap/1.0/">https://ns.adobe.com/xap/1.0/</a>&#8216;,  
followed by the  
<?xpacket begin=&#8217;\x{FEFF}&#8217; id=&#8217;W5M0MpCehiHzreSzNTczkc9d&#8217;?>  
&#8230;  
<?xpacket end=&#8217;w&#8217; ?>  
wrapper created by the toolkit  
* the resulting jpeg [4] still renders correctly as a jpeg,  
and also contains xmp data giving dc:creator as David Brophy  
* and works as expected with dan brickley&#8217;s XMP demo:  
* extracted metadata: [5], raw RDF/XML: [6]  
* the slightly shoddy code that does job 3 is available [7]

References

1. <a HREF="https://www.adobe.com/products/xmp/">https://www.adobe.com/products/xmp/</a>  
2. <a HREF="https://www.picdiary.com/~mattb/misc/xmpdump.txt">https://www.picdiary.com/~mattb/misc/xmpdump.txt</a>  
3. <a HREF="https://www.picdiary.com/~mattb/misc/xmpdump.png">https://www.picdiary.com/~mattb/misc/xmpdump.png</a>

4. <a HREF="https://www.picdiary.com/~mattb/misc/xmp.jpg">https://www.picdiary.com/~mattb/misc/xmp.jpg</a>  
5.  
<a HREF="https://www.w3.org/2001/sw/Europe/200206/imagemeta/extract/extract?uri=https://www.picdiary.com/~mattb/misc/xmp.jpg&#038;html=true">https://www.w3.org/2001/sw/Europe/200206/imagemeta/extract/extract?uri=https://www.picdiary.com/~mattb/misc/xmp.jpg&html=true</a>  
6.  
<a HREF="https://www.w3.org/2001/sw/Europe/200206/imagemeta/extract/extract?uri=https://www.picdiary.com/~mattb/misc/xmp.jpg&#038;html=false">https://www.w3.org/2001/sw/Europe/200206/imagemeta/extract/extract?uri=https://www.picdiary.com/~mattb/misc/xmp.jpg&html=false</a>  
7. <a HREF="https://www.picdiary.com/~mattb/misc/xmptest.cpp">https://www.picdiary.com/~mattb/misc/xmptest.cpp</a>

Cheers,  
Matt.

 [1]: https://lists.w3.org/Archives/Public/www-rdf-interest/2002Aug/0012
 [2]: https://www.w3.org/People/Bos/JPEG-XMP/