---
layout: post
title:  "Radiodan Neue"
date:   2017-01-03 15:51:32
author:
  name: Libby Miller
  github: libbymiller
---

We've had a big breakthrough after we showed Radiodan at the [V&A's 
Digital Design 
Weekend](http://www.vam.ac.uk/blog/news-learning-department/digital-design-weekend-2016) 
last October. Since Chromium 51 now comes with Raspian Jessie, and I'd 
accidentally discovered that Chromium works fine on the Pi without a 
screen, [Andrew](https://twitter.com/andrewn) whipped up the tiny and amazing [Radiodan Neue](Radiodan 
Neue).

It's massively simplified compared with the previous implementation, 
because it's basically all browser-based. This means that everything you 
need to write is in the browser too. There's almost no installation 
required as everything runs in two Chromium windows, connected using 
websockets, so it's trivial to get up and running, and trivial to make 
it run on a laptop before deploying. You can also debug on the Pi too. 
Andrew's also written an implmentation of the physical UI!

We've used it at work for our "Project Bedtime" prototype on a Pi Zero with 
a Phat DAC, using a wifi access point on a second screen as a remote control.

I'll gradually be updating the docs here, but everything is on [Andrew's 
github page](https://github.com/andrewn/neue-radio/blob/master/INSTALL.MD).

<a href="/assets/bedtime.jpg"><img class="alignnone size-large wp-image-714" src="/assets/bedtime.jpg?w=660" alt="project bedtime" /></a>
