---
layout: post
title: "Speed up/slow down HTML5 video"
description: ""
category:
tags: []
---
{% include JB/setup %}

I often use a tool called Enounce Myspeed to change the speed of Flash videos, it works very well and allows me to watch videos at any speed I want. This is often useful to watch tutorials at double speed to see if its worth watching and then slow it down to half speed when I need to focus on how something was done.

The problem is youtube randomly displays video in Html5, even although I have disabled the Html5 beta test.

This was rather annoying as I have become so used to playing video in double speed that going back to the normal speed seems rather slow.

So after a few google searches and trial and error I managed to make my own chrome bookmark which will allow me to pick the playback speed of the html5 video. just create a new chrome bookmark with the following in the url box:

```javascript
javascript:(function() { var videoNumber=prompt("Which video number (0 to x)","0"); var playbackSpeed=prompt("Playback speed?","2.0"); document.getElementsByTagName("video")[videoNumber].playbackRate=playbackSpeed;})();
```
Give it a title such as "Change video speed" and add it to the chrome bookmarks bar.

Now anytime you are on a site with html5 video, you can easily change the playback speed by entering which video and what speed you want it to play at.

Sadly it doesn't work on iOS since the playbackRate isn't supported, but hopefully one day, I will test on android later on (hopefully chrome for android will support it).

Good programming sites that this will work with include:
[http://channel9.msdn.com/](http://channel9.msdn.com/)

On iphone there is a great app for speeding up videos on the device and from youtube called SpeedUpTv:
[http://mix1009.com/en/?page_id=84](http://mix1009.com/en/?page_id=84)