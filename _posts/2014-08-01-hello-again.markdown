---
layout: post
title:  "Hello Again"
date:   2014-08-01 16:34:37
author:
  name: Libby Miller
  github: libbymiller
---

I've just realised it's almost exactly a year since I wrote the first post here. So, hello again.

<h2>May, June and July for Radiodan</h2>

May was a rush for AndrewN and Dan to get the Radiodan code and presentation ready for 
[Solid](http://solidcon.com/solid2014/public/schedule/detail/33250) while I helped by 
making a [Radiodan v2 NOOBS version](http://dev.notu.be/2014/05/radiodan/) and trying it 
all out. Mostly though I was [working on another 
project](http://www.bbc.co.uk/rd/blog/2014/06/infinite-trailers-user-test) until the end 
of June.

We've spent the last few weeks doing some pieces of 
[documentation](https://github.com/radiodan/magic-button/blob/master/doc/http-api.md) and 
[experimentation](https://www.flickr.com/photos/nicecupoftea/14550057628/) while gearing 
up for using Radiodan as an experimental platform for a [discovery prototype in our 
MediaScape project](http://www.bbc.co.uk/rd/blog/2014/07/protocols-for-device-discovery). 
AndrewW and Lianne have also been making some test boxes in order to improve the 
instructions for the cases.

Right now, Dan is updating the build to use Jessie, and AndrewN is refactoring the magic 
button so that it's easy to add different functionality to it. So things will change quite 
a lot. However, as of today now we have:

* a [Radiodan NOOBS](http://dev.notu.be/2014/05/radiodan/) that works
* [draft case-building documentation](https://github.com/radiodan/project/blob/master/docs/case_construction.md) and the [case as pdf](https://github.com/radiodan/project/blob/master/docs/assets/radiodan_3mm_laser_template.pdf)
* a [getting started document](https://github.com/radiodan/project/blob/master/docs/getting_started.markdown) for the software
* a handy [REST API](https://github.com/radiodan/magic-button/blob/master/doc/http-api.md) for the magic button functionalities (e.g. changing station, turning it on and off, setting the volume and so on).

So if you'd like a go, you can start 
[here](https://github.com/radiodan/project/blob/master/docs/case_construction.md).

Here's one I made earlier:

<img src="/assets/exclusively_archers_postcard.jpg" width="500" alt="Exclusively Archers Postcard"/>

This is a very simple radio, with no changes to the code, which uses a crontab and the 'magic button' REST API to turn itself on for the Archers, and off again afterwards - so a reverse [Archers Avoider](http://planb.nicecupoftea.org/2013/04/16/archers-avoider/).

    # turn it on at 14:02 weekdays
    2 13 * * 1-5  /usr/bin/curl -X POST http://localhost/radio/service/radio4  

    # turn it off at 14:15 weekdays
    15 13 * * 1-5,7  /usr/bin/curl -X DELETE http://localhost/radio/power

    # turn it on at 19:02 weekdays and sundays
    2 18 * * 1-5,7  /usr/bin/curl -X POST http://localhost/radio/service/radio4 

    # turn it off at 19:15 weekdays and sundays
    15 18 * * 1-5,7  /usr/bin/curl -X DELETE http://localhost/radio/power

    # turn it on at 10:00 on sundays for the omnibus edition
    0 9 * * 7 /usr/bin/curl -X POST http://localhost/radio/service/radio4

    # and turn it off at 11:15
    15 10 * * 7 /usr/bin/curl -X DELETE http://localhost/radio/power

</code>

<img src="/assets/exclusively_archers.jpg" width="500" alt="Exclusively Archers"/>
<p><img src="http://dev.notu.be/2014/07/pixel/transparent_2014-07-18.gif" alt="" /></p>
