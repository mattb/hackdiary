---
title: To bots about gatebot
author: Matt Biddulph
type: post
date: 2002-08-26T14:41:05+00:00
excerpt: \n
url: /2002/08/26/to-bots-about-gatebot/
categories:
  - bots
  - java
  - perl
  - rest

---
A mail [to the bots list][1] about a web-to-IRC gateway.

<!--more-->

  
**Subject: [Bots] gatebot &#8211; making bots URL-addressable**  
From: Matt Biddulph  
_Date: Mon Aug 26 14:41:05 2002_

I&#8217;ve put up a new experimental service that allows code to talk to IRC  
bots over the web without making a direct IRC connection.

You can try it out here via a dodgy web form interface:

<a HREF="https://www.picdiary.com/bot/index.html">https://www.picdiary.com/bot/index.html</a>

But it&#8217;s really meant as some kind of web API for access by code (e.g.  
so web apps could ask the foafbot for people-related information). It  
works like this:

POST to  
<a HREF="https://www.picdiary.com/bot/servlet/GatebotServlet/some.irc.server/somebotnick">https://www.picdiary.com/bot/servlet/GatebotServlet/some.irc.server/somebotnick</a>  
with a query of "say=what%20you%want%20to%say". The web service sends a  
proxy bot onto some.irc.server and privmsgs somebotnick with what you  
want to say.

You get back a simple HTML document, with a 201 Created status to  
indicate the creation of a new session URL for you to read back what is  
said. This session URL is given both in the HTML (for browser-based  
testing) and in the HTTP Location: header. Every time you hit this URL,  
it&#8217;ll give you a line-by-line dump of what have been privmsged back to  
the proxy bot (obviously this will be blank if you hit the URL quickly &#8211;  
if you expect an answer then poll it at some regular interval).

If nothing is said to the bot for 60 seconds, it leaves the IRC network  
but the URL remains available &#8216;indefinitely&#8217; (it&#8217;s kept in memory and  
will die when my webserver restarts). You should also be able to say  
further things to the same bot in the same session by POSTing to the  
session URL with "say=whatever"

Source code (perl for the bot bits, java servlet for the web bits) is  
here:  
<a HREF="https://www.picdiary.com/~mattb/bots/gatebot-0.2.tar.gz">https://www.picdiary.com/~mattb/bots/gatebot-0.2.tar.gz</a>  
Apologies for any hard-coded paths or other cruftiness. The version of  
Bot::BasicBot in there is slightly modified to listen on STDIN so that  
the web layer can communicate with its proxy bots by spawning processes  
and using STDIN/STDOUT.

There are a couple of pieces of demo client code in the tarball.  
getkarma asks the infobot &#8216;robert&#8217; on #pants for karma of things via a  
commandline interface. There&#8217;s also an infobotkarmabot that does the  
same thing but with an IRC interface.

Here&#8217;s the IRC karma bot connecting to #bots on london.rhizomatic.net:

&#8211;> robertpro (~<a HREF="mailto:robertpro@217.158.195.49">robertpro@217.158.195.49</a>) has joined #bots  
<mattb> robertkarma test  
<robertpro> robert says test has karma of 1

and the action this triggered on #gatebot (where proxy bots hang out  
while they&#8217;re privmsging) on the irc network where #pants lives:

&#8211;> EUUREbot (<a HREF="mailto:tomcat4@pod-124.dolphin-server.co.uk">tomcat4@pod-124.dolphin-server.co.uk</a>) has joined #gatebot  
<EUUREbot> robert said &#8216;test has karma of 1&#8217;

Feel free to play with this, and flame me royally if it breaks or sucks.

Cheers,  
Matt.

* * *

and a later [response][2] to a followup:

On Mon, 2002-08-26 at 17:16, Mark Fowler wrote:  
> Hmm. Any reason this can&#8217;t be a GET? Aside from the breaking of the  
> idempotent nature of requests I mean (pah, RFCs.) It&#8217;d just be nice so  
> that you can use it with Mozilla&#8217;s bookmark keywords function (where you  
> can type &#8216;$keyword $foo&#8217; and it looks up a url you&#8217;ve associated with  
> $keyword changing &#8216;%s&#8217; for a URI encoded version of $foo.)

Yeah, preserving the semantics of POST seems quite important here &#8211; this  
is initiating an action, which causes the creation of a resource (both  
in the sense of the URL and the process actually forked). This resource  
then becomes readable in an idempotent way, its content changing as it  
(hopefully) interacts with the remote bot it&#8217;s talking to.

In order to support an application such as &#8216;return me this information&#8217;  
for bookmark-keywords purposes, I would rather a wrapper application  
were used that was truly GETtable &#8211; it would make the initial POST and  
poll the resulting GETtable session until it returned some useful  
information. Only then would it return 200 OK and some content to the  
client. A directly GETtable gatebot service would 99% of the time simply  
return a blank screen to the browser because it has no way of knowing  
how long to wait (if it should wait for a response at all).

 [1]: https://london.pm.org/pipermail/bots/2002-August/000125.html
 [2]: https://london.pm.org/pipermail/bots/2002-August/000129.html