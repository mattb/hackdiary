---
title: Using HTTP conditional GET in java for efficient polling
author: Matt Biddulph
type: post
date: 2003-04-09T15:52:59+00:00
excerpt: \n
url: /2003/04/09/using-http-conditional-get-in-java-for-efficient-polling/
categories:
  - java

---
If you&#8217;re going to download a resource over HTTP from a URL more than once, there are a couple of features of HTTP you should make sure you&#8217;re using. By giving the server some metadata about what you saw when you last downloaded the resource, it can give you a status code indicating that the resource hasn&#8217;t changed and you should continue to use the version you already have.

This issue has been highlighted recently by the bandwidth load caused by the growth in popularity of RSS readers, which repeatedly download RSS files looking for changes. There&#8217;s a good writeup of the details at [The Fishbowl][1]. I didn&#8217;t find any sample Java source when I went looking recently, so here&#8217;s some code.

<!--more-->

  
If you&#8217;re using [Jakarta Commons HttpClient][2] and you have an etag and lastModified string cached with a document then use these lines on your GetMethod instance:

`GetMethod get = new UrlGetMethod(url);<br />
get.addRequestHeader(new Header("If-None-Match",etag));<br />
get.addRequestHeader(new Header("If-Modified-Since",lastModified));`

then check the response code like this:

`client.executeMethod(get);<br />
if(get.getStatusCode() < 300) {
&nbsp;            // server gave us a document
&nbsp;            HeaderElement[] etags = get.getResponseHeader("ETag").getValues();
&nbsp;            if(etags.length > 0) {<br />
&nbsp;&nbsp;               String newEtag = etags[0].getName(); // stash this somewhere<br />
&nbsp;            }</p>
<p>&nbsp;            HeaderElement[] mods = get.getResponseHeader("Last-Modified").getValues();<br />
&nbsp;            if(mods.length > 0) {<br />
&nbsp;&nbsp;                String newLastModified = mods[0].getName()); // stash this somewhere<br />
&nbsp;            }<br />
} else {<br />
&nbsp;            // server didn't give us a document, no update<br />
}`

The equivalent lines (taken from [nntp//rss][3]) for the standard JDK java.net package are:

`HttpURLConnection httpCon = ....<br />
httpCon.setRequestProperty("If-None-Match", etag);<br />
httpCon.setIfModifiedSince(lastModified);`

and

`if(httpCon.getResponseCode() == HttpURLConnection.HTTP_OK) {<br />
&nbsp;newEtag = httpCon.getHeaderField("ETag");<br />
&nbsp;newLastModified = httpCon.getHeaderFieldDate("Last-Modified", 0);<br />
}<br />
if(httpCon.getResponseCode() == HttpURLConnection.HTTP_NOT_MODIFIED) {<br />
&nbsp; // no change<br />
}`

 [1]: https://fishbowl.pastiche.org/archives/001132.html
 [2]: https://jakarta.apache.org/commons/httpclient/index.html
 [3]: https://www.methodize.org/nntprss/