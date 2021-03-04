---
title: Annotated source code for Second Life flickr screen
author: Matt Biddulph
type: post
date: 2006-06-19T18:17:12+00:00
url: /2006/06/19/annotated-source-code-for-second-life-flickr-screen/
categories:
  - misc

---
I&#8217;ve had quite a few requests for the source code of the [Flickr screen for Second Life][1] that I wrote about a few weeks ago. Here&#8217;s the code, annotated with links to the Second Life coding wiki and a few notes.

I&#8217;m only publishing the LSL code, because the serverside code isn&#8217;t very interesting and does pretty much exactly what it says in the previous post. If you want to run your own flickr screen, the URLs in the code below should work just as well for your objects as they do for mine. <del>If you have problems, <a href="mailto:mb@hackdiary.com">let me know</a></del>. I reserve the right to switch off the code if the traffic gets too high, but I&#8217;ll post here if I have to do that.

**UPDATE**: Sorry, but I no longer have the server capacity to run the backend for this service. I&#8217;m told that new features in the Second Life Viewer mean that you can achieve the same thing now with [Shared Media][2].

The code uses SL&#8217;s streaming media feature to load the jpeg into a texture. This comes with a number of restrictions: &#8216;You are allowed one movie (or &#8220;media&#8221; resource) per land parcel. The movie will be played by replacing a texture on an object with the movie. Users will only see the movie when they are standing on your land parcel. Otherwise they will see the static texture. Script functions only work for objects owned by the land owner or deeded to the group that owns the land. (Remember to set asset permissions on your script and object as well as sharing it with the group!)&#8217;. I&#8217;m hoping for much better media support than this in future Second Life versions.<!--more-->

<pre class="codeblock">// A place to remember the ID for the latest http request we made, so the callback doesn't process out-of-order responses
key http_id;
// Test pattern - Used as default video texture when one is missing in parcel media
key VIDEO_DEFAULT = "6e0f05ad-1809-4edc-df29-fae3d2a6c9b8";
// Set the texture to the jpeg provided by url
seturl(string url)
{
key video_texture = <a href="https://secondlife.com/badgeo/wakka.php?wakka=llList2Key">llList2Key</a>(<a href="https://secondlife.com/badgeo/wakka.php?wakka=llParcelMediaQuery">llParcelMediaQuery</a>( [PARCEL_MEDIA_COMMAND_TEXTURE]), 0);
if(video_texture == NULL_KEY)
{
video_texture = VIDEO_DEFAULT;
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llParcelMediaCommandList">llParcelMediaCommandList</a>([PARCEL_MEDIA_COMMAND_TEXTURE, VIDEO_DEFAULT]);
}
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llSetTexture">llSetTexture</a>(video_texture,ALL_SIDES);
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llParcelMediaCommandList">llParcelMediaCommandList</a>([PARCEL_MEDIA_COMMAND_URL,url]);
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llParcelMediaCommandList">llParcelMediaCommandList</a>([PARCEL_MEDIA_COMMAND_PLAY]);
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llParcelMediaCommandList">llParcelMediaCommandList</a>([PARCEL_MEDIA_COMMAND_AUTO_ALIGN,TRUE]);
}
default
{
<a href="https://secondlife.com/badgeo/wakka.php?wakka=state_entry">state_entry</a>()
{
// set a default jpeg
seturl("https://www.flickr.com/images/flickr_logo_gamma.gif.v1.2");
// start listening for nearby speech
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llListen">llListen</a>(1,"",NULL_KEY,"");
// start sensing nearby agents once a minute
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llSensorRepeat">llSensorRepeat</a>("",NULL_KEY,AGENT,10,10,60);
}
<a href="https://secondlife.com/badgeo/wakka.php?wakka=sensor">sensor</a>(integer num_detected)
{
integer i;
for (i = 0; i &lt; num_detected; i++)
{
// ping the server so we know who's around
string url = "https://www.hackdiary.com/secondlife/experiments/seen?name="+<a href="https://secondlife.com/badgeo/wakka.php?wakka=llDetectedName">llDetectedName</a>(i);
// but don't record the request ID, because we don't need
// http_response to care about this request
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llHTTPRequest">llHTTPRequest</a>(url,[],"");
}
}
<a href="https://secondlife.com/badgeo/wakka.php?wakka=listen">listen</a>(integer channel, string name, key id, string message)
{
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llSay">llSay</a>(0,"Setting the tag for "+name+" to "+message);
string url = "https://www.hackdiary.com/secondlife/experiments/set_tag?name="+name+"&tag="+message;
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llHTTPRequest">llHTTPRequest</a>(url,[],"");
}
<a href="https://secondlife.com/badgeo/wakka.php?wakka=touch_start">touch_start</a>(integer total_number)
{
// ask the server for a jpeg appropriate to the agent who touched us
string url = "https://www.hackdiary.com/secondlife/experiments/sensed?name="+<a href="https://secondlife.com/badgeo/wakka.php?wakka=llDetectedName">llDetectedName</a>(0);
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llSetText">llSetText</a>("Finding a picture for "+<a href="https://secondlife.com/badgeo/wakka.php?wakka=llDetectedName">llDetectedName</a>(0),&lt;0,0,1&gt;,1);
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llParcelMediaCommandList">llParcelMediaCommandList</a>([PARCEL_MEDIA_COMMAND_STOP]);
http_id = <a href="https://secondlife.com/badgeo/wakka.php?wakka=llHTTPRequest">llHTTPRequest</a>(url,[],"");
}
<a href="https://secondlife.com/badgeo/wakka.php?wakka=http_response">http_response</a>(key request_id, integer status, list metadata, string body) {
// make sure we're processing a response we care about
if(request_id == http_id) {
// only on request success
if(status == 200) {
// data is coming back as pipe-delimited
list data = <a href="https://secondlife.com/badgeo/wakka.php?wakka=llParseString2List">llParseString2List</a>(body,["|"],[]);
// url is the first field
string url = <a href="https://secondlife.com/badgeo/wakka.php?wakka=llList2String">llList2String</a>(data,0);
if(url == "UNKNOWN") {
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llWhisper">llWhisper</a>(0,"I don't know what kind of picture to show you.
Type '/1 sometag' to tell me what tag to search for on flickr and I'll remember it.");
} else {
// name is the second field
string name = <a href="https://secondlife.com/badgeo/wakka.php?wakka=llList2String">llList2String</a>(data,1);
<a href="https://secondlife.com/badgeo/wakka.php?wakka=llSetText">llSetText</a>("Showing a picture for "+name,&lt;0,0,1&gt;,0.5);
seturl(url);
}
}
}
}
}
</pre>

 [1]: https://www.hackdiary.com/archives/000085.html
 [2]: https://wiki.secondlife.com/wiki/Category:Shared_Media