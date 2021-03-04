---
title: A freetext-indexing IMAP spider
author: Matt Biddulph
type: post
date: 2003-02-06T23:00:09+00:00
excerpt: \n
url: /2003/02/06/a-freetext-indexing-imap-spider/
categories:
  - java

---
Because the Exchange mailserver at work is frustratingly slow and doesn&#8217;t have a flexible cross-folder search option, I wanted an indexing spider for IMAP. After a bit of struggling with the [javamail][1] API and almost no work at all plugging the messages into [Lucene][2] (which is impressively clean, flexible and powerful), I had some working code that will start at a folder and work down through its subfolders, indexing messages as it goes.

<!--more-->

  
This [tarball][3] contains the source, compiled class files and support jars, along with a [Jetty][4] setup that will let you run the demo servlet without needing an install of Tomcat or any other servlet engine. Point the indexer at your IMAP host and give it a folder to start from and it will recursively build an index of subject, date, from and mail body. Run Jetty via queryserver.sh and point your browser at https://localhost:9999

The indexer uses the Message-ID as a primary key; it will only index mail it hasn&#8217;t seen before when it does a run. This means it will work nicely from a regular cronjob. The query code uses the standard Lucene [query parser][5] so will support queries such as _+foo +bar_, _subject:fish_ and _&#8220;phrase search&#8221;_. The spider is independent of the indexer and just fires message events at a MessageListener interface, so it might be useful for other things. The main limitation at the moment (apart from some kind of nice interface) is that the code only copes with single-part messages of type text/plain. The MailDocument class is the place to start improving that.

 [1]: https://java.sun.com/products/javamail/
 [2]: https://jakarta.apache.org/lucene/
 [3]: https://www.hackdiary.com/src/mailindex-0.4.tar.gz
 [4]: https://www.mortbay.org/jetty/
 [5]: https://jakarta.apache.org/lucene/docs/queryparsersyntax.html