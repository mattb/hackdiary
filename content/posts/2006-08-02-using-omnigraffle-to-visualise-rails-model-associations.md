---
title: Using Omnigraffle to visualise Rails model associations
author: Matt Biddulph
type: post
date: 2006-08-02T14:57:19+00:00
excerpt: \n
url: /2006/08/02/using-omnigraffle-to-visualise-rails-model-associations/
categories:
  - rails

---
This week I&#8217;m doing some Rails consulting work for a company that&#8217;s already developed and deployed a major application. Getting to know a new codebase takes a little time and every diagram or visualisation helps. To help me understand their ActiveRecord model relationships, I knocked together a quick script to scan the associations between models and output it in the [Graphviz][1] DOT format.

<!--more-->

  
A quick Omnigraffle import later, and I get useful diagrams like this fragment from the [BBC Programme Catalogue][2] codebase:

![][3] 

Here&#8217;s the code, ready for running from the top of any Rails project (ymmv, etc):

<pre class="codeblock">#!/usr/bin/env ruby
require "config/environment"
Dir.glob("app/models/*rb") { |f|
require f
}
puts "digraph x {"
Dir.glob("app/models/*rb") { |f|
f.match(/\/([a-z_]+).rb/)
classname = $1.camelize
klass = Kernel.const_get classname
if klass.superclass == ActiveRecord::Base
puts classname
klass.reflect_on_all_associations.each { |a|
puts classname + " -> " + a.name.to_s.camelize.singularize + " [label="+a.macro.to_s+"]"
}
end
}
puts "}"
</pre>

 [1]: https://www.graphviz.org/
 [2]: https://www.hackdiary.com/archives/000081.html
 [3]: https://www.hackdiary.com/images/bbc_models.png