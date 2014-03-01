---
layout: post
title:  "Radiodan in February - designs and web interface"
date:   2014-02-28 16:45:00
author:
  -
    name: Libby Miller
    github: libbymiller
---

This is a quick post to summarise what we've been up to in the last few weeks.

Dan and AndrewN have been working really hard on Radiodan 2, as described in the previous 
[posts](/2014/01/08/radiodan-v1-retrospective.html) on 
[architecture](/2014/01/08/radiodan-v2-architectures.html). The big benefits are visible already:

* separable mini applications so that one failure won't crash the entire radiodan, and errors are properly traceable
* full testing of everything

AndrewN and Dan were able to whip up a basic web-based client for it in a couple of hours on 
Wednesday, which is a huge difference and proof that we are making things that developers will be 
able to use.

AndrewW and Joanne have been thinking more about the web application designs, and this led to a 
fairly substantial discussion about what we are actually trying to do, which is good.

AndrewN did a diagram explaining the different aspects:

![Radiodan Diagram](/assets/feb_post/radiodan_diagram.jpg)

The important thing to see here is that the thing we are working on at the moment is the "kit" - a 
list of physical things and software that shows off the possibilities but isn't in itself an 
application. This is a tricky tightrope walk. It's got to look pleasant and show the possibilities 
but without being 'finished' in this sense: people should regard it as a starting point for making 
their own radio. But it should nevertheless look good and be usable.

Once we're happy with v2, we want to start making some concept radios, which can and should look 
more polished.

Here are some of AndrewW's beautiful sketches for the web interface. The idea is that there's a 
very simple physical device, with a single button and a couple of dials for basic controls and 
signalling status. Then the 'remote control' - which is really a web page running off a server 
running within the Radiodan - can be as complicated as you like, and have much more functionality.

The designs are sketches at the moment, and very much work in progress. 

We have one button that we can then assign different actions, in order to show the different 
possibilities. So effectively we will have three example applications. Here's some sketches 
showing metadata about what's playing and the virtual "button" for the current application:

![Metadata Radiodan web interface sketches](/assets/feb_post/metadata.png)

And here are some sketches showing the different applications we plan to make:

![Application Radiodan web interface sketches](/assets/feb_post/apps.png)

It has been really helpful to have specific ideas to talk through with AndrewW, and it's made us 
realise that the web interface aspect is quite confusing in some ways - most people expect web 
pages to be in a cloud, not on a device.

This week we have also enjoyed BERG's article about their work on a [connected washing 
machine](http://bergcloud.com/case-studies/cloudwash/) - it's reassuring to see that we're looking 
at similar ideas for making impenetrable devices more controllable.
