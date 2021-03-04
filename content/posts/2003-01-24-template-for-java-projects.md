---
title: Template for Java projects
author: Matt Biddulph
type: post
date: 2003-01-24T18:53:05+00:00
excerpt: \n
url: /2003/01/24/template-for-java-projects/
categories:
  - java

---
Every time I start a new java project, no matter what size, the first thing I do is go hunting through my java directories looking for one to use as a template. Over time I&#8217;ve gathered some pretty useful [ant][1] targets and settled on a fairly rational directory structure. Today I got round to building a skeleton set of directories and files that I can reuse in the future. Here&#8217;s a [tarball][2] of the results.

<!--more-->

  
There are some features of the template that are specifically for deploying web apps into Tomcat. They can be easily ignored if you&#8217;re not doing that. The directory structure goes like this:

  * _etc_ &#8211; put any misc files to go in WEB-INF in here and they&#8217;ll be copied over when the project is deployed. _web.xml_ lives in here.
  * _lib_ &#8211; put the .jar files your code depends on in here and they will be automatically put into the classpath for compilation and deployed to the right place in the webapp.
  * _src_ &#8211; your java source.
  * _tests_ &#8211; the java source of your junit tests for the code in _src_.
  * _web_ &#8211; the web document tree for deployment.

Here are the targets in the ant buildfile:

  * _compile_ &#8211; compiles the java from _src_ into _build_.
  * _test_ &#8211; compiles the source and the tests and runs every test in _tests_ using junit.
  * _clean_ &#8211; nukes the build and testbuild directories.
  * _with.jikes_ &#8211; add this before any target that compiles to set jikes as the build compiler.
  * _with.clover_ &#8211; add this before any target that compiles to instrument the .class files with [clover][3].
  * _clover.report_ &#8211; runs the clover reporter. Best used after running tests, as in _ant clean with.clover test clover.report_.
  * _clover.report.html_ &#8211; runs the clover html reporter.
  * _deploy_ &#8211; compiles and deploys the project into a tomcat webapp directory, copying the classes, config files from _etc_, web tree from _web_ and the jars from _lib_.
  * _ctags_ &#8211; runs _ctags -R_ over the _src_ and _tests_ directories. This is run automatically by the _compile_ targets.
  * _javadoc_ &#8211; compile javadoc into _javadoc_.
  * _run_ &#8211; run some code from your source with the classpath all set up correctly for your libs and source.
  * _pause_ &#8211; pauses and waits for carriage-return before running the next target. I use this to make ant more responsive; I find that it can take several seconds for ant to start up and parse its build file, and I like to run the compiler a lot while I&#8217;m coding so that I can check my tests as often as possible. In the shell, I use this line: _while true; do ant with.jikes pause test; done_. This means that every time you hit enter, the compile-and-test run is done then ant makes itself ready for the next run.

 [1]: https://ant.apache.org
 [2]: https://www.hackdiary.com/misc/ant-project-template-1.0.tar.gz
 [3]: https://www.thecortex.net/clover/