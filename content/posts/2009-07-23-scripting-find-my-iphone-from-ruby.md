---
title: Scripting “Find My iPhone” from Ruby
author: Matt Biddulph
type: post
date: 2009-07-23T15:25:13+00:00
url: /2009/07/23/scripting-find-my-iphone-from-ruby/
categories:
  - Uncategorized

---
When the iPhone OS 3.0 came out with new Mobile Me features allowing you to remotely discover the location of your iPhone and send it a message and an alarm, I hoped that there&#8217;d be an API. While there&#8217;s no official way to access it, the enterprising [Tyler Hall][1] and [Sam Pullara][2] dug out their HTTP sniffers and figured out how the javascript on me.com talks to its backend service.

Their code is written in PHP and Java respectively, two languages I&#8217;m not particularly comfortable in. Translating from their source code, I&#8217;ve produced a [ruby version][3] and packaged it as a very simple gem. It lacks real documentation or elegant error handling, but it&#8217;s easy to figure out.

Use it like this to locate your phone:

`$ sudo gem install mattb-findmyiphone --source https://gems.github.com`

`>> require 'rubygems' ; require 'findmyiphone'`  
`>> i = FindMyIphone.new(username,password)`  
`>> i.locateMe`  
`=> {"status"=>1, "latitude"=>51.546544, "time"=>"8:06 AM", "date"=>"July 23, 2009", "accuracy"=>162.957953, "isLocationAvailable"=>true, "isRecent"=>true, "isLocateFinished"=>true, "statusString"=>"locate status available", "isAccurate"=>false, "isOldLocationResult"=>true, "longitude"=>-0.05744}`

<img style="float:right" src="https://www.hackdiary.com/misc/iphone_important_message.png" alt="Important Message on the iPhone" width="160" height="240" /> And to send a message:

`>> i.sendMessage("Unimportant message")`  
`=> {"status"=>1, "time"=>"8:17 AM", "date"=>"July 23, 2009", "unacknowledgedMessagePending"=>true, "statusString"=>"message sent"}`

Finally, if you look in the `examples` directory you&#8217;ll find a short script that uses the location data to update [Fire Eagle][4] via its API. Fill in the example YAML files with the appropriate credentials and it&#8217;ll do the rest.

Of course the code&#8217;s all open source and contributions via [Github][3] are very welcome.

 [1]: https://clickontyler.com/blog/2009/06/sosumi-a-mobileme-scraper/
 [2]: https://www.javarants.com/2009/07/03/creating-a-json-web-service-api-for-find-my-iphone/
 [3]: https://github.com/mattb/findmyiphone/tree/master
 [4]: https://fireeagle.yahoo.net