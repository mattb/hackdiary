---
title: MAC-address logging/blocking for linux iptables
author: Matt Biddulph
type: post
date: 2003-01-02T09:55:28+00:00
excerpt: \n
url: /2003/01/02/mac-address-loggingblocking-for-linux-iptables/
categories:
  - hardware
  - linux
  - wireless

---
Here&#8217;s a [little script][1] I wrote that checks incoming wireless requests for a known MAC address. I&#8217;ve been using it on my Linux gateway/router/wireless-bridge.

If it doesn&#8217;t know you, it transparent-proxies all your outgoing port 80 traffic to the local webserver&#8217;s port 81, where you could put a redirect to a polite message or something.

<!--more-->

  
In my case I&#8217;d just like to put some sort of guestbook page that logs your MAC and adds it automatically to the firewall rules after you leave a comment. I don&#8217;t mind sharing my bandwidth from time to time, but I&#8217;d love to know if someone benefitted from it.

I was impressed with the power of iptables, once I got my head round it. I found an [ascii-art diagram][2] that helped me understand the flow through the various tables and targets.

 [1]: https://www.picdiary.com/~mattb/wireless/macblock.txt
 [2]: https://www.sibbald.com/unixutil/iptables-firewall.html