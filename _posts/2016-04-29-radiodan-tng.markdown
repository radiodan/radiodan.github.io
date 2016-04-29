---
layout: post
title:  "Radiodan TNG"
date:   2016-04-29 13:50:32
author:
  name: Libby Miller
  github: libbymiller
---

It's a while since we've posted - but we're still working on Radiodan. We're 
at a transition point, as we've been moving from a series of 
experiments to more focused work on making an internet radio that can be 
easily hacked on to make it do what you want.

To make this easier, we've:

* Moved the code base fully to Raspbian Jessie
* Moved the wifi setup code to [Resin's version of the same thing](https://github.com/radiodan/resin-wifi-connect)
* Changed the code so that it installs the [skeleton application](https://github.com/radiodan/radiodan-skeleton) by default, which is simple but also much more hackable
* Tested it on various version of the Raspberry Pi (it works well on 2, 3 and Zero)
* Tried various audio options, concluding that a [DAC](https://shop.pimoroni.com/products/phat-dac) is the best option
* Started to update the documentation

I've also made a quick prototype to test these changes - a [Radio 3 "Red Button" 
prototype](https://github.com/radiodan-demos/r3_red_button) which allows you to switch between different strands of audio for 
a particular programme:

<iframe src="//player.vimeo.com/video/161914993" width="500" height="281"
frameborder="0" webkitallowfullscreen mozallowfullscreen
allowfullscreen></iframe>

