---
title: Natural Language Processing and Machine Learning, some pointers
author: Matt Biddulph
type: post
date: 2012-10-14T12:02:15+00:00
url: /2012/10/14/natural-language-processing-and-machine-learning-some-pointers/
categories:
  - data

---
I&#8217;ve been doing a lot of natural-language machine-learning work both for clients and in side-projects recently. [Mark Needham][1] asked me on Twitter for some pointers to good introductory material. Here&#8217;s what I wrote for him:

Nearly all text processing starts by transforming text into vectors:  
[https://en.wikipedia.org/wiki/Vector\_space\_model][2]

Often it uses transforms such as TFIDF to normalise the data and control for outliers (words that are too frequent or too rare confuse the algorithms):  
<https://en.wikipedia.org/wiki/Tf%E2%80%93idf>

Collocations is a technique to detect when two or more words occur more commonly together than separately (e.g. &#8220;wishy-washy&#8221; in English) &#8211; I use this to group words into n-gram tokens because many NLP techniques consider each word as if it&#8217;s independent of all the others in a document, ignoring order:  
<https://matpalm.com/blog/2011/10/22/collocations_1/>  
<https://matpalm.com/blog/2011/11/05/collocations_2/>

When you&#8217;ve got a lot of text and you don&#8217;t know what the patterns in it are, you can run an &#8220;unsupervised&#8221; clustering using Latent Dirichlet allocation:  
[https://www.cs.princeton.edu/~blei/papers/Blei2012.pdf][3]  
<https://www.youtube.com/watch?v=5mkJcxTK1sQ>

Or if you know how your data is divided into topics, otherwise known as &#8220;labeled data&#8221;, then you can run &#8220;supervised&#8221; techniques such as training a classifier to predict the labels of new similar data. I can&#8217;t find a really good page on this &#8211; I picked up a lot in IM with my friend Ben who is writing a book coming out next year: <https://blog.someben.com/2012/07/sequential-learning-book/>

Here are the tools I&#8217;ve mostly been using:

  * Vowpal Wabbit (classification and LDA, poor documentation, C++ high performance): <https://github.com/JohnLangford/vowpal_wabbit/wiki>
  * Gensim (LDA, vector similarity, text processing, python): <https://radimrehurek.com/gensim/index.html>
  * Mallet (classification and LDA, java): <https://mallet.cs.umass.edu/>
  * Lingpipe (text analysis, clustering, classification, linguistics, java, commercial open-source): <https://alias-i.com/lingpipe/demos/tutorial/read-me.html>
  * Mahout (Hadoop, classification, clustering, LDA, collaborative filtering, java): <https://mahout.apache.org/>
  * Langdetect (language detection, java): <https://code.google.com/p/language-detection/>

Some blogs I like:

  * <https://matpalm.com/blog/>
  * <https://blog.echen.me/>
  * <https://thedatachef.blogspot.co.uk/></il> 
      * <https://www.machinedlearnings.com></ul> 
    MetaOptimize Q+A is the Stack Overflow of ML: <https://metaoptimize.com/qa>
    
    The Mahout In Action book is quite good and practical: <https://manning.com/owen/></article>

 [1]: https://www.markhneedham.com/blog/
 [2]: https://en.wikipedia.org/wiki/Vector_space_model
 [3]: https://www.cs.princeton.edu/%7Eblei/papers/Blei2012.pdf