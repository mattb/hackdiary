---
title: 'Switching from scripting languages to Objective C and iPhone: useful libraries'
author: Matt Biddulph
type: post
date: 2009-01-26T23:17:36+00:00
url: /2009/01/26/switching-from-scripting-languages-to-objective-c-and-iphone-useful-libraries/
openid_comments:
  - 'a:2:{i:0;s:3:"233";i:1;s:3:"253";}'
categories:
  - iphone

---
For the last few months I&#8217;ve been spending much of my spare hacking time learning to code iPhone applications. I&#8217;ve found Objective C to be a surprisingly pleasant language, and Cocoa is one of the best frameworks I&#8217;ve ever worked with. I&#8217;ve reached a point where I feel I can go fairly quickly from simple app ideas to sketching in real code.

I&#8217;m a web developer at heart, and a scripting language user by preference. Coding for the iPhone doesn&#8217;t feel as fluid in text handling or HTTP access as the environments I&#8217;m used to. Fortunately I&#8217;ve been able to find some fantastic open-source libraries and wrappers that make up the difference. Here are my favourites so far:

### GTMHTTPFetcher from [Google Toolbox for Mac][1]

The iPhone&#8217;s [native HTTP handling][2] is capable, but low-level and verbose. Rather than handling the many callbacks, NSData objects and options I prefer this wrapper. It has a ton of convenience methods allowing you to specify POST data and basic auth, follow redirects automatically, keep cookies over a session, set headers, and have two simple callbacks for success and error handling. In many ways it&#8217;s comparable to [jQuery&#8217;s $.ajax() one-hit function][3]. 

### [JSON framework][4]

Having got some data over HTTP from a web API, chances are that it&#8217;s available in JSON format. This simple framework extends NSString with a `JSONValue` method to convert any legal JSON string to nested NSDictionaries and NSArrays. To go the other way, dictionaries and arrays gain a `JSONRepresentation` method.

### libxml2 wrappers for [XPath over XML and HTML][5]

Perhaps your web API returns XML, or perhaps you&#8217;re getting your data by screenscraping HTML. Did you know that the iPhone ships with libxml2, which has high-performance XML and HTML parsing and a high-quality XPath implementation? Don&#8217;t struggle with Cocoa&#8217;s NSXMLParser or get bogged down in the complex libxml2 docs; use these two simple wrapper functions, `PerformXMLXPathQuery` and `PerformHTMLXPathQuery`, to pull out the structured data you need in a Cocoa-friendly representation.

### [RegexKitLite][6] for regular expressions

Where would scripting be without regular expressions? Luckily they&#8217;re available on the iPhone, but buried deep within the [ICU libraries][7]. RegexKitLite extends NSString with core regex string handling, including &#8216;split&#8217; (known as `componentsSeparatedByRegex`) and a search-and-replace operator (`stringByReplacingOccurrencesOfRegex` and `replaceOccurrencesOfRegex`).

### [FMDB][8], an Objective C wrapper for sqlite

Every scripting language has convenient database driver wrappers. I was very happy to find that sqlite is available on the iPhone, but unfortunately its interface is all bare-metal C. The simplest wrapper I&#8217;ve found so far is FMDB. Apparently somewhat inspired by JDBC, it gives you connection and resultset objects, along with one-liner convenience functions allowing code like `[db intForQuery:@"SELECT COUNT(*) FROM things"]`.

### And there&#8217;s more&#8230;

I&#8217;ve used all of the above in a real project, but I&#8217;ve got yet more things to explore on my todo list. These include [Matt Gemmell&#8217;s web-style templating framework MGTemplateEngine][9], [ActorKit for Erlang-style messaging and thread management][10] and the [LLVM/Clang Static Analyzer for automatic bug detection][11]. What else do you use?

 [1]: https://code.google.com/p/google-toolbox-for-mac/
 [2]: https://developer.apple.com/documentation/Cocoa/Conceptual/URLLoadingSystem/URLLoadingSystem.html
 [3]: https://docs.jquery.com/Ajax/jQuery.ajax
 [4]: https://code.google.com/p/json-framework/
 [5]: https://cocoawithlove.com/2008/10/using-libxml2-for-parsing-and-xpath.html
 [6]: https://regexkit.sourceforge.net/RegexKitLite/
 [7]: https://www.icu-project.org/
 [8]: https://flycode.googlecode.com/svn/trunk/fmdb/
 [9]: https://mattgemmell.com/2008/05/20/mgtemplateengine-templates-with-cocoa
 [10]: https://code.google.com/p/plactorkit/
 [11]: https://www.oiledmachine.com/posts/2009/01/06/using-the-llvm-clang-static-analyzer-for-iphone-apps.html