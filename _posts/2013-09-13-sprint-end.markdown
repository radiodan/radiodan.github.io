---
layout: post
title:  "Sprint end"
date:   2013-09-13 10:44:44
author: libbymiller
---

Our two-week sprint on Radiodan ended last week. We didn't really get as far as we'd hoped, though that was 
partly us getting to understand the sort of velocity we have doing these kinds of projects. Which is to say, 
compared with pure software, things seem to take a looong time.

However we have done a bunch of interesting things, and particularly with respect to wifi configuration, Andrew and Chris have a very nice workflow going, which you can see in action in [this video]( (http://vimeo.com/73633646).

Our original approach was this:

* if the radiodan can't find a wifi network it knows about
* create a point to point network
* use your laptop or phone to connect to that network
* go to any webpage on that device. You should be edirected to a config page for the radiodan
* enter the network details
* click to reboot the radiodan

What Andrew and Chris discovered was that this solution was not very robust - quite often the network didn't seem to be created, and when it was, it was hard to connect to and often didn't work.

It's hard to know what exactly the problem was - at work there are a very large number of wifi networks, for 
example, so that may have been at least part of the issue.

After discussing the issue with TomN and others, Andrew developed a better solution - which is that you turn the 
Pi into a wifi router. This makes for a more robust network to connect to (usually), although it has the 
disadvantage that you can't both scan for networks and be an access point - so the code scans first and then 
becomes an access point, lengthening startup time. Andrew also implemented the nice 'captive portal' feature of 
the kind you get in hotels and similar, where as soon as you connect to the network a web page pops up requesting 
information.

Dan and I spent a lot of last week preparing for our nextrad.io presentation, which was a distraction in some 
ways, but also helped us get our thoughts in order about the overall goals of the project - essentially - make it 
easy for us and then others to quickly prototype the behaviours and appearance of connected radios. The 
conference was good fun too - it was very nice to meet and hear from people in the wider radio industry. 
Nextrad.io video all their presentations so when it's ready we'll link to it here - the slides don't mean much on 
their own as they are mostly pictures.

For the presentation, Dan put together this (very funny I think) [12 second video of the Archers 
Avoider](https://vimeo.com/73576108), which you should definitely watch. Radiodan is not the same as the Archers 
Avoider though, but just one of many applications of it.

I've also been preaparing for my class at the [XML Summer School next 
week](http://xmlsummerschool.com/curriculum-2013/trends-and-transients-2013/), talking about 
[radio-democracy](https://github.com/libbymiller/radio-democracy) and the experimental and partial implmentation of [BBC R&D's Universal 
Control API](http://www.bbc.co.uk/blogs/researchanddevelopment/2011/02/universal-control.shtml) in it.

This week Dan also created a non-physical web-only application of Radiodan (a erm, rApp?) using 
Twillio, which is a web API interface to SMS and calling. His request show rApp allows you to 
send an SMS and request an artist or song from his audio collection, which will then be queued 
up and play (on his machine). This necessitated various improvements to the Radiodan code 
including lays nothing ok; improved notifications, searching for music, adding music without 
using mpc.

Andrew and I experimented with an interrupt-based hardware interfaces - we created an event 
machine version - but the interupt needs making into a proper bit of code.
